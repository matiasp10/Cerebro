## ¿En qué consiste el patrón de punteros múltiples?

El patrón de punteros múltiples consiste en crear punteros o valores que corresponden a un índice o posición y moverse al inicio, al fin o a la parte media basado en una cierta condición.

Cuando tenemos una estructura linear como pudiera ser un arreglo o un string, la idea es que vamos a buscar algo que cumpla una condición y utilizamos para esto dos referencias.
## Ejemplo del uso del patrón de punteros múltiples

Escriba una función llamada `sumaCero` que acepte un arreglo ordenado de enteros. La función debe encontrar el primer par en donde la suma sea cero. Retorne el arreglo que incluya ambos valores que al sumar den `0` o `undefined` si este par no existe.

```js
sumaCero([-3, -3, -2, 0, 1, 2, 3]); // [3,-3]
sumaCero([-2, 0, 1, 3]); // undefined
sumaCero([1, 2, 3]); // undefined
```

El primer acercamiento que pudiéramos tener es generar una función cuadrática como la siguiente.

```js
function sumaCero(arreglo) {
    for (let i = 0; i < arreglo.length; i++) {
        for (let j = i + 1; j < arreglo.length; j++) {
            if (arreglo[i] + arreglo[j] === 0) {
                return [arreglo[i], arreglo[j]];
            }
        }
    }
}

sumaCero([-4, -3, -2, -1, 0, 1, 2, 5]);
```

Podemos utilizar el patrón de cursores múltiples que consiste en mover a partir de los extremos del arreglo para encontrar el par necesario.

```js
function sumaCero(a) {
    // definir puntero izquierdo y derecho
    let i = 0;
    let j = a.length - 1;

    // recorrer el arreglo por ambos lados
    while (i < j) {
        // calcula la diferencia
        let dif = a[j] + a[i];

        // si la diferencia es 0, retornar los indices
        // si es gt 0 entonces mueve el cursor de la derecha
        // si es lt 0 entonces mueve el cursor de la izquierda
        if (dif === 0) {
            return [i, j];
        } else if (dif > 0) {
            j--;
        } else {
            i++;
        }
    }

    return undefined;
}
```

> [!definition]
> Conseguimos el mismo resultado que una función cuadrática **O(n²)**, pero con mucho con un time complexity mucho menor **O(n)**.