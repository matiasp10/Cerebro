```
ReactDOMServer.renderToStaticMarkup(element)
```

Similar a [`renderToString`](https://es.reactjs.org/docs/react-dom-server.html#rendertostring), excepto que esto no crea atributos DOM adicionales que React usa internamente, como `data-reactroot`. Esto es útil si desea utilizar React como un simple generador de páginas estáticas, ya que eliminar los atributos adicionales puede ahorrar algunos bytes.

Si planeas usar React en el cliente para hacer que el marcado sea interactivo, no uses este método. En su lugar, usa [`renderToString`](https://es.reactjs.org/docs/react-dom-server.html#rendertostring) en el servidor y [`ReactDOM.hydrateRoot()`](https://es.reactjs.org/docs/react-dom-client.html#hydrateroot) en el cliente.