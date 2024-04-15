**Boolean** es un objeto primitivo envolvente que permite representar y manipular valores de tipo lógico `true` y `false`.

# Parámetro

## Valor

El valor pasado como primer parámetro se convierte en un valor booleano, si es necesario. Si el valor se omite o es 0, -0, null, false, NaN, undefined, o la cadena vacía (""), el objeto tiene un valor inicial de _false_. Todos los demás valores, incluido cualquier objeto, un arreglo vacío (`[]`) o la cadena "false", crean un objeto con un valor inicial de _true_.

> [!tip] 
> No confundas los valores del Boolean primitivo, true y false con los valores true y false del objeto Boolean.

Cualquier objeto cuyo valor no sea _undefined_ o _null_, incluido un objeto Boolean cuyo valor es false, se evalúa como true cuando se pasa a una declaración condicional.

```js
var x = new Boolean(false);
if (x) {
  // este código se ejecuta
}
```

Este comportamiento no se aplica a los _Boolean primitivos_. Por ejemplo, la condición en la siguiente instrucción `if` se evalúa como false:

```js
var x = false;
if (x) {
  // este código no se ejecuta
}
```

# Constructor

```js
let soyHumano = new Boolean(true)
```

# Métodos de instancia

## Boolean.prototype.toString()
Devuelve una cadena de true o false dependiendo del valor del objeto. Redefine el método `Object.prototype.toString()`.

## Boolean.prototype.valueOf()
Devuelve el valor primitivo del objeto Boolean. Redefine el método `Object.prototype.valueOf()`.

