**Input**: Una secuencia de $n$ números $\langle a_1; a_2;...;a_n \rangle$.
**Output**: Una permutación (reordenación) $\langle a'_1, a'_2, ..., a'_n \rangle$ de la secuencia de entrada dado que $a'_1$ $\le$ $a'_2$ $\le$ $...$ $\le$ $a'_n$.  

Los números que deseamos ordenar también se conocen como _claves_ (**keys**). Aunque conceptualmente estamos ordenando una secuencia, la entrada nos llega en forma de matriz con $n$ elementos.
![[Pasted image 20231110191430.png|center]]

Es un algoritmo _eficaz para ordenar un pequeño número de elementos_. La ordenación por inserción funciona como mucha gente ordena una mano de cartas. Empezamos con la mano izquierda vacía y las cartas boca abajo sobre la mesa. A continuación, retiramos una carta cada vez de la mesa y la insertamos en la posición correcta en la mano izquierda. Para encontrar la posición correcta de una carta, la comparamos con cada una de las cartas que ya están en la mano, de derecha a izquierda, como se ilustra en la figura. En todo momento, las cartas que se tienen en la mano izquierda están ordenadas, y estas cartas originalmente eran las cartas superiores del montón de la mesa.

Presentamos nuestro pseudocódigo para la ordenación por inserción como un procedimiento llamado $INSERTION\ SORT$, que toma como parámetro un array $A[1...n]$ que contiene una secuencia de longitud $n$ que debe ordenarse. (En el código, el número $n$ de elementos en $A$ se denota por `A.length`). El algoritmo ordena los números de entrada **en su lugar**: reordena los números dentro del **array A**, con un número constante de ellos almacenados fuera del array en cualquier momento. El array de entrada **A** contiene la secuencia de salida ordenada cuando finaliza el procedimiento **INSERTION-SORT**.

![[Pasted image 20231110192904.png|center]]

Operación **INSERTION-SORT** en el array **A** = $[5,2,4,6,1,3]$. Los índices del array aparecen sobre los rectángulos, y los valores almacenados en las posiciones del array aparecen dentro de los rectángulos.
- $(a)-(e)$ Las iteraciones del **bucle for** de las líneas $1-8$. En cada iteración, el rectángulo negro contiene la clave tomada de $A[j]$, que se compara con los valores en rectángulos sombreados a su izquierda en la prueba de la línea $5$. Las flechas sombreadas muestran los valores del array movidos una posición a la derecha en la línea $6$, y las flechas negras indican a dónde se mueve la clave en la línea $8$. 
- ($f$) El array ordenado final.

```java
for j = 2 to A.length
	key = A[j]
	// Insert A[j] into the sorted sequence A[1...j - 1].
	i = j - 1
	while i > 0 and A[i] > key
		A[i + 1] = A[i]
		i = i - 1
	A[i + 1] = key
```
### Invariantes de bucle y corrección de la ordenación por inserción

```ad-info 
title:¿Que es una invariante?
Magnitud o expresión matemática que no cambia de valor al sufrir determinadas transformaciones; por ejemplo, la distancia entre dos puntos de un sólido que se mueve pero no se deforma.
```

El índice $j$ indica la "**carta actual**" que se introduce en la mano. Al principio de cada iteración del **bucle `{js}for`**, que está _indexado_ por $j$, el subarray formada por los elementos $A\ [1...j - 1]$ constituye la mano actualmente ordenada, y el subarray restante $A\ [j + 1...n]$ corresponde al montón de cartas que aún están sobre la mesa. De hecho, los elementos $A\ [1...j - 1]$ son los elementos que originalmente estaban en las posiciones $1$ a $j - 1$, pero ahora ordenados. Enunciamos estas propiedades de $A \ [1...j - 1]$ formalmente como un invariante de bucle:

> [!hint] 
> Al comienzo de cada iteración del **bucle `{js}for`** de las líneas $1-8$, el subarray $A \ [1...j-1]$ está formada por los elementos originalmente en $A\ [1...j-1]$, pero ordenados.

Utilizamos invariantes de bucle para ayudarnos a entender por qué un algoritmo es correcto. Debemos demostrar tres cosas sobre un invariante de bucle:

