El valor de “_Symbol_” representa un **identificador único**.

```js
let id = Symbol("id")
```

Se garantiza que los símbolos son _únicos_. Aunque declaremos varios Symbols con la misma descripción, éstos tendrán valores distintos. La descripción es solamente una etiqueta que no afecta nada más.

```js
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

Un symbol es un “_valor primitivo único_” con una descripción opcional.

> [!warning]- Los symbols no se auto convierten
> La mayoría de los valores en JavaScript soportan la conversión implícita a string. Los Symbols son especiales, éstos no se auto convierten.
> ```js
> let id = Symbol("id");
> alert(id); // TypeError: No puedes convertir un valor Symbol en string
> ```
> Esta es una “_protección del lenguaje_” para evitar errores, ya que String y Symbol son fundamentalmente diferentes y no deben convertirse accidentalmente uno en otro.
> 
> Si realmente queremos mostrar un Symbol, necesitamos llamar el método `.toString()` explícitamente
> ```js
> let id = Symbol("id");
> alert(id.toString()); // Symbol(id), ahora sí funciona
> ```
> 
> U obtener `symbol.description` para mostrar solamente la descripción:
> ```js
> let id = Symbol("id");
> alert(id.description); // id
> ```

# Wrapper
[[Symbol()]]

# Claves ocultas

Los Symbols nos permiten crear propiedades “ocultas” en un objeto, a las cuales ninguna otra parte del código puede dar acceso ni sobrescribir accidentalmente.

Por ejemplo, si estamos trabajando con objetos `user` que pertenecen a código de terceros y queremos agregarles identificadores:

```js
let user = { // pertenece a otro código
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // podemos accesar a la información utilizando el symbol como nombre de clave
```

¿Cuál es la ventaja de usar `Symbol("id")` y no un string `"id"`?

Como los objetos `user` pertenecen a otro código, es inseguro agregarles campos pues podría afectar su comportamiento predefinido en ese otro código. Sin embargo, los símbolos no pueden ser accedidos accidentalmente. El código de terceros no se percataría de los símbolos nuevos, por lo que se considera seguro agregar símbolos a los objetos `user`.

Además, imagina que otro script quiere tener su propio identificador “id” dentro de `user` para sus propios fines.

Entonces ese script puede crear su propio `Symbol("id")`, como aquí:

```js
// ...
let id = Symbol("id");

user[id] = "Su valor de id";
```

No habrá conflicto porque los Symbols siempre son diferentes, incluso si tienen el mismo nombre.

…pero si utilizamos un string `"id"` en lugar de un Symbol para el mismo propósito, ciertamente _habrá_ un conflicto:

```js
let user = { name: "John" };

// Nuestro script usa la propiedad "id"
user.id = "Nuestro valor id";

// ...Otro script también quiere usar "id"  ...

user.id = "Su valor de id"
// Boom! sobreescrito por otro script!
```

## En objetos literales

Si queremos usar un Symbol en un objeto literal, debemos usar llaves.

```js
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123 // no "id": 123
};
```

Se hace así porque necesitamos que el valor de la variable id sea la clave, no el string “id”.

## Son omitidos en el for...in

Las claves de Symbol no participan dentro de los ciclos _for...in_.

```js
let id = Symbol("id");
let user = {
  name: "John",
  age: 30,
  [id]: 123
};

for (let key in user) alert(key); // nombre, edad (no aparecen symbols)

// el acceso directo por medio de symbol funciona
alert( "Direct: " + user[id] ); // Direct: 123
```

`Object.keys(user)` también los ignora. Esto forma parte del principio general de “_ocultamiento de propiedades simbólicas_”. Si otro script o si otra librería itera sobre nuestro objeto, este no dará acceso inesperadamente a la clave de Symbol.

En contraste, `Object.assign` copia tanto las claves string como symbol

```js
let id = Symbol("id");
let user = {
  [id]: 123
};

let clone = Object.assign({}, user);

alert( clone[id] ); // 123
```

No hay paradoja aquí. Es así por diseño. La idea es que cuando clonamos un objeto o cuando fusionamos objetos, generalmente queremos que se copien _todas_ las claves (incluidos los Symbol como `id`).
# Symbols globales
Normalmente todos los Symbols son diferentes aunque tengan el mismo nombre. Pero algunas veces necesitamos que symbols con el mismo nombre sean la misma entidad.

Para lograr esto, existe un _global symbol registry_. Ahí podemos crear symbols y acceder a ellos después, lo cual nos garantiza que cada vez que se acceda a la clave con el mismo nombre, esta te devuelva exactamente el mismo symbol.

[[Symbol()#Métodos estáticos|Métodos estáticos]]

# Symbols del sistema
Existen varios symbols del sistema que JavaScript utiliza internamente, y que podemos usar para ajustar varios aspectos de nuestros objetos.

[[Symbol()#Propiedades estáticas|Simbolos del sistema]]
