	[[Objetos]]

Los objetos te permiten almacenar colecciones de datos a través de nombres. Eso está bien.

Pero a menudo necesitamos una _colección ordenada_, donde tenemos un 1ro, un 2do, un 3er elemento y así sucesivamente. Por ejemplo, necesitamos almacenar una lista de algo: usuarios, bienes, elementos HTML, etc.

No es conveniente usar objetos aquí, porque no proveen métodos para manejar el orden de los elementos. No podemos insertar una nueva propiedad “entre” los existentes. Los objetos no están hechos para eso.

Existe una estructura llamada `Array` (llamada en español arreglo o matriz/vector) para almacenar colecciones ordenadas.

![[Pasted image 20230222210013.png|center]]
En JavaScript, los arrays no son primitivas, sino objetos Array con las siguientes características básicas:

- Las matrices de JavaScript son **redimensionables** y pueden contener una **mezcla de diferentes tipos de datos**. (Cuando esas características no sean deseables, utilice en su lugar arrays tipados).
- Los Arrays de JavaScript **no son array asociativos** y, por lo tanto, no se puede acceder a los elementos de la matriz utilizando cadenas arbitrarias como índices, sino que se debe acceder utilizando enteros no negativos (o su respectiva forma de cadena) como índices.
- Las matrices de JavaScript están **indexadas a cero**: el primer elemento de una matriz está en el índice 0, el segundo en el índice 1, y así sucesivamente - y el último elemento está en el valor de la propiedad `length` de la matriz menos 1.
- Las operaciones de **copia de arrays de JavaScript crean copias superficiales**. (Todas las operaciones de copia estándar incorporadas con cualquier objeto JavaScript crean copias superficiales, en lugar de copias profundas).

# Descripción
## Índices
Los objetos array no pueden utilizar cadenas arbitrarias como índices de elementos (como en un array asociativo), sino que _deben utilizar enteros no negativos_ (o su respectiva forma de cadena). El establecimiento o acceso a través de números no enteros no establecerá o recuperará un elemento de la propia lista de la matriz, sino que establecerá o accederá a una variable asociada con la colección de propiedades de objeto de esa matriz. Las propiedades de objeto de la matriz y la lista de elementos de la matriz son independientes, y las operaciones de recorrido y mutación de la matriz no se pueden aplicar a estas propiedades con nombre.

> [!failure] 
> ```js
> console.log(arr.0); // a syntax error
> ```

La sintaxis de JavaScript requiere que se acceda a las propiedades que empiezan por un dígito utilizando la _notación de corchetes_ en lugar de la _notación de puntos_. También es posible entrecomillar los índices de la matriz (por ejemplo, `years['2']` en lugar de `years[2]`), aunque no suele ser necesario.

El motor JavaScript convierte el 2 de `years[2]` en una cadena mediante una conversión implícita `toString`. Como resultado, `'2'` y `'02'` se referirían a dos ranuras diferentes en el objeto `years`, y el siguiente ejemplo podría ser `true`:

> [!success] 
> ```js
> console.log(years["2"] !== years["02"]);
> ```

Sólo `years['2']` es un índice real del array. `years['02']` es una propiedad de cadena arbitraria que no será visitada en la iteración del array.

## Relación entre la longitud y las propiedades numéricas
La propiedad de longitud de un array JavaScript y las propiedades numéricas están conectadas.

Varios de los métodos de array incorporados (por ejemplo, `join()`, `slice()`, `indexOf()`, etc.) tienen en cuenta el valor de la propiedad length de un array cuando se llaman.

Otros métodos (por ejemplo, `push()`, `splice()`, etc.) también resultan en actualizaciones de la propiedad length de un array.

```js
const fruits = [];
fruits.push("banana", "apple", "peach");
console.log(fruits.length); // 3
```

Al establecer una propiedad en una matriz JavaScript, cuando la propiedad es un índice de matriz válido y ese índice está fuera de los límites actuales de la matriz, el motor actualizará la propiedad de longitud de la matriz en consecuencia:

