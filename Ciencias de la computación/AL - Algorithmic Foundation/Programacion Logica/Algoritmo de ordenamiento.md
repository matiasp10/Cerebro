## Algoritmo de burbuja

La estrategia del método de ordenamiento por burbuja tiene su base en la comparación de pares de elementos adyacentes e intercambiarlos entre sí. Suponiendo que se desea ordenar un arreglo unidimensional por este método, entonces se deben recorrer sus elementos, se comparan de a pares en forma adyacente y se intercambia hasta llegar al final del arreglo. Este procedimiento se debe repetir hasta que todos los elementos del arreglo se encuentren ordenados.

Suponiendo un arreglo unidimensional X en N elementos, el pseudocodigo del algoritmo de ordenamiento por burbuja en orden creciente es el siguiente:

```
para i ← 1 hasta N-1 hacer

para j ← 1 hasta N-1 hacer

si X[j] > X [j+1] entonces

// intercambiar 

AUX ← X [j]

X[j] ←X [j+1]

X [j+1] ← AUX

fin-si

fin-para

fin-para
```
## Algoritmo de burbuja mejorado

La cantidad de comparaciones que se realizan utilizando el algoritmo de burbuja se puede reducir con una pequeña modificación. Si se ordena crecientemente un arreglo unidimensional utilizando el método burbuja, una vez finalizado el primer recorrido, el mayor elemento se encuentra en la última posición y, por consiguiente, no es necesario comparar el ultimo par de elementos en el siguiente recorrido, ya que el elemento más grande ya fue ordenado. Esta lógica de evitar comparaciones innecesarias se puede repetir a medida que se ordenan los mayores elementos en las ultimas posiciones. Esta variante del algoritmo de burbuja se denomina burbuja mejorada.

Suponiendo un arreglo unidimensional X de N elementos, el pseudocódigo del algoritmo de ordenamiento por burbuja mejorada en orden creciente es el siguiente:

```
para i ←1 hasta N-1 hacer

para j ← 1 hasta N-i hacer

si X [j] > X [j+1] entonces

//intercambiar

AUX ← X [j]

X[j] ← X [j+1]

X [j+1] ← AUX

fin-si

fin-para

fin-para
```
## Algoritmo de inserción

La estrategia de este método de ordenamiento consiste en tomar un elemento del conjunto e insertado en una parte ya ordenada. Se debe repetir este procedimiento para el resto de los elementos que restan por ordenar.

Suponiendo un arreglo unidimensional X de N elementos, el pseudocodigo del algoritmo de ordenamiento por inserción en orden creciente es el siguiente:

```
para i ← 2 hasta N hacer

AUX ← X[i]

k ← i-1

sw ← falso

mientras NO (sw) y (K>= 1) hacer

si AUX < X[k] entonces

X[k+1] ← X[k]

k ← k-1

si-no

sw ← verdadero

fin-si

fin-mientras

X[k+1] ← AUX

fin-para
```
## Algoritmo de selección

Suponiendo que se desea ordenar un arreglo unidimensional en forma creciente, el método de ordenamiento por selección consiste en recorrer el arreglo para buscar el menor elemento e intercambiarlo con el elemento de la primera posición. Se debe recorrer nuevamente el arreglo para buscar el segundo menor elemento e intercambiarlo con el elemento de la segunda posición. Este procedimiento se debe aplicar para el resto de los elementos hasta que el arreglo se encuentre ordenado.

Suponiendo un arreglo unidimensional X de N elementos, el pseudocodigo del algoritmo de ordenamiento por selección en orden creciente es el siguiente:

```
para i ← hasta N-1 hacer

AUX ← X[i]

k←i

para j ← i+1 hasta N hacer

si X[j] < AUX entonces

AUX ← X[j]

k←j

fin-si 

fin-para

X[k] ←X[i]

X[i] ← AUX

fin-para
```