- **Inicialización**: Es verdadero antes de la primera iteración del bucle. 
- **Mantenimiento**: Si es verdadera antes de una iteración del bucle, sigue siéndolo antes de la siguiente iteración.
- **Terminación**: Cuando el bucle termina, el invariante nos da una propiedad útil que ayuda a demostrar que el algoritmo es correcto.

Cuando se cumplen las dos primeras propiedades, _la invariante del bucle es cierta antes de cada iteración del bucle_. (Por supuesto, somos libres de utilizar hechos establecidos distintos de la propia invariante del bucle para demostrar que la invariante del bucle sigue siendo cierta antes de cada iteración). Nótese la similitud con la inducción matemática, donde para demostrar que una propiedad es cierta, se demuestra un caso base y un paso inductivo. Aquí, demostrar que la invariante se mantiene antes de la primera iteración corresponde al caso base, y demostrar que la invariante se mantiene de iteración en iteración corresponde al paso inductivo.

La tercera propiedad es quizás la más importante, ya que estamos utilizando la invariante de bucle para demostrar la corrección. Típicamente, usamos el invariante del bucle junto con la condición que causó la terminación del bucle. La propiedad de terminación difiere de cómo solemos utilizar la inducción matemática, en la que aplicamos el paso inductivo infinitamente; aquí, detenemos la "inducción" cuando el bucle termina.

Veamos cómo se mantienen estas propiedades para la ordenación por inserción.

- **Inicialización**: Empezamos mostrando que la invariante del bucle se mantiene antes de la primera iteración del bucle, cuando $j = 2.^1$ El subarray $A[1...j-1]$, por tanto, consiste en un único elemento $A[1]$, que es de hecho el elemento original de $A[1]$. Además, este subarray está ordenada (trivialmente, por supuesto), lo que muestra que la invariante del bucle se mantiene antes de la primera iteración del bucle. Además, este subarray está ordenada (trivialmente, por supuesto), lo que demuestra que la invariante del bucle se mantiene antes de la primera iteración del bucle. 

>[!info]- 1 
>Cuando el bucle es un **bucle for**, el momento en el que comprobamos la invariante del bucle justo antes de la primera iteración es inmediatamente después de la asignación inicial a la variable contador del bucle y justo antes de la primera prueba en la cabecera del bucle. En el caso de **INSERTION-SORT**, este momento es después de asignar $2$ a la variable $j$ pero antes de la primera prueba de si $j$ `<=` $A.length$.

- **Mantenimiento**: A continuación, abordamos la segunda propiedad: demostrar que cada iteración mantiene la invariante del bucle. Informalmente, el cuerpo del **bucle for** funciona moviendo $A[j-1]$, $A[j-2]$, $A[j-3]$, y así sucesivamente una posición a la derecha hasta que encuentra la posición adecuada para $A[j]$ (líneas $4-7$), momento en el que inserta el valor de $A[j]$ (línea $8$). La subarray $A[1...j]$ se compone entonces de los elementos originalmente en $A[1...j]$, pero en orden. El incremento de $j$ para la siguiente iteración del **bucle for** preserva la invariante del bucle.
  Un tratamiento más formal de la segunda propiedad nos exigiría enunciar y mostrar una invariante de bucle para el **bucle while** de las líneas $5-7$. En este punto, sin embargo, preferimos no enredarnos en tal formalismo, por lo que nos basamos en nuestro análisis informal para demostrar que la segunda propiedad se mantiene para el bucle exterior.

- **Terminación**: Por último, examinamos qué ocurre cuando el bucle termina. La condición que hace que el **bucle for** termine es que $j > A.length = n$. Como cada iteración del bucle incrementa $j$ en $1$, debemos tener $j = n + 1$ en ese momento. Sustituyendo $n+1$ por $j$ en el enunciado del invariante del bucle, tenemos que el subarray $A[1...n]$ está formada por los elementos originalmente en $A[1...n]$, pero ordenados. Observando que el subarray $A[1...n]$ es toda la matriz, concluimos que toda la matriz está ordenada. Por lo tanto, el algoritmo es correcto.

Utilizaremos este método de invariantes de bucle para demostrar la corrección más adelante en este capítulo y también en otros capítulos.

____

