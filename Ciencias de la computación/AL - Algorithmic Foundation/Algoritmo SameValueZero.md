Similar a la igualdad del mismo valor, pero +0 y -0 se consideran iguales.

La igualdad de valor igual a cero no está expuesta como API de JavaScript, pero puede implementarse con código personalizado:

```js
function sameValueZero(x, y) {
  if (typeof x === "number" && typeof y === "number") {
    // x and y are equal (may be -0 and 0) or they are both NaN
    return x === y || (x !== x && y !== y);
  }
  return x === y;
}
```

Mismo-valor-cero sólo difiere de la igualdad estricta al tratar NaN como equivalente, y sólo difiere de la igualdad del mismo valor al tratar -0 como equivalente a 0. Esto hace que normalmente tenga el comportamiento más sensato durante la búsqueda, especialmente cuando se trabaja con NaN. Es utilizado por `Array.prototype.includes()`, `TypedArray.prototype.includes()`, así como por los métodos Map y Set para comparar la igualdad de claves.