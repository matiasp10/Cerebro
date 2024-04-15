Es probable, sobre todo si no llevas mucho tiempo en el ecosistema Javascript, que te hayas encontrado con conceptos como **CommonJS** (_CJS_), **ES Modules** (_ESM_), o incluso algunos ya menos frecuentes como **AMD**, **System**, **UMD**, **IIFE** o similares. Dichas siglas o nombres, suelen hacer referencia al **sistema de módulos** (_importaciones desde otros archivos_) utilizado en Javascript.

### Un poco de historia

Antes de **2015**, momento en el que nace **ECMAScript 2015** (_antes llamado ES6_) con multitud de cambios y novedades, Javascript carecía de sistema de módulos oficial. Aunque pueda parecer extraño, tiene su sentido: Javascript nació como un lenguaje de programación para el navegador, que servía de apoyo a las páginas HTML+CSS para dotar de interactividad y de mayor dinamismo a su funcionamiento.

Con el tiempo, se comienza a utilizar más y más Javascript en los sitios web. Pero donde se produce un antes y un después, es cuando se hace posible utilizar **Javascript fuera del navegador**. Su implementación más popular es [NodeJS](https://nodejs.org/es/), aunque actualmente existen otras como por ejemplo [Deno](https://deno.land/). Todo esto, junto a la fuerte evolución de Javascript, vuelve muy necesario tener un sistema para incluir código desde ficheros externos y permitir organizar mejor código Javascript que comenzaba a ser muy extenso.

### ¿Qué es IIFE?

Las siglas **IIFE** significan **Expresión de función invocada inmediatamente** (_Immediately-invoked function expression_), y es una de las primeras formas que aparecen de conseguir encapsular contenido privado en Javascript, antes de **2015**. Esto solía conocerse como **patrón módulo revelador** (_Revealing Module Pattern_):

```js
var module = (function () {
  /* Data */
  /* Methods */

  // Revealing module
  return {
    /* Public data/methods */
  };
})();

module.data;
module.method();
```

Aunque no lo parezca, el funcionamiento era simple. Como no teníamos forma de declarar **datos privados**, la opción utilizada era crear una  que en su interior contiene variables y/o funciones. Por último, se devolvía un  con los datos/funciones que queríamos que fueran públicos. Los demás, eran privados porque no salían de la función, la cuál se encerraba entre paréntesis y se «autoejecutaba». De esta forma, lo que recibíamos en `module` era el «**objeto revelado**».

Como se puede ver, algo muy similar al concepto de clases que conocemos habitualmente. Sin embargo, seguíamos con el problema de no poder importarlo/exportarlo en ficheros a parte.

- [[CommonJS]]
- [[AMD]]
- [[ESM]]

### CommonJS vs ESM

Hoy en día, de todo lo anterior, lo más común suele ser utilizar **CommonJS** o **ESM**. En ecosistemas donde predomina la utilización de **NodeJS**, es más frecuente encontrarse usando **CommonJS**, mientras que en sistemas más modernos, de navegador o, por ejemplo, **Deno**, es más habitual utilizar el enfoque de **ESM**.

Al margen de su sintaxis, la cuál ya hemos visto en los ejemplos anteriores, ambos tienen sus diferencias pero las más populares son las siguientes:

![[Pasted image 20230728174256.png]]

- [NodeJS](https://nodejs.org/en/) soporta tradicionalmente la sintaxis `require` de **CommonJS**, y aunque cada vez soporta mejor **ESM**, aún el soporte no es completo y tiene una amplia comunidad con paquetes utilizando **CommonJS** a través de **NPM**.
    
- **CommonJS** sólo permite cargar módulos de forma síncrona, mientras que **ESM** permite carga síncrona y asíncrona.
    
- **NodeJS** permite hacer `require()` de [bare imports](https://lenguajejs.com/javascript/caracteristicas/modulos-es6/#bare-imports) utilizando `npm` mientras que **ESM** puede hacerlo mediante [import maps](https://wicg.github.io/import-maps/), un fichero `.json` que incluye la URL de referencias a los nombres de los paquetes «desnudos».
    
- Los `require` de **CommonJS** no son compatibles en el navegador de forma directa, mientras que los `import` de **ESM** si lo son si se indica el atributo `<script type="module">` en los scripts que los utilicen.
    
- **CommonJS** no permite cargar directamente desde una URL o CDN un módulo, mientras que con **ESM** puedes hacerlo sin problemas y funciona directamente desde un navegador.
    
- Con **ESM** es posible hacer **tree-shaking** (_eliminación de código no utilizado_) de serie, mientras que en cambio con **CommonJS** no es posible, aunque se puede conseguir utilizando plugins de terceros de Webpack como [webpack-common-shake](https://github.com/indutny/webpack-common-shake).
    
- **CommonJS** se utiliza en sistemas que generan bundles y utilizan técnicas de preprocesado o transpilado para generar builds. Por otro lado, **ESM** puede utilizarse tanto en entornos de procesados/transpilado o directamente desde el navegador, sin necesidad de transpilar. [SkyPack.dev](https://www.skypack.dev/) es un proyecto que pretende fomentar y popularizar el uso de paquetes de `npm` optimizados para utilizar sin necesidad de herramientas de preprocesado.
    
- [Deno utiliza ESM](https://deno.land/manual#comparison-to-nodejs) por defecto, y no soporta los `require` de **CommonJS**. Sin embargo, pueden soportarse con un [módulo para Deno de compatibilidad con Node](https://github.com/denoland/deno_std/tree/main/node).