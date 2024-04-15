> Nota:
> 
> `findDOMNode` es una vía de escape para acceder al componente DOM subyacente. En la mayoría de los casos no se recomienda, debido a que rompe la abstracción del componente. [Su uso esta censurado en el modo estricto (StrictMode).](https://es.reactjs.org/docs/strict-mode.html#warning-about-deprecated-finddomnode-usage)

```
findDOMNode(component)
```

Si este componente ha sido montado al DOM, este método retorna el elemento DOM nativo correspondiente. Este método es útil para leer valores fuera del DOM, como por ejemplo valores de formularios, o realizar mediciones del DOM. **En la mayoría de casos, puedes agregar una referencia al nodo del DOM, y evitar el uso de `findDOMNode` por completo**.

Cuando un componente es renderizado a `null` o `false`, `findDOMNode` retorna `null`. Cuando un componente es renderizado a una cadena de texto, `findDOMNode` retorna un nodo DOM de texto que contiene ese valor. En React 16, un componente puede retornar un fragmento con múltiples hijos, en este caso `findDOMNode` retornará el nodo del DOM correspondiente al primer hijo no vacío.

> Nota:
> 
> `findDOMNode` solo funciona con componentes montados (esto significa, componentes que han sido puestos en el DOM). Si tratas de llamar este método con un componente que aún no ha sido montado (por ejemplo, llamar `findDOMNode()` en `render()` con un componente que aún no ha sido creado) generará una excepción.
> 
> `findDOMNode` no puede ser utilizado en componentes de función.