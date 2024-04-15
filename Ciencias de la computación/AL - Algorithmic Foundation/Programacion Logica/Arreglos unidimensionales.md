Los tipos de datos pueden ser simples y estructurados. Los datos estructurados se clasifican en **estadísticos** y **dinámicos**. En las estructuras estáticas, la memoria se gestiona en tiempo de compilación, mientras que, paralas estructuras dinámicas, la memoria se gestiona en tiempo de ejecución.

Un arreglo es una estructura de datos estática y representa un conjunto finito y ordenado de elementos del mismo tipo (**homogéneos**). Los arreglos pueden ser _unidimensionales_, también llamados vectores (o **arreglos lineales**), _bidimensionales_ (**matrices**) o _multidimensionales_. El identificador del arreglo es utilizado para todos los elementos del conjunto, y el valor del índice asociado identifica en forma precisa a los elementos del arreglo. 

```
(vector) 6 3 2 8
```

El número de elementos que se pueden asociar a un vector se llama **rango del vector**. Los arreglos, en general, pueden contener datos numéricos y no numéricos.
El rango o tamaño del arreglo se debe indicar previamente a su uso dentro de un programa. En pseudocodigo, un arreglo unidimensional se declara de la siguiente forma:

```
Algoritmo declaración_arreglo
tipo 
array [límite inferior… límite superior] de < tipo de dato>: <nombre estructura arreglo> var
<nombre estructura arreglo>:<nombre variable de tipo arreglo>
inicio
. . .
```

Ejemplo

```
Algoritmo declaración_arreglo
tipo 
array[1…4] de entero: arreglo:enteros
var
arreglo_enteros: datos
inicio
. . .
```

Se debe notar que en el pseudocodigo anterior, hay una sección llamada tipo, en la cual se declaran las estructuras de datos de arreglos y otros tipos de datos definidos por el usuario. 
Se usa la palabra reservada **array** seguido de un par de corchetes con el rango o tamaño del arreglo indicados por el límite inferior y superior. A continuación, se indica el tipo de dato de los elementos del arreglo y el nombre que tiene la estructura de datos definida (en el ejemplo: `arreglos_enteros`). En la sección `var`, se declaran las variables que se utilizaran en el algoritmo, y en este caso se deben declarar las variables que tendrán la estructura del arreglo definido (en el ejemplo, el algoritmo utilizara una variable de nombre datos que tiene la estructura del arreglo).
Cada elemento de un vector se puede procesar como si fuese una variable simple. Por ejemplo, `datos [4] ← 8` almacena el valor entero **8** en el vector **datos** en la posición número **4**. Si se desea guardar el valor `“Matias”` en la segunda posición del vector nombres, la instrucción es `nombres [2]←“Matias”`.

La instrucción `escribir (datos[4])` muestra por pantalla el contenido de la posición **4** del vector llamado **datos**. En el siguiente ejemplo, se crean dos vectores distintos con la misma estructura definida:

```
Algoritmo declaración_arreglo_2
tipo 
array [1…10] de entero: lista
var
lista: origen, destino
entero: índice
inicio
. . .
```

Se declaran dos arreglos distintos definidos por las variables origen y destino. De la misma forma que se declara la variable índice de tipo de dato entero, también se declaran las variables origen y destino de tipo de dato lista.
El límite inferior no siempre tiene que iniciar en 1, pero es lo más frecuente. Puede ser definido con cualquier otro valor entero, siempre y cuando el rango definido sea correcto. Las siguientes referencias son válidas:

```
P[0], P[1], P[2], P[3], P[4], P[5]
```

En este caso, el rango del arreglo **P** es **6**, y la posición **1** le corresponde el subíndice **0**. Las operaciones que pueden realizarse con vectores son:

- Asignación
- Lectura/escritura
- Recorrido
- Ordenamiento
- Búsqueda

Las operaciones de lectura y escritura de los elementos de un arreglo lineal generalmente, se realizan con estructuras repetitivas. Por ejemplo, si se desea mostrar por pantalla el contenido de todo un arreglo, se usará una estructura repetitiva, como se muestra a continuación:

```
Algoritmo recorrer_arreglo
tipo
array [1…10] de entero: lista
var 
lista: datos
entero: índice
inicio
mostrar (“ingresar los 10 elementos del arreglo”)
desde indice ← 1 hasta 10 hacer
leer (datos[índice])
fin-desde
mostrar (“se muestran los elementos del arreglo”)
desde índice ← 1 hasta 10 hacer
escribir (datos[índice])
fin-desde
fin
```
