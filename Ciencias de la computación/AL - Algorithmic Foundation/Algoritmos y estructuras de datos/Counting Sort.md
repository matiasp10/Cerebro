> [!definition]
>En informática, la ordenación por recuento es un algoritmo para ordenar una colección de objetos según claves que son números enteros pequeños; es decir, es un algoritmo de ordenación por números enteros. Funciona contando el número de objetos que tienen cada valor de clave distinto y utilizando la aritmética de esos recuentos para determinar las posiciones de cada valor de clave en la secuencia de salida. Su tiempo de ejecución es lineal en el número de elementos y la diferencia entre los valores clave máximo y mínimo, por lo que sólo es adecuado para su uso directo en situaciones en las que la variación de las claves no es significativamente mayor que el número de elementos. Sin embargo, a menudo se utiliza como subrutina en otro algoritmo de ordenación, la ordenación radix, que puede manejar claves más grandes de manera más eficiente.
>
>Dado que la ordenación por recuento utiliza valores clave como índices de una matriz, no es una ordenación por comparación, y el límite inferior Ω(n log n) para la ordenación por comparación no se le aplica. La ordenación por cubos puede utilizarse para muchas de las mismas tareas que la ordenación por recuento, con un análisis de tiempo similar; sin embargo, en comparación con la ordenación por recuento, la ordenación por cubos requiere listas enlazadas, matrices dinámicas o una gran cantidad de memoria preasignada para almacenar los conjuntos de elementos dentro de cada cubo, mientras que la ordenación por recuento almacena un único número (el recuento de elementos) por cubo.
>
>La ordenación por recuento funciona mejor cuando el rango de números de cada elemento de la matriz es muy pequeño.

____
## Explicación
### Paso 1

En el primer paso calculamos el recuento de todos los elementos de la matriz de entrada A. A continuación, almacenamos el resultado en la matriz de recuento C. La forma en que contamos se representa a continuación.
![[countingsort.gif|center]]
### Paso 2

En el segundo paso calculamos cuántos elementos existen en la matriz de entrada A que son menores o iguales para el índice dado. Ci = número de elementos menores o iguales que i en la matriz de entrada.
![[countingsort2.gif]]
### Paso 3

En este paso colocamos el elemento de la matriz de entrada A en la posición ordenada con la ayuda de la matriz de recuento construida C, es decir, lo que construimos en el paso dos. Utilizamos la matriz de resultados B para almacenar los elementos ordenados. Aquí manejamos el índice de B a partir de cero.
![[countingsort3.gif]]
___
## Complejidad

|Name|Best|Average|Worst|Memory|Stable|Comments|
|---|:-:|:-:|:-:|:-:|:-:|:--|
|**Counting sort**|$n + r$|$n + r$|$n + r$|$n + r$|Yes|r - biggest number in array|
## Implementación 

```js
function countingSort(arr, min, max)
  {
    let i = min,
        j = 0,
        len = arr.length,
        count = [];

    for (i; i <= max; i++)
    {
        count[i] = 0;
    }

    for (i = 0; i < len; i++)
    {
        count[arr[i]] += 1;
    }

    for (i = min; i <= max; i++)
    {
        while (count[i] > 0)
        {
            arr[j] = i;
            j++;
            count[i]--;
        }
    }
    return arr;
}
```
