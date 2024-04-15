## ¿En qué consiste el patrón Divide and Conquer (Divide y vencerás)?

Este patrón implica dividir un grupo de datos en grupos mas pequeños y repetir este proceso con un subgrupo salido de cada una de estas divisiones.

Este patrón puede reducir de manera muy significativa el time complexity.
## Ejemplo

Dado un arreglo de enteros, escribir una función llamada buscar, esta debe aceptar un valor y retornar el índice del arreglo en el cual el segundo valor se encuentra, o -1 si no existe.

```js
function buscar(a, b) {
    // definir punteros
    let i = 0;
    let j = a.length - 1;

    // recorrer el arreglo entre ambos punteros
    while (i <= j) {
        // obtener el punto medio
        let puntoMedio = Math.floor((j + i) / 2);

        // si el punto medio es igual al valor
        // buscado retornar el índice, y si no
        // es así alineamos los punteros
        if (a[puntoMedio] === b) {
            return puntoMedio;
        } else if (a[puntoMedio] > b) {
            i = puntoMedio + 1;
        } else {
            j = puntoMedio - 1;
        }
    }

    // si no se encuentra el valor retornar -1
    return -1;
}
```