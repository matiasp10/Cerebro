Los _Hooks_ son una nueva incorporación en React 16.8. Te permiten usar estado y otras características de React sin escribir una clase.

El _Hook de efecto_ te permite llevar a cabo efectos secundarios en componentes funcionales:

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // De forma similar a componentDidMount y componentDidUpdate
  useEffect(() => {
    // Actualiza el título del documento usando la API del navegador
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

Este fragmento está basado en el [ejemplo de contador de la página anterior](https://es.reactjs.org/docs/hooks-state.html), pero le hemos añadido una funcionalidad nueva: actualizamos el título del documento con un mensaje personalizado que incluye el número de clicks.

Peticiones de datos, establecimiento de suscripciones y actualizaciones manuales del DOM en componentes de React serían ejemplos de efectos secundarios. Tanto si estás acostumbrado a llamar a estas operaciones “efectos secundarios” (o simplemente “efectos”) como si no, probablemente los has llevado a cabo en tus componentes con anterioridad.

> Consejo
> 
> Si estás familiarizado con el ciclo de vida de las clases de React y sus métodos, el _Hook_ `useEffect` equivale a `componentDidMount`, `componentDidUpdate` y `componentWillUnmount` combinados.

Hay dos tipos de efectos secundarios en los componentes de React: aquellos que no necesitan una operación de saneamiento y los que sí la necesitan. Vamos a profundizar más en esta distinción.

## [](https://es.reactjs.org/docs/hooks-effect.html#effects-without-cleanup)Efectos sin saneamiento

En ciertas ocasiones, queremos **ejecutar código adicional después de que React haya actualizado el DOM.** Peticiones de red, mutaciones manuales del DOM y registros, son ejemplos comunes de efectos que no requieren una acción de saneamiento. Decimos esto porque podemos ejecutarlos y olvidarnos de ellos inmediatamente. Vamos a comparar cómo las clases y los _Hooks_ nos permiten expresar dichos efectos.

### [](https://es.reactjs.org/docs/hooks-effect.html#example-using-classes)Ejemplo con clases

En los componentes de React con clases, el método `render` no debería causar efectos secundarios por sí mismo. Sería prematuro. Normalmente queremos llevar a cabo nuestros efectos _después_ de que React haya actualizado el DOM.

Y es por eso que en las clases de React ponemos los efectos secundarios en `componentDidMount` y `componentDidUpdate`. Volviendo a nuestro ejemplo, aquí tenemos el componente clase contador de React que actualiza el título del documento justo después de que React haga cambios en el DOM:

```jsx
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }
  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

Fíjate en cómo **hemos duplicado el código en los dos métodos del ciclo de vida en la clase**

Esto es porque en muchas ocasiones queremos llevar a cabo el mismo efecto secundario sin importar si el componente acaba de montarse o si se ha actualizado. Conceptualmente, queremos que ocurra después de cada renderizado, pero las clases de React no tienen un método que haga eso. Podríamos extraer un método, pero aún así tendríamos que llamarlo en los dos sitios.

Veamos ahora cómo podemos hacer lo mismo con el _Hook_ `useEffect`.

### [](https://es.reactjs.org/docs/hooks-effect.html#example-using-hooks)Ejemplo con _Hooks_

Ya hemos visto este ejemplo al principio de la página, pero veámoslo más detenidamente:

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

**¿Qué hace `useEffect`?** Al usar este _Hook_, le estamos indicando a React que el componente tiene que hacer algo después de renderizarse. React recordará la función que le hemos pasado (nos referiremos a ella como nuestro “efecto”), y la llamará más tarde después de actualizar el DOM. En este efecto, actualizamos el título del documento, pero también podríamos hacer peticiones de datos o invocar alguna API imperativa.

**¿Por qué se llama a `useEffect` dentro del componente?** Poner `useEffect` dentro del componente nos permite acceder a la variable de estado `count` (o a cualquier prop) directamente desde el efecto. No necesitamos una API especial para acceder a ella, ya que se encuentra en el ámbito de la función. Los _Hooks_ aprovechan los closures de JavaScript y evitan introducir APIs específicas de React donde JavaScript ya proporciona una solución.

**¿Se ejecuta `useEffect` después de cada renderizado?** ¡Sí! Por defecto se ejecuta después del primer renderizado _y_ después de cada actualización. Más tarde explicaremos [cómo modificar este comportamiento](https://es.reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects). En vez de pensar en términos de “montar” y “actualizar”, puede resultarte más fácil pensar en efectos que ocurren “después del renderizado”. React se asegura de que el DOM se ha actualizado antes de llevar a cabo el efecto.

### [](https://es.reactjs.org/docs/hooks-effect.html#detailed-explanation)Explicación detallada

Ahora que sabemos algo más sobre los efectos, estas líneas deberían cobrar sentido:

```
function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
}
```

Declaramos la variable de estado `count` y le indicamos a React que necesitamos usar un efecto. Le pasamos una función al _Hook_ `useEffect`. Esta función que pasamos _es_ nuestro efecto. Dentro de nuestro efecto actualizamos el título del documento usando la API del navegador `document.title`. Podemos leer el valor más reciente de `count` dentro del efecto porque se encuentra en el ámbito de nuestra función. Cuando React renderiza nuestro componente, recordará este efecto y lo ejecutará después de actualizar el DOM. Esto sucede en cada renderizado, incluyendo el primero.

Los desarrolladores experimentados en JavaScript se percatarán de que la función que le pasamos a `useEffect` es distinta en cada renderizado. Esto es intencionado. En realidad esto es lo que nos permite leer la variable `count` desde el interior de nuestro efecto sin preocuparnos de que su valor esté obsoleto. Cada vez que renderizamos, planificamos un _efecto_ diferente, reemplazando el anterior. En cierta manera, esto hace que los efectos funcionen más como parte del resultado del renderizado. Cada efecto pertenece a su correspondiente renderizado. [Más adelante](https://es.reactjs.org/docs/hooks-effect.html#explanation-why-effects-run-on-each-update) aclararemos por qué esto es útil.

> Consejo
> 
> A diferencia de `componentDidMount` o `componentDidUpdate`, los efectos planificados con `useEffect` no bloquean la actualización de la pantalla del navegador. Esto hace que tu aplicación responda mejor. La mayoría de efectos no necesitan suceder de manera síncrona. En los casos poco comunes en los que se necesita una ejecución síncrona (como en mediciones de la disposición de elementos), podemos usar el _Hook_ [`useLayoutEffect`](https://es.reactjs.org/docs/hooks-reference.html#uselayouteffect) con una API idéntica a la de `useEffect`.

## [](https://es.reactjs.org/docs/hooks-effect.html#effects-with-cleanup)Efectos con saneamiento

En el apartado anterior hemos visto cómo expresar efectos secundarios que no necesitan ningún saneamiento. Sin embargo, algunos efectos lo necesitan. Por ejemplo, **si queremos establecer una suscripción** a alguna fuente de datos externa. En ese caso, ¡es importante sanear el efecto para no introducir una fuga de memoria! Comparemos cómo se puede hacer esto con clases y con _Hooks_.

### [](https://es.reactjs.org/docs/hooks-effect.html#example-using-classes-1)Ejemplo con clases

En una clase de React, normalmente se establece una suscripción en `componentDidMount`, y se cancela la suscripción en `componentWillUnmount`. Por ejemplo, digamos que tenemos un módulo `ChatAPI` que nos permite suscribirnos para saber si un amigo está conectado. Así es como podemos establecer la suscripción y mostrar ese estado usando una clase:

```jsx
class FriendStatus extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }

  render() {
    if (this.state.isOnline === null) {
      return 'Loading...';
    }
    return this.state.isOnline ? 'Online' : 'Offline';
  }
}
```

Fíjate en cómo `componentDidMount` y `componentWillUnmount` necesitan ser un reflejo el uno del otro. Los métodos del ciclo de vida nos obligan a separar esta lógica incluso cuando, conceptualmente, el código de ambos está relacionado con el mismo efecto.

> Nota
> 
> Los lectores perspicaces podrán percatarse de que este ejemplo necesita también un método `componentDidUpdate` para ser completamente correcto. De momento vamos a ignorar este hecho, pero volveremos a él en una [sección posterior](https://es.reactjs.org/docs/hooks-effect.html#explanation-why-effects-run-on-each-update) de esta página.

### [](https://es.reactjs.org/docs/hooks-effect.html#example-using-hooks-1)Ejemplo usando _Hooks_

Veamos cómo podemos escribir este componente con _Hooks_.

Quizás puedas estar pensando que necesitaríamos un efecto aparte para llevar a cabo este saneamiento. Pero el código para añadir y eliminar una suscripción está tan estrechamente relacionado que `useEffect` está diseñado para mantenerlo unido. Si tu efecto devuelve una función, React la ejecutará en el momento de sanear el efecto:

```jsx
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Especifica cómo sanear este efecto:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

