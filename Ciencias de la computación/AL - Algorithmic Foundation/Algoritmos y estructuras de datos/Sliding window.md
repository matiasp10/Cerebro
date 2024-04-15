## ¿Qué es el patrón Sliding Window?

Este patrón implica crear una ventana la cual puede ser un arreglo o un número de una posición a otra.

Dependiendo de ciertas condiciones, la ventana puede incrementar o cerrarse (una nueva ventana es creada).

Este patrón es bastante útil para mantener un monitoreo de un subgrupo de datos en un arreglo/string etc.
## Ejemplo del uso del patrón Sliding Window

Escriba una función llamada `maxSubArraySum` que acepte un arreglo de enteros y un número llamado n. La función debe calcular la suma máximo consecutiva de n elementos en el arreglo.

```js
function maxSubArraySum(a, n) {
    // si el arreglo es menor que n retorna null
    if (a.length < n) {
        return null;
    }

    // contenedor del máximo valor
    let maxSum = 0;

    // recorre el primer grupo de valores n
    for (let i = 0; i < n; i++) {
        maxSum += a[i];
    }

    // mantener valor previo
    let prevSum = maxSum;

    // ahora recorre el resto de valores de
    // n a length(a)
    for (let i = n; i < a.length; i++) {
        // calcula el nuevo valor sumando el valor
        // corriente y restando el valor de i-n
        let newSum = prevSum + a[i] - a[i - n];

        // obten el nuevo maximo
        maxSum = newSum > maxSum ? newSum : maxSum;

        // actualiza la suma previa
        prevSum = newSum;
    }

    // retorna la suma maxima
    return maxSum;
}
```