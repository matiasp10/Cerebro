El método **`toUpperCase()`** devuelve el valor de la cadena de llamada convertido a mayúsculas (el valor se convertirá a una cadena si no lo es).

```js
const sentence = 'The quick brown fox jumps over the lazy dog.';

console.log(sentence.toUpperCase());
// Expected output: "THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG."
```

# Sintaxis

```js
toUpperCase()
```

## Valor de retorno

Una nueva cadena que representa la cadena de llamada convertida a mayúsculas.

## Excepciones

### TypeError

Cuando se llama a null o undefined, por ejemplo,. `String.prototype.toUpperCase.call(undefined)`.

# Descripción

El método **`toUpperCase()`** devuelve el valor de la cadena convertido a mayúsculas. Este método no afecta al valor de la cadena en sí, ya que las cadenas JavaScript son inmutables.

# Ejemplos

## Uso básico

```js
console.log("alphabet".toUpperCase()); // 'ALPHABET'
```

## Conversión de valores no string en strings

Este método convertirá cualquier valor que no sea una cadena a una cadena, cuando establezcas su `this` a un valor que no sea una cadena:

```js
const a = String.prototype.toUpperCase.call({
  toString() {
    return "abcdef";
  },
});

const b = String.prototype.toUpperCase.call(true);

// prints out 'ABCDEF TRUE'.
console.log(a, b);
```

# Compatibilidad

https://caniuse.com/mdn-javascript_builtins_string_touppercase