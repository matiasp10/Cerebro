Un registro es una estructura compuesta por diversos tipos de datos que se agrupan en una misma variable. La utilización de un registro es apropiada cuando se desea manejar datos relacionados sim importar sus tipos, bajo una misma unidad.

Por ejemplo, si se desea crear un programa que permita calcular el sueldo que pagar a los empleados de una institución, se debe conocer el nombre y apellido junto con el monto para pagar de cada empleado. Toda esta información en conjunto (registro) caracteriza a un empleado. Los datos que forman parte de esta colección son de distinto tipo, por lo tanto, no es posible utilizar un arreglo para almacenarlos, pero sí es posible utilizar registros.
## Declaración de un registro

En pseudocódigo, un registro se declara de la siguiente forma:

```
Algoritmo declaración_registro
tipo
registro: nombre_registro
inicio
<tipo de dato>: <nombre de variable, nombre de variable, etc> <tipo de dato>: <nombre de variable,nombre de variable, etc>
.
fin-registro
var
nombre_registro: nombre_variable
inicio
<sentencia ejecutable 1>
<sentencia ejecutable 2>
.
.
<sentencia ejecutable n>
fin
```

La composición de un registro define el programador, por lo tanto, al igual que los arreglos, su estructura debe definirse en la sección tipo del algoritmo y también debe indicarse un nombre a la estructura o tipo de dato definida. Dentro de la sección delimitada por las palabras reservadas inicio y fin, se declaran los elementos que componen el registro, que pueden ser de tipo primitivos (entero, real, lógico, cadena, carácter) o compuestos (array o incluso otro registro). Los elementos que componen un registro se denominan campos.
En la sección var, se declaran las variables que se utilizaran en el algoritmo, por lo tanto, si se utilizará el tipo de dato del registro definido, se deben indicar las variables que utilizaran dicho tipo de dato
## Acceso a los campos del registro

Para acceder a los elementos o campos de un registro, se utiliza el nombre o identificador de la variable de tipo registro y el operador punto (.), seguido del nombre del campo al que queremos acceder.
## Arreglo de registros

Si se desea manipular una lista de elementos cuyo tipo de dato es de un registro definido, entonces se puede utilizar un arreglo de registros. En este caso, cada posición del arreglo corresponde a un registro.