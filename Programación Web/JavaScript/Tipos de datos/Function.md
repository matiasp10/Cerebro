El objeto `Function` proporciona métodos para las funciones. En JavaScript, _cada función es en realidad un objeto `Function`_.

# Constructor

## Function()

Crea un nuevo objeto Function. Llamar al constructor directamente puede crear funciones dinámicamente pero sufre de problemas de seguridad y de rendimiento similares (pero mucho menos significativos) a los de `eval()`. Sin embargo, a diferencia de `eval()`, el constructor Function crea funciones que se ejecutan únicamente en el ámbito global.

# Herencia
[[Object()]]
# Propiedades de instancia

Estas propiedades se definen en _`Function.prototype`_ y son compartidas por todas las instancias de Function.

## Function.prototype.constructor

La función constructora que creó el objeto instancia. Para instancias Function, el valor inicial es el constructor Function.

## displayName ⚠ No estándar _Opcional_  
Nombre para mostrar de la función.  
  
## length  
Especifica el número de argumentos esperados por la función.  
  
## name  
El nombre de la función.  
  
## prototype  
Se utiliza cuando la función se usa como constructor con el operador `new`. Se convertirá en el prototipo del nuevo objeto.

# Métodos de instancia

## Function.prototype.apply()

Llama a una función con un valor `this` dado y argumentos opcionales proporcionados como un array (o un objeto tipo array).  
  
## Function.prototype.bind()  

Crea una nueva función que, cuando se llama, tiene su palabra clave this establecida a un valor proporcionado, opcionalmente con una secuencia dada de argumentos que preceden a cualquiera proporcionado cuando se llama a la nueva función.  
  
## Function.prototype.call()  

Llama a una función con un valor this dado y argumentos opcionales.  
  
## Function.prototype.toString() 

Devuelve una cadena que representa el código fuente de la función. Anula el método Object.prototype.toString.

