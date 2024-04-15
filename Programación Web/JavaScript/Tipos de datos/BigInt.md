En JavaScript, el tipo “number” no puede representar de forma segura valores enteros mayores que $(2^{53}-1)$ (eso es `9007199254740991`), o menor que $-(2^{53}-1)$ para negativos.

Para ser realmente precisos, el tipo de dato “number” puede almacenar enteros muy grandes (hasta $1.7976931348623157 * 10^{308}$), pero fuera del rango de enteros seguros $±(2^{53}-1)$ habrá un _error de precisión_, porque no todos los dígitos caben en el almacén fijo de 64-bit. Así que es posible que se almacene un valor “aproximado”.

Por ejemplo, estos dos números (justo por encima del rango seguro) son iguales:

```js
console.log(9007199254740991 + 1); // 9007199254740992
console.log(9007199254740991 + 2); // 9007199254740992
```

Podemos decir que ningún entero impar mayor que $(2^{53}-1)$ puede almacenarse en el tipo de dato “number”.

Para la mayoría de los propósitos, el rango $±(2^{53}-1)$ es suficiente, pero a veces necesitamos números realmente grandes; por ejemplo, para criptografía o marcas de tiempo de precisión de microsegundos.

**`BigInt`** se agregó recientemente al lenguaje para representar _enteros de longitud arbitraria_.

Un valor `BigInt` se crea agregando `n` al final de un entero o usando el wrapper:

```js
const bigint = 1234567890123456789012345678901234567890n;

const sameBigint = BigInt("1234567890123456789012345678901234567890");

const bigintFromNumber = BigInt(10); // lo mismo que 10n
```

# Wrapper
[[BigInt()]]
# Operadores matemáticos
BigInt puede ser usado mayormente como un número regular, por ejemplo:

```js
alert(1n + 2n); // 3

alert(5n / 2n); // 2
```

La división `5/2` devuelve el resultado redondeado a cero, sin la parte decimal. Todas las operaciones sobre bigints devuelven bigints.

No podemos mezclar bigints con números regulares:

```js
alert(1n + 2); // Error: No se puede mezclar BigInt y otros tipos.
```

Podemos convertirlos explícitamente cuando es necesario: usando BigInt() o Number() como aquí:

```js
let bigint = 1n;
let number = 2;

// De number a bigint
alert(bigint + BigInt(number)); // 3

// De bigint a number
alert(Number(bigint) + number); // 3
```

Las operaciones de conversión siempre son silenciosas, nunca dan error, pero si el bigint es tan gigante que no podrá ajustarse al tipo numérico, los bits extra serán recortados, entonces deberíamos ser cuidadosos al hacer tal conversión.

> [!info]- El unario + no tiene soporte en bigints
>  El operador unario más `+value` es una manera bien conocida de convertir <u>value</u> a <u>number</u>.
>  Para evitar las confusiones, con bigints eso _no es soportado_:
>  ```js
>  let bigint = 1n;
>  
>  alert( +bigint ); // error
>  ```
>  Entonces debemos usar _Number()_ para convertir un bigint a number.

# Comparaciones

Comparaciones tales como `<`, `>` funcionan bien entre bigints y numbers:

```js
alert( 2n > 1n ); // true

alert( 2n > 1 ); // true
```

Por favor, nota que como number y bigint pertenecen a diferentes tipos, ellos pueden ser iguales == pero no estrictamente iguales ===

```js
alert( 1 == 1n ); // true

alert( 1 === 1n ); // false
```

# Operaciones booleanas

Cuando están dentro de un if u otra operación booleana, los bigints _se comportan como numbers_.

Por ejemplo, en if, el bigint 0n es falso, los otros valores son verdaderos:

```js
if (0n) {
  // nunca se ejecuta
}
```

Los operadores booleanos, tales como `||`, `&&` y otros, también trabajan con bigints en forma similar a los number:

```js
alert( 1n || 2 ); // 1 (1n es considerado verdadero)

alert( 0n || 2 ); // 2 (0n es considerado falso)
```