TypeScript se encuentra en una relación inusual con JavaScript. TypeScript ofrece todas las características de JavaScript, y una capa adicional sobre éstas: El sistema de tipos de TypeScript.  
  
Por ejemplo, JavaScript proporciona primitivas del lenguaje como cadena y número, pero no comprueba que las hayas asignado de forma consistente. TypeScript lo hace.  
  
Esto significa que tu código JavaScript existente también es código TypeScript. El principal beneficio de TypeScript es que puede resaltar comportamientos inesperados en tu código, reduciendo la posibilidad de errores.  
  
Este tutorial proporciona una breve visión general de TypeScript, centrándose en su sistema de tipos.

## Tipos por inferencia

TypeScript conoce el lenguaje JavaScript y generará tipos por ti en muchos casos. Por ejemplo, al crear una variable y asignarle un valor concreto, TypeScript utilizará el valor como tipo.

```ts
let helloWorld = "Hello World"; // `let helloWorld: string`
```

Entendiendo cómo funciona JavaScript, TypeScript puede construir un sistema de tipos que acepte código JavaScript pero que tenga tipos. Esto ofrece un sistema de tipos sin necesidad de añadir caracteres extra para hacer explícitos los tipos en tu código. Así es como TypeScript sabe que `helloWorld` es un `string` en el ejemplo anterior.  
  
Puede que hayas escrito **JavaScript** en `Visual Studio Code`, y que hayas tenido autocompletado del editor. `Visual Studio Code` utiliza **TypeScript** para facilitar el trabajo con JavaScript.
## Definición de tipos

Puedes utilizar una gran variedad de patrones de diseño en JavaScript. Sin embargo, algunos patrones de diseño dificultan que los tipos se infieran automáticamente (por ejemplo, los patrones que utilizan programación dinámica). Para cubrir estos casos, TypeScript soporta una extensión del lenguaje JavaScript, que ofrece lugares para que le digas a TypeScript cuáles deberían ser los tipos.  
  
Por ejemplo, para crear un objeto con un tipo inferido que incluya `name: string` e `id: number`, puedes escribir:

```ts
const user = {
  name: "Hayes",
  id: 0,
};
```

Puede describir explícitamente la forma de este objeto mediante una declaración de interfaz:

```ts
interface User {
  name: string;
  id: number;
}
```

A continuación, puede declarar que un objeto JavaScript se ajusta a la forma de su nueva interfaz utilizando sintaxis como `: TypeName` después de la declaración de una variable:

```ts
const user: User = {
  name: "Hayes",
  id: 0,
};
```

Si proporcionas un objeto que no coincide con la interfaz que has proporcionado, TypeScript te avisará:

```ts error:8-9
interface User {
  name: string;
  id: number;
}
 
const user: User = {
  username: "Hayes",
// Type '{ username: string; id: number; }' is not assignable to type 'User'.
// Object literal may only specify known properties, and 'username' does not exist in type 'User'.
id: 0,
};
```

Dado que JavaScript soporta clases y programación orientada a objetos, también lo hace TypeScript. Puedes usar una declaración de interfaz con clases:

```ts
interface User {
  name: string;
  id: number;
}
 
class UserAccount {
  name: string;
  id: number;
 
  constructor(name: string, id: number) {
    this.name = name;
    this.id = id;
  }
}
 
const user: User = new UserAccount("Murphy", 1);
```

Puede utilizar interfaces para anotar parámetros y valores de retorno de funciones:

```ts
function deleteUser(user: User) {
  // ...
}
 
function getAdminUser(): User {
  //...
}
```

Ya existe un pequeño conjunto de tipos primitivos disponibles en JavaScript: boolean, bigint, null, number, string, symbol e undefined, que puedes usar en una interfaz. TypeScript amplía esta lista con algunos más, como any (permite cualquier cosa), unknown (asegura que alguien que utilice este tipo declare cuál es el tipo), never (no es posible que este tipo pueda ocurrir), y void (una función que devuelve indefinido o no tiene valor de retorno).  
  
Verás que hay dos sintaxis para construir tipos: Interfaces y Tipos. Deberías preferir interface. Utiliza type cuando necesites funciones específicas.
## Tipos de composición

