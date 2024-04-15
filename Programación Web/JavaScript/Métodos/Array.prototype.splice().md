El método `splice()` modifica el contenido de una matriz eliminando o sustituyendo elementos existentes y/o añadiendo nuevos elementos en su lugar.

```js
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// Inserts at index 1
console.log(months);
// Expected output: Array ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, 'May');
// Replaces 1 element at index 4
console.log(months);
// Expected output: Array ["Jan", "Feb", "March", "April", "May"]
```

# Sintaxis

```js
splice(start)
splice(start, deleteCount)
splice(start, deleteCount, item1)
splice(start, deleteCount, item1, item2, itemN)
```

## Parámetros

### start

Índice de base cero en el que empezar a cambiar la matriz, convertido a un número entero.

- El índice negativo cuenta hacia atrás desde el final de la matriz. Si `start < 0`, se utiliza `start + array.length`.
- Si `start < -array.length` o se omite `start`, se utiliza 0.
- Si `start >= array.length`, no se borrará ningún elemento, pero el método se comportará como una función de adición, añadiendo tantos elementos como se proporcionen.

### deleteCount (Opcional)

Un número entero que indica el número de elementos de la matriz que hay que eliminar desde el principio.  
  
Si se omite `deleteCount`, o si su valor es mayor o igual que el número de elementos después de la posición especificada por `start`, entonces se borrarán todos los elementos desde `start` hasta el final del `array`. Sin embargo, si desea pasar cualquier parámetro `itemN`, debe pasar `Infinity` como `deleteCount` para eliminar todos los elementos después de `start`, porque un indefinido explícito se convierte en 0.  
  
Si `deleteCount` es 0 o negativo, no se eliminará ningún elemento. En este caso, debe especificar al menos un nuevo elemento.

### item1, … , itemN (Opcional)

Los elementos a añadir al array, empezando por el inicio.
Si no se especifica ningún elemento, `splice()` sólo eliminará elementos de la matriz.

## Valor de retorno

Un array que contiene los elementos eliminados.
Si sólo se elimina un elemento, se devuelve un array de un elemento.  
Si no se elimina ningún elemento, se devuelve un array vacío.

# Descripción 

El método `splice()` es un método mutante. Puede cambiar el contenido de `this`. Si el número especificado de elementos a insertar difiere del número de elementos que se eliminan, la longitud del array también cambiará. Al mismo tiempo, utiliza @@species para crear una nueva instancia del array a devolver.

Si la parte eliminada es dispersa, la matriz devuelta por `splice()` también lo será, y los índices correspondientes serán ranuras vacías.

El método `splice()` es genérico. Sólo espera que este valor tenga una propiedad de longitud y propiedades de clave entera. Aunque las cadenas también son de tipo array, este método no es adecuado para ser aplicado sobre ellas, ya que las cadenas son inmutables.

# Ejemplos

## Eliminar 0 (cero) elementos antes del índice 2, e insertar "tambor"

```js
const myFish = ["angel", "clown", "mandarin", "sturgeon"];
const removed = myFish.splice(2, 0, "drum");

// myFish is ["angel", "clown", "drum", "mandarin", "sturgeon"]
// removed is [], no elements removed
```

## Elimina 0 (cero) elementos antes del índice 2, e inserta "tambor" y "guitarra".

```js
const myFish = ["angel", "clown", "mandarin", "sturgeon"];
const removed = myFish.splice(2, 0, "drum", "guitar");

// myFish is ["angel", "clown", "drum", "guitar", "mandarin", "sturgeon"]
// removed is [], no elements removed
```




