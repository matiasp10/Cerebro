```
static getDerivedStateFromError(error)
```

Este ciclo de vida se invoca después de que un error haya sido lanzado por un componente descendiente. Recibe el error que fue lanzado como parámetro y debe devolver un valor para actualizar el estado.

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {    // Actualiza el state, así el siguiente renderizado lo mostrará en la IU.    return { hasError: true };  }
  render() {
    if (this.state.hasError) {      // Puedes renderizar cualquier interfaz de usuario diferente      return <h1>Something went wrong.</h1>;    }
    return this.props.children;
  }
}
```

> Nota
> 
> `getDerivedStateFromError()` se llama durante la fase “render”, por lo que los efectos secundarios no están permitidos. Para estos casos de uso, use `componentDidMount()` en su lugar.