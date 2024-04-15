```jsx
componentDidMount()
```

`componentDidMount()` se invoca inmediatamente después de que un componente se monte (se inserte en el árbol). La inicialización que requiere nodos DOM debería ir aquí. Si necesita cargar datos desde un punto final remoto, este es un buen lugar para instanciar la solicitud de red.

Este método es un buen lugar para establecer cualquier suscripción. Si lo haces, no olvides darle de baja en `componentWillUnmount()`.

**Puedes llamar `setState()` inmediatamente** en `componentDidMount()`. Se activará un renderizado extra, pero sucederá antes de que el navegador actualice la pantalla. Esto garantiza que, aunque en este caso se invocará dos veces el `render()`, el usuario no verá el estado intermedio. Utiliza este patrón con precaución porque a menudo causa problemas de rendimiento. En la mayoría de los casos, deberías ser capaz de asignar el estado inicial en el `constructor()` en su lugar. Sin embargo, puede ser necesario para casos como modales y tooltips cuando se necesita medir un nodo DOM antes de representar algo que depende de su tamaño o posición.