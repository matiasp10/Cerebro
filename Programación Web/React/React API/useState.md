```
const [state, setState] = useState(initialState);
```

Devuelve un valor con estado y una función para actualizarlo.

Durante el renderizado inicial, el estado devuelto (`state`) es el mismo que el valor pasado como primer argumento (`initialState`).

La función `setState` se usa para actualizar el estado. Acepta un nuevo valor de estado y sitúa en la cola una nueva renderización del componente.

```
setState(newState);
```

En las renderizaciones siguientes, el primer valor devuelto por `useState` será siempre el estado más reciente después de aplicar las actualizaciones.

> Nota
> 
> React garantiza que la identidad de la función `setState` es estable y no cambiará en subsecuentes renderizados. Es por eso que es seguro omitirla de la lista de dependencias de `useEffect` o `useCallback`.

#### Actualizaciones funcionales

Si el nuevo estado se calcula utilizando el estado anterior, puede pasar una función a `setState`. La función recibirá el valor anterior y devolverá un valor actualizado. Aquí hay un ejemplo de un componente contador que usa ambas formas de `setState`:

```jsx
function Counter({initialCount}) {
  const [count, setCount] = useState(initialCount);
  return (
    <>
      Count: {count}
      <button onClick={() => setCount(initialCount)}>Reset</button>
      <button onClick={() => setCount(prevCount => prevCount - 1)}>-</button>
      <button onClick={() => setCount(prevCount => prevCount + 1)}>+</button>
    </>
  );
}
```

Los botones ”+” y ”-” usan la forma funcional, porque el valor actualizado se basa en el valor anterior. Pero el botón “Reset” usa la forma normal, porque siempre vuelve a establecer la cuenta al valor inicial.

Si tu función de actualización retorna el mismo valor que el valor del estado actual, el renderizado subsecuente será omitido completamente.

> Nota
> 
> A diferencia del método `setState` que se encuentra en los componentes de la clase,`useState` no combina automáticamente los objetos. Puede replicar este comportamiento combinando la función de actualizador de función con la sintaxis de propagación de objetos:

```jsx
const [state, setState] = useState({});
setState(prevState => {
  // Object.assign también funcionaría
  return {...prevState, ...updatedValues};
});
```

> Otra opción es `useReducer`, que es más adecuada para administrar objetos de estado que contienen múltiples subvalores.

#### Inicialización gradual

El argumento `initialState` es el estado utilizado durante el render inicial. En renderizados posteriores, se ignora. Si el estado inicial es el resultado de un cálculo costoso, puede proporcionar una función en su lugar, que se ejecutará solo en el render inicial:

```jsx
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```

#### Evitar una actualización del estado

Si se actualiza un Hook de estado con el mismo valor que el estado actual, React evitará renderizar los hijos y disparar los efectos. (React utiliza el [algoritmo de comparación `Object.is`](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Objetos_globales/Object/is#Description)).

Recuerda que React puede necesitar renderizar de nuevo ese componente en específico antes de evitarlo. Esto no debería ser un problema ya que React no irá innecesariamente “más profundo” en el árbol. Si estás realizando cálculos costosos mientras renderizas, puedes optimizarlos con `useMemo`.

#### Batching of state updates

React may group several state updates into a single re-render to improve performance. Normally, this improves performance and shouldn’t affect your application’s behavior.

Before React 18, only updates inside React event handlers were batched. Starting with React 18, [batching is enabled for all updates by default](https://es.reactjs.org/blog/2022/03/08/react-18-upgrade-guide.html#automatic-batching). Note that React makes sure that updates from several _different_ user-initiated events — for example, clicking a button twice — are always processed separately and do not get batched. This prevents logical mistakes.

In the rare case that you need to force the DOM update to be applied synchronously, you may wrap it in [`flushSync`](https://es.reactjs.org/docs/react-dom.html#flushsync). However, this can hurt performance so do this only where needed.