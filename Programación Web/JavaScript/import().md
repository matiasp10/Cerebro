En apartados anteriores hablamos de las **exportaciones e importaciones** de los módulos ESM en Javascript utilizando las palabras clave `export` e `import`. Mediante este mecanismo se nos permite exportar datos desde un fichero a otro, reutilizando contenido, haciendo el código más modular y organizando mejor nuestras aplicaciones o webs.

### [Import estático vs dinámico](https://lenguajejs.com/javascript/modulos/dynamic-import/#import-est%C3%A1tico-vs-din%C3%A1mico)

En dicho capítulo, tratamos la palabra clave `import` que es lo que se conoce como un **import estático**, una forma de importar módulos de ficheros externos. Se colocan en la parte superior del fichero Javascript y son algo similar a lo siguiente:

```js
import { name } from "./module.js";     // Static import
```

Sin embargo, existe otro tipo de importación en Javascript, popularmente conocida como **import dinámico**  (_dynamic import_), que tiene el siguiente aspecto, ligeramente diferente al anterior:

```js
import("./module.js")                   // Dynamic import
  .then(data => { /* ... */ });
```

En este segundo caso, el `import()` tiene unos paréntesis que lo diferencian del anterior, y por la existencia del `.then()` sabemos que nos devuelve una promesa, por lo que se trata de código asíncrono.

Su soporte es bastante bueno en la actualidad, aunque frecuentemente se utiliza mediante automatizadores o bundlers como **Webpack**, **Rollup** o similares:

![[Pasted image 20230728174901.png]]

#### [Diferencias](https://lenguajejs.com/javascript/modulos/dynamic-import/#diferencias)

Los **import estáticos** son muy útiles, pero tienen algunas desventajas si se presentan ciertos casos específicos. Los más frecuentes suelen ser los siguientes:

- Queremos importar un módulo si se cumple una determinada **condición**
- Queremos importar un módulo **interpolando** variables o constantes
- Queremos importar un módulo **dentro de un ámbito** específico
- Queremos importar un módulo desde un **script normal** (_sin type="module"_)
- Queremos importar un fichero javascript (_sin módulo_) y ejecutarlo bajo demanda

En cada uno de estos casos, no se puede utilizar el **import estático**, pero si el **import dinámico**:

```js
// Opción 1: Se carga functions.js si se cumple la condición
if (number > 42) {
  import("./functions.js")
    .then(module => module.func());
}

// Opción 2: Se carga functions.js interpolando la constante
const filename = "functions";
import(`./${filename}.js`)
  .then(module => module.func());

// Opción 3: Se carga aditional.js sólo si el usuario hace click en el botón
const button = document.querySelector("button.info");
button.addEventListener("click", () => import("aditional.js"), { once: true });
```

El **import dinámico** nos permite indicar entre los paréntesis del `import` el nombre del archivo Javascript. A diferencia del **import estático**, este fichero no se cargará siempre y desde el principio, sino que sólo lo hará cuando se llegue a esta parte del código, siendo posible incluirla dentro de condicionales, funciones o lógica diversa.

> [!seealso] 
>Si el archivo `.js` importado **es un módulo**, al trabajar con la promesa que devuelve simplemente accedemos a las propiedades o métodos que necesitemos. Por otro lado, si el archivo `.js` cargado **no es un módulo**, simplemente se ejecutará su contenido.

Esto nos proporciona una característica muy interesante de cara a **optimización y rendimiento**, y es que es posible no importar (_ni por lo tanto, procesar_) ficheros con código Javascript hasta que ocurra una cierta condición, evento o acción, **retrasando** así la descarga, procesamiento y ejecución de código Javascript por parte del navegador hasta que sea necesario (_o incluso nunca si no es necesario_).

### [Code splitting en bundlers](https://lenguajejs.com/javascript/modulos/dynamic-import/#code-splitting-en-bundlers)

En el ecosistema Javascript, existen ciertas herramientas denominadas **automatizadores** o **bundlers**. Dichas herramientas, entre otras cosas, suelen tener como objetivo generar un sólo archivo `.js` final donde se guardará todo el código Javascript de nuestra web o aplicación, que leerá el navegador.

> Esto tiene un significado y razones históricas (_cuando no existían los módulos en Javascript_), pero aún en la actualidad tiene ciertas ventajas y se utiliza mucho en frameworks SPA o librerías como **React**, **Vue** o similares.

Sin embargo, si estamos utilizando una de estas herramientas, al realizar dicha empaquetación **en un sólo archivo** `.js`, podemos pensar que estamos «rompiendo» esa característica deseable de separar el código y sólo ejecutarlo cuando sea necesario (_cuando el usuario haga click en un botón, cuando ocurra cierto evento, etc..._). Esta característica se denomina **Code Splitting** (_separación de código_).

Herramientas como **Webpack** o **Rollup** separan los archivos importados con **imports dinámicos** en ficheros aislados (_chunks_), que generalmente tienen el nombre del módulo fichero javascript importado, junto a un hash aleatorio. De esta forma, el código de dicho fichero o módulo no será incluído en ese fichero `.js` general, evitando que se cargue siempre por parte del navegador.