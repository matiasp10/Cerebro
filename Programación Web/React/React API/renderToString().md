```
ReactDOMServer.renderToString(element)
```

Renderiza un elemento React a su HTML inicial. React devolverá HTML en una cadena de texto. Puedes usar este método para generar HTML en el servidor y enviar el marcado en la solicitud inicial para que las páginas se carguen más rápido y permitir que los motores de búsqueda rastreen tus páginas con fines de SEO.

Si llamas [`ReactDOM.hydrateRoot()`](https://es.reactjs.org/docs/react-dom-client.html#hydrateroot) a un nodo que ya tiene este marcado desde el servidor, React lo conservará y solo adjuntará los controladores de eventos, lo que te permitirá tener una experiencia de primera carga muy eficaz.

> Nota
> 
> Esta API tiene compatibilidad limitada con Suspense y no permite realizar _streaming_.
> 
> En el servidor, se recomienda usar en cambio, o bien [`renderToPipeableStream`](https://es.reactjs.org/docs/react-dom-server.html#rendertopipeablestream) (para Node.js) o [`renderToReadableStream`](https://es.reactjs.org/docs/react-dom-server.html#rendertoreadablestream) (para Streams Web).