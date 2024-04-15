[[Programación Web/JavaScript/Tipos de datos/String|String]]

String es un **objeto primitivo envolvente** que permite representar y manipular cadena de caracteres.

Las cadenas se pueden crear como primitivas, a partir de _cadena literales_ o como _objetos_, usando el constructor **String()**:

```js
const string1 = "Una cadena primitiva";
const string2 = 'También una cadena primitiva';
const string3 = `Otra cadena primitiva más`;

const string4 = new String("Un objeto String");
```

Las `strings` primitivas y los objetos `string` se pueden usar indistintamente en la mayoría de las situaciones.

Los cadena literales se pueden especificar usando comillas simples o dobles, que se tratan de manera idéntica, o usando el backtick. Esta última forma especifica una _plantilla literal_ con esta forma puedes interpolar expresiones.

# Constructor

## String()
Crea un nuevo objeto String. Realiza la conversión de tipos cuando se llama como función, en lugar de como constructor, lo cual suele ser más útil.

```js
let cadena = new String("Hola mundo!")
```

# Métodos estáticos
## String.fromCharCode(num1 ``[, ...[, numN]]``)
Devuelve una cadena creada utilizando la secuencia de valores Unicode especificada.

## String.fromCodePoint(num1 ``[, ...[, numN]]``)
Devuelve una cadena creada utilizando la secuencia de puntos de código especificada.

## String.raw()
Devuelve una cadena creada a partir de una plantilla literal sin formato.

# Propiedades de instancia
## String.prototype.length
Refleja la longitud de la cadena. Solo lectura.

# Métodos de instancia

## String.prototype.charAt(index)
Devuelve el carácter (exactamente una unidad de código UTF-16) en el index especificado.

## String.prototype.charCodeAt(index)
Devuelve un número que es el valor de la unidad de código UTF-16 en el index dado.

## String.prototype.codePointAt(pos)
Devuelve un número entero no negativo que es el valor del punto de código codificado en UTF-16 que comienza en la pos especificada.

## String.prototype.concat(str`[, ...strN]`)
Combina el texto de dos (o más) cadenas y devuelve una nueva cadena.

## String.prototype.includes(searchString `[, position]`)
Determina si la cadena de la llamada contiene searchString.

## String.prototype.endsWith(searchString`[, length]`)
Determina si una cadena termina con los caracteres de la cadena searchString.

## String.prototype.indexOf(searchValue`[, fromIndex]`)
Devuelve el índice dentro del objeto String llamador de la primera aparición de searchValue, o -1 si no lo encontró.

## String.prototype.lastIndexOf(searchValue`[, fromIndex]`)
Devuelve el índice dentro del objeto String llamador de la última aparición de searchValue, o -1 si no lo encontró.

## String.prototype.localeCompare (compareString `[, locales[, options]]`)
Devuelve un número que indica si la cadena de referencia compareString viene antes, después o es equivalente a la cadena dada en el orden de clasificación.

## String.prototype.match(regexp)
Se utiliza para hacer coincidir la expresión regular regexp con una cadena.

## String.prototype.matchAll(regexp)
Devuelve un iterador de todas las coincidencias de regexp.

## String.prototype.normalize(`[form]`)
Devuelve la forma de normalización Unicode del valor de la cadena llamada.

## String.prototype.padEnd(targetLength`[, padString]`)
Rellena la cadena actual desde el final con una cadena dada y devuelve una nueva cadena de longitud targetLength.

## String.prototype.padStart(targetLength`[, padString]`)
Rellena la cadena actual desde el principio con una determinada cadena y devuelve una nueva cadena de longitud targetLength.

## String.prototype.repeat(count)
Devuelve una cadena que consta de los elementos del objeto repetidos count veces.

## String.prototype.replace(searchFor, replaceWith)
Se usa para reemplazar ocurrencias de searchFor usando replaceWith. searchFor puede ser una cadena o expresión regular, y replaceWith puede ser una cadena o función.

## String.prototype.replaceAll(searchFor, replaceWith)
Se utiliza para reemplazar todas las apariciones de searchFor usando replaceWith. searchFor puede ser una cadena o expresión regular, y replaceWith puede ser una cadena o función.

## String.prototype.search(regexp)
Busca una coincidencia entre una expresión regular regexp y la cadena llamadora.

## String.prototype.slice(beginIndex`[, endIndex]`)
Extrae una sección de una cadena y devuelve una nueva cadena.
[[String.prototype.slice()]]

## String.prototype.split(`[sep[, limit] ]`)
Devuelve un arreglo de cadenas pobladas al dividir la cadena llamadora en las ocurrencias de la subcadena sep.

## String.prototype.startsWith(searchString`[, length]`)
Determina si la cadena llamadora comienza con los caracteres de la cadena searchString.

## String.prototype.substr()
Devuelve los caracteres en una cadena que comienza en la ubicación especificada hasta el número especificado de caracteres.

## String.prototype.substring(indexStart`[, indexEnd]`)
Devuelve una nueva cadena que contiene caracteres de la cadena llamadora de (o entre) el índice (o índices) especificados.

## String.prototype.toLocaleLowerCase( `[locale, ...locales]`)
Los caracteres dentro de una cadena se convierten a minúsculas respetando la configuración regional actual. Para la mayoría de los idiomas, devolverá lo mismo que `toLowerCase()`.

## String.prototype.toLocaleUpperCase( `[locale, ...locales]`)
Los caracteres dentro de una cadena se convierten a mayúsculas respetando la configuración regional actual. Para la mayoría de los idiomas, devolverá lo mismo que `toUpperCase()`.

## String.prototype.toLowerCase()
Devuelve el valor de la cadena llamadora convertido a minúsculas.

## String.prototype.toString()
Devuelve una cadena que representa el objeto especificado. Redefine el método `Object.prototype.toString()`.

## String.prototype.toUpperCase()
Devuelve el valor de la cadena llamadora convertido a mayúsculas.
[[String.prototype.toUpperCase()]]

## String.prototype.trim()
Recorta los espacios en blanco desde el principio y el final de la cadena. Parte del estándar ECMAScript 5.

## String.prototype.trimStart()
Recorta los espacios en blanco desde el principio de la cadena.

## String.prototype.trimEnd()
Recorta los espacios en blanco del final de la cadena.

## String.prototype.valueOf()
Devuelve el valor primitivo del objeto especificado. Redefine el método `Object.prototype.valueOf()`.

## String.prototype.@@iterator()
Devuelve un nuevo objeto **Iterator** que itera sobre los puntos de código de un valor de cadena, devolviendo cada punto de código como un valor de cadena.