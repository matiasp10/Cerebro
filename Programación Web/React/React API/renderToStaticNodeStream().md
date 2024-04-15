```
ReactDOMServer.renderToStaticNodeStream(element)
```

Similar a [`renderToNodeStream`](https://es.reactjs.org/docs/react-dom-server.html#rendertonodestream), excepto que esto no crea atributos DOM adicionales que React usa internamente, como `data-reactroot`. Esto es útil si desea utilizar React como un simple generador de páginas estáticas, ya que eliminar los atributos adicionales puede ahorrar algunos bytes.

La salida HTML de este flujo es exactamente igual a lo que [`ReactDOMServer.renderToStaticMarkup`](https://es.reactjs.org/docs/react-dom-server.html#rendertostaticmarkup) devolvería.

Si planeas usar React en el cliente para hacer que el marcado sea interactivo, no use este método. En su lugar, utilice [`renderToNodeStream`](https://es.reactjs.org/docs/react-dom-server.html#rendertonodestream) en el servidor y [`ReactDOM.hydrateRoot()`](https://es.reactjs.org/docs/react-dom-client.html#hydrateroot) en el cliente.

> Nota:
> 
> Solo para el servidor. Esta API no está disponible en el navegador.
> 
> El flujo devuelto por este método devolverá un flujo de bytes codificado en utf-8. Si necesita un flujo en otra codificación, chequea un proyecto como [iconv-lite](https://www.npmjs.com/package/iconv-lite), que proporciona flujos de transformación para la transcodificación de texto.