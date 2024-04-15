## Entendiendo Process.nextTick()

[[Event Loop en NodeJS]]

Puede que hayas notado que process.nextTick() no aparecía en el diagrama, a pesar de que forma parte de la API asíncrona. Esto se debe a que **process.nextTick() no es técnicamente parte del bucle de eventos**. En su lugar, **nextTickQueue** se procesará después de que la operación actual se complete, _independientemente de la fase actual del bucle de eventos_. Aquí, una operación se define como una transición desde el manejador C/C++ subyacente, y el manejo del JavaScript que necesita ser ejecutado.

Volviendo a nuestro diagrama, **cada vez que llames a process.nextTick()** en una fase dada, todos los _callbacks_ pasados a **process.nextTick()** serán resueltos antes de que el bucle de eventos continúe. Esto puede crear algunas malas situaciones porque te permite "matar de hambre" tu E/S haciendo llamadas recursivas a process.nextTick(), lo que impide que el bucle de eventos alcance la fase de sondeo.

### ¿Por qué se permitiría eso?

¿Por qué se incluiría algo como esto en Node.js? _Parte de esto es una filosofía de diseño en la que una API siempre debe ser asíncrona, incluso cuando no tiene por qué serlo_. Tome este fragmento de código, por ejemplo:

```js
function apiCall(arg, callback) {
  if (typeof arg !== 'string')
    return process.nextTick(
      callback,
      new TypeError('argument should be string')
    );
}
```

El fragmento realiza una comprobación de argumentos y, si no es correcto, pasará el error a la devolución de llamada. La API se actualizó recientemente para permitir pasar argumentos a **process.nextTick()**, lo que le permite tomar cualquier argumento pasado después de la devolución de llamada para que se propague como argumento a la devolución de llamada para que no tenga que anidar funciones.

Lo que estamos haciendo es _pasar un error de vuelta al usuario pero sólo después de haber permitido que el resto del código del usuario se ejecute_. Usando **process.nextTick()** garantizamos que **apiCall()** siempre _ejecuta su callback después del resto del código del usuario y antes de que el bucle de eventos pueda continuar_. Para lograr esto, se permite que la pila de llamadas JS se desenrolle y luego ejecute inmediatamente la llamada de retorno proporcionada, lo que permite a una persona hacer llamadas recursivas a **process.nextTick()** sin llegar a un **RangeError: Maximum call stack size exceeded from v8**.

Esta filosofía puede dar lugar a situaciones **potencialmente problemáticas**. Tomemos este fragmento como ejemplo:

```js
let bar;

// this has an asynchronous signature, but calls callback synchronously
function someAsyncApiCall(callback) {
  callback();
}

// the callback is called before `someAsyncApiCall` completes.
someAsyncApiCall(() => {
  // since someAsyncApiCall hasn't completed, bar hasn't been assigned any value
  console.log('bar', bar); // undefined
});

bar = 1;
```

El usuario define **someAsyncApiCall()** para que tenga una firma asíncrona, pero en realidad opera de forma síncrona. Cuando es llamada, el **callback** proporcionado a _someAsyncApiCall()_ es llamado en la misma fase del bucle de eventos porque _someAsyncApiCall()_ en realidad no hace nada de forma asíncrona. Como resultado, el callback intenta hacer referencia a bar aunque no tenga esa variable en el ámbito todavía, porque el script no ha podido ejecutarse hasta su finalización.

Colocando la llamada de retorno en **process.nextTick()**, el script todavía tiene la capacidad de ejecutarse hasta su finalización, permitiendo que todas las variables, funciones, etc., sean _inicializadas antes de que el callback sea llamado_. También tiene la ventaja de no permitir que el bucle de eventos continúe. Puede ser útil para alertar al usuario de un error antes de permitir que el bucle de eventos continúe. Aquí está el ejemplo anterior usando process.nextTick():

```js
let bar;

function someAsyncApiCall(callback) {
  process.nextTick(callback);
}

someAsyncApiCall(() => {
  console.log('bar', bar); // 1
});

bar = 1;
```

Aquí hay otro ejemplo del mundo real:

```js
const server = net.createServer(() => {}).listen(8080);

server.on('listening', () => {});
```

Cuando solo se pasa un puerto, el puerto se enlaza inmediatamente. Por lo tanto, el callback de '**escucha**' podría llamarse inmediatamente. El problema es que el callback **.on('listening')** no se habrá configurado en ese momento.

Para evitar esto, el evento de '**escucha**' se pone en cola en **nextTick()** para permitir que el script se ejecute hasta su finalización. Esto permite al usuario establecer cualquier controlador de eventos que desee.

## process.nextTick() vs setImmediate()

Tenemos dos llamadas que son similares en lo que a usuarios se refiere, pero sus nombres son confusos.

- **process.nextTick()** se dispara _inmediatamente en la misma fase_ 
- **setImmediate()** se activa en la _siguiente iteración o 'tick' del bucle de eventos_

En esencia, los nombres deben ser intercambiados. _process.nextTick() se dispara más inmediatamente que setImmediate()_, pero esto es un artefacto del pasado que es poco probable que cambie. Hacer este cambio rompería un gran porcentaje de los paquetes en npm. Cada día se añaden más módulos nuevos, lo que significa que cada día que esperamos, se producen más roturas potenciales. Aunque son confusos, los nombres en sí no cambiarán.

Recomendamos a los desarrolladores que **utilicen setImmediate() en todos los casos porque es más fácil de razonar**.

## Porque usar proccess.nextTick() ?

Hay dos razones principales:

1. Permitir a los usuarios **manejar errores**, limpiar cualquier recurso innecesario, o quizás intentar la petición de nuevo **antes de que el bucle de eventos continúe**.
2. A veces es necesario permitir que un _callback se ejecute después de que la pila de llamadas se haya desenrollado pero antes de que el bucle de eventos continúe_.

Un ejemplo es para satisfacer las expectativas del usuario. Un ejemplo sencillo:

```js
const server = net.createServer();
server.on('connection', (conn) => {});

server.listen(8080);
server.on('listening', () => {});
```

Digamos que **listen()** se ejecuta al principio del bucle de eventos, pero el callback de escucha se coloca en un **setImmediate()**. A menos que se pase un nombre de host, la conexión con el puerto ocurrirá inmediatamente. Para que el bucle de eventos continúe, debe llegar a la fase de sondeo, lo que significa que hay una posibilidad no nula de que se haya recibido una conexión permitiendo que el evento de conexión se dispare antes que el evento de escucha.

Otro ejemplo es extender un **EventEmitter** y emitir un evento desde el constructor:

```js
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {
  constructor() {
    super();
    this.emit('event');
  }
}

const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('an event occurred!');
});
```

_No puedes emitir un evento desde el constructor inmediatamente porque el script no se habrá procesado hasta el punto en que el usuario asigne un callback a ese evento_. Así que, dentro del propio constructor, puedes usar process.nextTick() para establecer un callback para emitir el evento después de que el constructor haya terminado, lo que proporciona los resultados esperados:

```js
const EventEmitter = require('events');

class MyEmitter extends EventEmitter {
  constructor() {
    super();

    // use nextTick to emit the event once a handler is assigned
    process.nextTick(() => {
      this.emit('event');
    });
  }
}

const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('an event occurred!');
});
```