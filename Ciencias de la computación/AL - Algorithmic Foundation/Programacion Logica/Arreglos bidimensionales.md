Existen escenarios en los que la información es mejor organizarla en forma de tabla o matriz con dos subíndices: uno para recorrer las filas y otro para recorrer las filas y otro para recorrer las columnas. Un arreglo bidimensional es un vector de vectores cuya representación gráfica puede ser representa mediante una tabla.

![[Pasted image 20240120180528.png|center]]

Cada elemento de un arreglo bidimensional se referencia con un mismo nombre y dos subíndices. En notación estándar el primer subíndice hace referencia a las filas y el segundo a las columnas del arreglo. En pseudocódigo, los arreglos bidimensionales se declaran de la siguiente forma:

```
Algoritmo declaración_arreglo_bidimensional

tipo

array [límite inferior filas…límite superior filas] [límite inferior columnas… límite superior columnas] de <tipo de dato>:<nombre estructura arreglo>

var

<nombre estructura arreglo>:<nombre variable de tipo arreglo>

inicio
. . .
```

Para recorrer arreglos bidimensionales, es necesario tener dos estructuras repetitivas anidadas. Las estructuras que mejor se adaptan a estos casos son las estructuras desde/fin-desde. Por ejemplo, para leer datos desde el teclado, guardarlos en un arreglo bidimensional y luego recorrerlo para mostrar los elementos en la pantalla, se puede utilizar el siguiente pseudocodigo.

```
Algoritmo recorrer_arreglo_bidimensional

tipo 

array[1…5][1…3] de entero: lista

var

lista:notas

entero: i, j

inicio

//cargar arreglo bidimensional

desde i ← 1 hasta 5 hacer

desde j ← 1 hasta 3 hacer

leer (notas[i, j]

fin-desde

fin-desde

// recorrer y mostrar elementos del arreglo bidimensional 

desde i ← 1 hasta 5 hacer

desde j ← 1 hasta 3 hacer

mostrar (notas[i, j]

fin-desde

fin-desde

fin
```

La estructura repetitiva desde externa recorre las filas y, para cada una de ellas, la estructura desde interna recorre cada una de las columnas.