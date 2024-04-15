```
getSnapshotBeforeUpdate(prevProps, prevState)
```

`getSnapshotBeforeUpdate()` se invoca justo antes de que la salida renderizada más reciente se entregue, por ejemplo, al DOM. Permite al componente capturar cierta información del DOM (por ejemplo, la posición del scroll) antes de que potencialmente se cambie. Cualquier valor que se devuelva en este método de ciclo de vida se pasará como parámetro a `componentDidUpdate()`.

Este caso de uso no es común, pero puede ourrir en IUs como un hilo de chat que necesita manejar la posición del scroll de manera especial.

Debe devolverse un valor instantáneo (o `null`).

Por ejemplo:

```jsx
class ScrollingList extends React.Component {
  constructor(props) {
    super(props);
    this.listRef = React.createRef();
  }

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // ¿Estamos agregando nuevos elementos a la lista?
    // Captura la posición del scroll para que podamos ajustar el scroll después.
    if (prevProps.list.length < this.props.list.length) {
      const list = this.listRef.current;
      return list.scrollHeight - list.scrollTop;
    }
    return null;
  }

  componentDidUpdate(prevProps, prevState, snapshot) {
    // Si tenemos un valor snapshot, agregamos nuevos elementos
    // Ajusta el scroll para que los nuevos elementos no empujen a los viejos fuera de la vista
    // (snapshot aquí es el valor que regresa de getSnapshotBeforeUpdate)
    if (snapshot !== null) {
      const list = this.listRef.current;
      list.scrollTop = list.scrollHeight - snapshot;
    }
  }

  render() {
    return (
      <div ref={this.listRef}>{/* ...contents... */}</div>
    );
  }
}
```

En los ejemplos anteriores, es importante leer la propiedad `scrollHeight` en `getSnapshotBeforeUpdate` porque puede haber retrasos entre los ciclos de vida de la fase “render” (como `render`) y los ciclos de fase de “commit” (como `getSnapshotBeforeUpdate` y `componentDidUpdate`).