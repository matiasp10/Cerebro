Hay muchas reglas distintas para representar el pseudocódigo. Nosotros utilizaremos las siguientes:

- **Cabecera del algoritmo**: La cabecera del algoritmo es una sentencia simple que comienza con la palabra reservada _algoritmo_. A continuación, debe indicarse el nombre asignado al algoritmo.
- **Declaración de estructuras de datos (arreglos y registros)**:  En el caso de que se utilizaran estructuras de datos definidas por el programador, como arreglos y registros, estas deben declararse en un bloque de código con la palabra reservada _tipo_.
- **Declaración de variables y constantes**: Aquí se declaran todas aquellas variables y constantes que se utilicen en el algoritmo. Para definir las variables y constantes utilizaremos las palabras reservadas _var_ y _const_ respectivamente.
- **Sentencias ejecutables**: Las sentencias ejecutables son las instrucciones que constituyen los pasos del algoritmo, que se ejecutarán cuando el programa inicie. Para delimitar esta última sección, utilizaremos las palabras reservadas _inicio_ y _fin_.

```
algoritmo <nombre de algoritmo>
tipo
<definición de arreglos y registros>
var
<tipo de dato>: <nombre de variable, nombre de variable, etc.>
<tipo de dato>: <nombre de variable>
.
.
const
<tipo de dato>: <nombre de constante> <valor>
<tipo de dato>: <nombre de constante> <valor>
.
.
inicio
<sentencia ejecutable 1>
<sentencia ejecutable 2>
<sentencia ejecutable n>
fin
```
#### Ejemplo

```
algoritmo suma_dos_numeros
var
entero: a, b, suma
inicio
leer(a, b)
suma = a + b
mostrar(suma)
fin
```
