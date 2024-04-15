Los números regulares en JavaScript son almacenados con el formato de 64-bit [IEEE-754](https://es.wikipedia.org/wiki/IEEE_754), conocido como “_números de doble precisión de coma flotante_”.

# Wrapper

[[Number()]]

# Azúcar sintáctica

## Guion bajo

Imagina que necesitamos escribir mil millones (En inglés “1 billion”). La forma obvia es:

```js
let billion = 1000000000;
```

También podemos usar guion bajo `_` como separador:

```js
let billion = 1_000_000_000;
```

Esto hace el numero mas legible. El motor JavaScript simplemente ignora `_` entre dígitos, así que es exactamente igual al “_billion_” de más arriba.

## Notación científica

En JavaScript, acortamos un número agregando la letra _"e"_ y especificando la cantidad de ceros:

```js
let billion = 1e9;  // 1 billion, literalmente: 1 y 9 ceros

alert( 7.3e9 );  // 7.3 billions (tanto 7300000000 como 7_300_000_000)
```

En otras palabras, _"e"_ multiplica el número por el `1` seguido de la cantidad de ceros dada.

```js
1e3 === 1 * 1000; // e3 significa *1000 
1.23e6 === 1.23 * 1000000; // e6 significa *1000000
```

Para cosas mas pequeñas por ejemplo

```js
let mсs = 0.000001;
```

Igual que antes, el uso de _"e"_ puede ayudar. Si queremos evitar la escritura de ceros explícitamente, podríamos expresar lo mismo como:

```javascript
let mcs = 1e-6; // cinco ceros a la izquierda de 1
```

Si contamos los ceros en `0.000001`, hay 6 de ellos en total. Entonces naturalmente es `1e-6`.

En otras palabras, un número negativo detrás de _"e"_ significa una división por el 1 seguido de la cantidad dada de ceros:

```js
// -3 divide por 1 con 3 ceros
1e-3 === 1 / 1000; // 0.001

// -6 divide por 1 con 6 ceros
1.23e-6 === 1.23 / 1000000; // 0.00000123

// un ejemplo con un número mayor
1234e-2 === 1234 / 100; // 12.34, el punto decimal se mueve 2 veces
```


# Hexadecimales, binarios y octales
Los números [Hexadecimales](https://es.wikipedia.org/wiki/Sistema_hexadecimal) son ampliamente usados en JavaScript para representar colores, codificar caracteres y muchas otras cosas. Es natural que exista una forma breve de escribirlos: `0x` y luego el número.

Por ejemplo:

````js
alert( 0xff ); // 255 
alert( 0xFF ); // 255 (lo mismo en mayúsculas o minúsculas )
````

Los sistemas binario y octal son raramente usados, pero también soportados mediante el uso de los prefijos `0b` y `0o`:

````js
let a = 0b11111111; // binario de 255 
let b = 0o377; // octal de 255

alert( a == b ); // true, el mismo número 255 en ambos lados
````

Solo 3 sistemas numéricos tienen tal soporte. Para otros sistemas numéricos, debemos usar la función `parseInt`.
