Los _Hooks_ son una nueva incorporación en React 16.8. Te permiten usar estado y otras características de React sin escribir una clase.

Los Hooks son [compatibles con versiones anteriores](https://es.reactjs.org/docs/hooks-intro.html#no-breaking-changes). Esta página proporciona una descripción general de Hooks para usuarios experimentados de React. Esta es una rápida mirada. Si te confundes, busca un recuadro amarillo como este:

> Explicación Detallada
> 
> Lee la [Motivación](https://es.reactjs.org/docs/hooks-intro.html#motivation) para entender por qué estamos introduciendo Hooks a React.

**↑↑↑ Cada sección termina con un recuadro amarillo como este.** Ellos vinculan a explicaciones detalladas.

## 📌 Hook de estado

Este ejemplo renderiza un contador. Cuando haces click en el botón, incrementa el valor:

```jsx
import React, { useState } from 'react';
function Example() {
  // Declara una nueva variable de estado, que llamaremos "count".  const [count, setCount] = useState(0);
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

Aquí, `useState` es un _Hook_ (hablaremos de lo que esto significa en un momento). Lo llamamos dentro de un componente de función para agregarle un estado local. React mantendrá este estado entre re-renderizados. `useState` devuelve un par: el valor de estado _actual_ y una función que le permite actualizarlo. Puedes llamar a esta función desde un controlador de eventos o desde otro lugar. Es similar a `this.setState` en una clase, excepto que no combina el estado antiguo y el nuevo. (Mostraremos un ejemplo comparando `useState` con `this.state` en [Usando el Hook de estado](https://es.reactjs.org/docs/hooks-state.html)).

El único argumento para `useState` es el estado inicial. En el ejemplo anterior, es `0` porque nuestro contador comienza desde cero. Ten en cuenta que a diferencia de `this.state`, el estado aquí no tiene que ser un objeto — aunque puede serlo si quisieras. El argumento de estado inicial solo se usa durante el primer renderizado.

#### Declarando múltiples variables de estado

Puedes usar el Hook de estado más de una vez en un mismo componente:

```jsx
function ExampleWithManyStates() {
  // Declarar múltiple variables de estado!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

La sintaxis de [desestructuración de un array](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Operadores/Destructuring_assignment) nos permite dar diferentes nombres a las variables de estado que declaramos llamando a `useState`. Estos nombres no forman parte de la API `useState`. En su lugar, React asume que si llamas a `useState` muchas veces, lo haces en el mismo orden durante cada renderizado. Volveremos a explicar por qué esto funciona y cuándo será útil más adelante.

#### ¿Pero qué es un Hook?

Los Hooks son funciones que te permiten “enganchar” el estado de React y el ciclo de vida desde componentes de función. Los hooks no funcionan dentro de las clases — te permiten usar React sin clases. ([No recomendamos](https://es.reactjs.org/docs/hooks-intro.html#gradual-adoption-strategy) reescribir tus componentes existentes de la noche a la mañana, pero puedes comenzar a usar Hooks en los nuevos si quieres).

React proporciona algunos Hooks incorporados como `useState`. También puedes crear tus propios Hooks para reutilizar el comportamiento con estado entre diferentes componentes. Primero veremos los Hooks incorporados.

> Explicación Detallada
> 
> Puedes aprender más sobre el Hook de estado en la página dedicada: [Usando el Hook de estado](https://es.reactjs.org/docs/hooks-state.html).

## ⚡️ Hook de efecto {#️effect-hook}

Es probable que hayas realizado recuperación de datos, suscripciones o modificación manual del DOM desde los componentes de React. Llamamos a estas operaciones “efectos secundarios” (o “efectos” para abreviar) porque pueden afectar a otros componentes y no se pueden hacer durante el renderizado.

El Hook de efecto, `useEffect`, agrega la capacidad de realizar efectos secundarios desde un componente de función. Tiene el mismo propósito que `componentDidMount`,`componentDidUpdate` y `componentWillUnmount` en las clases React, pero unificadas en una sola API. (Mostraremos ejemplos comparando `useEffect` con estos métodos en [Usando el Hook de efecto](https://es.reactjs.org/docs/hooks-effect.html)).

Por ejemplo, este componente establece el título del documento después de que React actualiza el DOM:

```jsx
import React, { useState, useEffect } from 'react';
function Example() {
  const [count, setCount] = useState(0);

  // Similar a componentDidMount y componentDidUpdate:  useEffect(() => {    // Actualiza el título del documento usando la Browser API    document.title = `You clicked ${count} times`;  });
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

Cuando llamas a `useEffect`, le estás diciendo a React que ejecute tu función de “efecto” después de vaciar los cambios en el DOM. Los efectos se declaran dentro del componente para que tengan acceso a sus props y estado. De forma predeterminada, React ejecuta los efectos después de cada renderizado — _incluyendo_ el primer renderizado. (Hablaremos más sobre cómo se compara esto con los ciclos de vida de una clase en [Usando el Hook de efecto](https://es.reactjs.org/docs/hooks-effect.html)).

Los efectos también pueden especificar opcionalmente cómo “limpiar” después de ellos devolviendo una función. Por ejemplo, este componente utiliza un efecto para suscribirse al estado en línea de un amigo, y se limpia al anular su suscripción:

```jsx
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);    return () => {      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);    };  });
  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

En este ejemplo, React cancelará la suscripción de nuestra `ChatAPI` cuando se desmonte el componente, así como antes de volver a ejecutar el efecto debido a un renderizado posterior. (Si prefieres, hay una manera de [decirle a React que omita la re-suscripcion](https://es.reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects) si el `props.friend.id` que pasamos a la `ChatAPI` no ha cambiado).

Al igual que con `useState`, puedes usar más de un solo efecto en un componente:

```jsx
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }
  // ...
```

Los Hooks te permiten organizar efectos secundarios en un componente según qué partes están relacionadas (como agregar y eliminar una suscripción), en lugar de forzar una división basada en métodos del ciclo de vida.

> Explicación detallada
> 
> Puede obtener más información sobre `useEffect` en la página dedicada: [Usando el Hook de efecto](https://es.reactjs.org/docs/hooks-effect.html).

## ✌️ Reglas de Hooks {#️rules-of-hooks}

Los Hooks son funciones de JavaScript, pero imponen dos reglas adicionales:

-   Solo llamar Hooks **en el nivel superior**. No llames Hooks dentro de loops, condiciones o funciones anidadas.
-   Solo llamar Hooks **desde componentes de función de React**. No llames Hooks desde las funciones regulares de JavaScript. (Solo hay otro lugar válido para llamar Hooks: tus propios Hooks personalizados. En un momento aprenderemos sobre estos).

Proporcionamos un [plugin de linter](https://www.npmjs.com/package/eslint-plugin-react-hooks) para forzar estas reglas automáticamente. Entendemos que estas reglas pueden parecer limitantes o confusas al principio, pero son esenciales para hacer que los Hooks funcionen bien.

> Explicación Detallada
> 
> Puedes aprender más sobre estas reglas en la página dedicada: [Reglas de Hooks](https://es.reactjs.org/docs/hooks-rules.html).

## 💡 Construyendo tus propios Hooks

A veces, queremos reutilizar alguna lógica de estado entre componentes. Tradicionalmente, había dos soluciones populares para este problema: [componente de orden superior](https://es.reactjs.org/docs/higher-order-components.html) y [render props](https://es.reactjs.org/docs/render-props.html). Los Hooks personalizados te permiten hacer esto, pero sin agregar más componentes a tu árbol.

Anteriormente en esta página, presentamos un componente `FriendStatus` que llama a los Hooks `useState` y `useEffect` para suscribirse al estado en línea de un amigo. Digamos que también queremos reutilizar esta lógica de suscripción en otro componente.

Primero, extraeremos esta lógica en un Hook personalizado llamado `useFriendStatus`:

```jsx
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

Toma `friendID` como argumento, y retorna si nuestro amigo está en línea o no.

Ahora lo podemos usar desde ambos componentes:

```jsx
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);
  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

```jsx
function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);
  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```

El estado de cada componente es completamente independiente. Los Hooks son una forma de reutilizar _la lógica de estado_, no el estado en sí. De hecho, cada _llamada_ a un Hook tiene un estado completamente aislado — por lo que incluso puedes usar el mismo Hook personalizado dos veces en un componente.

Los Hooks personalizados son más una convención que una funcionalidad. Si el nombre de una función comienza con ”`use`” y llama a otros Hooks, decimos que es un Hook personalizado. La convención de nomenclatura `useSomething` es cómo nuestro plugin de linter puede encontrar errores en el código usando Hooks.

Puedes escribir Hooks personalizados que cubran una amplia gama de casos de uso como manejo de formularios, animación, suscripciones declarativas, temporizadores y probablemente muchos más que no hemos considerado. Estamos muy entusiasmados de ver los Hooks personalizados que la comunidad de React creará.

> Explicación Detallada
> 
> Puedes aprender más sobre Hooks personalizados en la página dedicada: [Construyendo Tus Propios Hooks](https://es.reactjs.org/docs/hooks-custom.html).

## 🔌 Otros Hooks

Hay algunos Hooks incorporados de uso menos común que pueden resultarte útiles. Por ejemplo, [`useContext`](https://es.reactjs.org/docs/hooks-reference.html#usecontext) te permite suscribirte al contexto React sin introducir el anidamiento:

```jsx
function Example() {
  const locale = useContext(LocaleContext);  const theme = useContext(ThemeContext);  // ...
}
```

Y [`useReducer`](https://es.reactjs.org/docs/hooks-reference.html#usereducer) te permite manejar el estado local de componentes complejos con un reducer:

```jsx
function Todos() {
  const [todos, dispatch] = useReducer(todosReducer);  // ...
```

> Explicación Detallada
> 
> Puedes aprender más sobre todos los Hooks incorporados en la página dedicada: [Referencia de la Hooks API](https://es.reactjs.org/docs/hooks-reference.html).

## Próximos pasos

¡Uf, eso fue rápido! Si algunas cosas no tienen mucho sentido o si te gustaría aprender más en detalle, puedes leer las siguientes páginas, comenzando con la documentación de [Hook de estado](https://es.reactjs.org/docs/hooks-state.html).

También puede consultar la [Referencia de la Hooks API](https://es.reactjs.org/docs/hooks-reference.html) y las [Preguntas Frecuentes sobre Hooks](https://es.reactjs.org/docs/hooks-faq.html).

Finalmente, no dejes de visitar la [página de introducción](https://es.reactjs.org/docs/hooks-intro.html) que explica _por qué_ estamos agregando Hooks y cómo comenzaremos a usarlos junto a las clases — sin volver a escribir nuestras aplicaciones.