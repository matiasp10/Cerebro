El método pop() elimina el último elemento de una matriz y devuelve ese elemento. Este método cambia la longitud de la matriz.

```js
const plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];

console.log(plants.pop());
// Expected output: "tomato"

console.log(plants);
// Expected output: Array ["broccoli", "cauliflower", "cabbage", "kale"]

plants.pop();

console.log(plants);
// Expected output: Array ["broccoli", "cauliflower", "cabbage"]
```

# Sintaxis

```js
pop()
```

## Valor de retorno

El elemento eliminado del array; `undefined` si el array está vacío.

# Descripción

El método `pop()` elimina el último elemento de una matriz y devuelve ese valor a quien lo llama. Si se llama a `pop()` con una matriz vacía, devuelve un valor `undefined`.

`Array.prototype.shift()` tiene un comportamiento similar a `pop()`, pero aplicado al primer elemento de un array.

El método `pop()` es un _método mutante_. Cambia la longitud y el contenido de este. En caso de que quieras que el valor de `this` sea el mismo, pero devuelva un nuevo array con el último elemento eliminado, puedes usar `arr.slice(0, -1)` en su lugar.

El método `pop()` es _genérico_. Sólo espera que este valor tenga una propiedad `length` y propiedades `integer-keyed`. Aunque las cadenas también son de tipo array, este método no es adecuado para ser aplicado sobre ellas, ya que las cadenas son inmutables.

# Ejemplos

## Eliminar el último elemento de una matriz

El siguiente código crea la matriz `myFish` que contiene cuatro elementos, y luego elimina su último elemento.

```js
const myFish = ["angel", "clown", "mandarin", "sturgeon"];

const popped = myFish.pop();

console.log(myFish); // ['angel', 'clown', 'mandarin' ]

console.log(popped); // 'sturgeon'
```

## Llamada a pop() en objetos que no son matrices

El método `pop()` lee la propiedad length de esto. Si la longitud normalizada es 0, length se vuelve a poner a 0 (mientras que antes podía ser negativa o indefinida). En caso contrario, se devuelve y elimina la propiedad length - 1.

```js
const arrayLike = {
  length: 3,
  unrelated: "foo",
  2: 4,
};
console.log(Array.prototype.pop.call(arrayLike));
// 4
console.log(arrayLike);
// { length: 2, unrelated: 'foo' }

const plainObj = {};
// There's no length property, so the length is 0
Array.prototype.pop.call(plainObj);
console.log(plainObj);
// { length: 0 }
```

## Utilizar un objeto en forma de matriz

`push` y `pop` son intencionadamente genéricos, y podemos usar eso a nuestro favor, como muestra el siguiente ejemplo.

> [!note] Nota
> Observa que en este ejemplo, no creamos un array para almacenar una colección de objetos. En su lugar, almacenamos la colección en el propio objeto y usamos llamadas a Array.prototype.push y Array.prototype.pop para engañar a esos métodos y que piensen que estamos tratando con un array.

```js
const collection = {
  length: 0,
  addElements(...elements) {
    // obj.length will be incremented automatically
    // every time an element is added.

    // Returning what push returns; that is
    // the new value of length property.
    return [].push.call(this, ...elements);
  },
  removeElement() {
    // obj.length will be decremented automatically
    // every time an element is removed.

    // Returning what pop returns; that is
    // the removed element.
    return [].pop.call(this);
  },
};

collection.addElements(10, 20, 30);
console.log(collection.length); // 3
collection.removeElement();
console.log(collection.length); // 2
```

# Compatibilidad

https://caniuse.com/mdn-javascript_builtins_array_pop