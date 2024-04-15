#Sorting 
___
> [!note]
> La ordenación por selección es un algoritmo de ordenación simple y eficiente que funciona seleccionando repetidamente el elemento más pequeño (o más grande) de la parte no ordenada de la lista y moviéndolo a la parte ordenada de la lista.

![[selectionsort.gif|center]]
El algoritmo **selecciona repetidamente el elemento más pequeño** (o más grande) de la parte no ordenada de la lista y lo intercambia con el primer elemento de la parte no ordenada. Este proceso se repite para el resto de la parte sin ordenar hasta que toda la lista está ordenada.
![[selectionsort2.gif|center]]
____
## Explicación

Consideremos la siguiente matriz como ejemplo: `arr[] = {64, 25, 12, 22, 11}`
### Primer paso

- Para la primera posición de la matriz ordenada, se recorre toda la matriz desde el índice `0` al `4` secuencialmente. La primera posición en la que se almacena actualmente **64**, después de recorrer toda la matriz está claro que **11** es el valor más bajo.  
- Por lo tanto, sustituye **64** por **11**. Después de una iteración, **11**, que resulta ser el valor más bajo de la matriz, tiende a aparecer en la primera posición de la lista ordenada.

![[Pasted image 20231030111453.png|center]]
### Segundo paso

- Para la segunda posición, donde está el **25**, volvemos a recorrer el resto de la matriz de forma secuencial.  
- Después de recorrer, encontramos que **12** es el segundo valor más bajo en la matriz y debe aparecer en el segundo lugar en la matriz, por lo tanto intercambiar estos valores.

![[Pasted image 20231030111529.png|center]]
### Tercer paso

- Ahora, para el tercer lugar, donde **25** está presente de nuevo recorrer el resto de la matriz y encontrar el tercer menor valor presente en la matriz.  
- Al recorrer, **22** resultó ser el tercer menor valor y debe aparecer en el tercer lugar en la matriz, por lo tanto cambiar **22** con el elemento presente en la tercera posición.

![[Pasted image 20231030111611.png]]
### Cuarto paso

- De forma similar, para la cuarta posición, recorre el resto de la matriz y encuentra el cuarto elemento más pequeño de la matriz.  
- Como **25** es el cuarto valor más bajo, se colocará en la cuarta posición.

![[Pasted image 20231030111638.png]]
### Quinto paso

- Por último, el valor más grande presente en la matriz se coloca automáticamente en la última posición de la matriz.  
- El array resultante es el array ordenado.

![[Pasted image 20231030111702.png]]
____
## Complejidad

|Name|Best|Average|Worst|Memory|Stable|Comments|
|---|:-:|:-:|:-:|:-:|:-:|:--|
|**Selection sort**|$n^2$|$n^2$|$n^2$|$1$|No|

**Complejidad temporal**: La complejidad temporal de Selection Sort es $O(N^2)$ ya que hay dos bucles anidados: 

- Un bucle para seleccionar un elemento de la matriz uno por uno = $O(N)$ 
- Otro bucle para comparar ese elemento con cualquier otro elemento de la matriz = $O(N)$  
- Por lo tanto la complejidad total = $O(N) * O(N)$ = $O(N*N)$ = $O(N^2)$

**Espacio auxiliar**: $O(1)$ ya que la única memoria extra utilizada es para variables temporales mientras se intercambian dos valores en el array. La ordenación por selección nunca hace más de $O(N)$ intercambios y puede ser útil cuando la escritura en memoria es costosa.
## Ventajas

- Sencillo y fácil de entender.  
- Funciona bien con conjuntos de datos pequeños.
## Desventajas

- La ordenación por selección tiene una complejidad temporal de O(n^2) en el peor caso y en el caso medio.  
- No funciona bien en grandes conjuntos de datos.  
- No conserva el orden relativo de los elementos con claves iguales, lo que significa que no es estable.
## Ejemplo en JavaScript

```js
function selectionSort(array) {
  for (let i = 0; i < array.length - 1; i++) {

    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[j] < array[minIndex]) {
        minIndex = j;
      }     
    }
    [array[i], array[minIndex]] = [array[minIndex], array[i]];
  }
  return array;
}
```

En primer lugar, vamos a declarar nuestra función, su valor de retorno (la matriz ordenada), y el bucle inicial en el que vamos a hacer toda nuestra lógica:

```js
function selectionSort(array) {
  for (let i = 0; i < array.length - 1; i++) {

  }
  return array;
}
```

Puede que te preguntes por qué le estamos diciendo a nuestro bucle que se detenga en array.length - 1 en lugar de en array.length. Esto es porque en el siguiente bucle, empezaremos comparando i contra su vecino i + 1 en el array. Esto significa que tendremos que detener nuestro bucle inicial un índice por debajo de la longitud total del array.  
  
A continuación declararemos la variable que contendrá el índice de nuestro elemento más pequeño actual, minIndex, y el segundo bucle que hará nuestro trabajo de comparación:

```js
function selectionSort(array) {
  for (let i = 0; i < array.length - 1; i++) {

    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {

    }

  }
  return array;
}
```

Como puedes ver, este bucle comienza en i + 1, asignando ese valor al puntero j. La variable minIndex sólo se establece en i como medida temporal, ya que es probable que cambie dentro de este bucle. Sin embargo, existe la posibilidad de que i sea de hecho el siguiente valor más pequeño en la sección no ordenada del array y simplemente se quede donde está.  
  
Por último, pero no menos importante, vamos a añadir en la lógica de comparación de núcleo dentro de nuestro bucle anidado, así como el intercambio ES6 que intercambia los dos valores una vez que el bucle se completa:

```js
function selectionSort(array) {
  for (let i = 0; i < array.length - 1; i++) {

    let minIndex = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[j] < array[minIndex]) {
        minIndex = j;
      }     
    }
    [array[i], array[minIndex]] = [array[minIndex], array[i]];
  }
  return array;
}
```

Como vimos al principio de este tutorial, el núcleo de la ordenación por selección es la idea de seleccionar el siguiente valor más bajo y realizar un seguimiento de él hasta que lleguemos al final de la matriz, y luego intercambiarlo con el límite derecho de la sección ordenada de la matriz (nuestro índice i inicial).  
  
Hacemos esto aquí evaluando si `array[j] < array[minIndex]`. Si es así, esto significa que j debe ser intercambiado con el final de nuestra sección ordenada (a menos que un valor aún más bajo se encuentra.) Hacemos esto mediante el establecimiento de minIndex = j.  
  
Una vez completado este bucle, habremos encontrado el siguiente valor más bajo en la sección no ordenada del array, y lo intercambiaremos a su lugar apropiado usando la sintaxis ES6 `[a, b] = [b, a]`.  
  
Y ¡listo! Hemos implementado con éxito un algoritmo de Ordenación por Selección en JavaScript. ¡Woohoo!