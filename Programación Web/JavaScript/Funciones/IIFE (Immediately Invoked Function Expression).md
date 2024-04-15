Las expresiones de función ejecutadas inmediatamente (**IIFE** por su sigla en inglés) son funciones que _se ejecutan tan pronto como se definen_.

```js
(function () {
    statements
})();
```

Es un patrón de diseño también conocido cómo **función autoejecutable** y se compone por dos partes. 

- La primera es la **función anónima** con _alcance léxico encerrado_ por el `Operador de Agrupación` `()`. Esto impide accesar variables fuera del IIFE, así cómo contaminar el alcance (scope) global.
- La segunda parte crea la **expresión de función** cuya ejecución es inmediata `()`, siendo _interpretado directamente_ en el motor de JavaScript.

# Ejemplos

La función se convierte en una expresión de función que es ejecutada inmediatamente. La variable dentro de la expresión no puede ser accesada desde afuera.

```
(function () {
    var aName = "Barry";
})();
// La variable aName no es accesible desde el exterior
aName // retorna "Uncaught ReferenceError: aName is not defined"
```

Asignar el IIFE a una variable _almacena el valor de retorno, no la definición de la función_.

```js
var result = (function () {
    var name = "Barry";
    return name;
})();
// Crea inmediatamente la salida:
result; // "Barry"
```
