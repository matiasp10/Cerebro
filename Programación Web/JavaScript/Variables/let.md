El ámbito de una variable declarada con `let` es una de las siguientes sintaxis encerradas entre llaves que más se aproxime a la declaración `let`:

- Sentencia de bloque  
- sentencia `switch`  
- sentencia `try...catch`  
- Cuerpo de una de las sentencias `for`, si el `let` está en la cabecera de la sentencia  
- Cuerpo de una función  
- Bloque de inicialización estático

O el módulo o script actual, si no está contenido en ninguno de ellos.  
  
Comparadas con `var`, las declaraciones `let` tienen las siguientes diferencias:

- Las declaraciones `let` se aplican tanto a bloques como a funciones.
- Sólo se puede acceder a las declaraciones `let` una vez alcanzado el lugar de la declaración (véase zona muerta temporal). Por esta razón, las declaraciones `let` se consideran comúnmente como no-hoisted.
- Las declaraciones `let` no crean propiedades en [[GlobalThis]] cuando se declaran en el nivel superior de un script.
- Las declaraciones `let` no pueden ser redeclaradas por ninguna otra declaración en el mismo ámbito.
- `let` inicia declaraciones, no sentencias. Esto significa que no puedes usar una única declaración let como cuerpo de un bloque (lo cual tiene sentido, ya que no hay forma de acceder a la variable).

```js
if (true) let a = 1; // SyntaxError: Lexical declaration cannot appear in a single-statement context
```

Tenga en cuenta que let está permitido como nombre de identificador cuando se declara con var o function en modo no estricto, pero debe evitar utilizar let como nombre de identificador para evitar ambigüedades sintácticas inesperadas.  
  
Muchas guías de estilo (incluida la de MDN) recomiendan usar const en lugar de let siempre que una variable no se reasigne en su ámbito. Esto deja claro que el tipo de una variable (o valor, en el caso de una primitiva) nunca puede cambiar. Otros pueden preferir let para no primitivas que son mutadas.  
  
La lista que sigue a la palabra clave let se denomina lista de vinculación y está separada por comas, donde las comas no son operadores de coma y los signos = no son operadores de asignación. Los inicializadores de variables posteriores pueden referirse a variables anteriores de la lista.

## Temporal dead zone (TDZ)

La [[Temporal dead zone (TDZ)|temporal dead zone (TDZ)]] de **JavaScript** es un área de un bloque de código donde una variable no es accesible hasta que la computadora la inicializa con un valor. La TDZ comienza al principio del bloque de código y termina cuando la variable se inicializa.

En otras palabras, si intentas acceder a una variable let o const antes de que se declare e inicialice, obtendrás un error.

```js
function foo() {
  let x;
  console.log(x); // Error: ReferenceError: x is not defined
}
```

Para evitar la TDZ, debes declarar e inicializar la variable antes de usarla. Por ejemplo, el siguiente código funciona correctamente:

```js
function foo() {
  let x = 1;
  console.log(x); // 1
}
```

La TDZ se introdujo en JavaScript para evitar errores causados por el acceso a variables no declaradas.

## Redeclaración

Las declaraciones let no pueden estar en el mismo ámbito que ninguna otra declaración, incluidas las declaraciones let, const, class, function, var e import.

```js
{
  let foo;
  let foo; // SyntaxError: Identifier 'foo' has already been declared
}
```
