#AL 
___

Supongamos que los ordenadores fueran infinitamente rápidos y la memoria fuera gratuita. ¿Tendría usted alguna razón para estudiar algoritmos? La respuesta es sí, aunque sólo sea porque le gustaría demostrar que su método de solución termina y lo hace con la respuesta correcta. 
Si los ordenadores fueran infinitamente rápidos, cualquier método correcto para resolver un problema valdría. Probablemente querría que su implementación estuviera dentro de los límites de las buenas prácticas de ingeniería de software (por ejemplo, su implementación debería estar bien diseñada y documentada), pero lo más habitual es que utilizara el método que fuera más fácil de implementar. 
Por supuesto, los ordenadores pueden ser rápidos, pero no infinitamente rápidos. Y la memoria puede ser barata, pero no gratuita. Por tanto, el tiempo de cálculo es un recurso limitado, al igual que el espacio en la memoria. Hay que utilizar estos recursos con prudencia, y los algoritmos que son eficientes en términos de tiempo o espacio te ayudarán a hacerlo.
# Eficiencia

Los distintos algoritmos ideados para resolver el mismo problema suelen diferir drásticamente en su eficacia.
Estas diferencias pueden ser mucho más significativas que las debidas al hardware y al software. 
Por ejemplo, El algoritmo **ordenación por inserción** ([[Insertion Sort]]), tarda un tiempo aproximadamente igual a $c_1n^2$ en ordenar $n$ elementos, donde $c_1$ es una constante que no depende de $n$. Es decir, tarda un tiempo aproximadamente proporcional a $n^2$. 
La **ordenación por fusión** ([[Merge Sort]]), tarda aproximadamente lo mismo que $c_{2} n \ lg \ n$, donde $lg \ n$ significa $log_2 \ n$ y $c_2$ es otra constante que tampoco depende de $n$.
La **ordenación por inserción** ([[Insertion Sort]]) suele tener un _factor constante menor que la ordenación por fusión_ ([[Merge Sort]]), de modo que $c_1 < c_2$. 
Los factores constantes pueden tener un impacto mucho menor en el tiempo de ejecución que la dependencia del tamaño de entrada $n$. Escribamos el tiempo de ejecución de la **ordenación por inserción** como $c_{1}n * n$ y el tiempo de ejecución de la **ordenación por fusión** como $c_{2}n * lg \ n$.

Entonces vemos que mientras que la **ordenación por inserción** tiene un factor de $n$ en su tiempo de ejecución, la **ordenación por fusión** tiene un factor de $lg\ n$, que es mucho menor. (Por ejemplo, cuando $n = 1000$, $lg\ n$ es aproximadamente $10$, y cuando $n$ es igual a un millón, $lg\ n$ es aproximadamente sólo $20$). Aunque la **ordenación por inserción** suele ser _más rápida_ que la **ordenación por fusión** para _tamaños de entrada pequeños_, una vez que el tamaño de entrada $n$ es lo suficientemente grande, la ventaja de $lg\ n$ frente a $n$ de la ordenación por fusión compensará con creces la diferencia de factores constantes.

Por mucho que $c_1$ sea más pequeño que $c_2$, siempre habrá un punto de cruce a partir del cual la ordenación por fusión será más rápida. Para ver un ejemplo concreto, enfrentemos a un ordenador más rápido (ordenador $A$) que ejecuta la ordenación por inserción con un ordenador más lento (ordenador $B$) que ejecuta la ordenación por fusión. Cada uno debe ordenar un array de $10$ millones de números (Aunque $10$ millones de números puedan parecer muchos, si los números son enteros de ocho bytes, la entrada ocupa unos $80$ megabytes). Supongamos que el ordenador $A$ ejecuta $10.000$ millones de instrucciones por segundo (más rápido que cualquier ordenador secuencial en el momento de escribir estas líneas) y que el ordenador $B$ ejecuta sólo $10$ millones de instrucciones por segundo, de modo que el ordenador $A$ es $1.000$ veces más rápido que el ordenador $B$ en potencia de cálculo bruta.
Para que la diferencia sea aún más dramática, supongamos que el programador más astuto del mundo codifica la **ordenación por inserción** en lenguaje máquina para el ordenador $A$, y el código resultante requiere $2n^2$ instrucciones para ordenar $n$ números. Supongamos además que un programador mediocre implementa la **ordenación por fusión** utilizando un lenguaje de alto nivel con un compilador ineficiente, y que el código resultante requiere $50n \ lg\ n$ instrucciones. Para ordenar $10$ millones de números, el ordenador A necesita

