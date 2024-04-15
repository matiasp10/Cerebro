[[Objetos]]

# Parámetros
## value
Cualquier valor.
# Constructor
- Si el valor es null o undefined, este crea y regresa un objeto vacío.
- En caso contrario, devuelve un objeto de un tipo que corresponde al valor dado.
- Si el valor ya es un objeto, devuelve el valor.

```js
new Object(value)
Object(value)
```

> [!warning] 
> Nota: **Object()** puede ser llamado con o sin _new_. Ambos crean un nuevo objeto.

# Métodos estáticos
## Object.assign()
Copia los valores de todas las propiedades enumerables propias de uno o más objetos fuente al objeto asignado. [[Object.assign()]]

## Object.create()
Crea un nuevo objeto con el objeto prototipal especificado y sus propiedades.

## Object.defineProperty()
Agrega la propiedad nombrada descrita por el descriptor dado a un objeto.

## Object.defineProperties()
Añade las propiedades nombradas a un objeto.

## Object.entries()
Devuelve un array que contiene todos los pares `[key, value]` de las propiedades enumerables en formato cadena de texto que le pertenecen a un objeto dado.

## Object.freeze()
Congela un objeto. Otro código no puede borrar ni cambiar sus propiedades.

## Object.fromEntries()
Devuelve un nuevo objeto de los pares iterables `[key, value]`. (Este método hace lo contrario a Object.entries).

## Object.getOwnPropertyDescriptor()
Devuelve un descriptor de propiedad para una propiedad nombrada en un objeto.

## Object.getOwnPropertyDescriptors()
Devuelve un objeto con todos los descriptores de propiedad pertenecientes a un objeto.

## Object.getOwnPropertyNames()
Devuelve un arreglo que contiene todos los nombres de las propiedades enumerables y no enumerables que le pertenecen a un objeto dado.

## Object.getOwnPropertySymbols()
Devuelve un objeto que contiene todas las propiedades símbolo encontradas directamente en un objeto dado.

## Object.getPrototypeOf()
Devuelve el prototipo (la propiedad interna `[[Prototype]]`) del objeto especificado.

## Object.is()
Compara si dos valores son el mismo valor. Iguala todos los valores _NaN_ (lo que difiere de la Comparación Abstracta de Igualdad y de la Comparación Estricta de Igualdad).

## Object.isExtensible()
Determina si está permitido extender un objeto.

## Object.isFrozen()
Determina si un objeto está congelado.

## Object.isSealed()
Determines si un objeto está sellado.

## Object.keys()
Devuelve un arreglo que contiene todos los nombres de las propiedades enumerables de tipo cadena de texto pertenecientes al objeto dado.

## Object.preventExtensions()
Previene que un objeto pueda extenderse.

## Object.seal()
Previene que otro código pueda borrar propiedades de un objeto.

## Object.setPrototypeOf()
Estipula el prototipo de un objeto (su propiedad interna `[[Prototype]]`).

## Object.values()
Devuelve un arreglo que contiene todos los valores correspondientes a las propiedades enumerables de tipo cadena de texto pertenecientes a un objeto dado.

# Propiedades de instancia
## Object.prototype.constructor
Especifica la función que crea el prototipo de un objeto.

## Object.prototype.`__proto__`
Apunta al objeto que fue usado como prototipo cuando el objeto fue instanciado.

# Métodos de instancia
## Object.prototype.`__defineGetter__`()
Asocia una función a una propiedad que, cuando es accedida, ejecuta la función y retorna su valor de retorno.

## Object.prototype.`__defineSetter__`()
Asocia una función a una propiedad que, cuando es estipulada, ejecuta la función que modificará dicha propiedad.

## Object.prototype.`__lookupGetter__`()
Devuelve la función asociada a la propiedad establecida por el método `Object.prototype.__defineGetter__()`.

## Object.prototype.`__lookupSetter__`()
Devuelve la función asociada a la propiedad establecida por el método `Object.prototype.__defineSetter__()`.

## Object.prototype.hasOwnProperty()
Devuelve un booleano que indica si el objeto contiene una propiedad determinada como una propiedad directa del objeto y que no haya sido heredada a través de la cadena de prototipos.

## Object.prototype.isPrototypeOf()
Devuelve un booleano que indica si el objeto por el cual este método está siendo llamado está en la cadena de prototipos del objeto especificado.

## Object.prototype.propertyIsEnumerable()
Devuelve un booleano indicando si el `[atributo ECMAScript [Enumerable]]` interno está establecido.

## Object.prototype.toLocaleString()
Llama a `toString()`.

## Object.prototype.toString()
Devuelve una representación del objeto en formato cadena de texto.

## Object.prototype.valueOf()
Devuelve el valor primitivo del objeto especificado.