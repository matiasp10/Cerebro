El objeto `ReactDOMServer` te permite renderizar componentes a un marcado estático. Normalmente, se usa en un servidor de Node:

```
// módulos ES
import * as ReactDOMServer from 'react-dom/server';
// CommonJS
var ReactDOMServer = require('react-dom/server');
```

## Resumen

Estos métodos solo están disponibles en los **entornos con [Streams de Node.js](https://nodejs.dev/learn/nodejs-streams):**

-   [[renderToPipeableStream()]]
-   [[renderToNodeStream()]] (Deprecated)
-   [[renderToStaticNodeStream()]]

Estos métodos solo están disponibles en los **entornos con [Streams Web](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API)** (esto incluye navegadores, Deno y algunos _runtimes_ modernos de _edge computing_):

-   [[renderToReadableStream()]]

Los siguientes métodos se pueden utilizar en entornos que no tienen disponibles _streams_:

-   [[renderToString()]]
-   [[renderToStaticMarkup()]]