```
componentDidUpdate(prevProps, prevState, snapshot)
```

`componentDidUpdate()` se invoca inmediatamente después de que la actualización ocurra. Este método no es llamado para el renderizador inicial.

Use esto como una oportunidad para operar en DOM cuando el componente se haya actualizado. Este es también un buen lugar para hacer solicitudes de red siempre y cuando compare los accesorios actuales con los anteriores (por ejemplo, una solicitud de red puede no ser necesaria si las props no han cambiado).

```
componentDidUpdate(prevProps) {
  // Uso tipico (no olvides de comparar las props):
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

**Puedes llamar `setState()` inmediatamente** en `componentDidUpdate()` pero ten en cuenta que **debe ser envuelto en una condición** como en el ejemplo anterior, o causará un bucle infinito. También causaría una renderización adicional que, aunque no sea visible para el usuario, puede afectar el rendimiento del componente. Si estás intentando crear un “espejo” desde un estado a una prop que viene desde arriba, considera usar la prop directamente en su lugar. Lee más sobre [por qué copiar props en el estado causa errores](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html).

Si tu componente implementa el ciclo de vida `getSnapshotBeforeUpdate()`(que es raro), el valor que devuelve se pasará como un tercer parámetro “snapshot” a `componentDidUpdate()`. De lo contrario, este parámetro será indefinido.

> Nota
> 
> `componentDidUpdate()` no será invocado si [`shouldComponentUpdate()`](https://es.reactjs.org/docs/react-component.html#shouldcomponentupdate) devuelve falso.