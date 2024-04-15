[[Number]]

**Number** es un objeto primitivo envolvente que permite representar y manipular valores numéricos cómo 37 o -9.25. El constructor Number contiene constantes y métodos para trabajar con números. Valores de otro tipo pueden ser convertidos a números usando la función _Number()_.

```js
new Number(value);
var a = new Number('123'); // a === 123 es false
var b = Number('123'); // b === 123 es true
a instanceof Number; // es true
b instanceof Number; // es false
```

> [!note]- Descripción
> Los principales usos del objeto Number(valor) son convertir un string u otro valor a uno de tipo numérico; si el argumento no puede ser convertido a un número, devuelve NaN.

# Parámetros

## Valor

El valor numérico de un objeto que está siendo creado.

# Constructor

```js
new Number(valor)
Number(valor)
```

# Propiedades

## Number.EPSILON
El intervalo más pequeño entre dos números representables

## Number.MAX_SAFE_INTEGER
El número máximo representable en JavaScript (253 - 1).

## Number.MAX_VALUE
El número más grande representable.

## Number.MIN_SAFE_INTEGER
El número mínimo representable en JavaScript (-(253 - 1)).

## Number.MIN_VALUE
El número más pequeño representable - que es el número positivo más cercano a cero (sin llegar a ser cero)-.

## Number.NaN
Valor especial "no es número" NaN.

## Number.NEGATIVE_INFINITY
Valor especial para representar infinitos negativos; retorno de un desborde de pila overflow.

## Number.POSITIVE_INFINITY
Valor especial para representar infinitos positivos; retorno de un desborde de pila overflow.

## Number.prototype
Permite la adición de propiedades a un objeto Number.
# Métodos 

## Number.isNaN()
Determina si el valor es NaN.

## Number.isFinite()
Determina si el valor es un numero infinito.

## Number.isInteger()
Determina si un numero es entero.

## Number.isSafeInteger()
Determine si el valor pasado es un entero seguro (número entre -(253 - 1) y 253 - 1).

## Number.parseFloat()
El valor es el mismo que ``parseFloat()`` del objeto global.

## Number.parseInt()
El valor es el mismo que ``parseInt()`` del objeto global.
# Instancias Number

Todas las instancias heredan de _Number.prototype_.

## Métodos

### Number.prototype.toExponential(fractionDigits)
Devuelve una cadena que representa el número en notación exponencial.

### Number.prototype.toFixed(digits)
Devuelve una cadena que representa el número en notación de punto fijo.

### Number.prototype.toLocaleString(``[locales [, options]]``)
Devuelve una cadena con una representación sensible al idioma de este número. Invalida el método ``Object.prototype.toLocaleString()``.