#AL 
# ¿Qué es un algoritmo?

> [!definition|*]+ Definición formal
> 
*> Conjunto ordenado y finito de operaciones que permite hallar la solución de un problema*

Informalmente un algoritmo es cualquier procedimiento computacional bien definido el cual toma un valor o un grupo de valores como input y produce algunos valores o un grupo de valores como output.

Entonces nuestra definición puede decirse que es:

> [!definition|*]+ Definición
> _Un algoritmo es una secuencia de pasos computacionales que transforman la entrada en una salida_

También podríamos ver un algoritmo como una **herramienta** para resolver problemas computacionales específicos.
Los planteamientos de un problema especifican en general las entradas y salidas deseadas. El algoritmo _describe un procedimiento computacional especifico para lograr la relación entre la entrada y la salida_.

Por ejemplo, alguna vez necesitaríamos ordenar una secuencia de números en un orden decreciente. Este problema surge con frecuencia en la practica y es bueno para introducir técnicas estándar de diseño y herramientas de análisis. De la siguiente manera es como se define formalmente el problema de ordenamiento:

$$\begin{align*}
	&\textbf{Algoritmo } \text{Ordenamiento}\\
	&\textbf{Input } \text{Una secuencia de n numeros } \langle a_1,a_2,...a_n \rangle \\ 
	&\textbf{Output } \text{Una permutacion (Reordenamiento) } \langle a´_1, a´_2,...,a´_n \rangle \\
    &\text{ de la secuencia de entrada tal que } \langle a´_1 \leqslant a´_2 \leqslant ... \leqslant a´_n \rangle \\
\end{align*}$$

Por ejemplo, dada la entrada
$$\langle 31,41,59,26,41,58 \rangle$$
un algoritmo de ordenamiento devolvería como salida la secuencia 
$$\langle 26,31,41,41,58,59 \rangle$$
Una secuencia de entrada de este tipo se denomina _instancia del problema de ordenamiento_. En general, una instancia de un problema consiste en la entrada (que satisface cualquier restricción impuesta en el enunciado del problema) necesaria para calcular una solución al problema.

Dado que muchos programas la utilizan como paso intermedio, la ordenación es una _operación fundamental en informática_. Como resultado, disponemos de un gran número de buenos algoritmos de ordenación.
El algoritmo más adecuado para una aplicación determinada depende, entre otros factores, **del número de elementos que haya que ordenar**, de **si los elementos ya están algo ordenados**, de las **posibles restricciones en los valores de los elementos**, de la **arquitectura del ordenador** y del **tipo de dispositivos de almacenamiento que se vayan a utilizar**: _memoria principal_, _discos_ o _incluso cintas_.

Se dice que un algoritmo es **correcto** si, para cada instancia de entrada, se detiene con la _salida correcta_.

Un algoritmo **incorrecto** puede no detenerse en algunos casos de entrada, o puede detenerse con una respuesta incorrecta. Al contrario de lo que cabría esperar, los algoritmos incorrectos a veces pueden ser útiles, si podemos controlar su tasa de error.

Un algoritmo se puede especificar en **inglés**, como un programa de ordenador o incluso como un diseño de hardware. El único requisito es que la especificación debe proporcionar una descripción precisa del procedimiento computacional a seguir.

# Estructuras de datos

Una estructura de datos es una forma de almacenar y organizar datos para facilitar su acceso y modificación. Ninguna estructura de datos funciona bien para todos los fines, por lo que es importante conocer los puntos fuertes y las limitaciones de varias de ellas.

# Ejercicios

1. Dé un ejemplo del mundo real que requiera ordenar o un ejemplo del mundo real que requiera calcular un casco convexo. 
2. Además de la velocidad, ¿Qué otras medidas de eficiencia podrían utilizarse en el mundo real?
3. Seleccione una estructura de datos que haya visto anteriormente y analice sus ventajas y limitaciones.
4. ¿En qué se parecen los problemas del camino más corto y del viajante de comercio? ¿En qué se diferencian? 
5. Plantee un problema del mundo real en el que sólo sirva la mejor solución. A continuación, proponga uno en el que una solución que sea "aproximadamente" la mejor sea suficiente.

## Soluciones

1. Un ejemplo podría ser una agenda telefónica donde necesitamos ordenar los nombres de las personas por orden alfabético.
2. Supongo que el espacio que ocupe.
3. 