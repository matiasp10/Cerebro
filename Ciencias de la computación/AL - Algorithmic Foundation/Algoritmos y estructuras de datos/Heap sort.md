> [!definition]
> **Heapsort** es un algoritmo de ordenación basado en la comparación. Heapsort puede considerarse como una ordenación por selección mejorada: como ese algoritmo, divide su entrada en una región ordenada y otra sin ordenar, y reduce iterativamente la región sin ordenar extrayendo el elemento más grande y moviéndolo a la región ordenada. La mejora consiste en el uso de una estructura de datos de montón en lugar de una búsqueda en tiempo lineal para encontrar el máximo.

**Heap Sort** se considera mejor que **quicksort** en el peor de los casos ya que su complejidad temporal es $O(nlogn)$ que es mejor que $O(n²)$ de **quicksort**. Puede que te preguntes qué es un árbol binario casi completo en el que se realiza la ordenación en montón. Entendámoslo primero.
___
## ¿Qué es el árbol binario casi completo?

Un árbol binario es casi completo si cumple las siguientes condiciones -  
  
1. Cada nodo debe tener primero un hijo izquierdo antes de tener un hijo derecho. Es decir, ningún nodo puede tener sólo hijo derecho sin tener hijo izquierdo.  
2. Cada nivel del árbol debe estar completo antes de pasar al siguiente nivel.
![[Pasted image 20231030191313.png|center]]

Obsérvese que se cumplen ambas condiciones.
![[Pasted image 20231030191332.png|center]]

En el árbol anterior, la segunda condición no se cumple, ya que este árbol tiene un tercer nivel antes de completar el segundo nivel (el nodo padre no tiene el hijo derecho).  
  
Ahora, el árbol binario casi completo debe ser `max-heap` o `min-heap` para realizar la ordenación.
### ¿Qué es max-heap?

> [!note] 
> Un árbol binario casi completo en el que el nodo padre es siempre mayor que sus hijos se denomina max-heap.

Veamos un ejemplo en el que cada padre es mayor que sus hijos.

![[Pasted image 20231030191603.png|center]]

Ten en cuenta que el max-heap aún no está ordenado, si lo representamos en un array lo entenderás mejor.

![[Pasted image 20231030191620.png|center]]
### ¿Qué es min-heap?

> [!note] 
> Un árbol binario casi completo en el que el nodo padre es siempre más pequeño que sus hijos se denomina minicúmulo.

![[Pasted image 20231030191802.png|center]]

Si queremos ordenar los elementos en orden decreciente podemos hacerlo fácilmente con un min-heap y si queremos ordenarlos en orden creciente entonces max-heap puede hacerlo fácilmente.
## Explicación 

En primer lugar, necesitamos construir un max-heap o min-heap a partir de un árbol binario casi completo. Vamos a construir max-heap aquí para que los elementos pueden ser ordenados en orden creciente. Vamos a llamar a la construcción de max-heap como un proceso de max-heapify.

### 1. Building max-heap

Para construir el max-heap, el último padre que está presente en la posición $(n/2)-1$ (n es el número total de elementos) se compara con sus hijos.
![[Pasted image 20231030192228.png|center]]
![[Pasted image 20231030192238.png|center]]

Voila!! We now have a max-heap —

![[Pasted image 20231030192254.png|center]]

```js
function max_heapify(a,i,n){
    let left = 2*i;              //Left child index
    let right = 2*i+1;           //Right child index
    let maximum;
    if(right<n){                 //Checks if right child exist
        if(a[left]>=a[right]){    //Compares children to find maximum
            maximum = left;
        }
        else{
            maximum = right;
        }
    }
    else if(left<n){                //Checks if left child exists
        maximum = left;
    }
    else return;                    //In case of no children return
    if(a[i]<a[maximum]){            //Checks if the largest child is greater than parent
        swap(a,i,maximum);          //If it is then swap both
        max_heapify(a,maximum,n);       //max-heapify again
    }
    return;
}
```

La complejidad temporal para construir max-heap es $O(n)$. La complejidad temporal depende del número de intercambios y comparaciones realizadas. Como empezamos a construir max-heap desde el índice 2, el bucle se ejecuta $n/2$ veces. Para los elementos en los índices 1 y 2, se realizan dos comparaciones con cada uno de sus hijos, pero sólo se realiza un intercambio para ellos. Por lo tanto, para un intercambio hay dos comparaciones ya que el bucle se ejecuta $n/2$ veces por lo tanto para $n/2$ intercambios hay n comparaciones. Por tanto, Complejidad temporal = $O(n/2 +n) = O(n)$.
### 2. Deleting the root element

El montón todavía no está ordenado. Para ordenar los elementos en orden ascendente tenemos que eliminar el elemento más grande y colocarlo en la última posición y seguir haciendo eso hasta que tengamos elementos ordenados.  
  
Así que aquí 50 se elimina y luego el último elemento se coloca en su posición.

![[Pasted image 20231030192741.png|center]]

El heap obtenido no es un max-heap por lo tanto necesitamos max-heapificarlo de nuevo.  
  
Complejidad temporal del paso de borrado  
  
Este paso requiere un tiempo de $O(1)$, ya que sólo intercambiamos el último elemento y el elemento raíz.
### 3. Fixing the max-heap

![[Pasted image 20231030192829.png|center]]

![[Pasted image 20231030192837.png|center]]

Se repite el proceso de borrar el elemento raíz y luego realizar max-heapify hasta que obtenemos un array ordenado de elementos. Esto se hace n veces ya que hay n número de elementos.  
  
Complejidad temporal para fijar max-heap  
  
Como nos estamos moviendo en un solo camino del árbol de altura $logn$ para obtener el max-heap de nuevo, por lo tanto, su complejidad temporal es $O(log n)$

```js
function heapSort(a){
    let n = a.length;
    for(let i=Math.floor(n/2)-1;i>=0;i--){
        max_heapify(a,i,n);            //Building max heap
    }
    for(let i = n-1;i>=0;i--){
        swap(a,0,i);              //Deleting root element
        max_heapify(a,0,i);           //Building max heap again
    }
    return a;
}
```
## Complejidad

La complejidad temporal se divide en dos pasos  
  
1. Max-heapify - $O(n)$  
2. n veces-  
	1. Deletion - $O(1)$  
	2. Max-heapify - $O(log n)$  = $O(n + n * O(logn)) = O(nlogn)$
