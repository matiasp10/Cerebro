Una [variable](https://es.wikipedia.org/wiki/Variable_(programaci%C3%B3n)) es un “almacén con un nombre” para guardar datos. Podemos usar variables para almacenar golosinas, visitantes, y otros datos.

> [!attention] Definición 
> En programación, una variable está formada por un **espacio en el sistema de almacenaje** (memoria principal de un ordenador) y un **nombre simbólico** (un identificador) que está asociado a dicho espacio.

Para generar una variable se usan una de las siguientes palabras clave:

- #### **[[let]]**
- #### **[[const]]**
- #### **[[Programación Web/JavaScript/Variables/var|var]]**

## Declarar variables

JavaScript distingue entre mayúsculas y minúsculas (es **case-sensitive**) y utiliza el conjunto de caracteres **Unicode**. Por ejemplo, la palabra «Früh» (que significa "temprano" en Alemán) se podría usar como el nombre de una variable.

Pero, la variable `früh` no es la misma que `Früh` porque JavaScript distingue entre mayúsculas y minúsculas.

```js
let Früh = "foobar";
```

En JavaScript, las instrucciones se denominan [declaraciones](https://developer.mozilla.org/es/docs/Glossary/Statement) y están separadas por punto y coma (;).

No es necesario un punto y coma después de una declaración si está escrita en su propia línea. Pero si se deseas más de una declaración en una línea, entonces _debes_ separarlas con punto y coma.

>[!note] Nota
>ECMAScript también tiene reglas para la inserción automática del punto y coma —`IAPC`— (_ASI_ en inglés, por sus siglas «_Automatic Semicolon Insertion_») al final de las declaraciones. (Para obtener más información, consulta la referencia detallada sobre la `gramática léxica` de JavaScript).

Sin embargo, se considera una buena práctica escribir siempre un punto y coma después de una declaración, incluso cuando no sea estrictamente necesario. Esta práctica reduce las posibilidades de que se introduzcan errores en el código.

El texto fuente del script JavaScript se escanea de izquierda a derecha y se convierte en una secuencia de elementos de entrada que son _fragmentos_, _caracteres de control_, _terminadores de línea_, _comentarios_ o [espacios en blanco](https://developer.mozilla.org/es/docs/Glossary/Whitespace). (Los espacios, tabulaciones y caracteres de nueva línea se consideran espacios en blanco).
### Puedes declarar una variable de dos formas:

- Con la palabra clave `var`. Por ejemplo, `var x = 42`. Esta sintaxis se puede utilizar para declarar variables **locales** y **globales**, dependiendo del _contexto de ejecución_.
- Con la palabra clave `const` o `let`. Por ejemplo, `let y = 13`. Esta sintaxis se puede utilizar para declarar una variable local con ámbito de bloque.

También puedes simplemente asignar un valor a una variable. Por ejemplo, `x = 42`. Este formulario crea una variable `global no declarada`. También genera una advertencia estricta de JavaScript. Las variables globales no declaradas a menudo pueden provocar un comportamiento inesperado. Por lo tanto, se desaconseja utilizar variables globales no declaradas.

## Una analogía de la vida real

Podemos comprender fácilmente el concepto de una “**variable**” si nos la imaginamos como una “_caja_” con una etiqueta de nombre único pegada en ella.

Por ejemplo, podemos imaginar la variable `message` como una caja etiquetada `"message"` con el valor `"Hola!"` adentro:

![[variablesdef|center|260]]
Podemos introducir cualquier valor a la caja.

También la podemos cambiar cuantas veces queramos:

````js
let message;

message = 'Hola!';

message = 'Mundo!'; // valor alterado

alert(message);
````

Cuando el valor ha sido alterado, los datos antiguos serán removidos de la variable:

También podemos declarar dos variables y copiar datos de una a la otra.
````js
let hello = 'Hola mundo!';

let message;

// copia 'Hola mundo' de hello a message
message = hello;

// Ahora, ambas variables contienen los mismos datos
alert(hello); // Hola mundo!
alert(message); // Hola mundo!
````

>[!abstract] Declarar dos veces lanza un error
> 
> Una variable debe ser declarada solamente una vez.
> 
> Una declaración repetida de la misma variable es un error:
> ````js
> let message = "This";
> 
> // 'let' repetidos lleva a un error
> let message = "That"; // SyntaxError: 'message' ya fue declarado
> ````
> 
> Debemos declarar una variable una sola vez y desde entonces referirnos a ella sin `let`.

>[!hint] Lenguajes funcionales
> 
> Es interesante notar el hecho que lenguajes de programación [funcional](https://es.wikipedia.org/wiki/Programaci%C3%B3n_funcional), como [Scala](https://www.scala-lang.org/) o [Erlang](https://www.erlang.org/) prohíben cambiar el valor de las variables.
> 
> En tales lenguajes, una vez la variable ha sido almacenada “en la caja”, permanece allí por siempre. Si necesitamos almacenar algo más, el lenguaje nos obliga a crear una nueva caja (generar una nueva variable). No podemos reusar la antigua.
> 
> Aunque puede parecer un poco extraño a primera vista, estos lenguajes son muy capaces de desarrollo serio. Más aún, existen áreas como computación en paralelo en las cuales esta limitación otorga ciertos beneficios. Estudiar tales lenguajes (incluso sin la intención de usarlo en el futuro cercano) es recomendable para ampliar la mente.
## [[Nombramiento de variables]]
## [[Hoisting]]
