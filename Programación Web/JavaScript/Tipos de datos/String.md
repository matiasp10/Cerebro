En JavaScript, los datos textuales son almacenados como **strings** (cadena de caracteres). No hay un tipo de datos separado para caracteres unitarios.

El formato interno para strings es siempre [UTF-16](https://es.wikipedia.org/wiki/UTF-16), _no está vinculado a la codificación de la página_.

# Wrapper

[[String()]]

# Tipos de comillas

Los strings pueden estar entre **comillas simples**, **comillas dobles** o **backticks** (acento grave):

```js
let single = 'comillas simples';
let double = "comillas dobles";

let backticks = `backticks`;
```

Comillas simples y dobles son esencialmente lo mismo. En cambio, los “_backticks_” nos permiten además ingresar _expresiones_ dentro del string envolviéndolos en `${…}`:

```js
function sum(a, b) {
  return a + b;
}

alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3.
```

Otra ventaja de usar backticks es que nos permiten extender en múltiples líneas el string:

```js
let guestList = `Invitados:
 * Juan
 * Pedro
 * Maria
`;

alert(guestList); // una lista de invitados, en múltiples líneas
```

Se ve natural, ¿no es cierto? Pero las comillas simples y dobles no funcionan de esa manera.

Si intentamos usar comillas simples o dobles de la misma forma, obtendremos un error:

```js
let guestList = "Invitados:  // Error: Unexpected token ILLEGAL
  * Juan";
```

Las comillas simples y dobles provienen de la creación de lenguajes en tiempos ancestrales, cuando la necesidad de múltiples líneas no era tomada en cuenta. Los backticks aparecieron mucho después y por ende son más versátiles.

Los backticks además nos permiten especificar una “_función de plantilla_” antes del primer backtick. La sintaxis es: ``func`string` ``. La función `func` es llamada automáticamente, recibe el string y la expresión insertada, y los puede procesar. Eso se llama “_plantillas etiquetadas_”.

# Caracteres especiales
Es posible crear strings de múltiples líneas usando comillas simples, usando un llamado “_carácter de nueva línea_”, escrito como `\n`, lo que denota un salto de línea:

```js
let guestList = 'Invitados:\n * Juan\n * Pedro\n * Maria';

alert(guestList); // lista de invitados en múltiples líneas, igual a la de más arriba
```

Como ejemplo más simple, estas dos líneas son iguales, pero escritas en forma diferente:

```js
let str1 = "Hello\nWorld"; // dos líneas usando el "símbolo de nueva línea"

// dos líneas usando nueva línea normal y backticks
let str2 = `Hello
World`;

alert(str1 == str2); // true

```

Existen distintos tipos de caracteres especiales:

| Código                                                                                                   | Salida                                                                      |
| -------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `\XXX` (donde `XXX` es de 1 a 3 dígitos octales; rango de `0`-`377`)                                     | Punto de código Unicode/carácter ISO-8859-1 entre `U+0000` y `U+00FF`       |
| `\'`                                                                                                     | Comilla sencilla                                                            |
| `\"`                                                                                                     | Comilla doble                                                               |
| ``\\``                                                                                                   | Barra inversa                                                               |
| `\n`                                                                                                       | Nueva línea                                                                 |
| `\r`                                                                                                       | Retorno de carro                                                            |
| `\v`                                                                                                       | Tabulación vertical                                                         |
| `\t`                                                                                                       | Tabulación                                                                  |
| `\b`                                                                                                       | Retroceso                                                                   |
| `\f`                                                                                                       | Avance de pagina                                                            |
| `\uXXXX` (donde `XXXX` son 4 dígitos hexadecimales; rango de `0x0000`-`0xFFFF`)                          | Unidad de código UTF-16/punto de código Unicode entre `U+0000` y `U+FFFF`   |
| `\u{X}` ... `\u{XXXXXX}` (donde `X…XXXXXX` es de 1 a 6 dígitos hexadecimales; rango de `0x0`-`0x10FFFF`) | Unidad de código UTF-32/punto de código Unicode entre `U+0000` y `U+10FFFF` |
| `\xXX` (donde `XX` son 2 dígitos hexadecimales; rango de `0x00`-`0xFF`)                                  | Punto de código Unicode/carácter ISO-8859-1 entre `U+0000` y `U+00FF`                                                                            |

Como puedes ver, todos los caracteres especiales empiezan con la barra invertida `\`. Se lo llama “_carácter de escape_”.

Y como es tan especial, si necesitamos mostrar el verdadero carácter `\` dentro de un string, ==necesitamos duplicarlo==:

```js
alert( `La barra invertida: \\` ); // La barra invertida: \
```

# Los strings son inmutables
Los strings no pueden ser modificados en JavaScript. Es imposible modificar un carácter.

Intentémoslo para demostrar que no funciona:

```js
let str = 'Hola';

str[0] = 'h'; // error
alert(str[0]); // no funciona
```

Lo usual para resolverlo es crear un nuevo string y asignarlo a `str` reemplazando el string completo.

Por ejemplo:

```js
let str = 'Hola';

str = 'h' + str[1] + str[2] + str[3]; // reemplaza el string

alert( str ); // hola
```


