La complejidad temporal en programación es una **medida de la cantidad de tiempo que tarda un algoritmo en ejecutarse**. Se utiliza para _comparar la eficiencia de diferentes algoritmos para resolver un mismo problema_.

La complejidad temporal se expresa en términos de la entrada del algoritmo, que generalmente es el tamaño del problema que se está resolviendo. Por ejemplo, el algoritmo de búsqueda binaria tiene una complejidad temporal de $O(log n)$, donde `n` es el tamaño del conjunto de datos que se está buscando. Esto significa que el tiempo de ejecución del algoritmo aumenta en proporción al logaritmo del tamaño de la entrada.
## Categorías de complejidad temporal

### $O(1)$

El tiempo de ejecución es constante, independientemente del tamaño de la entrada.
**Por ejemplo**: La búsqueda de un elemento en un arreglo ordenado, la suma de dos números, la multiplicación de dos números.
### $O(n)$

El tiempo de ejecución es lineal, es decir, aumenta en proporción al tamaño de la entrada.
**Por ejemplo**: El barrido de un arreglo, la búsqueda de un elemento en un arreglo sin ordenar, la ordenación de un arreglo por selección.
### $O(n^2)$

El tiempo de ejecución es cuadrático, es decir, aumenta en proporción al cuadrado del tamaño de la entrada.
**Por ejemplo**: La ordenación de un arreglo por burbuja, la búsqueda de un elemento en un árbol binario completo.

La complejidad temporal _también se puede expresar en términos de funciones más complejas_, como la función exponencial o la función logarítmica.

Aquí hay algunos ejemplos de complejidad temporal con funciones más complejas:

- $O(2^n)$: La búsqueda exhaustiva de un elemento en un conjunto, el cálculo del factorial de un número.
- $O(log n)$: La búsqueda binaria, el cálculo de la raíz cuadrada de un número.

La complejidad temporal es un concepto importante en la informática, ya que ayuda a los programadores a elegir el algoritmo más eficiente para resolver un problema.