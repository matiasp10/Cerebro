```
setState(updater[, callback])
```

`setState()` hace cambios al estado del componente y le dice a React que este componente y sus elementos secundarios deben volverse a procesar con el estado actualizado. Este es el método principal que utiliza para actualizar la interfaz de usuario en respuesta a los manejadores de eventos y las respuestas del servidor.

Considera `setState()` como una _solicitud_ en lugar de un comando para actualizar el componente. Para que se perciba un mejor rendimiento, React puede retrasarlo, y luego actualizar varios componentes en una sola pasada. En el caso inusual que necesites forzar a que la actualización del DOM se aplique de manera síncrona, puedes envolverlo en [`flushSync`](https://es.reactjs.org/docs/react-dom.html#flushsync), pero esto puede afectar el rendimiento.

`setState()` no siempre actualiza inmediatamente el componente. Puede procesar por lotes o diferir la actualización hasta más tarde. Esto hace que leer `this.state` después de llamar a `setState()` sea una trampa potencial. En su lugar, usa `componentDidUpdate` o un callback `setState` (`setState(updater, callback)`), se garantiza que cualquiera de los dos se activará una vez la actualización haya sido aplicada. Si necesitas establecer el estado en función del estado anterior, lee a continuación sobre el argumento `updater`.

`setState()` siempre llevará al re-renderizado a menos que `shouldComponentUpdate()` devuelva `false`. Si se usan objetos mutables y no se puede implementar la lógica de representación condicional en `shouldComponentUpdate()`, llamar a `setState()` solo cuando el nuevo estado difiera del estado anterior evitará re-renderizados innecesarios.

El primer argumento es una función `updater` con la firma:

```jsx
(state, props) => stateChange
```

`state` es una referencia al estado del componente en el momento en que se está aplicando el cambio. No debería ser mutado directamente. En cambio, los cambios deberían ser representados construyendo un nuevo objeto basado en la entrada de `prevState` y `props`. Por ejemplo, supongamos que quisiéramos incrementar un valor en el estado por `props.step`:

```jsx
this.setState((state, props) => {
  return {counter: state.counter + props.step};
});
```

Ambos `state` y `props` recibidos por la función de actualizador están garantizados de estar actualizados. La salida del actualizador se fusiona de forma superficial (_shallow_) con `state`.

El segundo parámetro para `setState()` es una devolución de llamada opcional que será ejecutada una vez `setState` sea completada y el componente sea re-renderizado. Generalmente recomendamos usar `componentDidUpdate()` para dicha lógica.

Opcionalmente puedes pasar un objeto como el primer argumento a `setState()` en lugar de una función:

```jsx
setState(stateChange[, callback])
```

Esto realiza una combinación superficial de `stateChange` en el nuevo estado, por ejemplo, para ajustar una cantidad de elementos del carrito de compras:

```jsx
this.setState({quantity: 2})
```

Esta forma de `setState()` también es asincrónica, y varias llamadas durante el mismo ciclo pueden agruparse juntas. Por ejemplo, si intentas aumentar la cantidad de un articulo mas de una vez en el mismo ciclo, resultará en el equivalente de:

```jsx
Object.assign(
  previousState,
  {quantity: state.quantity + 1},
  {quantity: state.quantity + 1},
  ...
)
```

Las llamadas posteriores anularán los valores de llamadas anteriores en el mismo ciclo, por lo que la cantidad solo se incrementará una vez. Si el siguiente estado depende del estado actual, recomendamos utilizar una actualizador a través de una función formulario.

```jsx
this.setState((state) => {
  return {quantity: state.quantity + 1};
});
```

Para más detalles, visite:

-   [Guía: Estado y ciclo de vida](https://es.reactjs.org/docs/state-and-lifecycle.html)
-   [En profundidad: ¿Cuándo y por qué las llamadas de `setState()` se hacen en lotes?](https://stackoverflow.com/a/48610973/458193)
-   [En profundidad: ¿Por qué `this.state` no se actualiza inmediatamente?](https://github.com/facebook/react/issues/11527#issuecomment-360199710)