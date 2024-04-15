El primer patrón que vamos a analizar tiene como objetivo utilizar un objeto para recolectar una serie de valores y la frecuencia con que estos se presentan.

Este mecanismo nos permite prevenir el uso de **loops anidados (O²)** con arreglos o strings.
## Ejemplo de un problema utilizando Frecuency Counter

Escribe una función llamada **frecIgual**, la cual acepte dos arreglos. La función debe retornar true (verdadero) si cada valor en el arreglo tiene su valor correspondiente al cuadrado en el segundo arreglo. La frecuencia de los valores debe ser la misma.

Entradas - Salidas.

```js
frecIgual([1, 2, 3], [4, 1, 9]); // true
frecIgual([1, 2, 3], [1, 9]); // false
frecIgual([1, 2, 1], [4, 4, 1]); // false (no se cumple la frecuencia)
```

Implementación del algoritmo.

```js
function frecIgual(arreglo1, arreglo2) {
    if (arreglo1.length !== arreglo2.length) {
        return false;
    }
    let frecuencia1 = {};
    let frecuencia2 = {};
    for (let val of arreglo1) {
        frecuencia1[val] = (frecuencia1[val] || 0) + 1;
    }
    for (let val of arreglo2) {
        frecuencia2[val] = (frecuencia2[val] || 0) + 1;
    }
    for (let key in frecuencia1) {
        if (!(key ** 2 in frecuencia2)) {
            return false;
        }
        if (frecuencia2[key ** 2] !== frecuencia1[key]) {
            return false;
        }
    }
    return true;
}

frecIgual([1, 2, 3, 2, 5], [9, 1, 4, 4, 11]);
```

> [!definition]
> La clave de esta solución es evitar **O(n²)** y para ello hemos echado mano de 2 mapas o diccionarios que guardan un key/pair para número/frecuencia. Estos mantienen **O(n)** que siempre es preferible sobre una función cuadrática. La clave de **frequency counter** es utilizar un objeto/mapa/diccionario para crear un perfil de un arreglo que pueda ser rápidamente comparado con otro objeto.