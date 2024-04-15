### ¿Qué es CommonJS (CJS)?

**CommonJS** surge cerca de 2009 como una serie de pautas para crear un sistema de módulos en el ecosistema Javascript. Algo más tarde, el equipo de **NodeJS** implementó parcialmente una versión síncrona de CommonJS, por lo que consigue popularizar un sistema de módulos no oficial como el que puedes ver a continuación:

```js
// module-name.js
module.exports = {
  /* ... */
}

// index.js
const module = require("./module-name.js");
const package = require("package");

module.method();
```

De esta forma, haciendo un `require()` podemos importar módulos **CommonJS** que se exportan con un `module.exports` desde otros archivos. También es habitual encontrar importaciones de paquetes que habitualmente residen en la carpeta [node_modules](https://lenguajejs.com/npm/administracion/carpeta-node_modules/), obteniendo la carpeta principal del campo `main` del [package.json](https://lenguajejs.com/npm/administracion/package-json/). Este sistema se conocería más tarde como [bare imports](https://lenguajejs.com/javascript/caracteristicas/modulos-es6/#bare-imports) (_importaciones desnudas_), haciendo referencia a que no se indica una ruta de un archivo, sino un  con el nombre del paquete.

Sin embargo, estos `require()` son creados por **NodeJS** y no son compatibles directamente en navegadores, salvo que se **preprocese o transpile** antes con alguna herramienta como podría ser un empaquetador o automatizador del estilo de **Webpack**, **Parcel**, **Rollup**, **Babel** o similar. Estas herramientas buscan los `require()` y los sustituyen por el código del fichero correspondiente, uniendo y empatando todos los archivos Javascript necesarios de nuestra aplicación web en un sólo archivo Javascript llamado **bundle**.