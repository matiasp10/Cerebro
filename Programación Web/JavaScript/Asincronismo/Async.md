La declaración de función **`async`** define una _función asíncrona_, la cual devuelve un objeto [`AsyncFunction`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/AsyncFunction).

## Sintaxis

```js
async function name([param[, param[, ... param]]]) {
   statements
}
```

## Parámetros

- `name`: El nombre de la función.
- `param`: El nombre de un argumento que se debe pasar a la función.
- `statements`: Las declaraciones que conforman el cuerpo de la función.

## Valor de retorno

Un objeto [`AsyncFunction`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/AsyncFunction), que representa una función asíncrona que ejecuta el código contenido dentro de la función.

## Descripción

Cuando se llama a una función `async`, esta devuelve un elemento [`Promise`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Promise). Cuando la función `async` devuelve un valor, `Promise` se resolverá con el valor devuelto. Si la función `async` genera una excepción o algún valor, `Promise` se rechazará con el valor generado.

Una función `async` puede contener una expresión [`await`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/await), la cual pausa la ejecución de la función asíncrona y espera la resolución de la `Promise` pasada y, a continuación, reanuda la ejecución de la función `async` y devuelve el valor resuelto.