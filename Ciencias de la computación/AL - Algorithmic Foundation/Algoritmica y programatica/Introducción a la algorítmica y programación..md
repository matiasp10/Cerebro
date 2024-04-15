Todo usuario que se sienta por primera vez frente a un ordenador debe adquirir unos conceptos básicos que le permitan utilizarlo con eficacia. El ordenador siempre hará lo que le digamos pero no siempre lo que queremos, y ahí está el problema: ¿cómo decirle que haga lo que realmente queremos? Los ordenadores no son inteligentes, son simplemente máquinas capaces de hacer muchas cosas. Los usuarios si tenemos que ser inteligentes para que la máquina haga las cosas que realmente queremos.

A pesar de que los ordenadores actuales no se parecen en casi nada a los ordenadores de primeras generaciones, su esquema de funcionamiento sigue siendo el mismo que hace 20 años: a través de distintos dispositivos de entrada introducimos los datos en la memoria del ordenador. Una vez en memoria el microprocesador realiza algún proceso y produce un resultado por los dispositivos de salida.

Este esquema se repite invariablemente. Veamos algunos ejemplos: escribimos una carta con Word utilizando el teclado como dispositivo de entrada. Realizamos procesos con el texto. Finalmente imprimimos en una impresora como dispositivo de salida. Introducimos una lista desordenada de nombres de personas por el teclado, el microprocesador las ordena, obtenemos por pantalla o impresora la lista de nombres ordenados alfabéticamente.

<img src="https://i.imgur.com/EgJTYvR.png" alt="intro-algo-01a" />

Llamamos periféricos tanto a los dispositivos de entrada como los de salida. Ciertos periféricos son exclusivamente de entrada (teclado) o de salida (impresora). Otros periféricos (discos) pueden funcionar como dispositivos de entrada (los datos están guardados en el disco) y como dispositivos dispositivos de salida (guardamos los datos en el disco).

Simplificando más el esquema tenemos dos bloques: periféricos y CPU (Unidad Central de Proceso). En la CPU encontramos la memoria principal y el microprocesador integrados en la placa base. Un ordenador puede definirse como un microprocesador conectado a una memoria principal. El microprocesador es el circuito más importante de la máquina, puesto que es el que interpreta, ejecuta y procesa los datos que se encuentren en la memoria principal. Esta última tendrá por finalidad almacenar los datos que son procesados por el microprocesador. El resto de dispositivos (teclado, discos, pantalla, ratón...) son periféricos.

Si tenemos en cuenta lo anteriormente expuesto, el esquema funcional puede expresarse de forma mas detallada como arquitectura básica como se observa en el siguiente gráfico:

<img src="https://i.imgur.com/wMOq1V6.png" alt="intro-algo-01a" />

Los datos circulan por los circuitos de la placa base a través de los llamados Buses. El Bus más importante es el del sistema, que comunica la memoria principal con el microprocesador, que a su vez se comunica con una memoria especial muy rápida de uso exclusivo del microprocesador llamada memoria Caché. Otros Buses son AGP, PCI, etc. Un circuito especializado controla el tráfico por los buses. Es el llamado ChipSet.

# Pasos básicos para la resolución de problemas

La **'resolución de un problema'** mediante un ordenador consiste en el proceso que a partir de la descripción de un problema, expresado habitualmente en lenguaje natural y en términos propios del dominio del problema, permite desarrollar un programa que resuelva dicho problema.

Este proceso exige los siguientes pasos:

- [[Definición del problema]]. 
- [[Análisis del problema]].
- [[Diseño o desarrollo de un algoritmo]].
- [[Transformación del algoritmo en un programa (codificación)]].
- [[Ejecución y validación del programa]].

Los dos primeros pasos son los más difíciles del proceso. Una vez analizado el problema y obtenido un algoritmo que lo resuelva, su transformación a un programa de ordenador es una tarea de mera traducción al lenguaje de programación deseado.

# Definiciones

> [!info] Acción
> Una acción es una implementación adicional. Se puede crear en un lenguaje diferente al de la implementación básica. A cada acción se le da un nombre. Las acciones trabajan con los datos del bloque de funciones o programa al cual pertenecen.

> [!info] Proceso
> Un proceso es la ejecución de un programa, es decir, los datos e instrucciones están cargados en la memoria principal, ejecutándose o esperando a hacerlo. Un proceso no tiene porqué estar siempre en ejecución.

> [!info] Algoritmo
> Cualquier procedimiento computacional bien definido que parte de un estado inicial y un valor o un conjunto de valores de entrada, a los cuales se les aplica una secuencia de pasos computacionales finitos, produciendo una salida o solución.

> [!info] Programa
> Conjunto de código escrito que al ejecutarse se encarga de decirle a la computadora las tareas que debe llevar a cabo.

> [!info] Información
> Conjunto de datos organizados y procesados que funcionan como mensajes, instrucciones y operaciones o cualquier otro tipo de actividad que tenga lugar en una computadora.

> [!info] Estado
> Es una configuración única de información en un programa o máquina.

> [!info] Léxico
> Vocabulario o conjunto de palabras y símbolos válidos de un idioma o lenguaje.
> - Comentarios
> - Espacios en blanco
> - Palabras reservadas
> - Identificadores
> - Delimitadores
> - Separadores
> - Operadores

> [!info] Sintaxis
> Parte de la gramática que enseña a coordinar y unir las palabras o símbolos para formar oraciones y expresar conceptos. Conjunto de reglas que definen las secuencias correctas de los elementos léxicos de un lenguaje de programación.
> 
> Estructura del texto (de las secuencias de símbolos que lo componen)

> [!info] Semántica
> Perteneciente o relativo al significado de las palabras y oraciones.
> 
> Significado del texto y de las frases (secuencias de símbolos) que lo componen.