En términos generales, una función es un "subprograma" que puede ser llamado por código externo (o interno, en el caso de la recursividad) a la función. Al igual que el propio programa, una función se compone de una secuencia de sentencias denominada cuerpo de la función. A una función se le pueden pasar valores como parámetros, y la función devolverá un valor.

En JavaScript, las funciones son objetos de primera clase, porque pueden ser pasadas a otras funciones, devueltas desde funciones y asignadas a variables y propiedades. También pueden tener propiedades y métodos como cualquier otro objeto. Lo que las distingue de otros objetos es que las funciones pueden ser llamadas.

# Function

[[Function]]

# Descripción

Los valores de Function son típicamente instancias de Function. Consulte Function para obtener información sobre las propiedades y métodos de los objetos Function. Los valores invocables hacen que typeof devuelva "función" en lugar de "objeto".

> [!note] Nota
> No todos los valores invocables son instanceof Function. Por ejemplo, el objeto Function.prototype es invocable pero no es una instancia de Function. También puede establecer manualmente la cadena de prototipos de su función para que ya no herede de Function.prototype. Sin embargo, estos casos son extremadamente raros.

## Valor de return

Por defecto, si la ejecución de una función no termina en una sentencia return, o si la palabra clave return no tiene una expresión después de ella, entonces el valor de retorno es _`undefined`_. La sentencia return permite devolver un valor arbitrario de la función. Una llamada a una función _sólo puede devolver un valor_, pero puede simular el efecto de devolver varios valores devolviendo un objeto o matriz y desestructurando el resultado.

> [!note] Nota
> Los constructores llamados con new tienen una lógica diferente para determinar sus valores de retorno.

## Parámetros y argumentos

```js
function formatNumber(num) {
  return num.toFixed(2);
}

formatNumber(2);
```

En este ejemplo, la variable `num` se denomina **parámetro** de la función: se declara en la lista _entre paréntesis de la definición de la función_. La función espera que el parámetro `num` sea un número, aunque esto no es exigible en JavaScript sin escribir código de validación en tiempo de ejecución. En la llamada a `formatNumber(2)`, el número _2_ es el **argumento** de la función: es _el valor que se pasa realmente a la función en la llamada a la función_. Se puede acceder al valor del argumento dentro del cuerpo de la función a través del _nombre del parámetro_ correspondiente o del _objeto arguments_.

Los argumentos siempre se pasan por valor y nunca por referencia. Esto significa que si una función reasigna un parámetro, el valor no cambiará fuera de la función. Más concretamente, los argumentos de los objetos se pasan por compartición, lo que significa que si las propiedades del objeto mutan, el cambio afectará al exterior de la función. Por ejemplo:

```js
function updateBrand(obj) {
  // Mutating the object is visible outside the function
  obj.brand = "Toyota";
  // Try to reassign the parameter, but this won't affect
  // the variable's value outside the function
  obj = null;
}

const car = {
  brand: "Honda",
  model: "Accord",
  year: 1998,
};

console.log(car.brand); // Honda

// Pass object reference to the function
updateBrand(car);

// updateBrand mutates car
console.log(car.brand); // Toyota
```

La palabra clave `this` se refiere al objeto sobre el que se accede a la función - no se refiere a la función actualmente en ejecución, por lo que debe referirse al valor de la función por su nombre, incluso dentro del cuerpo de la función.

## Definición de función

En términos generales, JavaScript tiene cuatro _tipos de funciones_:

- **Función regular**: puede devolver cualquier cosa; siempre se ejecuta hasta su finalización tras la invocación.
- **Función Generator**: devuelve un objeto Generator; se puede pausar y reanudar con el operador yield.
- **Función asíncrona**: devuelve un Promise; puede pausarse y reanudarse con el operador await.
- **Función generadora asíncrona**: devuelve un objeto AsyncGenerator; se pueden utilizar los operadores await y yield.

Para cada tipo de función, hay tres maneras de _definirla_:

- **Declaracion**:
	- function
	- function*
	- async function
	- async function*
- **Expresion**:
	- function
	- function*
	- async function
	- async function*
- **Constructor**:
	- Function()
	- GeneratorFunction()
	- AsyncFunction()
	- AsyncGeneratorFunction()

Además, existen sintaxis especiales para definir funciones y métodos de flecha, que proporcionan una semántica más precisa para su uso. Las clases conceptualmente no son funciones (porque lanzan un error cuando se llaman sin new), pero también heredan de `Function.prototype` y tienen `typeof MyClass === "function"`.

