```jsx
ReactDOMServer.renderToPipeableStream(element, options)
```

Renderiza un elemento React a su HTML inicial. Devuelve un _stream_ (flujo) con un método `pipe(res)` que conduce la salida y `abort()` para abortar la petición. Es completamente compatible con Suspense y con la realización de _streaming_ de HTML con bloques de contenido «demorados» que luego «aparecen» usando etiquetas `<script>`. [Lee más en](https://github.com/reactwg/react-18/discussions/37).

Si llamas [`ReactDOM.hydrateRoot()`](https://es.reactjs.org/docs/react-dom-client.html#hydrateroot) en un nodo que ya tiene este marcado de servidor, React lo conservará y solo adjuntará controladores de eventos, lo que te permitirá tener una experiencia de primera carga muy eficaz.

```jsx
let didError = false;
const stream = renderToPipeableStream(
  <App />,
  {
    onShellReady() {
      // The content above all Suspense boundaries is ready.
      // If something errored before we started streaming, we set the error code appropriately.
      res.statusCode = didError ? 500 : 200;
      res.setHeader('Content-type', 'text/html');
      stream.pipe(res);
    },
    onShellError(error) {
      // Something errored before we could complete the shell so we emit an alternative shell.
      res.statusCode = 500;
      res.send(
        '<!doctype html><p>Loading...</p><script src="clientrender.js"></script>'
      );
    },
    onAllReady() {
      // If you don't want streaming, use this instead of onShellReady.
      // This will fire after the entire page content is ready.
      // You can use this for crawlers or static generation.

      // res.statusCode = didError ? 500 : 200;
      // res.setHeader('Content-type', 'text/html');
      // stream.pipe(res);
    },
    onError(err) {
      didError = true;
      console.error(err);
    },
  }
);
```

Mira la [lista completa de opciones](https://github.com/facebook/react/blob/14c2be8dac2d5482fda8a0906a31d239df8551fc/packages/react-dom/src/server/ReactDOMFizzServerNode.js#L36-L46).

> Nota:
> 
> Esta es una API específica de Node.js. Los entornos con [Streams Web](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API), como Deno y _runtimes_ modernos de _edge computing_, deberían usar en su lugar [`renderToReadableStream`](https://es.reactjs.org/docs/react-dom-server.html#rendertoreadablestream).