```js
fruits[5] = "mango";
console.log(fruits[5]); // 'mango'
console.log(Object.keys(fruits)); // ['0', '1', '2', '5']
console.log(fruits.length); // 6
```

Aumentar la longitud.

```js
fruits.length = 10;
console.log(fruits); // ['banana', 'apple', 'peach', empty x 2, 'mango', empty x 4]
console.log(Object.keys(fruits)); // ['0', '1', '2', '5']
console.log(fruits.length); // 10
console.log(fruits[8]); // undefined
```

Sin embargo, al reducir la propiedad de longitud se eliminan elementos.

```js
fruits.length = 2;
console.log(Object.keys(fruits)); // ['0', '1']
console.log(fruits.length); // 2
```

## Métodos de matrices y ranuras vacías

Las ranuras vacías en matrices dispersas se comportan de forma inconsistente entre los métodos de matrices. Por lo general, los métodos más antiguos omiten las ranuras vacías, mientras que los más recientes las tratan como `undefined`.

## Métodos de copia y métodos de mutación

Algunos métodos no mutan el array existente sobre el que se ha llamado al método, sino que devuelven un nuevo array. Lo hacen accediendo primero a `this.constructor[Symbol.species]` para determinar el constructor a utilizar para el nuevo array. A continuación, la nueva matriz se rellena con elementos. La copia siempre se realiza de forma superficial: el método nunca copia nada más allá de la matriz creada inicialmente. Los elementos de la(s) matriz(es) original(es) se copian en la nueva matriz de la siguiente manera:

- **Objetos**: la referencia al objeto se copia en la nueva matriz. Tanto la matriz original como la nueva hacen referencia al mismo objeto. Es decir, si se modifica un objeto referenciado, los cambios son visibles tanto en el array nuevo como en el original.
- **Tipos primitivos como cadenas, números y booleanos** (no objetos String, Number y Boolean): sus valores se copian en el nuevo array.

Otros métodos mutan el array sobre el que se ha llamado al método, en cuyo caso su valor de retorno difiere según el método: a veces una referencia al mismo array, a veces la longitud del nuevo array.

## Métodos iterativos

Muchos métodos de matrices toman como argumento una función callback. La función callback se llama secuencialmente y como máximo una vez por cada elemento del array, y el valor de retorno de la función callback se utiliza para determinar el valor de retorno del método. Todos comparten la misma firma:

```js
method(callbackFn, thisArg)
```

Donde `callbackFn` toma tres argumentos:

- _`element`_: El elemento actual que se está procesando en el array.
- _`index`_: El índice del elemento actual que se está procesando en la matriz.
- _`array`_: El array sobre el que se ha llamado al método.

Lo que se espera que devuelva `callbackFn` depende del método de array que fue llamado.

El argumento `thisArg` (por defecto `undefined`) se utilizará como el valor `this` cuando se llame a `callbackFn`. El valor `this` observable en última instancia por `callbackFn` se determina según las reglas habituales: si `callbackFn` no es estricto, los valores `this` primitivos se envuelven en objetos, y `undefined/null` se sustituye por `globalThis`. El argumento `thisArg` es irrelevante para cualquier `callbackFn` definido con una función de flecha, ya que las funciones de flecha no tienen su propio enlace `this`.

Todos los métodos iterativos son copiadores y genéricos, aunque se comportan de forma diferente con ranuras vacías.

## Métodos de array genéricos

Los métodos de array son siempre genéricos - no acceden a ningún dato interno del objeto array. Sólo acceden a los elementos del array a través de la propiedad length y a los elementos indexados. Esto significa que también pueden invocarse en objetos tipo array.

```js
const arrayLike = {
  0: "a",
  1: "b",
  length: 2,
};
console.log(Array.prototype.join.call(arrayLike, "+")); // 'a+b'
```

### Normalización de la propiedad de longitud

La propiedad `length` se _convierte a un entero_ y luego se sujeta al rango entre 0 y $2^{53} - 1$. `NaN` se convierte en 0, por lo que incluso cuando `length` no está presente o es `undefined`, se comporta como si tuviera valor 0.

