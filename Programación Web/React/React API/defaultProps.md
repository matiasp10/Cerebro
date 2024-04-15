`defaultProps` puede ser definida como una propiedad en la propia clase de componente, para establecer las props predeterminadas para la clase. Esto se utiliza para props con valor `undefined`, pero no para props con valor `null`. Por ejemplo:

```jsx
class CustomButton extends React.Component {
  // ...
}

CustomButton.defaultProps = {
  color: 'blue'
};
```

Si no se proporciona `props.color`, se establecerá por defecto a `'blue'`:

```jsx
  render() {
    return <CustomButton /> ; // props.color será asignada a azul
  }
```

Si `props.color` es `null`, permanecerá `null`:

```jsx
  render() {
    return <CustomButton color={null} /> ; // props.color se mantendrá en null
  }
```