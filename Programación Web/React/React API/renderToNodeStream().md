```
ReactDOMServer.renderToNodeStream(element)
```

Renderiza un elemento React a su HTML inicial. Devuelve un [Readable stream de Node.js](https://nodejs.org/api/stream.html#stream_readable_streams) que genera una cadena HTML. La salida HTML de este flujo es exactamente igual a lo que devolvería [`ReactDOMServer.renderToString`](https://es.reactjs.org/docs/react-dom-server.html#rendertostring) Puede usar este método para generar HTML en el servidor y enviar el marcado en la solicitud inicial para que las páginas se carguen más rápido y permitir que los motores de búsqueda rastreen sus páginas con fines de SEO.

Si llamas [`ReactDOM.hydrateRoot()`](https://es.reactjs.org/docs/react-dom-client.html#hydrateroot) en un nodo que ya tiene este marcado de servidor, React lo conservará y solo adjuntará controladores de eventos, lo que te permitirá tener una experiencia de primera carga muy eficaz.

> Nota:
> 
> Solo para el servidor. Esta API no está disponible en el navegador.
> 
> El flujo devuelto por este método devolverá un flujo de bytes codificado en utf-8. Si necesita un flujo en otra codificación, observa un proyecto como [iconv-lite](https://www.npmjs.com/package/iconv-lite), que proporciona flujos de transformación para la transcodificación de texto.