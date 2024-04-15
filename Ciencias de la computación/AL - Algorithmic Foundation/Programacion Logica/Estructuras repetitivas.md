En el diseño de algoritmos, hay una gran variedad de situaciones que requieren que una o más instrucciones se repitan varias veces. Las instrucciones iterativas o de repetición permiten ejecutar una secuencia de instrucciones más de una vez. 

Un **bucle** es una sección de código que se repite. Es decir que cuando se termina de ejecutar la última instrucción del conjunto, el flujo de control retorna a la primera sentencia y comienza una nueva repetición. Se denomina iteración al hecho de repetir la ejecución de una secuencia de acciones.

Hay varios tipos de estructuras repetitivas, entre ellas tenemos:
### Estructura mientras o while

Se ejecuta un conjunto de sentencias mientras el resultado de una expresión (condición) sea verdadera. 
En la estructura mientras, se evalúa primero la condición y si esta es verdadera, entonces se ejecutan las sentencias definidas en el bucle. 
Al finalizar la iteración,se vuelve a evaluar la condición para volver a ejecutar una nueva iteración hasta que la condición dé como resultado un valor falso.

```
mientras <condición> hacer
sentencia 1
fin-mientras
```

![[Excalidraw/while|while|center]]

En una estructura mientras, lo primero que se ejecuta es la evaluación de la condición y si esta es falsa la primera vez que se ingresa a esta estructura, las sentencias asociadas al bucle nunca se ejecutarán.

Un bucle de una estructura repetitiva que nunca deja de ejecutarse se denomina bucle infinito.
### Estructura repetir-hasta o do-while

Esta estructura repetitiva se utiliza cuando se desea que se ejecute una iteración al menos una vez antes de comprobar la condición de repetición. Es decir, primero se ejecuta el bucle y luego se comprueba la condición para reproducir una nueva iteración o no del bucle. Esta estructura ejecuta el bucle de repetición mientras el resultado de la condición que se evalúa sea falso.

```
repetir <condición>
sentencia 1
hasta-que <condición>
```

![[dowhile|center]]
### Estructura para/desde

En muchas ocasiones se conoce el número de veces que se desea que un bucle se repita. Una estructura de control muy comúnmente usada en estos casos es el ciclo para o desde. Se utiliza una variable como índice que se incrementa o decrementa en forma automática al finalizar cada ciclo.

Para ejecutar el bucle, se evalúa una condición que debe ser verdadera. La condición más comúnmente usada es que el valor delíndice sea menor o igual a un valor final. Si esto se cumple, entonces se ejecuta el bucle. Al finalizar, se incrementa o decrementa el índice y se vuelve a evaluar la condición. Cuando la condición es falsa, se ignora el bucle y se continúa con el resto del algoritmo.

```
desde v <-- vi hasta vf <inc/dec> hacer
sentencia 1
sentencia 2
fin-desde
```

La variable v es una variable entera que debe ser declarada. Los valores vi y vf son los valores inicial y final que tomará la variable v. En el formato de esta estructura, hay que elegir entre incrementaro decrementar la variable de control v, ya que no pueden ocurrir al mismo tiempo ambas opciones. Si el incremento es por el valor 1, entonces se puede obviar la sentencia inc 1 en la estructura. Se pueden utilizar indistintamente las palabras reservadas desde/fin-desde y para/fin-para.

```
desde v <-- 1 hasta 5 inc 2 hacer
<sentencias>
fin-desde
```

![[paradesde|center]]
