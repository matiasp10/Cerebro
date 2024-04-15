```jsx
React.createElement(
  type,
  [props],
  [...children]
)
```

Crea y retorna un nuevo [elemento React](https://es.reactjs.org/docs/rendering-elements.html) del tipo dado. El tipo del argumento puede ser ya sea un string de nombre de etiqueta (tales como `'div'` o `'span'`), un tipo de [componente React](https://es.reactjs.org/docs/components-and-props.html) (una clase o una función), o un tipo de [fragmento React](https://es.reactjs.org/docs/react-api.html#reactfragment) .

El código escrito con [JSX](https://es.reactjs.org/docs/introducing-jsx.html) será convertido para usar `React.createElement()`. Normalmente no se invocará `React.createElement()` directamente si se está usando JSX. Para aprender más, ver [React Sin JSX](https://es.reactjs.org/docs/react-without-jsx.html).