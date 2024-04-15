Lo primero a considerar es que los [[Array]] están ordenados, mantienen una relación profunda con tareas de ordenamiento. Cada elemento de un arreglo posee un índice numérico.

En general si no requieres ordenar algo, no requieres utilizar un arreglo, sin embargo si requieres optimizar por cuestiones de rendimiento, lo mejor es utilizar otro tipo de estructuras, e incluso cuando se requiere algunos tipos de ordenamiento, existen estructuras pensadas para esto, como pueden ser las listas o listas enlazadas.
## ¿Cuándo utilizar un arreglo?

Los arreglos son recomendables cuando cuando se requiere realizar mantener un orden.
## ¿Cuál es el time complexity de los arreglos?

- Para insertar valores (depende la posición).
- Para eliminar valores (depende la posición).
- Para buscar valores $O(n)$.
- Para acceder a valores $0(1)$.

Cuando hablamos de acceder a valores nos referimos a utilizar el índice directamente. Cuando accedemos a un valor, independientemente del tamaño del arreglo, esta operación resulta inmediata.

Para el proceso de insertar, la complejidad depende de la posición en la cual se va a insertar. Si por ejemplo se hace al final del arreglo entonces es una operación inmediata $0(1)$, pero si se se hace al inicio se tienen que desplazar todos los índices posteriores $O(n)$. Lo mismo aplica para el proceso de eliminar valores de un arreglo, si eliminamos el primer elemento esto implica reajustar todos los índices $O(n)$. Por ello las operaciones **push (empujar al final)** y **pop (eliminar del final)** son inmediatas $O(1)$, mientras que **shift (agregar al inicio)** y **unshift (eliminar del inicio)** son proporcionales al valor de “n” $O(n)$.

## ¿Cuál es el time complexity de los métodos de arreglos de JavaScript?

La siguiente es la lista de complejidad de algunos métodos de JavaScript.

- push $O(1)$
- pop $O(1)$
- shift $O(n)$
- unshift $O(n)$
- concat $O(n)$
- slice $O(n)$
- splice $O(n)$
- sort $O(n log n)$
- forEach / map / filter / reduce / etc $O(n)$