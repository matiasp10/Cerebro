El método `endsWith()` determina si una cadena termina con los caracteres de una cadena especificada, devolviendo `true` o `false` según corresponda.

```js
const str1 = 'Cats are the best!';

console.log(str1.endsWith('best!'));
// Expected output: true

console.log(str1.endsWith('best', 17));
// Expected output: true

const str2 = 'Is this a question?';

console.log(str2.endsWith('question'));
// Expected output: false
```

# Sintaxis

```js
endsWith(searchString)
endsWith(searchString, endPosition)
```

## Parámetros

### searchString

Los caracteres que deben buscarse al final de `str`. No puede ser una expresión regular. Todos los valores que no son expresiones regulares se convierten en cadenas, por lo que omitirlo o pasar `undefined` hace que `endsWith()` busque la cadena "`undefined`", que rara vez es lo que se desea.

### endPosition (Opcional)

La posición final en la que se espera encontrar `searchString` (el índice del último carácter de `searchString` más 1). Por defecto es `str.length`.

## Valor de retorno

`true` si los caracteres dados se encuentran al final de la cadena, incluso cuando `searchString` es una cadena vacía; en caso contrario, `false`.

## Excepciones

### TypeError

Si `searchString` es una expresión regular.

# Descripción

Este método permite determinar si una cadena termina o no con otra cadena. Este método _distingue entre mayúsculas y minúsculas_.

# Ejemplos

## Usando endsWith()

```js
const str = "To be, or not to be, that is the question.";

console.log(str.endsWith("question.")); // true
console.log(str.endsWith("to be")); // false
console.log(str.endsWith("to be", 19)); // true
```

# Compatibilidad

https://caniuse.com/mdn-javascript_builtins_string_endswith
















