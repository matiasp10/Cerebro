Cada uno de los algoritmos que resuelven estos subproblemas se denominan subalgoritmos o subprogramas.
Esta técnica permite que el programador se pueda concentrar en pequeñas partes del problema para construir la solución general con cada uno de los subalgoritmos. Cada uno de estos subalgoritmos pueden ser visto como una unidad más pequeña del algoritmo principal que se encarga de resolver una tarea especifica. Al asignar un nombre a esta división o conjunto de acciones, se la puede invocar desde diferentes secciones del algoritmo principal por medio del nombre que lo identifica.

Como parte de un pequeño ejemplo de la aplicación de subalgoritmos en un problema, se puede mencionar el escenario planteado en la lectura del Modulo 1 sobre el calculo del promedio de tres notas de un alumno y la definición de la condición final de acuerdo con el promedio

Este problema se puede dividir en los siguientes subproblemas:

- **Subproblema 1**: entrada de datos (nota 1, nota 2 y nota 3)
- **Subproblema 2**: cálculo del promedio.
- **Subproblema 3**: cálculo de la condición del alumno.
- **Subproblema 4**: salida de resultados.

Algunas ventajas de la utilización de subalgoritmos son:

- Una vez implementado un subalgoritmo, si se tuviese que modificar, es más fácil y rápido efectuar el cambio en el subalgoritmo, en comparación con si el cambio tuviese que realizarse en el algoritmo principal.
- Se pueden construir librerías propias del usuario con los subalgoritmos que se desarrollan.
- La verificación del correcto funcionamiento de un algoritmo es más fácil.
- Desarrollar programas gradualmente con subalgoritmos permite probar estos módulos aisladamente antes de integrarlos en el algoritmo principal.
- El diseño de un programa con subalgoritmos hace más sencillo trabajar en ambientes colaborativos, donde distintos programadores desarrollan los subalgoritmos y luego se unen en el programa principal.

Los subalgoritmos se clasifican en funciones y procedimientos.
## Funciones 

Una función es un subalgoritmo que retorna un valor al algoritmo que lo haya invocado. Los lenguajes de programación ya incluyen un conjunto de funciones básicas disponibles para los programadores denominadas funciones internas o del sistema.

- RC(X) o RAIZ(X) Retorna la raíz cuadrada de X.
- ABS(X) Retorna el valor absoluto de X
- AZAR(X) Retorna un entero aleatorio en el rango `[0; x-1]`
- ALEATORIO (A,B) Retorna un entero aleatorio en el rango `[A,B]`
- MAYUSCULAS (S) Retorna una copia de la cadena S con todos sus caracteres en mayúsculas.
- CONVERTIRANUMERO(X) Recibe una cadena de caracteres que contiene un número y devuelve una variable numérica con el mismo.

El programador también puede definir sus propias funciones. La sintaxis utilizada para definir una función en un algoritmo es la siguiente:

```
<tipo de dato> función <nombre función> (lista de parámetros)

var   

Declaración de variables locales

inicio      
	<acciones>// cuerpo de la función     
	devolver (<expresión>)
fin-función
```

La definición de una función comienza indicando el tipo de dato de valor que devolverá la función. A continuación, se define el nombre o identificador de la función utilizando la palabra reservada función. Posteriormente, entre paréntesis, se coloca la lista de parámetros indicando el tipo de dato y nombre o identificador de las variables. Los parámetros se separan con coma. Se pueden definir también variables locales a la función en la sección var. A continuación, el cuerpo de acciones de la función debe delimitarse con las palabras reservadas inicio y fin-función. 
En la última sección del cuerpo de la función debe indicarse el valor que se retornara utilizando la sintaxis devolver (`<expresión>`). Para llamar a la función, se debe invocar su nombre con la lista de parámetros que esta requiere.
## Procedimiento

Un procedimiento es un subalgoritmo que realiza una tarea, pero no retorna ningún valor al algoritmo que lo haya invocado. Alguno de los procedimientos internos puede ser: 

- escribir (parámetro) o mostrar (parámetro): muestra por consola el parámetro que se envía al procedimiento.
- leer(parámetro) o ingresar(parámetro): asigna un valor ingresado por el usuario a la variable que figura como parámetro.

El programador también puede definir sus propios procedimientos utilizando la siguiente sintaxis:

```
procedimiento <nombre procedimiento>(lista de parámetros)

var    
	Declaración de variables locales
inicio    
	<acciones>//cuerpo del procedimiento
fin-procedimiento
```
## Ámbito de variables

Una variable local es aquella que se define en un subprograma o subalgoritmo. Estas variables son visibles y existen dentro del subalgoritmo; fuera de él la variable no existe y no puede ser utilizada.

Una variable global es aquella que está definida en el algoritmo principal y su ámbito es abierto a todo el programa, incluidos los subalgoritmos. Es decir, desde un subalgoritmo se puede utilizar una variable global.
## Paso de parámetros

Un subalgoritmo puede requerir de información de entrada para poder realizar su tarea, y esta la puede obtener por medio de un paso de parámetros. En el siguiente ejemplo, se define una función que devuelve el cálculo de la hipotenusa de un triángulo rectángulo y, para ello, necesita el valor de los catetos.

```
real función calcular_hipotenusa(real:cateto1, real:cateto2)

var   
	real:hipotenusainicio    
	hipotenusa ← raiz (cateto1* cateto1 + cateto2 * cateto 2)
	devolver (hipotenusa)
fin-función
```

Cuando un programa invoca un subalgoritmo, le puede enviar información por medio de parámetros.

Los parámetros definidos en la cabecera del subalgoritmo se denominan parámetros formales, y los parámetros que se envían cuando se invoca al subalgoritmo se denominan parámetros actuales. Cuando se invoca un subalgoritmo, los parámetros formales toman el valor de los parámetros actuales.

El paso de parámetros se clasifica en paso por valor y paso por referencia. 
### Por valor

Cuando se pasan por valor, los parámetros formales de un subalgoritmo reciben el valor de los parámetros actuales. Cualquier modificación sobre los parámetros formales no afecta a los parámetros actuales. Cuando el subalgoritmo finalice, el parámetro actual en la sección del algoritmo que invocó al subprograma tendría el mismo valor original sin importar lo que se realice en el subprograma.

Si ejecutamos el algoritmo anterior, se mostrarán en pantalla los siguientes mensajes:

- El valor de A en el algoritmo principal es 2.
- El valor de num en el subalgoritmo es 2
- El valor de num en el subalgoritmo es 10
- El valor de A en el algoritmo principal es 2
### Por referencia

Cuando se utiliza el paso de parámetros por referencia, los parámetros formales de un subalgoritmo reciben las referencias de los parámetros actuales. 
Cualquier modificación que se haga sobre estos últimos tendrá impacto sobre las referencias y, en consecuencia, sobre los parámetros actuales en el caso de que sean variables, ya que ambos tipos de parámetros (actuales y formales) hacen referencia a la misma dirección de memoria. 

Cuando finaliza el subalgoritmo, la variable que representa el parámetro actual del algoritmo que invocó el subprograma tendrá el mismo valor que el parámetro formal del subprograma.