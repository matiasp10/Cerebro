Dado un algoritmo para resolver un problema concreto, es natural que nos preguntemos:

1. _¿Qué se supone que debe hacer?_
2. _¿Hace realmente lo que se supone que debe hacer?_
3. _¿Con qué eficacia lo hace?_

Los términos técnicos utilizados normalmente para estos tres aspectos son:

1. **Especificación**.
2. **Verificación**.
3. **Análisis del rendimiento**

Los detalles de estos tres aspectos dependerán normalmente del problema.

La **especificación** debe formalizar los detalles cruciales del problema que el algoritmo pretende resolver. A veces se basará en una representación concreta de los datos asociados, y a veces se presentará de forma más abstracta. Normalmente, tendrá que especificar cómo se relacionan las entradas y salidas del algoritmo, aunque no hay ningún requisito general de que la especificación sea completa o no ambigua.

En el caso de los problemas sencillos, a menudo es fácil ver que un algoritmo concreto siempre funciona, es decir, que satisface su especificación.
Sin embargo, en el caso de especificaciones y/o algoritmos, _el hecho de que un algoritmo satisfaga su especificación puede no ser obvio en absoluto_. En este caso, tenemos que dedicar algún esfuerzo a **verificar** si el algoritmo es realmente correcto.
En general, las pruebas con unas pocas entradas específicas pueden bastar para demostrar que el algoritmo es incorrecto.

Sin embargo, dado que el número de entradas potenciales diferentes para la mayoría de los algoritmos es infinito en teoría, y enorme en la práctica, se necesita algo más que probar casos particulares para asegurarse de que el algoritmo satisface su especificación. **Necesitamos pruebas de corrección**.

Por último, la **eficiencia o el rendimiento de un algoritmo** están relacionados con los _recursos que necesita_, como la velocidad a la que se ejecuta o la cantidad de memoria que utiliza.
Esto suele depender del _tamaño de la instancia del problema_, de la _elección de la representación de los datos_ y de _los detalles del algoritmo_. De hecho, esto es lo que normalmente impulsa el desarrollo de _nuevas estructuras de datos y algoritmos_. 