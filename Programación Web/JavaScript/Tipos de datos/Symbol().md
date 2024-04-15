[[Symbol]]

# Parámetros
## Symbol name

```js
let id = new Symbol(name)
```

El valor name es un string opcional llamado etiqueta o symbol name y seria útil solo para depuración.

# Constructor

```js
let id = new Symbol("id")
```

# Propiedades estáticas
## Symbol.asyncIterator
Un método que devuelve el `AsyncIterator` por defecto para un objeto. Utilizado por for `await...of.`

## Symbol.hasInstance
Un método que determina si un objeto constructor reconoce un objeto como su instancia. Utilizado por `instanceof`.

## Symbol.isConcatSpreadable
Un valor booleano que indica si un objeto debe ser convertido a sus elementos de matriz. Utilizado por `Array.prototype.concat()`.

## Symbol.iterator
Un método que devuelve el iterador por defecto de un objeto. Utilizado por `for...of`.

## Symbol.match
Un método que coincide con una cadena, también se utiliza para determinar si un objeto puede ser utilizado como una expresión regular. Utilizado por `String.prototype.match()`.

## Symbol.matchAll
Un método que devuelve un iterador, que devuelve las coincidencias de la expresión regular con una cadena. Utilizado por `String.prototype.matchAll()`.

## Symbol.replace
Un método que reemplaza las subcadenas coincidentes de una cadena. Utilizado por `String.prototype.replace()`.

## Symbol.search
Un método que devuelve el índice dentro de una cadena que coincide con la expresión regular. Utilizado por `String.prototype.search()`.

## Symbol.split
Un método que divide una cadena en los índices que coinciden con una expresión regular. Utilizado por `String.prototype.split()`.

## Symbol.species
Una función constructora que se utiliza para crear objetos derivados.

## Symbol.toPrimitive
Un método que convierte un objeto en un valor primitivo.

## Symbol.toStringTag
Valor de cadena utilizado para la descripción por defecto de un objeto. Utilizado por `Object.prototype.toString()`.

## Symbol.unscopables
Un valor de objeto cuyos nombres de propiedades propias y heredadas se excluyen de los enlaces de entorno `with` del objeto asociado.

# Métodos estáticos
## Symbol.for(key)
Busca los Symbols existentes con la key dada y los devuelve si los encuentra. En caso contrario, se crea un nuevo Symbol en el registro global de Symbols con la "key".

## Symbol.keyFor(sym)
Recupera una clave de Symbol compartida del registro global de Symbols para el Symbol dado.

# Propiedades de instancia
## Symbol.prototype.description
Una cadena de sólo lectura que contiene la descripción del Symbol.

# Métodos de instancia
## Symbol.prototype.toString()
Devuelve una cadena que contiene la descripción del Symbol. Anula el método `Object.prototype.toString()`.

## Symbol.prototype.valueOf()
Devuelve el Symbol. Anula el método `Object.prototype.valueOf()`.

## Symbol.prototype`[@@toPrimitive]`
Devuelve el Symbol.
