Node.js es un **entorno de ejecución** JavaScript de código abierto y multiplataforma. Es una herramienta popular para casi cualquier tipo de proyecto.

Node.js ejecuta el **motor V8** de JavaScript, el núcleo de Google Chrome, _fuera del navegador_. Esto permite que Node.js tenga un gran rendimiento.

Una aplicación Node.js se ejecuta en **un solo proceso**, sin crear un nuevo hilo para cada solicitud. Node.js proporciona un conjunto de primitivas de E/S asíncronas en su biblioteca estándar que evitan que el código JavaScript se bloquee y, en general, las bibliotecas en Node.js están escritas utilizando **paradigmas de no-bloqueo**, haciendo que el comportamiento de bloqueo sea la excepción y no la norma.

Cuando Node.js realiza una operación de E/S, como leer de la red, acceder a una base de datos o al sistema de archivos, en lugar de bloquear el hilo y desperdiciar ciclos de CPU esperando, Node.js reanudará las operaciones cuando la respuesta vuelva.

Esto permite a Node.js manejar miles de _conexiones concurrentes con un solo servidor sin introducir la carga de gestionar la concurrencia de hilos_, que podría ser una fuente importante de errores.

Node.js tiene una ventaja única porque millones de desarrolladores de frontend que escriben JavaScript para el navegador pueden ahora escribir el código del lado del servidor además del código del lado del cliente sin necesidad de aprender un lenguaje completamente diferente.

En Node.js se pueden utilizar los nuevos estándares de **ECMAScript** sin problemas, ya que no tienes que esperar a que todos tus usuarios actualicen sus navegadores - tú eres el encargado de decidir qué versión de ECMAScript utilizar cambiando la versión de Node.js, y también puedes habilitar características experimentales específicas ejecutando Node.js con **flags**.

## Un ejemplo

```node
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

## Diferencias entre Node.js y el navegador

Tanto el navegador como Node.js utilizan JavaScript como lenguaje de programación. Construir aplicaciones que se ejecutan en el navegador es algo completamente diferente a construir una aplicación Node.js. A pesar de que siempre es JavaScript, hay algunas diferencias clave que hacen que la experiencia sea radicalmente diferente.

Desde la perspectiva de un desarrollador de frontend que utiliza ampliamente JavaScript, las aplicaciones Node.js traen consigo una enorme ventaja: **la comodidad de programar todo -el frontend y el backend- en un único lenguaje**.

Tienes una gran oportunidad porque sabemos lo difícil que es aprender de forma completa y profunda un lenguaje de programación, y al utilizar el mismo lenguaje para realizar todo tu trabajo en la web - tanto en el cliente como en el servidor, estás en una posición de ventaja única.

### Lo que cambia es el ecosistema

En el navegador, la mayor parte del tiempo lo que estás haciendo es interactuar con el **DOM**, u otras **APIs** de la plataforma web como las _cookies_. Esos no existen en Node.js, por supuesto. No tienes el documento, la ventana y todos los demás objetos que proporciona el navegador.

Y en el navegador, no tenemos todas las bonitas **APIs** que Node.js proporciona a través de sus módulos, como la funcionalidad de acceso al sistema de archivos.

Otra gran diferencia es que **en Node.js tú controlas el entorno**. A menos que estés construyendo una aplicación de código abierto que cualquiera pueda desplegar en cualquier lugar, tú sabes en qué versión de Node.js vas a ejecutar la aplicación. En comparación con el entorno de los navegadores, en el que no puedes permitirte el lujo de elegir qué navegador utilizarán tus visitantes, esto es muy conveniente.

Esto significa que puedes escribir todo el JavaScript moderno ES2015+ que tu versión de Node.js soporte. Dado que JavaScript se mueve tan rápido, pero los navegadores pueden ser un poco lentos para actualizar, a veces en la web estás atascado con el uso de versiones antiguas de JavaScript / ECMAScript. Puedes usar Babel para transformar tu código para que sea compatible con ES5 antes de enviarlo al navegador, pero en Node.js, no necesitarás eso.

Otra diferencia es que Node.js es compatible con los sistemas de módulos **CommonJS** y **ES** (desde Node.js v12), mientras que en el navegador estamos empezando a ver cómo se implementa el estándar **ES Modules**.

En la práctica, esto significa que puedes usar tanto **require()** como **import** en _Node.js_, mientras que estás limitado a **import** en el _navegador_.

### Node.js utiliza el motor V8

Para funcionar Node.js utiliza el motor de JavaScript V8.

- [[Motor V8]]

### Node Package Manager

``npm`` es el gestor de paquetes estándar para Node.js.

Comenzó como una forma de descargar y gestionar las dependencias de los paquetes de Node.js, pero desde entonces se ha convertido en una herramienta utilizada también en el frontend de JavaScript.

[[NPM]]

#### Otras alternativas

- Yarn
- pnpm

### Event Loop

Es un proceso con un bucle que gestiona, de forma asíncrona, todos los eventos de la aplicación. Gracias a esto toda nuestra aplicación se convierte en asíncrona, por lo cual no se bloquea en ningún momento.

[[Event Loop]]
[[Event Loop en NodeJS]]

## Sistema de módulos

[[Sistema de módulos]]

## API

- [[Assertion Testing]]
- [[Asynchronous context tracking]]
- [[Async hooks]]
- [[Buffer]]
- [[C++ addons]]
- [[C/C++ addons with Node-API]]
- [[C++ embedder API]]
- [[Child processes]]
- [[Cluster]]
- [[Command-line options]]
- [[Console]]
- [[Corepack]]
- [[Crypto]]
- [[Debugger]]
- [[Deprecated APIs]]
- [[Diagnostics Channel]]
- [[DNS]]
- [[Domain]]
- [[Errors]]
- [[Events]]
- [[fs|File system]]
- [[Globals]]
- [[NodeJS/HTTP]]
- [[HTTP/2]]
- [[HTTPS]]
- [[Inspector]]
- [[Internationalization]]
- [[Modules: CommonJS modules]]
- [[Modules: ECMAScript modules]]
- [[Modules: node:module API]]
- [[Modules: Packages]]
- [[Net]]
- [[os]]
- [[Path]]
- [[Performance hooks]]
- [[Permissions]]
- [[Process]]
- [[Punycode]]
- [[Query strings]]
- [[Readline]]
- [[REPL]]
- [[Report]]
- [[Stream]]
- [[String decoder]]
- [[Test runner]]
- [[Timers]]
- [[TLS/SSL]]
- [[Trace events]]
- [[TTY]]
- [[UDP/datagram]]
- [[URL]]
- [[Utilities]]
- [[V8]]
- [[VM]]
- [[WASI]]
- [[Web Crypto API]]
- [[Web Streams API]]
- [[Worker threads]]
- [[Zlib]]

