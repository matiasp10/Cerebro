Los objetos se utilizan para almacenar _colecciones de datos_ y entidades mas complejas asociados con un nombre clave.
Podemos crear un objeto usando las llaves `{…}` con una lista opcional de propiedades. Una propiedad es un par “`key:value`”, donde **key** es un _string_ (también llamado “nombre clave”), y **value** puede ser _cualquier cosa_.

```js
let user = new Object(); // sintaxis de "constructor de objetos"
let user = {};  // sintaxis de "objeto literal"
```

Normalmente se utilizan las llaves {...}. Esa declaración se llama objeto literal.
# Wrapper

[[Object()]]

# Literales y propiedad
Podemos poner inmediatamente algunas propiedades dentro de `{...}` como pares “_clave:valor_”:

```js
let user = {     // un objeto
  name: "John",  // En la clave "name" se almacena el valor "John"
  age: 30        // En la clave "age" se almacena el valor 30
};
```

Una propiedad tiene una _clave_ (también conocida como “nombre” o “identificador”) antes de los dos puntos ":" y un _valor_ a la derecha.

En el objeto user hay dos propiedades:

1. La primera propiedad tiene la clave "name" y el valor "John".
2. La segunda tienen la clave "age" y el valor 30.

Podemos agregar, eliminar y leer archivos del objeto en cualquier momento.

Se puede acceder a los valores de las propiedades utilizando la notación de punto, el valor puede ser de cualquier tipo.

```js
// Obteniendo los valores de las propiedades del objeto:
alert( user.name ); // John
alert( user.age ); // 30
```

Para eliminar una propiedad podemos usar el operador delete:

```js
delete user.age;
```

También podemos nombrar propiedades con más de una palabra. Pero, de ser así, debemos colocar la clave entre comillas "...":

```js
let user = {
  name: "John",
  age: 30,
  "likes birds": true  // Las claves con más de una palabra deben ir entre comillas
};
```

La última propiedad en la lista puede terminar con una coma:

```js
let user = {
  name: "John",
  age: 30,
}
```

Eso se llama una coma “final” o “colgante”. Facilita agregar, eliminar y mover propiedades, porque todas las líneas se vuelven similares.

# Corchetes

La notación de punto no funciona para acceder a propiedades con claves de más de una palabra:

```js
// Esto nos daría un error de sintaxis
user.likes birds = true
```

JavaScript no entiende eso. Piensa que hemos accedido a `user.likes` y entonces nos da un _error de sintaxis_ cuando aparece el inesperado `birds`.

El punto requiere que la clave sea un identificador de variable válido. Eso implica que: _no contenga espacios_, _no comience con un dígito_ y _no incluya caracteres especiales_ ($ y _ sí se permiten).

Existe una “**notación de corchetes**” alternativa que funciona con cualquier string:

```js
let user = {};

// asignando
user["likes birds"] = true;

// obteniendo
alert(user["likes birds"]); // true

// eliminando
delete user["likes birds"];
```

Ahora todo está bien. Nota que el string dentro de los corchetes está adecuadamente entre comillas (cualquier tipo de comillas servirían).

Las llaves también nos proveen de una forma para obtener la clave de la propiedad como resultado de cualquier expresión como una variable – en lugar de una cadena literal – de la siguiente manera:

```js
let key = "likes birds";

// Tal cual: user["likes birds"] = true;
user[key] = true;
```

Aquí la variable _key_ puede calcularse en tiempo de ejecución o depender de la entrada del usuario y luego lo usamos para acceder a la propiedad. Eso nos da mucha flexibilidad.

Por ejemplo:

```js
let user = {
  name: "John",
  age: 30
};

let key = prompt("¿Qué te gustaría saber acerca del usuario?", "name");

// acceso por medio de una variable
alert( user[key] ); // John (si se ingresara "name")
```

La notación de punto no puede ser usada de manera similar:

```js
let user = {
  name: "John",
  age: 30
};

let key = "name";
alert( user.key ) // undefined
```

## Propiedades calculadas

