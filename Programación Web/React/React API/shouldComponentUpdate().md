```
shouldComponentUpdate(nextProps, nextState)
```

Usa `shouldComponentUpdate()` para avisar a React si la salida de un componente no se ve afectada por el cambio actual en el estado o los accesorios. El comportamiento predeterminado es volver a procesar cada cambio de estado y, en la gran mayoría de los casos, debe confiar en el comportamiento predeterminado.

`shouldComponentUpdate()` es invocado antes de renderizar cuando los nuevos accesorios o el estado están siendo recibidos. Por defecto es `true`. Este método no es llamado para el renderizado inicial o cuando `forceUpdate()` es usado.

Este método sólo existe como **[optimización de rendimiento](https://es.reactjs.org/docs/optimizing-performance.html).** No confíes en él para “prevenir” un renderizado, ya que esto puede conducir a errores. **Considere usar el componente integrado [`PureComponent`](https://es.reactjs.org/docs/react-api.html#reactpurecomponent)** en lugar de escribir `shouldComponentUpdate()` a mano. `PureComponent` realiza una comparación superficial de props y estado, y reduce la posibilidad de saltar una actualización necesaria.

Si estás seguro de querer escribirlo a mano, puedes comparar `this.props` con `nextProps` y `this.state` con `nextState` y devolver `false` para indicar a React que se puede omitir la actualización. Devolver `false` no previene a los componentes hijos de volverse a renderizar cuando _su_ estado cambia.

No recomendamos realizar comprobaciones de igualdad profundas ni utilizar `JSON.stringify()` en `shouldComponentUpdate()`. Es muy ineficiente y dañará el rendimiento.

Actualmente, si `shouldComponentUpdate()` devuelve `false`, entonces [`componentWillUpdate()`](https://es.reactjs.org/docs/react-component.html#unsafe_componentwillupdate), [`render()`](https://es.reactjs.org/docs/react-component.html#%20render), y [`componentDidUpdate()`](https://es.reactjs.org/docs/react-component.html#componentdidupdate) no serán invocados. Ten en cuenta que en el futuro React puede tratar a `shouldComponentUpdate()` como una sugerencia en lugar de una directiva estricta, y devolver `false` puede aun dar como resultado una nueva renderización del componente.