> [!definition]
> La **ordenación por inserción** es un algoritmo de ordenación sencillo que funciona de forma similar a como se ordenan las cartas en las manos. La matriz se divide virtualmente en una parte ordenada y otra sin ordenar. Los valores de la parte sin ordenar se eligen y se colocan en la posición correcta en la parte ordenada.
> 
> Para ordenar un array de tamaño N en orden ascendente iteramos sobre el array y comparamos el elemento actual (clave) con su predecesor, si el elemento clave es menor que su predecesor, lo comparamos con los elementos anteriores. Mueve los elementos mayores una posición hacia arriba para hacer espacio para el elemento intercambiado.

![[insertionsort.gif|center]]
![[insertionsort2.gif|center]]
___
## Explicación

`arr[]: {12, 11, 13, 5, 6}`

|12|11|13|5|6|
|---|---|---|---|---|
### Primer paso

- Inicialmente, los dos primeros elementos de la matriz se comparan en la ordenación por inserción.

| **12** | **11** | 13  | 5   | 6   | 
| ------ | ------ | --- | --- | --- |

- Aquí, 12 es mayor que 11, por lo que no están en orden ascendente y 12 no está en su posición correcta. Por lo tanto, intercambia 11 y 12.  
- Así, por ahora 11 se almacena en un subarray ordenado.

| **11** | **12** | 13  | 5   | 6   | 
| ------ | ------ | --- | --- | --- |
### Segundo paso

- Ahora, pasa a los dos elementos siguientes y compáralos

| 11  | **12** | **13** | 5   | 6   |
| --- | ------ | ------ | --- | --- |

- Aquí, 13 es mayor que 12, por lo que ambos elementos parecen estar en orden ascendente, por lo tanto, no se producirá ningún intercambio. 12 también se almacena en una submatriz ordenada junto con 11
### Tercer paso

- Ahora, dos elementos están presentes en la submatriz ordenada que son 11 y 12  
- Pasamos a los dos elementos siguientes que son 13 y 5

| 11  | 12  | **13** | **5** | 6   | 
| --- | --- | ------ | ----- | --- |

- Tanto 5 como 13 no están presentes en su lugar correcto así que intercámbialos

| 11  | 12  | **5** | **13** | 6   | 
| --- | --- | ----- | ------ | --- |

- Tras el intercambio, los elementos 12 y 5 no están ordenados, por lo que se intercambian de nuevo

| 11  | **5** | **12** | 13  | 6   | 
| --- | ----- | ------ | --- | --- |

- Aquí, de nuevo 11 y 5 no están ordenados, por lo tanto intercambiar de nuevo

| **5** | **11** | 12  | 13  | 6   | 
| ----- | ------ | --- | --- | --- |

- Aquí, 5 está en su posición correcta
### Cuarto paso

- Ahora, los elementos que están presentes en la submatriz ordenada son 5, 11 y 12  
- Pasamos a los dos elementos siguientes 13 y 6

| 5   | 11  | 12  | **13** | **6** | 
| --- | --- | --- | ------ | ----- |

- Evidentemente, no están ordenados, por lo que realizar el intercambio entre ambos

| 5   | 11  | 12  | **6** | **13** | 
| --- | --- | --- | ----- | ------ |

- Ahora, 6 es menor que 12, por lo tanto, intercambiar de nuevo

| 5   | 11  | **6** | **12** | 13  | 
| --- | --- | ----- | ------ | --- |

- Aquí, también el intercambio hace 11 y 6 sin clasificar por lo tanto, el intercambio de nuevo

| 5   | **6** | **11** | 12  | 13  |
| --- | ----- | ------ | --- | --- |

- Por último, la matriz está completamente ordenada.

![[Pasted image 20231030180446.png|center]]
___
## Complejidad

|Name|Best|Average|Worst|Memory|Stable|Comments|
|---|:-:|:-:|:-:|:-:|:-:|:--|
|**Insertion sort**|$n$|$n^2$|$n^2$|$1$|Yes|

Complejidad temporal: $O(N^2)$  
Espacio auxiliar: $O(1)$
## Implementación

```js
const insertionSort = (array) => {
  for (let i = 1; i < array.length; i++) {
    let currentElement = array[i];
    let lastIndex = i - 1;

    while (lastIndex >= 0 && array[lastIndex] > currentElement) {
      array[lastIndex + 1] = array[lastIndex];
      lastIndex--;
    }
    array[lastIndex + 1] = currentElement;
  }

  return array;
};
```

