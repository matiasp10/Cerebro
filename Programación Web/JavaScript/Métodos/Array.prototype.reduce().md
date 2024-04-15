El método **`reduce()`** ejecuta una función **reductora** sobre cada elemento de un array, devolviendo como resultado un único valor.

```js
const array1 = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array1.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  initialValue
);

console.log(sumWithInitial);
// Expected output: 10

```

La función **reductora** recibe cuatro argumentos:

1. Acumulador (`acc`)
2. Valor Actual (`cur`)
3. Índice Actual (_`idx`_)
4. Array (_`src`_)

El valor devuelto de la función **reductora** se asigna al acumulador, cuyo valor se recuerda en cada iteración de la matriz y, en última instancia, se convierte en el valor final, único y resultante.
# Sintaxis

```js
arr.reduce(callback(acumulador, valorActual[, índice[, array]])[, valorInicial])
```
## Parámetros
### callback

Función a ejecutar sobre cada elemento del array (excepto para el primero, si no se proporciona `valorInicial`), que recibe cuatro parámetros:_ `acumulador` _ : El acumulador acumula el valor devuelto por la función callback. Es el valor acumulado devuelto en la última invocación de callback, o el `valorInicial`, si se proveyó. (Ver a continuación).
#### valorActual

El elemento actual que está siendo procesado en el array.
#### índice (Opcional)

El índice del elemento actual que está siendo procesado en el array. Empieza desde el índice 0 si se provee `valorInicial`. En caso contrario, comienza desde el índice 1.
#### array (Opcional)

El array sobre el cual se llamó el método `reduce()`.
### valorInicial (Opcional)

Un valor a usar como primer argumento en la primera llamada de la función _`callback`_. Si no se proporciona el _`valorInicial`_, el primer elemento del array será utilizado y saltado. Llamando a `reduce()` sobre un array vacío sin un _`valorInicial`_ lanzará un [`TypeError`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/TypeError).
# Descripción 

El método `reduce()` ejecuta `callback` una vez por cada elemento presente en el array, excluyendo los huecos del mismo, recibe cuatro argumentos:

- `valorAnterior`
- `valorActual`
- `indiceActual`
- `array`

La primera vez que se llama la función, `valorAnterior` y `valorActual` pueden tener uno de dos valores. Si se proveyó un `valorInicial` al llamar a `reduce`, entonces `valorAnterior` será igual al `valorInicial` y `valorActual` será igual al primer elemento del array. Si no se proveyó un `valorInicial`, entonces `valorAnterior` será igual al primer valor en el `array` y `valorActual` será el segundo.

Si el `array` está vacío y no se proveyó un `valorInicial` lanzará un [`TypeError`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/TypeError). Si el `array` tiene un sólo elemento (sin importar la posición) y no se proveyó un `valorInicial`, o si se proveyó un `valorInicial` pero el arreglo está vacío, se retornará ese único valor sin llamar a la `función`.

Suponga que ocurre el siguiente uso de `reduce`:

```js
[0,1,2,3,4].reduce(function(valorAnterior, valorActual, indice, vector){
  return valorAnterior + valorActual;
});

// Primera llamada
valorAnterior = 0, valorActual = 1, indice = 1

// Segunda llamada
valorAnterior = 1, valorActual = 2, indice = 2

// Tercera llamada
valorAnterior = 3, valorActual = 3, indice = 3

// Cuarta llamada
valorAnterior = 6, valorActual = 4, indice = 4

// el array sobre el que se llama a reduce siempre es el objeto [0,1,2,3,4]

// Valor Devuelto: 10
```

Y si proporcionas un `valorInicial`, el resultado sería como este:

```js
[0,1,2,3,4].reduce(function(valorAnterior, valorActual, indice, vector){
  return valorAnterior + valorActual;
}, 10);

// Primera llamada
valorAnterior = 10, valorActual = 0, indice = 0

// Segunda llamada
valorAnterior = 10, valorActual = 1, indice = 1

// Tercera llamada
valorAnterior = 11, valorActual = 2, indice = 2

// Cuarta llamada
valorAnterior = 13, valorActual = 3, indice = 3

// Quinta llamada
valorAnterior = 16, valorActual = 4, indice = 4

// el array sobre el que se llama a reduce siempre es el objeto [0,1,2,3,4]

// Valor Devuelto: 20
```