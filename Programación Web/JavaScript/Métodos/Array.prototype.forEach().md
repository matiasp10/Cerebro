El método forEach() ejecuta una función proporcionada una vez por cada elemento de la matriz.

```js
const array1 = ['a', 'b', 'c'];

array1.forEach(element => console.log(element));

// Expected output: "a"
// Expected output: "b"
// Expected output: "c"
```

# Sintaxis

```js
// Arrow function
forEach((element) => { /* … */ })
forEach((element, index) => { /* … */ })
forEach((element, index, array) => { /* … */ })

// Callback function
forEach(callbackFn)
forEach(callbackFn, thisArg)

// Inline callback function
forEach(function (element) { /* … */ })
forEach(function (element, index) { /* … */ })
forEach(function (element, index, array) { /* … */ })
forEach(function (element, index, array) { /* … */ }, thisArg)
```

## Parámetros

### callbackFn

Una función a ejecutar para cada elemento del array. Su valor de retorno se descarta.

#### element

El elemento actual que se está procesando en el array.

#### index (opcional)

El índice del elemento actual que se está procesando en la matriz.

#### array (opcional)

El array en el que `forEach()` esta siendo aplicado.

### thisArg (opcional)

Valor que se usará como `this` cuando se ejecute el `callback`.

## Valor de retorno

[[Undefined]]

# Descripción

El método `forEach()` es un _método iterativo_. Llama a una función `callbackFn` proporcionada una vez por cada elemento de una matriz en orden de índice ascendente. A diferencia de map(), forEach() _siempre devuelve undefined_ y no es encadenable. El caso de uso típico es ejecutar efectos secundarios al final de una cadena.

`callbackFn` sólo se invoca para índices de matrices que tienen valores asignados. No se invoca para ranuras vacías en matrices dispersas.

forEach() no muta la matriz sobre la que se invoca, pero la función proporcionada como `callbackFn` sí puede hacerlo. Tenga en cuenta, sin embargo, que la longitud de la matriz se guarda antes de la primera invocación de `callbackFn`. Por lo tanto:

- `callbackFn` no visitará ningún elemento añadido más allá de la longitud inicial del array cuando comenzó la llamada a `forEach()`.
- Los cambios en los índices ya visitados no hacen que `callbackFn` vuelva a invocarlos.
- Si un elemento existente y aún no visitado del array es cambiado por `callbackFn`, su valor pasado a `callbackFn` será el valor en el momento en que ese elemento sea visitado. Los elementos borrados no se visitan.

> [!warning] Advertencia 
> Las modificaciones concurrentes del tipo descrito anteriormente suelen dar lugar a código difícil de entender y, por lo general, deben evitarse (salvo en casos especiales).

El método forEach() es _genérico_. Sólo espera que el valor this tenga una _propiedad length_ y propiedades _integer-keyed_.

No hay forma de parar o romper un bucle forEach() más que lanzando una excepción. Si necesita tal comportamiento, el método forEach() es la herramienta equivocada.

La terminación anticipada puede lograrse con sentencias de bucle como for, for...of y for...in. Los métodos de matriz como every(), some(), find() y findIndex() también detienen la iteración inmediatamente cuando no es necesario seguir iterando.

forEach() espera una función síncrona - no espera promesas. Asegúrese de conocer las implicaciones de utilizar promesas (o funciones asíncronas) como callbacks de forEach.

```js
const ratings = [5, 4, 5];
let sum = 0;

const sumFunction = async (a, b) => a + b;

ratings.forEach(async (rating) => {
  sum = await sumFunction(sum, rating);
});

console.log(sum);
// Naively expected output: 14
// Actual output: 0
```