$$
\frac{2 * (10^7)^2 \ instrucciones}{10^{10} \ instrucciones/segundo} = 20.000 \ segundos \ (mas \ de \ 5.5 \ horas)
$$
Mientras que la computadora $B$ necesita

$$
\frac{50 * (10^7) \ lg \ 10^7 \ instrucciones}{10^{7} \ instrucciones/segundo} \thickapprox 1.163 \ segundos \ (menos \ de \ 20 \ minutos)
$$

Al utilizar un algoritmo cuyo tiempo de ejecución crece más lentamente, incluso con un compilador deficiente, ¡el ordenador $B$ funciona más de $17$ veces más rápido que el ordenador $A$! La ventaja de la **ordenación por fusión** es aún más pronunciada cuando ordenamos $100$ millones de números: mientras que la **ordenación por inserción** tarda más de $23$ días, la **ordenación por fusión** tarda menos de $4$ horas. En general, a medida que aumenta el tamaño del problema, también lo hace la ventaja relativa de la ordenación por fusión.
# Algoritmos y otras tecnologías

El ejemplo anterior demuestra que debemos **considerar los algoritmos**, al igual que el hardware informático, como una tecnología. El rendimiento total del sistema depende de la elección de algoritmos eficientes tanto como de la elección de hardware rápido. Al igual que se producen rápidos avances en otras tecnologías informáticas, también se producen en los algoritmos. Puede que se pregunte si los algoritmos son realmente tan importantes en los ordenadores actuales a la luz de otras tecnologías avanzadas, como:

- Arquitecturas informáticas y tecnologías de fabricación avanzadas.
- Interfaces gráficas de usuario (GUI) intuitivas y fáciles de usar.
- Sistemas orientados a objetos.
- Tecnologías Web integradas.
- Redes rápidas, tanto alámbricas como inalámbricas.

La respuesta es afirmativa. Aunque algunas aplicaciones no requieren explícitamente contenido algorítmico a nivel de aplicación (como algunas aplicaciones sencillas basadas en la Web), muchas sí lo requieren. Por ejemplo, consideremos un servicio basado en la Web que determine cómo viajar de un lugar a otro. Su implementación dependería de un hardware rápido, una interfaz gráfica de usuario, una red de área amplia y posiblemente también de la orientación a objetos. Sin embargo, también necesitaría algoritmos para determinadas operaciones, como la búsqueda de rutas (probablemente mediante un algoritmo de camino más corto), la representación de mapas y la interpolación de direcciones.

Además, incluso una aplicación que no requiera contenido algorítmico a nivel de aplicación depende en gran medida de los algoritmos. ¿La aplicación depende de un hardware rápido? El diseño del hardware utiliza algoritmos. ¿Se basa la aplicación en interfaces gráficas de usuario? El diseño de cualquier interfaz gráfica se basa en algoritmos. ¿La aplicación se basa en redes? El enrutamiento en las redes se basa en gran medida en algoritmos. ¿La aplicación está escrita en un lenguaje distinto del código máquina? Entonces fue procesada por un compilador, un intérprete o un ensamblador, todos los cuales hacen un uso extensivo de algoritmos. Los algoritmos son el núcleo de la mayoría de las tecnologías utilizadas en los ordenadores actuales.

Además, con la capacidad cada vez mayor de los ordenadores, los utilizamos para resolver problemas más grandes que nunca. Como hemos visto en la comparación anterior entre la ordenación por inserción y la ordenación por fusión, las diferencias de eficiencia entre algoritmos son especialmente notables en problemas de mayor tamaño.

Tener una base sólida de conocimientos y técnicas algorítmicas es una característica que separa a los programadores verdaderamente hábiles de los novatos. Con la tecnología informática moderna, puedes realizar algunas tareas sin saber mucho de algoritmos, pero con una buena base de algoritmos, puedes hacer mucho, mucho más.

# Ejercicios 

1. Dé un ejemplo de una aplicación que requiera contenido algorítmico a nivel de aplicación, y discuta la función de los algoritmos involucrados.
2. Supongamos que estamos comparando implementaciones de ordenación por inserción y ordenación por fusión en la misma máquina. Para entradas de tamaño n, la ordenación por inserción se ejecuta en 8n2 pasos, mientras que la ordenación por fusión se ejecuta en 64n lg n pasos. ¿Para qué valores de n supera la ordenación por inserción a la ordenación por fusión? 
3. ¿Cuál es el valor más pequeño de n tal que un algoritmo cuyo tiempo de ejecución es 100n2 se ejecuta más rápido que un algoritmo cuyo tiempo de ejecución es 2n en la misma máquina?

## Soluciones

# Flashcards
