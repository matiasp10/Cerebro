```jsx
static getDerivedStateFromProps(props, state)
```

`getDerivedStateFromProps` se invoca justo antes de llamar al método de render, tanto en la montura inicial como en las actualizaciones posteriores. Debes devolver un objeto para actualizar el estado, o `null` para no actualizar nada.

Este método existe para [casos de uso raros](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#when-to-use-derived-state) donde el estado depende de los cambios en props con el tiempo. Por ejemplo, puede ser util para implementar un componente `<Transition>` que compare su anterior hijo y el siguiente para decidir cual de los dos animar en la entrada y salida.

Derivar el estado conduce al código verboso y hace que tus componentes sean difíciles de pensar. [Asegúrate de que estás familiarizado con alternativas más simples](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html)

-   Si necesitas **realizar un efecto secundario** (por ejemplo, obtención de datos o animaciones) en una respuesta debido a un cambio en las props, utiliza [`componentDidUpdate`](https://es.reactjs.org/docs/react-component.html#componentdidupdate).
-   Si quieres **recalcular algunos datos solo cuando una prop cambie**,[usa memoization](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#what-about-memoization).
-   Si quieres **restablecer algún estado cuando una prop cambie** considera hacer un [completamente controlado](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#recommendation-fully-controlled-component) o [un componente no controlado con una `key`](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#recommendation-fully-uncontrolled-component-with-a-key).

Este método no tiene acceso a la instancia del componente. Si quieres, puedes reutilizar algún código entre `getDerivedStateFromProps()` y los otros métodos de clase mediante la extracción de funciones puras de las props del componente y el estado fuera de la definición de clase.

Ten en cuenta que este método se activa en _cada_ renderizado, independientemente de la causa. En caso contrario, `UNSAFE_componentWillReceiveProps`, que sólo se dispara cuando el padre causa un nuevo renderizado y no como resultado de un `setState` local.