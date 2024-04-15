Existen dos limitaciones de nombre de variables en JavaScript:

1.  El nombre **únicamente puede incluir letras, dígitos, o los símbolos `$` y `_`**.
2.  El **primer carácter** _no puede ser un dígito_.

Ejemplos de nombres válidos:

````js
let userName;
let test123;
````

Cuando el nombre contiene varias palabras, comúnmente se utiliza **camelCase**. Es decir: palabras van una detrás de otra, con cada palabra iniciando con letra mayúscula: `miNombreMuyLargo`.

Es interesante notar que el símbolo del dólar `'$'` y el guion bajo `'_'` también se utilizan en nombres. Son símbolos comunes, tal como las letras, sin ningún significado especial.

Los siguientes nombres _son válidos_:

````js
let $ = 1; // Declara una variable con el nombre "$"
let _ = 2; // y ahora una variable con el nombre "_"

alert($ + _); // 3
````

Ejemplos de nombres **incorrectos**:

````js
let 1a; // no puede iniciar con un dígito

let my-name; // los guiones '-' no son permitidos en nombres
````

>[!check] La Capitalización es Importante
> 
> Dos variables con nombres `manzana` y `MANZANA` son variables distintas.

>[!check] Las letras que no son del alfabeto inglés están permitidas, pero no se recomiendan
> 
> Es posible utilizar letras de cualquier alfabeto, incluyendo letras del cirílico, logogramas chinos, etc.:
> 
> ````js
> let имя = '...';
> let 我 = '...';
> ````
> 
> Técnicamente, no existe ningún error aquí. Tales nombres están permitidos, pero existe una tradición internacional de utilizar inglés en el nombramiento de variables. Incluso si estamos escribiendo un script pequeño, este puede tener una larga vida por delante. Puede ser necesario que gente de otros países deba leerlo en algún momento.

>[!check] Nombres reservados
> 
> Hay una [lista de palabras reservadas](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords), las cuales no pueden ser utilizadas como nombre de variable porque el lenguaje en sí las utiliza.
> 
> Por ejemplo: `let`, `class`, `return`, y `function` están reservadas.
> 
> El siguiente código nos da un error de sintaxis:
> 
> ````js
> let let = 5; // no se puede le nombrar "let" a una variable  ¡Error!
> let return = 5; // tampoco se le puede nombrar "return", ¡Error!
> ````
> 

>[!check] Una asignación sin utilizar `use strict`
> 
> Normalmente, debemos definir una variable antes de utilizarla. Pero, en los viejos tiempos, era técnicamente posible crear una variable simplemente asignando un valor sin utilizar ‘let’. Esto aún funciona si no ponemos ‘use strict’ en nuestros scripts para mantener la compatibilidad con scripts antiguos.
> 
> ````js
> // nota: no se utiliza "use strict" en este ejemplo
> 
> num = 5; // se crea la variable "num" si no existe antes
> 
> alert(num); // 5
> ````
> 
> Esto es una mala práctica que causaría errores en ‘strict mode’:
> 
> ````js
> "use strict";
> 
> num = 5; // error: num no está definida
> ````

## Nombrar cosas correctamente

Estando en el tema de las variables, existe una cosa de mucha importancia.

Una variable debe tener un **nombre claro**, de **significado evidente**, que **describa el dato que almacena**.

Nombrar variables es una de las habilidades más importantes y complejas en la programación. Un vistazo rápido a el nombre de las variables nos revela cuál código fue escrito por un principiante o por un desarrollador experimentado.

En un proyecto real, la mayor parte de el tiempo se pasa modificando y extendiendo una base de código en vez de empezar a escribir algo desde cero. Cuando regresamos a algún código después de hacer algo distinto por un rato, _es mucho más fácil encontrar información que está bien etiquetada_. O, en otras palabras, cuando las variables tienen nombres adecuados.

Por favor pasa tiempo pensando en el nombre adecuado para una variable antes de declararla. Hacer esto te da un retorno muy sustancial.

Algunas reglas buenas para seguir:

- Use **términos legibles** para humanos como `userName` p `shoppingCart`.
- **Evite abreviaciones o nombres cortos** `a`, `b`, `c`, al menos que en serio sepa lo que está haciendo.
- Cree **nombres que describen al máximo lo que son y sean concisos**. Ejemplos que no son adecuados son `data` y `value`. Estos nombres no nos dicen nada. Estos solo está bien usarlos en el contexto de un código que deje excepcionalmente obvio cuál valor o cuales datos está referenciando la variable.
- **Acuerda en tu propia mente y con tu equipo cuáles términos se utilizarán**. Si a un visitante se le llamara “user”, debemos llamar las variables relacionadas `currentUser` o `newUser` en vez de `currentVisitor` o `newManInTown`.

¿Suena simple? De hecho lo es, pero no es tan fácil crear nombres de variables descriptivos y concisos a la hora de practicar.

>[!warning] ¿Reusar o crear?
> 
> Una última nota. Existen programadores haraganes que, en vez de declarar una variable nueva, **tienden a reusar las existentes**.
> 
> El resultado de esto es que sus variables son como cajas en las cuales la gente introduce cosas distintas sin cambiar sus etiquetas. ¿Que existe dentro de la caja? ¿Quién sabe? Necesitamos acercarnos y revisar.
> 
> Dichos programadores se ahorran un poco durante la declaración de la variable, pero pierden diez veces más a la hora de depuración.
> 
> Una variable extra es algo bueno, no algo malvado.
> 
> Los minificadores de JavaScript moderno, y los navegadores optimizan el código suficientemente bien para no generar cuestiones de rendimiento. Utilizar diferentes variables para distintos valores incluso puede ayudar a optimizar su código