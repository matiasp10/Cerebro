```jsx
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

Una alternativa a [`useState`](https://es.reactjs.org/docs/hooks-reference.html#usestate). Acepta un reducer de tipo `(state, action) => newState` y devuelve el estado actual emparejado con un método `dispatch`. (Si está familiarizado con Redux, ya sabe cómo funciona).

`useReducer` a menudo es preferible a `useState` cuando se tiene una lógica compleja que involucra múltiples subvalores o cuando el próximo estado depende del anterior. `useReducer` además te permite optimizar el rendimiento para componentes que activan actualizaciones profundas, porque [puedes pasar hacia abajo `dispatch` en lugar de _callbacks_](https://es.reactjs.org/docs/hooks-faq.html#how-to-avoid-passing-callbacks-down).

Aquí está el ejemplo del contador de la sección [`useState`], reescrito para usar un reductor:

```jsx
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

> Nota
> 
> React garantiza que la identidad de la función `dispatch` es estable y no cambiará en subsecuentes renderizados. Es por eso que es seguro omitirla de la lista de dependencias de `useEffect` o `useCallback`.

#### Especificar el estado inicial

Hay dos formas diferentes de inicializar el estado de `useReducer`. Puedes elegir uno u otro dependiendo de tu caso. La forma más simple para pasar el estado inicial es como un segundo argumento:

```jsx
  const [state, dispatch] = useReducer(
    reducer,
    {count: initialCount}
  );
```

> Nota
> 
> React no utiliza la convención del argumento `state = initialState` popularizada por Redux. El valor inicial a veces necesita tener una dependencia en las props y por lo tanto tanto se especifica en la llamada al Hook. Si te parece muy importante, puedes llamar a `useReducer(reducer, undefined, reducer)` para emular el comportamiento de Redux, pero no se recomienda

#### Inicialización diferida

También puedes crear el estado inicial de manera diferida. Para hacerlo, le puedes pasar una función `init` como tercer argumento. El estado inicial será establecido como `init(initialArg)`.

Esto te permite extraer la lógica para calcular el estado inicial fuera del reductor. También es útil para reiniciar el estado luego en respuesta a una acción:

```jsx
function init(initialCount) {
  return {count: initialCount};
}

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    case 'reset':
      return init(action.payload);
    default:
      throw new Error();
  }
}

function Counter({initialCount}) {
  const [state, dispatch] = useReducer(reducer, initialCount, init);
  return (
    <>
      Count: {state.count}
      <button
        onClick={() => dispatch({type: 'reset', payload: initialCount})}>
        Reset
      </button>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

#### Evitar un _dispatch_

Si devuelves el mismo valor del estado actual desde un Hook reductor, React evitará renderizar los hijos y disparar efectos. (React utiliza el [algoritmo de comparación `Object.is`](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object/is#Description)).

Ten en cuenta que React podría aún necesitar renderizar nuevamente ese componente específico antes de evitar el renderizado. Esto no debería ser una preocupación ya que React no va “más adentro” del árbol de forma innecesaria. Si estás haciendo cálculos muy costosos mientras renderizas, puedes optimizarlos con `useMemo`.