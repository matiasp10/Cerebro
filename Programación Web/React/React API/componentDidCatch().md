```
componentDidCatch(error, info)
```

Este ciclo de vida se invoca después de que un error haya sido lanzado por un componente descendiente. Recibe dos parámetros:

1.  `error` - Es un error que ha sido lanzado.
2.  `info`- Un objeto con una clave`componentStack` contiene [información sobre que componente ha devuelto un error](https://es.reactjs.org/docs/error-boundaries.html#component-stack-traces).

`componentDidCatch()`se llama durante la fase “commit”, por lo tanto, los efectos secundarios se permiten. Debería utilizarse para cosas como errores de registro:

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Actualiza el state, así el siguiente renderizado lo mostrará en la IU.
    return { hasError: true };
  }

  componentDidCatch(error, info) {    // Ejemplo "componentStack":    //   in ComponentThatThrows (created by App)    //   in ErrorBoundary (created by App)    //   in div (created by App)    //   in App    logComponentStackToMyService(info.componentStack);  }
  render() {
    if (this.state.hasError) {
      // Puedes renderizar una interfaz de usuario customizada
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

Los compilados de producción y desarrollo de React difieren ligeramente en la forma en que `componentDidCatch` maneja los errores.

En desarrollo, los errores subirán hacia `window`, esto significa que cualquier `window.onerror` o `window.addEventListener('error', callback)` interceptará los errores que han sido atrapados por `componentDitCatch`.

En producción, en cambio, los errores no subirán, lo que significa que cualquier manejador de errores ancestro solo recibirá errores que no hayan sido explícitamente atrapados por `componentDidCatch()`.

> Nota
> 
> En el evento de un error, puedes renderizar una interfaz de usuario con `componentDidCatch()` llamando a `setState()`, pero esto estará obsoleto en una futura versión. Usa `static getDerivedStateFromError()` para controlar el plan de renderizado.