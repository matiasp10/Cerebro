#palabra-reservada

La declaración **`const`** es muy similar a `let`:  

- Las declaraciones **`const`** se aplican tanto a bloques como a funciones.  
- Sólo se puede acceder a las declaraciones **`const`** una vez alcanzado el lugar de la declaración (véase zona muerta temporal). Por esta razón, las declaraciones **`const`** se consideran comúnmente como _no-hoisted_.  
- Las declaraciones **`const`** no crean propiedades en [[GlobalThis]] cuando se declaran en el nivel superior de un script.  
- Las declaraciones **`const`** no pueden ser redeclaradas por ninguna otra declaración en el mismo ámbito.  
- **`const`** comienza declaraciones, no sentencias. Esto significa que no puedes usar una única declaración **`const`** como cuerpo de un bloque (lo que tiene sentido, ya que no hay forma de acceder a la variable).

```js
if (true) const a = 1; // SyntaxError: Lexical declaration cannot appear in a single-statement context
```

Se _requiere un inicializador para una constante_. Debe especificar su valor en la misma declaración. (Esto tiene sentido, dado que no se puede cambiar más tarde).

```js
const FOO; // SyntaxError: Missing initializer in const declaration
```

La declaración **`const`** crea una referencia inmutable a un valor. _No significa que el valor que contiene sea inmutable_, sino que **el identificador de la variable no puede reasignarse**. Por ejemplo, en el caso de que el contenido sea un objeto, esto significa que el contenido del objeto (por ejemplo, sus propiedades) puede ser alterado. Debes entender las declaraciones **`const`** como "crear una variable cuya identidad permanece constante", no "cuyo valor permanece constante" - o, "crear enlaces inmutables", no "valores inmutables".  
  
Muchas guías de estilo (incluida la de MDN) recomiendan usar **`const`** en lugar de `let` _siempre que una variable no se reasigne en su ámbito_. Esto deja claro que el tipo de una variable (o valor, en el caso de una primitiva) nunca puede cambiar. Otros pueden preferir `let` para no primitivas que son mutadas.  
  
La lista que sigue a la palabra clave **`const`** se llama lista de enlaces y está separada por comas, donde las comas no son operadores de coma y los signos ` = ` no son operadores de asignación. Los inicializadores de variables posteriores pueden referirse a variables anteriores en la lista. 

```js
const a = 1, b = a + 1;
```

En este código, la variable `a` se inicializa con el valor `1`, y la variable `b` se inicializa con el valor de `a + 1`, que es `2`.

Es importante tener en cuenta que las comas en la lista de enlaces **no son operadores de coma**. Esto significa que no se puede realizar ninguna operación aritmética con las variables en la lista de enlaces.