Con TypeScript, puedes crear tipos complejos combinando tipos simples. Hay dos formas populares de hacerlo: con uniones y con genéricos.
### Uniones

Con una unión, puede declarar que un tipo puede ser uno de muchos tipos. Por ejemplo, puede describir un tipo booleano como verdadero o falso:

```ts
type MyBool = true | false;
```

> [!note] Nota
> Si pasas el ratón por encima de `MyBool`, verás que está clasificado como booleano. Es una propiedad del Sistema de Tipos Estructurales.

Un caso de uso popular para los tipos de unión es describir el conjunto de literales de cadena o numéricos que un valor puede ser:

```ts
type WindowStates = "open" | "closed" | "minimized";
type LockStates = "locked" | "unlocked";
type PositiveOddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
```

Las uniones también permiten manejar distintos tipos. Por ejemplo, puedes tener una función que tome un array o una cadena:

```ts
function getLength(obj: string | string[]) {
  return obj.length;
}
```

Para conocer el tipo de una variable, utilice `typeof`:

|   Tipo    |             Predicado              |
|:---------:|:----------------------------------:|
|  string   |      `typeof s === "string"`       |
|  number   |      `typeof n === "number"`       |
|  boolean  |      `typeof b === "boolean"`      |
| undefined | `typeof undefined === "undefined"` |
| function  |     `typeof f === "function"`      |
|   array   |         `Array.isArray(a)`         |

Por ejemplo, puede hacer que una función devuelva valores diferentes dependiendo de si se le pasa una cadena o una matriz:

```ts
function wrapInArray(obj: string | string[]) {
  if (typeof obj === "string") {
    return [obj];
  }
  return obj;
}
```
### Genéricos

Los genéricos proporcionan variables a los tipos. Un ejemplo común es un array. Un array sin genéricos puede contener cualquier cosa. Un array con genéricos puede describir los valores que contiene.

```ts
type StringArray = Array<string>;
type NumberArray = Array<number>;
type ObjectWithNameArray = Array<{ name: string }>;
```

Puedes declarar tus propios tipos que utilicen genéricos:

```ts error:15
interface Backpack<Type> {
  add: (obj: Type) => void;
  get: () => Type;
}
 
// This line is a shortcut to tell TypeScript there is a
// constant called `backpack`, and to not worry about where it came from.
declare const backpack: Backpack<string>;
 
// object is a string, because we declared it above as the variable part of Backpack.
const object = backpack.get();
 
// Since the backpack variable is a string, you can't pass a number to the add function.
backpack.add(23);
Argument of type 'number' is not assignable to parameter of type 'string'.
```
## Sistema de tipo estructural

Uno de los principios básicos de TypeScript es que la comprobación de tipos se centra en la forma que tienen los valores. Esto se llama a veces "tipado de pato" o "tipado estructural".  
  
En un sistema de tipos estructural, si dos objetos tienen la misma forma, se considera que son del mismo tipo.

```ts
interface Point {
  x: number;
  y: number;
}
 
function logPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}
 
// logs "12, 26"
const point = { x: 12, y: 26 };
logPoint(point);
```

La variable point nunca se declara como tipo Point. Sin embargo, TypeScript compara la forma de point con la forma de Point en la comprobación de tipo. Tienen la misma forma, por lo que el código pasa.  
  
La comprobación de la forma sólo requiere que coincida un subconjunto de los campos del objeto.

```ts error:9-10
const point3 = { x: 12, y: 26, z: 89 };
logPoint(point3); // logs "12, 26"
 
const rect = { x: 33, y: 3, width: 30, height: 80 };
logPoint(rect); // logs "33, 3"
 
const color = { hex: "#187ABF" };
logPoint(color);
Argument of type '{ hex: string; }' is not assignable to parameter of type 'Point'.
  Type '{ hex: string; }' is missing the following properties from type 'Point': x, y
```

No hay diferencia entre cómo las clases y los objetos se ajustan a las formas:

```ts
class VirtualPoint {
  x: number;
  y: number;
 
  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
}
 
const newVPoint = new VirtualPoint(13, 56);
logPoint(newVPoint); // logs "13, 56"
```

Si el objeto o clase tiene todas las propiedades requeridas, TypeScript dirá que coinciden, independientemente de los detalles de implementación.