El módulo _node:repl_ proporciona una implementación del bucle de **Read-Eval-Print-Loop** (**REPL**) que está disponible como un programa independiente o que se puede incluir en otras aplicaciones. Se puede acceder utilizando:

```js
const repl = require('node:repl');
```

### Diseño y características 

El módulo node:repl exporta la clase repl.REPLServer. Mientras se ejecutan, las instancias de repl.REPLServer aceptarán líneas individuales de entrada del usuario, las evaluarán de acuerdo con una función de evaluación definida por el usuario y, a continuación, emitirán el resultado. La entrada y la salida pueden provenir de stdin y stdout, respectivamente, o pueden conectarse a cualquier flujo de Node.js.

Las instancias de repl.REPLServer soportan la finalización automática de entradas, vista previa de finalización, edición simplista de líneas al estilo Emacs, entradas multilínea, búsqueda-i-inversa al estilo ZSH, búsqueda en el historial basada en subcadenas al estilo ZSH, salida al estilo ANSI, guardar y restaurar el estado actual de la sesión REPL, recuperación de errores y funciones de evaluación personalizables. Los terminales que no soportan los estilos ANSI y la edición de líneas al estilo Emacs retroceden automáticamente a un conjunto de características limitadas.

- [Documentacion](https://nodejs.org/api/repl.html#repl_repl)