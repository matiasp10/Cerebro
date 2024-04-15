```
React.createFactory(type)
```

Retorna una función que produce elementos React de un tipo dado. Como [`React.createElement()`](https://es.reactjs.org/docs/react-api.html#createElement), el tipo del argumento puede ser un string de nombre de etiqueta (como `'div'` o `'span'`), un tipo de [componente React](https://es.reactjs.org/docs/components-and-props.html) (una clase o una función) o un [fragmento React](https://es.reactjs.org/docs/react-api.html#reactfragment).

Este auxiliar es considerado antiguo y en su lugar fomentamos el uso de JSX o de `React.createElement()`.

Normalmente no se invocará `React.createFactory()` directamente si se está usando JSX. Para aprender más, ver [React sin JSX](https://es.reactjs.org/docs/react-without-jsx.html).