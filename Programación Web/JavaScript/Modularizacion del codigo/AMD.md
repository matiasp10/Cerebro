### ¿Qué es AMD?

**AMD** (_Asynchronous Module Definition_) nació del descontento de las limitaciones síncronas que tenía **CommonJS**, que no permitían cargar eficientemente módulos en el lado del cliente. No se llegó a hacer tan popular y extendido como **CommonJS**, además su sintaxis era algo más compleja de entender:

```js
define(['dep1', 'dep2'], function (dep1, dep2) {
  /* ... */

  return {
    /* ... */
  };
});
```

**AMD** podría verse como una mezcla del **patrón módulo revelador** y una sintaxis donde se usa `define(deps, module)` para cargar módulos. El parámetro `deps` es un  donde se definen los nombres de las dependencias que se necesitan para ejecutar la función `module`. Si están cargados, se ejecuta, si no, se carga asincronamente hasta que estén disponibles.

La implementación más popular de AMD fue [require.js](https://requirejs.org/) y era bastante prometedora, sin embargo, los **ES Modules** aterrizaron en 2015 y al ser nativos y estándar (_y mucho más simples_), todos estos sistemas de módulos pasarían a un segundo plano o un plano **legacy**.

> [!summary] UMD
> Antes de popularizarse **CommonJS** con Node, nunca se llegó a decidir de forma unánime entre **AMD** y **CommonJS**, por lo que apareció también un patrón llamado **UMD** (_Universal Module Definition_), que básicamente era un fragmento de código que permitía cargar módulos independientemente de si eran **AMD** o **CommonJS**, ya que permitía cargar ambos. Eso sí, la sintaxis era considerablemente más fea y compleja. Poco más tarde, aparecería [System.js](https://github.com/systemjs/systemjs) ofreciendo lo mismo.