```js
// Constructor
const multiply = new Function("x", "y", "return x * y");

// Declaration
function multiply(x, y) {
  return x * y;
} // No need for semicolon here

// Expression; the function is anonymous but assigned to a variable
const multiply = function (x, y) {
  return x * y;
};
// Expression; the function has its own name
const multiply = function funcName(x, y) {
  return x * y;
};

// Arrow function
const multiply = (x, y) => x * y;

// Method
const obj = {
  multiply(x, y) {
    return x * y;
  },
};
```

Todas las sintaxis hacen aproximadamente lo mismo, pero existen algunas sutiles diferencias de comportamiento.

- El constructor Function(), la expresión de función y las sintaxis de declaración de función crean objetos de función completos, que pueden construirse con new. Sin embargo, las funciones de flecha y los métodos no pueden construirse. Las funciones asíncronas, las funciones generadoras y las funciones generadoras asíncronas no se pueden construir independientemente de la sintaxis.
- La _declaración de función crea funciones que son elevadas_. Otras sintaxis no elevan la función y el valor de la función sólo es visible después de la definición.
- La _función flecha_ y el _constructor Function()_ siempre crean **funciones anónimas**, lo que significa que no pueden llamarse a sí mismas recursivamente con facilidad. Una forma de llamar a una función flecha recursivamente es asignándola a una variable.
- La sintaxis de la función flecha _no tiene acceso a argumentos o a `this`_.
- El _constructor Function()_ no puede acceder a ninguna variable local - _sólo tiene acceso al ámbito global_.
- El _constructor Function() causa compilación en tiempo de ejecución_ y suele ser más lento que otras sintaxis.

En las expresiones de función, existe una distinción entre el nombre de la función y la variable a la que se asigna la función. El nombre de la función no puede modificarse, mientras que la variable a la que se asigna la función puede reasignarse. El nombre de la función puede ser diferente de la variable a la que se asigna la función, no tienen ninguna relación entre sí. El nombre de la función sólo puede utilizarse dentro del cuerpo de la función. Si se intenta utilizar fuera del cuerpo de la función, se produce un error (o se obtiene otro valor, si se declara el mismo nombre en otro lugar). Por ejemplo:

```js
const y = function x() {};
console.log(x); // ReferenceError: x is not defined
```

Por otra parte, la variable a la que se asigna la función sólo está limitada por su ámbito, que está garantizado que incluye el ámbito en el que se declara la función.

Una declaración de función también crea una variable con el mismo nombre que el de la función. Así, a diferencia de las definidas mediante expresiones de función, a las funciones definidas mediante declaraciones de función se puede acceder por su nombre en el ámbito en el que se definieron, así como en su propio cuerpo.

Una función definida por new Function tendrá dinámicamente su fuente ensamblada, lo que es observable cuando la serializas. Por ejemplo, console.log(new Function().toString()) da:

```js
function anonymous(
) {

}
```

Esta es la fuente real utilizada para compilar la función. Sin embargo, aunque el constructor Function() creará la función con nombre anonymous, este nombre no se añade al ámbito del cuerpo. El cuerpo sólo tiene acceso a las variables globales. Por ejemplo, lo siguiente produciría un error:

```js
new Function("alert(anonymous);")();
```

Una función definida por una expresión de función o por una declaración de función hereda el ámbito actual. Es decir, la función forma un cierre. En cambio, una función definida por un constructor de función no hereda ningún ámbito distinto del ámbito global (que heredan todas las funciones).

```js
// p is a global variable
globalThis.p = 5;
function myFunc() {
  // p is a local variable
  const p = 9;

  function decl() {
    console.log(p);
  }
  const expr = function () {
    console.log(p);
  };
  const cons = new Function("\tconsole.log(p);");

  decl();
  expr();
  cons();
}
myFunc();

// Logs:
// 9 (for 'decl' by function declaration (current scope))
// 9 (for 'expr' by function expression (current scope))
// 5 (for 'cons' by Function constructor (global scope))
```

Las funciones definidas por expresiones de función y declaraciones de función sólo se analizan una vez, mientras que una función definida por el constructor Function analiza la cadena que se le pasa cada vez que se llama al constructor. Aunque una expresión de función crea un cierre cada vez, el cuerpo de la función no se vuelve a analizar, por lo que las expresiones de función siguen siendo más rápidas que new Function(...). Por lo tanto, el constructor Function debe evitarse siempre que sea posible.

Una declaración de función puede convertirse involuntariamente en una expresión de función cuando aparece en un contexto de expresión.

```js
// A function declaration
function foo() {
  console.log("FOO!");
}

doSomething(
  // A function expression passed as an argument
  function foo() {
    console.log("FOO!");
  },
);
```