Podemos usar corchetes en un objeto literal al crear un objeto. A esto se le llama _propiedades calculadas_.

Por ejemplo:
```js
let fruit = prompt("¿Qué fruta comprar?", "Manzana");

let bag = {
  [fruit]: 5, // El nombre de la propiedad se obtiene de la variable fruit
};

alert( bag.apple ); // 5 si fruit es="apple"
```

El significado de una propiedad calculada es simple: `[fruit]` significa que se debe tomar la clave de la propiedad `fruit`.

Entonces, si un visitante ingresa "`apple`", bag se convertirá en `{apple: 5}`.

Esencialmente esto funciona igual que:

```js
let fruit = prompt("¿Qué fruta comprar?", "Manzana");
let bag = {};

// Toma el nombre de la propiedad de la variable fruit
bag[fruit] = 5;
```

…Pero luce mejor.

Podemos usar expresiones más complejas dentro de los corchetes:

```js
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

Los corchetes son mucho más potentes que la notación de punto. Permiten cualquier nombre de propiedad, incluso variables. Pero también es más engorroso escribirlos.

Entonces, la mayoría de las veces, cuando los nombres de propiedad son conocidos y simples, se utiliza el punto. Y si necesitamos algo más complejo, entonces cambiamos a corchetes.

# Atajos para valores de propiedad

En el código real, a menudo usamos variables existentes como valores de los nombres de propiedades.

Por ejemplo:

```js
function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // ...otras propiedades
  };
}

let user = makeUser("John", 30);
alert(user.name); // John
```

En el ejemplo anterior las propiedades tienen los mismos nombres que las variables. El uso de variables para la creación de propiedades es tan común que existe un atajo para valores de propiedad especial para hacerla más corta.

En lugar de `name:name`, simplemente podemos escribir `name`, tal cual:
```js
function makeUser(name, age) {
  return {
    name, // igual que name:name
    age,  // igual que age:age
    // ...
  };
}
```

Podemos usar ambos tipos de notación en un mismo objeto, la normal y el atajo:

```js
let user = {
  name,  // igual que name:name
  age: 30
};
```

# Limitaciones de nombres de propiedad
Como sabemos, una variable no puede tener un nombre igual a una de las palabras reservadas del lenguaje, como `for`, `let`, `return`, etc.

Pero para una propiedad de objeto no existe tal restricción:

```js
// Estas propiedades están bien
let obj = {
  for: 1,
  let: 2,
  return: 3
};

alert( obj.for + obj.let + obj.return );  // 6
```

En resumen, _no hay limitaciones en los nombres de propiedades_. Pueden ser cadenas o símbolos (un tipo especial para identificadores que se cubrirán más adelante).

Otros tipos se convierten automáticamente en cadenas.

Por ejemplo, un número 0 se convierte en cadena "0" cuando se usa como clave de propiedad:

```js
let obj = {
  0: "test" // igual que "0": "test"
};

// ambos alerts acceden a la misma propiedad (el número 0 se convierte a una cadena "0")
alert( obj["0"] ); // test
alert( obj[0] ); // test (la misma propiedad)
```

Hay una pequeña sorpresa por una propiedad especial llamada `__proto__`. No podemos establecerlo dentro de un valor que no sea de objeto:

```js
let obj = {};
obj.__proto__ = 5; // asignando un número
alert(obj.__proto__); // [objeto Object] - el valor es un objeto, no funciona como se "debería"
```

Como podemos ver en el código, se ignora la asignación de un valor primitivo 5.

# Probar si una propiedad existe
Una notable característica de los objetos en JavaScript, en comparación con muchos otros lenguajes, es que es posible acceder a cualquier propiedad. _¡No habrá error si la propiedad no existe!_

La lectura de una propiedad no existente solo devuelve [[Undefined]]. Así que podemos probar fácilmente si la propiedad existe:

```js
let user = {};

