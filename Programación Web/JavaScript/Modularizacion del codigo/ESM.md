### ¿Qué es ES Modules (ESM)?

En 2015, aterriza [[ES6|ECMAScript 2015]] (_antiguamente ES6_) y con ella multitud de novedades en Javascript. Una de ellas, el sistema de módulos nativos de Javascript. Los tienes detalladamente explicados en [Módulos ECMAScript (ESM)](https://lenguajejs.com/javascript/caracteristicas/modulos-es6/), pero básicamente, son una evolución de lo mejor de los anteriores, en versión simplificada:

```js
// module.js
export const data = 42;
export const method = () => console.log("Hello");

// index.js
import { data, method } from "./module.js";
```

Este sistema de módulos nativo por fin nos permite cargar módulos externos con una sintaxis simple y de forma síncrona y asíncrona. Eso sí, con una pequeña pega que seguiremos sufriendo durante un tiempo: esperar que la industria vaya abandonando **CommonJS** a favor de **ESM**.

### ¿Qué son los módulos ES?

A partir de **ECMAScript**  se introduce una característica nativa denominada **Módulos ES** (_ESM_), que permite la importación y exportación de fragmentos de datos entre diferentes ficheros Javascript, eliminando las desventajas que teníamos hasta ahora y permitiendo trabajar de forma más flexible en nuestro código Javascript.

Para trabajar con **módulos** tenemos a nuestra disposición las siguientes palabras clave:

| Declaración| Descripción|
|---|---|
|`export`|Pone los datos indicados (variables, funciones, clases...) a disposición de **otros ficheros**|
|`import`|Incorpora datos (variables, funciones, clases...) desde otros ficheros `.js` al código actual.|
|`import()`|Permite importar módulos de forma más flexible, en tiempo real (imports dinámicos).|

- [[Export]]
- [[Import]]
- [[import()]]

Mediante la palabra clave `export` crearemos lo que se llama un **módulo de exportación** que contiene datos. Estos datos pueden ser variables, funciones, clases u objetos más complejos (_a partir de ahora, elementos_). Si dicho módulo ya existe, podremos ir añadiendo más propiedades.

Por otro lado, con la palabra clave `import` podremos leer dichos módulos exportados desde otros ficheros y utilizar sus elementos en el código de nuestro fichero actual.

Veamos un ejemplo sencillo para ver el funcionamiento de `import` y `export` en su modo más básico. Tenemos un fichero `constants.js` donde vamos a exportar una constante numérica:

```js
// Fichero constants.js
export const magicNumber = 42;
```

Por otro lado, en el fichero `index.js`, vamos a traernos esa constante numérica para utilizarla en el fichero actual:

```js
// Fichero index.js
import { magicNumber } from "./constants.js";

console.log(magicNumber);   // 42
```

Obviamente, esto es sólo la modalidad básica de importación y exportación de elementos, pero existen múltiples modalidades, matices y diferencias que iremos viendo en los siguientes artículos.

### [Antes de usar módulos](https://lenguajejs.com/javascript/modulos/que-es-esm/#antes-de-usar-m%C3%B3dulos)

Antes de empezar, recuerda que para poder utilizar `export` o `import` en nuestro código Javascript que se ejecuta directamente en el navegador, debemos cargar el fichero `.js` con la etiqueta y atributo `<script type="module">` para indicarle que utilizaremos módulos. Si no lo hacemos, obtendremos el siguiente error:

```html
<script>
  import { nombre } from "./file.js";
</script>
```

> [!danger] Error
>Uncaught SyntaxError: Cannot use import statement outside a module

Al añadir el atributo `type="module"` a nuestra etiqueta `<script>` estaremos avisando al navegador que estamos cargando un módulo en el que podemos utilizar `import` y `export`:

```html
<script type="module">
  import { nombre } from "./file.js";
</script>
```

Algunos frameworks utilizan automatizadores que pueden «oscurecer» esto, ya que puede parecer que no es necesario, ya que los automatizadores lo hacen internamente, o convierten a otros sistemas de módulos, como **CommonJS** (NodeJS).