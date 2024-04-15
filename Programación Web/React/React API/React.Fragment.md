El componente `React.Fragment` permite retornar elementos múltiples en un método de `render()` sin crear un elemento DOM adicional:

```
render() {
  return (
    <React.Fragment>
      Some text.
      <h2>A heading</h2>
    </React.Fragment>
  );
}
```

También se puede usar con la sintaxis abreviada `<></>`. Para más información, ver [React v16.2.0: Soporte mejorado para fragmentos](https://es.reactjs.org/blog/2017/11/28/react-v16.2.0-fragment-support.html).