```js
Array.prototype.flat.call({}); // []
```

Algunos métodos de array establecen la propiedad length del objeto array. Siempre establecen el valor después de la normalización, por lo que la longitud siempre termina como un entero.

```js
const a = { length: 0.7 };
Array.prototype.push.call(a);
console.log(a.length); // 0
```

### Objetos array-like
El término objeto tipo array se refiere a cualquier objeto que no se lance durante el proceso de conversión de longitud descrito anteriormente. En la práctica, se espera que dicho objeto tenga realmente una _propiedad `length`_ y que tenga _elementos indexados_ en el rango de 0 a $length - 1$. (Si no tiene todos los índices, será funcionalmente equivalente a un array disperso).

Muchos objetos DOM son del tipo array - por ejemplo, `NodeList` y `HTMLCollection`. El objeto `arguments` también es un array-like. Puedes llamar a métodos de array en ellos incluso si ellos mismos no tienen estos métodos.

```js
function f() {
  console.log(Array.prototype.join.call(arguments, "+"));
}

f("a", "b"); // 'a+b'
```

# Herencia

[[Function]]
[[Object()]]

# Constructor
El constructor **`Array()`** se utiliza para crear objetos [`Array`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array).

```js
new Array(element0, element1, /* … ,*/ elementN)
new Array(arrayLength)
Array(element0, element1, /* … ,*/ elementN)
Array(arrayLength)
```

> [!note] Nota
> `Array()` puede ser llamado con o sin [`new`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/new). Ambos crean una nueva instancia de `Array`.

## Parámetros

### elementN

Un array de JavaScript se inicializa con los elementos dados, excepto en el caso donde se pase un solo argumento al constructor de `Array` y ese argumento sea un número (véase el parámetro `arrayLength` más abajo). Tenga en cuenta que este caso especial sólo se aplica a los arrays de JavaScript creadas con el constructor `Array`, no a los arrays literales, creadas con la sintaxis de corchetes.

### arrayLength

Si el único argumento pasado al constructor de `Array` es un número entero entre 0 y $2^{32}-1$ (incluido), éste devuelve un nuevo array de JavaScript con su propiedad de `length` establecida a ese número.

## Excepciones

### RangeError

Se lanza si sólo hay un argumento (`arrayLength`) y su valor no está entre 0 y $2^{32}-1$ (incluido).


# Propiedades estáticas

## get Array`[@@species]`
La función del constructor se utiliza para crear objetos derivados.

# Métodos estáticos

## Array.from()
Crea una nueva instancia de Array a partir de ArrayLike, un objeto iterable o parecido a un array.

## Array.isArray()
Devuelve true si valor es un array, y false en caso contrario.

## Array.of()
Crea una nueva instancia de Array con un número variable de parámetros, independientemente del número y del tipo de dichos parámetros.

# Propiedades de instancia

## Array.prototype.length
Indica el número de elementos de un array.

## Array.prototype`[@@unscopables]`
Símbolo que contiene todos los nombres de las propiedades que se excluyen de un ámbito de enlace with.

# Métodos de instancia

## Array.prototype.concat()
Devuelve un nuevo array que es la concatenación de aquél sobre el que se invoca, seguido de otros array(s) o valor(es).

## Array.prototype.copyWithin()
Copia una secuencia de elementos de un array dentro del propio array.

## Array.prototype.entries()
Devuelve un nuevo objeto Array Iterator que contiene los pares clave/valor para cada índice del array.

## Array.prototype.every()
Devuelve true si todos los elementos del array cumplen el predicado que recibe como parámetro.

## Array.prototype.fill()
Asigna un valor estático a todos los elementos del array entre las posiciones inicio y fin.

## Array.prototype.filter()
Devuelve un nuevo array que contiene todos los elementos de aquél para el cual se llama que cumplan el predicado que se le pasa como parámetro.

## Array.prototype.find()
Devuelve el primer elemento del array que cumpla el predicado que se pasa como parámetro, o undefined si ninguno lo cumple.

