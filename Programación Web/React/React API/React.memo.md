```jsx
const MyComponent = React.memo(function MyComponent(props) {
  /* renderiza usando props */
});
```

`React.memo` es un [componente de orden superior](https://es.reactjs.org/docs/higher-order-components.html).

Si el componente renderiza el mismo resultado dadas las mismas props, se puede envolver en una llamada a `React.memo` para una mejora en el desempeño en algunos casos memoizando el resultado. Esto significa que React omitirá renderizar el componente y reusará el último resultado renderizado.

`React.memo` solamente verifica los cambios en las props. Si tu componente de función envuelto en `React.memo` tiene un Hook [`useState`](https://es.reactjs.org/docs/hooks-state.html), [`useReducer`](https://es.reactjs.org/docs/hooks-reference.html#usereducer) o [`useContext`](https://es.reactjs.org/docs/hooks-reference.html#usecontext) en su implementación, continuará volviéndose a renderizar cuando el estado o el contexto cambien.

Por defecto solo comparará superficialmente objetos complejos en el objeto de props. Si se desea controlar la comparación, se puede proporcionar también una función de comparación personalizada como el segundo argumento.

```jsx
function MyComponent(props) {
  /* renderiza usando props */
}
function areEqual(prevProps, nextProps) {
  /*
  retorna true si al pasar los nextProps a renderizar retorna
  el mismo resultado que al pasar los prevProps a renderizar,
  de otro modo retorna false
  */
}
export default React.memo(MyComponent, areEqual);
```

Este método solamente existe como una **[optimización del desempeño](https://es.reactjs.org/docs/optimizing-performance.html).** No dependas de ello para “evitar” un renderizado, ya que puede conducir a errores.

> Nota
> 
> A diferencia del método [`shouldComponentUpdate()`](https://es.reactjs.org/docs/react-component.html#shouldcomponentupdate) en los componentes de clases, la función `areEqual` retorna `true` si los props son iguales y `false` si los props no son iguales. Esto es lo opuesto a `shouldComponentUpdate`.