alert( user.noSuchProperty === undefined ); // true significa que "no existe tal propiedad"
```

También existe un operador especial para ello: [[in]].

## Bucle for...in

Si queremos recorrer el objeto existe una estructura de control llamada [[for...in]].

# Referencias de objetos
Una de las diferencias fundamentales entre objetos y primitivos es que los objetos son almacenados y copiados “_por referencia_”, en cambio los primitivos: strings, number, boolean, etc.; son asignados y copiados “_como un valor completo_”.

> [!important] 
> Una variable no almacena el objeto mismo sino su “**dirección en memoria**”, en otras palabras “**una referencia**” a él.

Cuando una variable de objeto es copiada, _se copia solo la referencia_. El objeto no es duplicado.

```js
let user = { name: "John" };

let admin = user; // copia la referencia
```

Ahora las dos variables `user` y `admin` poseen una referencia al mismo objeto.
Podemos usar cualquiera de las variables para acceder al objeto y modificar su contenido:

```js
let user = { name: 'John' };

let admin = user;

admin.name = 'Pete'; // cambiado por la referencia "admin"

alert(user.name); // 'Pete', los cambios se ven desde la referencia "user"
```

## Comparación por referencia 

Dos objetos son iguales solamente si ellos son el mismo objeto.

Por ejemplo, aquí a y b tienen referencias al mismo objeto, por lo tanto son iguales:

```js
let a = {};
let b = a; // copia la referencia

alert( a == b ); // true, verdadero. Ambas variables hacen referencia al mismo objeto
alert( a === b ); // true
```

Y aquí dos objetos independientes no son iguales, aunque se vean iguales (ambos están vacíos):

```js
let a = {};
let b = {}; // dos objetos independientes

alert( a == b ); // false
```

Para comparaciones como `obj1 > obj2`, o comparaciones contra un primitivo `obj == 5`, los objetos son convertidos a primitivos. Estudiaremos cómo funciona la conversión de objetos pronto, pero a decir verdad tales comparaciones ocurren raramente y suelen ser errores de código.

> [!info]- Const y los objetos
> Un efecto importante de almacenar objetos como referencias es que un objeto declarado como `const` puede ser modificado.
> Por ejemplo:
> ```js
> const user = {
> name: "John"
> };
> 
> user.name = "Pete"; // (*)
> 
> alert(user.name); // Pete
> ```
> Puede parecer que la línea (*) causaría un error, pero no lo hace. El valor de user es constante, _este valor debe siempre hacer referencia al mismo objeto_, pero las propiedades de dicho objeto pueden cambiar. En otras palabras: `const user` da un error solamente si tratamos de establecer `user=...` como un todo.
> Dicho esto, si realmente necesitamos hacer constantes las propiedades del objeto, también es posible, pero usando métodos totalmente diferentes.

# Clonación de objetos

Podemos crear un nuevo objeto y replicar la estructura del existente iterando a través de sus propiedades y copiándolas en el nivel primitivo.

```js
let user = {
  name: "John",
  age: 30
};

let clone = {}; // el nuevo objeto vacío

// copiemos todas las propiedades de user en él
for (let key in user) {
  clone[key] = user[key];
}

// ahora clone es un objeto totalmente independiente con el mismo contenido
clone.name = "Pete"; // cambiamos datos en él

alert( user.name ); // John aún está en el objeto original
```

## Mediante métodos

- [[Object.assign()]]
- [[structuredClone()]]

## Usando la sintaxis spread ...


# Conversión de objeto a tipos primitivos

¿Qué sucede cuando los objetos se suman `obj1 + obj2`, se restan `obj1 - obj2` o se imprimen utilizando `alert(obj)`?

[[Conversión de objetos]]
# Tipos de objetos

- [[Array]]
- [[Programación Web/JavaScript/Tipos de datos/Funciones|Funciones]]
- [[Date()]]
- [[Programación Web/JavaScript/Tipos de datos/Map]]
- [[WeakMap]]
- [[Set]]
- [[WeakSet]]
- [[Programación Web/JavaScript/Tipos de datos/Promesas|Promesas]]
- [[Error()]]

# This

- [[This]]
- [[Optional chaining]]
- [[Getters & Setters]]
- [[Descriptores de propiedad]]