## Array.prototype.findIndex()
Devuelve el índice del primer elemento del array que cumpla el predicado que se pasa como parámetro, o -1 si ninguno lo cumple.

## Array.prototype.findLast()
Devuelve el valor del último elemento de la matriz que satisface la función de comprobación proporcionada, o `undefined` si no se encuentra ningún elemento apropiado.

## Array.prototype.findLastIndex()
Devuelve el índice del último elemento de la matriz que satisface la función de comprobación proporcionada, o -1 si no se ha encontrado ningún elemento apropiado.

## Array.prototype.flat()
Devuelve una nuevo array con todos los elementos de los subarrays concatenados en ella recursivamente hasta la profundidad especificada.

## Array.prototype.flatMap()
Devuelve un nuevo array formado aplicando una función de devolución de llamada dado a cada elemento de la matriz de llamada y, a continuación, aplanando el resultado en un nivel.

## Array.prototype.forEach()
Llama a la función pasada como parámetro para todos los elementos del array.

## Array.prototype.group()
Agrupa los elementos de un array en un objeto según las cadenas devueltas por una función de prueba.

## Array.prototype.groupToMap()
Agrupa los elementos de un array en un Map según los valores devueltos por una función de prueba.

## Array.prototype.includes()
Determina si el array de llamada contiene un valor, devolviendo verdadero o falso según corresponda.

## Array.prototype.indexOf()
Devuelve el primer (mínimo) índice en el que se puede encontrar un elemento dado en el array de llamada.

## Array.prototype.join()
Concatena en un string todos los elementos de un array.

## Array.prototype.keys()
Devuelve un nuevo Array Iterator que contiene las claves de cada índice del array.

## Array.prototype.lastIndexOf()
Devuelve el último (mayor) índice en el que se puede encontrar un elemento dado en la matriz de llamada, o -1 si no se encuentra ninguno.

## Array.prototype.map()
Devuelve un nuevo array que contiene el resultado de llamar a la función pasada como parámetro a todos los elementos del array sobre el que se invoca.

## Array.prototype.pop()
Elimina el último elemento de un array, y devuelve dicho elemento.
[[Array.prototype.pop()]]

## Array.prototype.push()
Añade uno o más elementos al final de un array y devuelve el nuevo valor de su propiedad length.

## Array.prototype.reduce()
Aplica la función pasada como parámetro a un acumulador y a cada valor del array, que se recorre de izquierda a derecha, para reducirlo a un único valor.

## Array.prototype.reduceRight()
Aplica la función pasada como parámetro a un acumulador y a cada valor del array, que se recorre de derecha a izquierda, para reducirlo a un único valor.

## Array.prototype.reverse()
Invierte el orden de los elementos de un array (el primero pasa a ser el último y el último a ser el primero) en el propio array. Este método modifica el array.

## Array.prototype.shift()
Elimina el primer elemento de un array, y devuelve dicho elemento.

## Array.prototype.slice()
Extrae una porción del array sobre el que se llama y devuelve un nuevo array.

## Array.prototype.some()
Devuelve true si al menos un elemento del array cumple con el predicado que se pasa como parámetro.

## Array.prototype.sort()
Ordena los elementos de un array, modificando éste, y devuelve el array ordenado.

## Array.prototype.splice()
Añade, borra o modifica elementos de un array.

## Array.prototype.toLocaleString()
Devuelve un string adaptado a la configuración regional que representa el array y sus elementos. Redefine el método Object.prototype.toLocaleString().

## Array.prototype.toString()
Devuelve un string que representa el array y sus elementos. Redefine el método Object.prototype.toString().

## Array.prototype.unshift()
Añada uno o más elementos al inicio de un array y devuelve el nuevo valor de length para el array resultante.

## Array.prototype.values()
Devuelve un nuevo objeto Array Iterator que contiene los valores para cada índice del array.

## Array.prototype`[@@iterator]()`
Devuelve un nuevo objeto Array Iterator que contiene los valores para cada índice del array.