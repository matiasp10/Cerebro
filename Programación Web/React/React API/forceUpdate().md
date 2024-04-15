```
component.forceUpdate(callback)
```

Por defecto, cuando el componente de tu estado o accesorio cambia, tu componente re-renderizará. Si tu método `render()` depende de algunos otros datos, puedes decirle a React que el componente necesita re-renderizado llamando a `forceUpdate()`.

Llamar a `forceUpdate()` causará que `render()` sea llamado en el componente, saltando `shouldComponentUpdate()`. Esto activará los métodos de ciclo de vida normales para los componentes hijos, incluyendo el método `shouldComponentUpdate()` de cada hijo. React solo actualizará el DOM si el marcado cambia.

Normalmente, debes intentar evitar todos los usos de `forceUpdate()` y solo leer desde `this.props` y `this.state` en `render()`.