**¿Por qué hemos devuelto una función en nuestro efecto?** Este es un mecanismo opcional de los efectos. Todos los efectos pueden devolver una función que los sanea más tarde. Esto nos permite mantener la lógica de añadir y eliminar suscripciones cerca la una de la otra. ¡Son parte del mismo efecto!

**¿Cuándo sanea React el efecto exactamente?** React sanea el efecto cuando el componente se desmonta. Sin embargo, como hemos aprendido anteriormente, los efectos no se ejecutan solo una vez, sino en cada renderizado. He aquí el motivo por el cual React _también_ sanea los efectos de renderizados anteriores antes de ejecutar los efectos del renderizado actual. Más adelante analizaremos [por qué esto ayuda a evitar errores](https://es.reactjs.org/docs/hooks-effect.html#explanation-why-effects-run-on-each-update) y [cómo omitir este funcionamiento en el caso de que provoque problemas de rendimiento](https://es.reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects).

> Nota
> 
> No tenemos que nombrar la función devuelta por el efecto. La hemos llamado `cleanup` esta vez para clarificar su propósito, pero podemos devolver una función flecha o nombrarla de otra forma.

## [](https://es.reactjs.org/docs/hooks-effect.html#recap)Recapitulación

Hemos aprendido que `useEffect` nos permite expresar diferentes tipos de efectos secundarios después de que un componente se renderice. Algunos efectos pueden devolver una función cuando requieran saneamiento:

```
  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

Otros efectos pueden no tener fase de saneamiento y no devolver nada.

```
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
```

El _Hook_ de efecto unifica ambos casos en una única API.

---

**Si crees que ya tienes un nivel de comprensión decente de como funciona el _Hook_ de efecto o estás sobrepasado, puedes pasar a la [página siguiente sobre las reglas de los _Hooks_](https://es.reactjs.org/docs/hooks-rules.html) ahora.**

---

## [](https://es.reactjs.org/docs/hooks-effect.html#tips-for-using-effects)Consejos para usar efectos

Vamos a continuar profundizando en algunos aspectos de `useEffect` que les resultarán curiosos de alguna forma a los usuarios de React experimentados. No te sientas obligado a indagar en ello ahora mismo. Siempre puedes volver a esta página para conocer más detalles del _Hook_ de efecto.

### [](https://es.reactjs.org/docs/hooks-effect.html#tip-use-multiple-effects-to-separate-concerns)Consejo: Usa varios efectos para separar conceptos

Uno de los problemas que esbozamos en la [Motivación](https://es.reactjs.org/docs/hooks-intro.html#complex-components-become-hard-to-understand) para crear los _Hooks_ es que los métodos del ciclo de vida de las clases suelen contener lógica que no está relacionada, pero la que lo está, se fragmenta en varios métodos. Este es un componente que combina la lógica del contador y el indicador de estado del amigo de los ejemplos anteriores:

```jsx
class FriendStatusWithCounter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0, isOnline: null };
    this.handleStatusChange = this.handleStatusChange.bind(this);
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  handleStatusChange(status) {
    this.setState({
      isOnline: status.isOnline
    });
  }
  // ...
