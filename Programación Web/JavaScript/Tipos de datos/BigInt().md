[[BigInt]]

# Parámetros
## Valor
El valor numérico del objeto que se está creando. Puede ser una cadena, un entero, un booleano u otro BigInt.

# Constructor

```js
let numero = BigInt(valor)
```

> [!warning] 
> `BigInt()` sólo puede invocarse sin `new`. Si se intenta construir con new se produce un `TypeError`.

# Métodos estáticos
## BigInt.asIntN()
Convierte un valor BigInt en un valor entero con signo y lo devuelve.

## BigInt.asUintN()
Sujeta un valor BigInt a un valor entero sin signo, y devuelve ese valor.

# Propiedades de instancia
## BigInt.prototype`[@@toStringTag]`
El valor inicial de la propiedad `@@toStringTag` es la cadena "BigInt". Esta propiedad se utiliza en `Object.prototype.toString()`. Sin embargo, como BigInt también tiene su propio método `toString()`, esta propiedad no se utiliza a menos que se llame a `Object.prototype.toString.call()` con un BigInt como `thisArg`.

# Métodos de instancia 
## BigInt.prototype.toLocaleString()
Devuelve una cadena con una representación sensible al idioma de este valor BigInt. Anula el método `Object.prototype.toLocaleString()`.

## BigInt.prototype.toString()
Devuelve una cadena que representa este valor BigInt en el radix (base) especificado. Anula el método `Object.prototype.toString()`.

## BigInt.prototype.valueOf()
Devuelve este valor BigInt. Anula el método `Object.prototype.valueOf()`.
