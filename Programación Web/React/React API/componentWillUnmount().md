```
componentWillUnmount()
```

`componentWillUnmount()` se invoca inmediatamente antes de desmontar y destruir un componente. Realiza las tareas de limpieza necesarias en este método, como la invalidación de temporizadores, la cancelación de solicitudes de red o la eliminación de las suscripciones que se crearon en `componentDidMount()`.

**No debes llamar `setState()`** en `componentWillUnmount()` porque el componente nunca será vuelto a renderizar. Una vez que una instancia de componente sea desmontada, nunca será montada de nuevo.