```

Fíjate en como la lógica que asigna `document.title` se divide entre `componentDidMount` y `componentDidUpdate`. La lógica de la suscripción también se reparte entre `componentDidMount` y `componentWillUnmount`. Y `componentDidMount` contiene código de ambas tareas.

Entonces, ¿cómo resuelven los _Hooks_ este problema? Del mismo modo que [puedes usar el _Hook de estado_ más de una vez](https://es.reactjs.org/docs/hooks-state.html#tip-using-multiple-state-variables), puedes usar varios efectos. Esto nos permite separar la lógica que no está relacionada en diferentes efectos:

```jsx
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
  // ...
}
```

**Los _Hooks_ nos permiten separar el código en función de lo que hace** en vez de en función del nombre de un método de ciclo de vida. React aplicará _cada_ efecto del componente en el orden en el que han sido especificados.

### [](https://es.reactjs.org/docs/hooks-effect.html#explanation-why-effects-run-on-each-update)Explicación: Por qué los efectos se ejecutan en cada actualización

Si estás familiarizado con las clases, te preguntarás por qué la fase de saneamiento de efecto ocurre después de cada rerenderizado y no simplemente cuando el componente se desmonta. Veamos un ejemplo práctico para ver por qué este diseño nos ayuda a crear componentes con menos errores.

[En apartados anteriores](https://es.reactjs.org/docs/hooks-effect.html#example-using-classes-1) hemos presentado el ejemplo de un componente `FriendStatus` que muestra si un amigo está conectado o no. Nuestra clase lee `friend.id` de `this.props`, se suscribe al estado del amigo al montarse y cancela la suscripción al desmontarse.

```
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```

**¿Pero qué sucede si la propiedad `friend` cambia** mientras el componente está en la pantalla? Nuestro componente continuaría mostrando el estado de un amigo diferente. Esto es un error. Además podríamos causar una fuga de memoria o un fallo crítico al desmontar dado que la llamada que cancela la suscripción usaría un identificador erróneo.

En un componente de clase, necesitaríamos añadir `componentDidUpdate` para manejar este caso:

```jsx
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentDidUpdate(prevProps) {
    // Cancela la suscripción del friend.id anterior
    ChatAPI.unsubscribeFromFriendStatus(
      prevProps.friend.id,
      this.handleStatusChange
    );
    // Se suscribe al siguiente friend.id
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```

No gestionar `componentDidUpdate` correctamente es una fuente de errores común en las aplicaciones React.

Ahora consideremos la versión de este componente que usa _Hooks_:

```
function FriendStatus(props) {
  // ...
  useEffect(() => {
    // ...
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
```

No padece el mismo error. (Aunque tampoco hemos hecho ningún cambio)

No hay un código especial para gestionar las actualizaciones porque `useEffect` las gestiona _por defecto_. Sanea los efectos anteriores antes de aplicar los nuevos. Para ilustrar esto, esta es una secuencia de llamadas de suscripción y cancelación que produciría este componente a lo largo del tiempo:

```
// Se monta con las props { friend: { id: 100 } }
ChatAPI.subscribeToFriendStatus(100, handleStatusChange);     // Ejecuta el primer efecto

// Se actualiza con las props { friend: { id: 200 } }
ChatAPI.unsubscribeFromFriendStatus(100, handleStatusChange); // Sanea el efecto anterior
ChatAPI.subscribeToFriendStatus(200, handleStatusChange);     // Ejecuta el siguiente efecto

// Se actualiza con las props { friend: { id: 300 } }
ChatAPI.unsubscribeFromFriendStatus(200, handleStatusChange); // Sanea el efecto anterior
ChatAPI.subscribeToFriendStatus(300, handleStatusChange);     // Ejecuta el siguiente efecto

// Se desmonta
ChatAPI.unsubscribeFromFriendStatus(300, handleStatusChange); // Sanea el último efecto
```

Este comportamiento asegura la consistencia por defecto y previene errores que son comunes en los componentes de clase debido a la falta de lógica de actualización.

### [](https://es.reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects)Consejo: Omite efectos para optimizar el rendimiento

En algunos casos, sanear o aplicar el efecto después de cada renderizado puede crear problemas de rendimiento. En los componentes de clase podemos solucionarlos escribiendo una comparación extra con `prevProps` o `prevState` dentro de `componentDidUpdate`:

```
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    document.title = `You clicked ${this.state.count} times`;
  }
}
```

Este requerimiento es tan común que está incorporado en la API del _Hook_ `useEffect`. Puedes indicarle a React que _omita_ aplicar un efecto si ciertos valores no han cambiado entre renderizados. Para hacerlo, pasa un array como segundo argumento opcional a `useEffect`:

```jsx
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Solo se vuelve a ejecutar si count cambia
```

En el ejemplo anterior pasamos `[count]` como segundo argumento. ¿Qué significa esto? Si `count` es `5`, y cuando nuestro componente se vuelve a renderizar `count` continúa siendo igual a `5`, React comparará el `[5]` del renderizado anterior con el `[5]` del siguiente renderizado. Dado que todos los elementos en el array (`5 === 5`), React omitirá el efecto. Esa es nuestra optimización.

Cuando renderizamos con `count` actualizado a `6`, React comparará los elementos en el array `[5]` del renderizado anterior con los elementos del array `[6]` del siguente renderizado. En esta ocasión, React volverá a aplicar el efecto dado que `5 !== 6`. Si el array contiene varios elementos, React volverá a ejecutar el efecto si cualquiera de los elementos es diferente.

Esto también funciona para efectos que tienen fase de saneamiento:

```jsx
useEffect(() => {
  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, [props.friend.id]); // Solo se vuelve a suscribir si la propiedad props.friend.id cambia
```

En el futuro, el segundo argumento podría ser añadido automáticamente por una transformación en tiempo de compilación.

> Nota
> 
> Si usas esta optimización, asegúrate de que incluyes **todos los valores del ámbito del componente (como props y estado) que cambien a lo largo del tiempo y que sean usados por el efecto**. De otra forma, tu código referenciará valores obsoletos de renderizados anteriores. Aprende más [cómo tratar con funciones](https://es.reactjs.org/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) y [qué hacer cuando el array cambia con mucha frecuencia](https://es.reactjs.org/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often).
> 
> Si quieres ejecutar un efecto y sanearlo solamente una vez (al montar y desmontar), puedes pasar un array vacío (`[]`) como segundo argumento. Esto le indica a React que el efecto no depende de _ningún_ valor proveniente de las props o el estado, de modo que no necesita volver a ejecutarse. Esto no se gestiona como un caso especial, obedece directamente al modo en el que siempre funciona el array de dependencias.
> 
> Si pasas un array vacío (`[]`), las props y el estado dentro del efecto siempre tendrán sus valores iniciales. Si bien pasar `[]` como segundo argumento se acerca al conocido modelo mental de `componentDidMount` y `componentWillUnmount`, a menudo hay [mejores](https://es.reactjs.org/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) [soluciones](https://es.reactjs.org/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often) para evitar volver a ejecutar los efectos con demasiada frecuencia. Además, no olvides que React pospone la ejecución de `useEffect` hasta que el navegador finaliza el trazado, de modo que hacer algún trabajo extra no es tan problemático.
> 
> Recomendamos usar la regla [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) que forma parte de nuestro paquete [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation). Esta regla advierte cuando las dependencias se especifican incorrectamente y sugiere una solución.

## [](https://es.reactjs.org/docs/hooks-effect.html#next-steps)Próximos pasos

¡Enhorabuena! Esta página ha sido muy larga, pero esperamos que al final la mayoría de tus dudas sobre los efectos hayan sido resueltas. Has aprendido los _Hooks_ de estado y de efecto, y puedes hacer _muchas_ cosas combinándolos. Estos _Hooks_ abarcan la mayoría de casos de uso de las clases. Y en el caso de no ser suficientes, existen [_Hooks_ adicionales](https://es.reactjs.org/docs/hooks-reference.html) que pueden servirte de ayuda.

También hemos empezado a ver cómo los _Hooks_ solucionan problemas esbozados en [Motivación](https://es.reactjs.org/docs/hooks-intro.html#motivation). Hemos visto cómo el saneamiento de efectos evita la duplicidad en `componentDidUpdate` y `componentWillUnmount`, consolidando el código asociado y ayudándonos a evitar errores. Además hemos visto cómo podemos separar efectos por su propósito, que era algo que no podíamos hacer con clases.

Llegados a este punto puedes estar preguntándote cómo funcionan los _Hooks_. ¿Cómo puede saber React qué llamada a `useState` corresponde a qué variable de estado entre renderizados? ¿Cómo identifica React los efectos anteriores y posteriores en cada actualización? **En la siguiente página aprenderemos las [reglas de los _Hooks_](https://es.reactjs.org/docs/hooks-rules.html), las cuales son esenciales para que funcionen correctamente.**