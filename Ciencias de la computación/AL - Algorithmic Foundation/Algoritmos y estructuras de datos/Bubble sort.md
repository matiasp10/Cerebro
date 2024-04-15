Bubble Sort es el algoritmo de ordenación más sencillo que funciona intercambiando repetidamente los elementos adyacentes si están en el orden incorrecto. Este algoritmo no es adecuado para grandes conjuntos de datos, ya que su complejidad temporal media y en el peor de los casos es bastante alta.

>[!info]
>En este algoritmo, se recorre desde la izquierda y se comparan los elementos adyacentes y el más alto se coloca a la derecha.
>De este modo, el elemento más grande se desplaza primero al extremo derecho.
>Este proceso continúa para encontrar el segundo más grande y colocarlo, y así sucesivamente hasta que los datos estén ordenados.

![[bubblesort.gif|center]]
## Explicación 

Input: `arr[] = {6, 3, 0, 5}`
### Primer paso

El elemento más grande se coloca en su posición correcta, es decir, al final de la matriz.

![[Pasted image 20231030133702.png]]
### Segundo paso

Coloca el segundo elemento más grande en la posición correcta

![[Pasted image 20231030133718.png]]
### Tercer paso

Coloca los dos elementos restantes en sus posiciones correctas.

![[Pasted image 20231030134106.png]]

- Nº total de pasadas: $n-1$  
- Nº total de comparaciones: $n*(n-1)/2$
___
## Complejidad

|Name|Best|Average|Worst|Memory|Stable|Comments|
|---|:-:|:-:|:-:|:-:|:-:|:--|
|**Bubble sort**|$n$|$n^2$|$n^2$|$1$|Yes|

Complejidad temporal: $O(N^2)$ 
Espacio auxiliar: $O(1)$
## Ventajas

- La clasificación por burbujas es fácil de entender y aplicar.  
- No requiere espacio de memoria adicional.  
- Es un algoritmo de ordenación estable, lo que significa que los elementos con el mismo valor clave mantienen su orden relativo en la salida ordenada.
## Desventajas

- La ordenación por burbujas tiene una complejidad temporal de O(N2), lo que la hace muy lenta para grandes conjuntos de datos.  
- La ordenación por burbujas es un algoritmo de ordenación basado en la comparación, lo que significa que requiere un operador de comparación para determinar el orden relativo de los elementos en el conjunto de datos de entrada. Esto puede limitar la eficacia del algoritmo en determinados casos.
## Implementación 

```js
const bubbleSort = (arr) => {
  let swapped;

  do {
    swapped = false;
    for (let i = 0; i < arr.length - 1; i++) {
      if (arr[i] > arr[i + 1]) {
        let temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;
        swapped = true;
      }
    }
  } while (swapped);

  return arr;
};
```
### Paso 1: Crear una variable booleana  

Necesitarás saber si se ha realizado algún intercambio en la iteración actual del array. Para ello, crea una variable booleana llamada "swapped".

```js
let swapped;
```
### Paso 2: Crear un bucle "`do-while`" para iterar hasta que el array esté ordenado  

Usemos el bucle "`do-while`" para iterar a través del array hasta que esté ordenado. El bucle se ejecuta al menos una vez, incluso si el array ya está ordenado - por eso es mejor usarlo para esto.  
  
También utilizaremos la variable "swapped" para comprobar si se ha realizado algún intercambio en la iteración actual.

```js
do {
  // code to be executed
} while (swapped);
```
### Paso 3: Poner la variable booleana a false al principio de cada iteración  

Al principio de cada iteración, tienes que poner la variable "swapped" a false. Esto se debe a que aún no se ha realizado ningún intercambio en la iteración actual.

```js
do {
  swapped = false;
  // code to be executed
} while (swapped);
```
### Paso 4: Utilizar un bucle "`for`" para comparar elementos adyacentes  

Dentro del bucle "do-while", utilizamos un bucle "for" para comparar cada elemento de la matriz con el elemento contiguo. Si el elemento actual es mayor que el siguiente, se intercambian.  
  
También establecemos la variable "swapped" a true si se realiza un intercambio, indicando que la matriz aún no está ordenada.

```js
for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] > arr[i + 1]) {
      let temp = arr[i];
      arr[i] = arr[i + 1];
      arr[i + 1] = temp;
      swapped = true;
    }
  }
} while (swapped);
```
### Paso 5: Repetir el bucle hasta que no se realicen más intercambios.  

Si no se realiza ningún intercambio en la iteración actual, la variable "swapped" permanece falsa. Esto significa que el array está ordenado y podemos salir del bucle.  
  
Si se han intercambiado elementos, la variable "swapped" se pone a true, y el bucle continúa iterando hasta que el array está ordenado.
### Probar el algoritmo de ordenación por burbujas  

Para probar el algoritmo de ordenación por burbujas, puede crear un array de números aleatorios y pasarlo a la función `bubbleSort()`.  
  
He aquí un ejemplo:

```js
let myArray = [12, 10, 3, 7, 4];
console.log(bubbleSort(myArray)); // Output: [3, 4, 7, 10, 12]
```
