El método **`slice()`** extrae una sección de una cadena y la devuelve como una nueva cadena, sin modificar la cadena original.

```js
const str = 'The quick brown fox jumps over the lazy dog.';

console.log(str.slice(31));
// Expected output: "the lazy dog."

console.log(str.slice(4, 19));
// Expected output: "quick brown fox"

console.log(str.slice(-4));
// Expected output: "dog."

console.log(str.slice(-9, -5));
// Expected output: "lazy"
```

# Sintaxis

```js
slice(indexStart)
slice(indexStart, indexEnd)
```

## Parámetros

### indexStart

El índice del primer carácter a incluir en la subcadena devuelta.

### indexEnd (opcional)

El índice del primer carácter a excluir de la subcadena devuelta.

## Valor de retorno

Una nueva cadena que contiene la sección extraída de la cadena.

# Descripción

**`slice()`** extrae el texto de una cadena y devuelve una nueva cadena. Los cambios en el texto de una cadena no afectan a la otra.

**`slice()`** extrae hasta `indexEnd` pero sin incluirlo. Por ejemplo, `str.slice(1, 4)` extrae del segundo al cuarto carácter (caracteres indexados 1, 2 y 3).

- Si `indexStart >= str.length`, se devuelve una cadena vacía.
- Si `indexStart < 0`, el índice se cuenta desde el final de la cadena. Más formalmente, en este caso, la subcadena comienza en `max(indexStart + str.length, 0)`.
- Si `indexStart` se omite, no se define o no se puede convertir a un número (utilizando Number(indexStart)), se trata como 0.
- Si `indexEnd` se omite, no se define o no se puede convertir a un número (utilizando `Number(indexEnd)`), o si `indexEnd >= str.length`, `slice()` extrae hasta el final de la cadena.
- Si `indexEnd < 0`, el índice se cuenta desde el final de la cadena. Más formalmente, en este caso, la subcadena termina en `max(indexEnd + str.length, 0)`.
- Si `indexEnd <= indexStart` después de normalizar los valores negativos (es decir, `indexEnd` representa un carácter que está antes de `indexStart`), se devuelve una cadena vacía.

# Ejemplos

## Uso de `slice()` para crear una nueva cadena

El siguiente ejemplo utiliza slice() para crear una nueva cadena.

```js
const str1 = "The morning is upon us."; // The length of str1 is 23.
const str2 = str1.slice(1, 8);
const str3 = str1.slice(4, -2);
const str4 = str1.slice(12);
const str5 = str1.slice(30);
console.log(str2); // he morn
console.log(str3); // morning is upon u
console.log(str4); // is upon us.
console.log(str5); // ""
```

## Uso de `slice()` con índices negativos

El siguiente ejemplo utiliza `slice()` con índices negativos.

```js
const str = "The morning is upon us.";
str.slice(-3); // 'us.'
str.slice(-3, -1); // 'us'
str.slice(0, -1); // 'The morning is upon us'
str.slice(4, -1); // 'morning is upon us'
```

Este ejemplo cuenta hacia atrás desde el final de la cadena por 11 para encontrar el índice de inicio y hacia adelante desde el inicio de la cadena por 16 para encontrar el índice final.

```js
console.log(str.slice(-11, 16)); // "is u"
```

Aquí se cuenta hacia adelante desde el principio por 11 para encontrar el índice de inicio y hacia atrás desde el final por 7 para encontrar el índice final.

```js
console.log(str.slice(11, -7)); // " is u"
```

Estos argumentos cuentan hacia atrás desde el final en 5 para encontrar el índice inicial y hacia atrás desde el final en 1 para encontrar el índice final.

```js
console.log(str.slice(-5, -1)); // "n us"
```

# Compatibilidad

https://caniuse.com/mdn-javascript_builtins_string_slice

