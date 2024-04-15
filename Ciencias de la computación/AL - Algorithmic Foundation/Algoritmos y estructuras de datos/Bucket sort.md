> [!definition]
> La **clasificación por cubos** es una técnica de clasificación que consiste en dividir los elementos en varios grupos, o cubos. Estos cubos se forman distribuyendo uniformemente los elementos. Una vez divididos los elementos en cubos, pueden ordenarse utilizando cualquier otro algoritmo de ordenación. Por último, los elementos clasificados se reúnen de forma ordenada.

Crea **n** cubos vacíos (O listas) y haz lo siguiente para cada elemento del array `arr[i]`.  
  
- Inserta `arr[i]` en `bucket[n*array[i]]`.  
- Ordena los cubos individuales utilizando la ordenación por inserción.  
- Concatenar todos los cubos ordenados.
![[Pasted image 20231030181327.png|center]]
![[Pasted image 20231030181338.png|center]]
___
## Explicación

### Paso 1: Crear una matriz de tamaño 10, donde cada ranura representa un cubo.

![[Pasted image 20231030181549.png|center]]
### Paso 2: Insertar elementos en los cubos de la matriz de entrada en función de su rango.

Inserción de elementos en los cubos:  
  
- Tome cada elemento de la matriz de entrada.  
- Multiplique el elemento por el tamaño de la matriz de cubos (10 en este caso). Por ejemplo, para el elemento `0.23`, obtenemos `0.23 * 10 = 2.3`.  
- Convierta el resultado en un número entero, que nos da el índice del cubo. En este caso, 2,3 se convierte en el número entero 2.  
- Inserte el elemento en el cubo correspondiente al índice calculado.  
- Repite estos pasos para todos los elementos de la matriz de entrada.

![[Pasted image 20231030181629.png|center]]
### Paso 3: Ordenar los elementos de cada cubo. En este ejemplo, utilizamos `quicksort` (o cualquier algoritmo de ordenación estable) para ordenar los elementos dentro de cada cubo.

Clasificación de los elementos dentro de cada cubo:  
  
- Aplique un algoritmo de ordenación estable (por ejemplo, `quicksort`) para ordenar los elementos de cada cubo.  
- Los elementos de cada cubo ya están ordenados.

![[Pasted image 20231030181730.png|center]]
### Paso 4: Recoge los elementos de cada cubo y vuelve a colocarlos en la matriz original.

Reunir elementos de cada cubo:  
  
- Recorrer cada cubo en orden.  
- Inserta cada elemento individual del cubo en la matriz original.  
- Una vez copiado un elemento, se elimina del cubo.  
- Repita este proceso para todos los cubos hasta que todos los elementos se han reunido.

![[Pasted image 20231030181804.png|center]]
### Paso 5: El array original contiene ahora los elementos ordenados.

El array ordenado final usando bucket sort para la entrada dada es `[0.12, 0.17, 0.21, 0.23, 0.26, 0.39, 0.68, 0.72, 0.78, 0.94]`.

![[Pasted image 20231030181847.png|center]]
____
## Complejidad

- **Complejidad temporal**: $O(n^2)$.
- **Espacio auxiliar**: $O(n+k)$.

La complejidad computacional depende del algoritmo utilizado para ordenar cada cubo, del número de cubos a utilizar y de si la entrada está uniformemente distribuida.  
  
En el **peor de los casos**, la complejidad temporal de la ordenación por cubos es $O(n^2)$ si el algoritmo de ordenación utilizado en el cubo es la ordenación por inserción, que es el caso de uso más común, ya que se espera que los cubos no tengan demasiados elementos en relación con la lista completa. En el peor de los casos, todos los elementos se colocan en un cubo, con lo que el tiempo de ejecución se reduce a la complejidad en el peor de los casos de la ordenación por inserción (todos los elementos están en orden inverso). Si el tiempo de ejecución en el peor de los casos de la ordenación intermedia utilizada es $O(n * log(n))$, entonces el tiempo de ejecución en el peor de los casos de la ordenación por cubos también será $O(n * log(n))$.  
  
Por término medio, cuando la distribución de los elementos en los cubos es razonablemente uniforme, se puede demostrar que la ordenación en cubos se ejecuta en $O(n + k)$ para k cubos.
## Implementación

```js
// InsertionSort to be used within bucket sort
function insertionSort(array) {
  var length = array.length;
  
  for(var i = 1; i < length; i++) {
    var temp = array[i];
    for(var j = i - 1; j >= 0 && array[j] > temp; j--) {
      array[j+1] = array[j];
    }
    array[j+1] = temp;
  }
  
  return array;
}

// Implement bucket sort
function bucketSort(array, bucketSize) {
  if (array.length === 0) {
    return array;
  }

  // Declaring vars
  var i,
      minValue = array[0],
      maxValue = array[0],
      bucketSize = bucketSize || 5;
  
  // Setting min and max values
  array.forEach(function (currentVal) {
  	if (currentVal < minValue) {
  		minValue = currentVal;
  	} else if (currentVal > maxValue) {
  		maxValue = currentVal;
  	}
  })

  // Initializing buckets
  var bucketCount = Math.floor((maxValue - minValue) / bucketSize) + 1;
  var allBuckets = new Array(bucketCount);
  
  for (i = 0; i < allBuckets.length; i++) {
    allBuckets[i] = [];
  }
  
  // Pushing values to buckets
  array.forEach(function (currentVal) {
  	allBuckets[Math.floor((currentVal - minValue) / bucketSize)].push(currentVal);
  });

  // Sorting buckets
  array.length = 0;
  
  allBuckets.forEach(function(bucket) {
  	insertionSort(bucket);
  	bucket.forEach(function (element) {
  		array.push(element)
  	});
  });

  return array;
}
```
