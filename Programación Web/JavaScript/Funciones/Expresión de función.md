Esta función puede ser **anónima**; no tiene por qué tener un nombre. Por ejemplo, la función `square` se podría haber definido como:

```js
const square = function (number) {
  return number * number;
};
var x = square(4); // x obtiene el valor 16
```

Sin embargo, puedes proporcionar un nombre con una expresión function. Proporcionar un nombre permite que la función se refiera a sí misma y también facilita la identificación de la función en el seguimiento de la pila de un depurador:

```js
const factorial = function fac(n) {
  return n < 2 ? 1 : n * fac(n - 1);
};

console.log(factorial(3));
```

Las expresiones `function` son convenientes cuando se pasa una función como argumento a otra función. El siguiente ejemplo muestra una función `map` que debería recibir una función como primer argumento y un arreglo como segundo argumento.

```js
function map(f, a) {
  let result = []; // Crea un nuevo arreglo
  let i; // Declara una variable
  for (i = 0; i != a.length; i++) result[i] = f(a[i]);
  return result;
}
```

En el siguiente código, la función recibe una función definida por una expresión de función y la ejecuta por cada elemento del arreglo recibido como segundo argumento.

```js
function map(f, a) {
  let result = []; // Crea un nuevo arreglo
  let i; // Declara una variable
  for (i = 0; i != a.length; i++) result[i] = f(a[i]);
  return result;
}
const f = function (x) {
  return x * x * x;
};
let numbers = [0, 1, 2, 5, 10];
let cube = map(f, numbers);
console.log(cube);
```

La función devuelve: `[0, 1, 8, 125, 1000]`.

En JavaScript, una función se puede definir en función de una condición. Por ejemplo, la siguiente definición de función define `myFunc` solo si `num` es igual a `0`:

```js
var myFunc;
if (num === 0) {
  myFunc = function (theObject) {
    theObject.make = "Toyota";
  };
}
```

Además de definir funciones como se describe aquí, también puedes usar el constructor Function para crear funciones a partir de una cadena en tiempo de ejecución, muy al estilo de eval().

Un método es una función que es propiedad de un objeto. Obtén más información sobre objetos y métodos en Trabajar con objetos.
