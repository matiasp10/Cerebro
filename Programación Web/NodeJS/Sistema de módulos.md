El sistema de módulos utilizado actualmente en Node.js extiende del estándar de CommonJS, aunque hay que destacar que se están implementando otras soluciones como los módulos de ES. Sin embargo, al principio este vacío no estaba cubierto y CommonJS fue quien lo lleno.

### ¿Qué es un modulo?

Un módulo no es nada más que una unidad de código organizado en archivos o directorios, la cual puede ser exportada con facilidad para poder reutilizarse en otras partes de la aplicación.

### Tipos de modulo

Hay 3 tipos de módulos. Todos funcionan de una manera similar pero difieren en el origen.

- **Built-in modules**: Son los módulos nativos de la API de Node.js. No hace falta que se instalen, ya que vienen incluidos por defecto con Node.js. Algunos ejemplos son los módulos `fs` o `stream`. Estos paquetes solo son actualizados si cambias la versión de Node.js.
- **Local modules**: Son los módulos escritos por los desarrolladores y forman en su conjunto gran parte de la aplicación. Como ya has leído, se estructuran así con la finalidad de poder ser un código reutilizable.
- **External modules**: Son, en esencia, los paquetes de terceros distribuidos a través de *[[NPM]]* (aunque pueden provenir de otros repositorios). Estos paquetes se instalan como dependencias y, aunque aportan funcionalidad a la aplicación, no deben incluirse en el repositorio ya que no son parte de la misma.

### ¿Cómo funciona?

En Node.js cada archivo cuenta con un objeto global llamado module. Su estructura es bastante sencilla:

```js
Module {
  id: `.`,
  path: `/Users/mac/Desktop/examples`,
  exports: {},
  parent: null,
  filename: `/Users/mac/Desktop/examples/index.js`,
  loaded: false,
  children: [],
  paths: [
    `/Users/mac/Desktop/examples/node_modules`,
    `/Users/mac/Desktop/node_modules`,
    `/Users/mac/Desktop/node_modules`,
    `/Users/mac/node_modules`,
    `/Users/node_modules`,
    `/node_modules`,
  ],
};
```

Hay cierta información que puede ser relevante en algún momento determinado pero por lo general no usarás con frecuencia. La propiedad clave en el objeto Module es `exports`, la cual te permitirá exportar código para ser reutilizado con posterioridad en tantos sitios como sea necesario.