Por otro lado, una expresión de función también puede convertirse en una declaración de función. Una declaración de expresión no puede comenzar con las palabras clave function o async function, lo cual es un error común al implementar IIFEs (Expresiones de Función Inmediatamente Invocadas).

> [!missing] Error
> ```js
> function () { // SyntaxError: Function statements require a function name
> 	console.log("FOO!");
> }();
> 
> function foo() {
>   console.log("FOO!");
> }(); // SyntaxError: Unexpected token ')'
>   ```

En su lugar, comience la expresión con otra cosa, de modo que la palabra clave function inicie inequívocamente una expresión de función. Algunas opciones comunes son la agrupación y el uso de void.

> [!success] 
> ```js
> (function () {
>   console.log("FOO!");
> })();
> 
> void function () {
>   console.log("FOO!");
> }();
> ```

## Parámetros de función

Cada parámetro de función es un simple identificador al que se puede acceder en el ámbito local.

```js
function myFunc(a, b, c) {
  // You can access the values of a, b, and c here
}
```

Existen tres sintaxis de parámetros especiales:

- Los _parámetros por defecto_ permiten inicializar los parámetros formales con valores por defecto si no se pasa ningún valor o undefined.
- El _parámetro `rest`_ permite representar un número indefinido de argumentos como una matriz.
- La _desestructuración_ permite desempaquetar elementos de matrices, o propiedades de objetos, en variables distintas.

```js
function myFunc({ a, b }, c = 1, ...rest) {
  // You can access the values of a, b, c, and rest here
}
```

Existen algunas **consecuencias** si se utiliza una de las sintaxis de parámetros especiales:

- No se puede aplicar _"`use strict`"_ al cuerpo de la función - esto causa un error de sintaxis.
- Incluso si la función no está en modo estricto, _el objeto `arguments` deja de sincronizarse con los parámetros nombrados_, y `arguments.callee` lanza un error cuando se accede a él.

## El objeto arguments

Puede hacer referencia a los argumentos de una función dentro de la función utilizando el objeto arguments.

- _`arguments`_: Un objeto tipo array que contiene los argumentos pasados a la función que se está ejecutando en ese momento.
- _`arguments.callee`_: La función que se está ejecutando actualmente.
- _`arguments.length`_: El número de argumentos pasados a la función.

## Funciones getters y setters

Puede definir propiedades accesorias en cualquier objeto incorporado estándar u objeto definido por el usuario que admita la adición de nuevas propiedades. Dentro de los literales de objeto y las clases, puedes utilizar sintaxis especiales para definir el `getter` y el `setter` de una propiedad accesoria.

- _`get`_: Vincula una propiedad de un objeto a una función que será llamada cuando se busque esa propiedad.
- _`set`_: Vincula una propiedad de un objeto a una función que se llamará cuando se intente establecer dicha propiedad.

Tenga en cuenta que estas sintaxis crean una propiedad de objeto, no un método. Sólo se puede acceder a las funciones getter y setter utilizando APIs reflexivas como `Object.getOwnPropertyDescriptor()`.

## Funciones a nivel de bloque

En modo estricto, las funciones dentro de los bloques se limitan a ese bloque. Antes de ES2015, las funciones a nivel de bloque estaban prohibidas en modo estricto.

```js
"use strict";

function f() {
  return 1;
}

{
  function f() {
    return 2;
  }
}

f() === 1; // true

// f() === 2 in non-strict mode
```

## Funciones a nivel de bloque en código no estricto

> [!warning] No hacer esto

En código no estricto, las declaraciones de función dentro de bloques se comportan de forma extraña. Por ejemplo:

```js
if (shouldDefineZero) {
  function zero() {
    // DANGER: compatibility risk
    console.log("This is zero.");
  }
}
```

La semántica de esto en modo estricto está bien especificada - cero sólo existe dentro del ámbito del bloque if. Si `shouldDefineZero` es false, entonces cero nunca debe ser definido, ya que el bloque nunca se ejecuta. Sin embargo, históricamente, esto se dejaba sin especificar, por lo que los distintos navegadores lo implementaban de forma diferente en modo no estricto. Para más información, consulte la referencia de declaración de funciones.

Una forma más segura de definir funciones condicionalmente es asignar una expresión de función a una variable:

```js
// Using a var makes it available as a global variable,
// with closer behavior to a top-level function declaration
var zero;
if (shouldDefineZero) {
  zero = function () {
    console.log("This is zero.");
  };
}
```

# Tipos de funciones

- [[IIFE (Immediately Invoked Function Expression)]]
- [[Funciones Declarativas]]
- [[Expresión de función]]