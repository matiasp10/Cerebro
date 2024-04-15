JavaScript es **de subproceso** único (_Único Hilo_): solo se puede ejecutar **una tarea a la vez**. Por lo general, eso no es gran cosa, pero ahora imagina que estás ejecutando una tarea que toma 30 segundos... Ya... Durante esa tarea estamos esperando 30 segundos antes de que algo más pueda suceder (JavaScript se ejecuta en el subproceso principal del navegador de forma predeterminada, por lo que toda la interfaz de usuario está atascada).

Afortunadamente, el navegador nos brinda algunas características que el motor de JavaScript en sí mismo no proporciona: una API web. Esto incluye la API DOM `setTimeout`, las solicitudes HTTP, etc. Esto puede ayudarnos a crear un comportamiento **asíncrono** y **sin bloqueo** 🚀.

Cuando invocamos una función, se agrega a algo llamado pila de llamadas. La pila de llamadas es parte del motor JS, esto no es específico del navegador. Es una pila, lo que significa que es el primero en entrar, el último en salir (piense en una pila de panqueques). Cuando una función devuelve un valor, se saca de la pila 👋.

![[callstack1.gif]]

La función `respond` devuelve una función `setTimeout`. Nos lo proporciona la Web API: nos permite retrasar tareas sin bloquear el hilo principal. La función de devolución de llamada que pasamos a la función `setTimeout`, la función de flecha `() => { return` `'``Hey``'`} se agrega a la API web. Mientras tanto, la función `setTimeout`y la función de respuesta se sacan de la pila, ¡ambas devolvieron sus valores!

![](https://res.cloudinary.com/practicaldev/image/fetch/s--d_n4m4HH--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif2.1.gif)

En la API web, un temporizador se ejecuta durante el segundo argumento que le pasamos, 1000 ms. La devolución de llamada no se agrega inmediatamente a la pila de llamadas, sino que se pasa a algo llamado cola.

[![](https://res.cloudinary.com/practicaldev/image/fetch/s--MewGMdte--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif3.1.gif)](https://res.cloudinary.com/practicaldev/image/fetch/s--MewGMdte--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif3.1.gif)
Esto puede ser una parte confusa: ¡no significa que la función de devolución de llamada se agregue a la pila de llamadas (por lo tanto, devuelve un valor) después de 1000 ms! Simplemente se agrega a la _cola_ después de 1000 ms. ¡Pero es una cola, la función tiene que esperar su turno!

Ahora bien, esta es la parte que todos hemos estado esperando... Es hora de que el bucle de eventos haga su única tarea: **¡conectar la cola con la pila de llamadas!** Si la pila de llamadas está **vacía** , es decir, si todas las funciones invocadas anteriormente han devuelto sus valores y se han extraído de la pila, el _primer elemento_ de la cola se agrega a la pila de llamadas. En este caso, no se invocó ninguna otra función, lo que significa que la pila de llamadas estaba vacía cuando la función de devolución de llamada fue el primer elemento de la cola.

[![](https://res.cloudinary.com/practicaldev/image/fetch/s--b2BtLfdz--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif4.gif)](https://res.cloudinary.com/practicaldev/image/fetch/s--b2BtLfdz--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif4.gif)
La devolución de llamada se agrega a la pila de llamadas, se invoca, devuelve un valor y se saca de la pila.

[![](https://res.cloudinary.com/practicaldev/image/fetch/s--NYOknEYi--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif5.gif)](https://res.cloudinary.com/practicaldev/image/fetch/s--NYOknEYi--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif5.gif)

---

Leer un artículo es divertido, pero solo te sentirás completamente cómodo trabajando con él una y otra vez. Intente averiguar qué se registra en la consola si ejecutamos lo siguiente:  

```js

const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"), 500);
const baz = () => console.log("Third");

bar();
foo();
baz();
```

¿Entendido? Echemos un vistazo rápido a lo que sucede cuando ejecutamos este código en un navegador:

[![](https://res.cloudinary.com/practicaldev/image/fetch/s--BLtCLQcd--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif14.1.gif)](https://res.cloudinary.com/practicaldev/image/fetch/s--BLtCLQcd--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif14.1.gif)

1. invocamos `bar`. `bar` devuelve una función `setTimeout`.
2. La devolución de llamada a la que pasamos `setTimeout`se agrega a la API web, la `setTimeout`función y `bar` se elimina de la pila de llamadas.
3. El temporizador se ejecuta, mientras tanto `foo` se invoca y registra `First`. `foo` regresa (indefinido), `baz` se invoca y el callback se agrega a la cola.
4. `baz` registra `Third`. El bucle de eventos ve que la pila de llamadas está vacía después de que se devuelve `baz`, después de lo cual la devolución de llamada se agrega a la pila de llamadas.
5. El callback registra `Second`.

### Conceptos

[[Glosario#^064d3b|Memory Heap]]
[[Glosario#^b4476a|Callstack]]
[[Glosario#^8bb8a8|Task Queue]]
[[Glosario#^afc0fd|Microtask Queue o PromiseJobs]]





