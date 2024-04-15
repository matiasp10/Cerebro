Hoisting es uno de esos términos que todos los desarrolladores de JS han oído hablar porque buscaste en Google tu molesto error y terminaste en StackOverflow, donde esta persona te dijo que este error fue causado por hoisting.

>[!faq] Definición 
>JavaScript Hoisting se refiere al **proceso por el cual el intérprete parece mover la declaración de funciones, variables, clases o importaciones a la parte superior de su ámbito**, antes de la ejecución del código.

Si eres nuevo en JavaScript, puede que hayas experimentado un comportamiento "raro" en el que algunas variables están indefinidas aleatoriamente, se lanzan _ReferenceErrors_, etc. Hoisting se explica a menudo como poner las variables y funciones en la parte superior del archivo, eso no es lo que está pasando, aunque el comportamiento puede parecer que es así.

Cuando el motor JS recibe nuestro script, lo primero que hace es **configurar la memoria** para los datos de nuestro código. En este punto no se ejecuta ningún código, simplemente está preparando todo para la ejecución. La forma en que se almacenan las declaraciones de funciones y variables es diferente. Las funciones **se almacenan con una referencia a la función completa**.

![[hoisting1.gif]]
Con las **variables** es un poco diferente. ES6 introdujo dos nuevas palabras clave para declarar variables: `let` y `const`. Las variables declaradas con la palabra clave `let` o `const` **se almacenan sin inicializar**.

![[hoisting2.gif]]
Las variables declaradas con la palabra clave `var` se almacenan con el valor por defecto de `undefined`.

![[hoisting3.gif]]
Ahora que la fase de creación está hecha, podemos ejecutar el código. Veamos qué pasa si tuviéramos 3 sentencias `console.log` en la parte superior del archivo, antes de declarar la función o cualquiera de las variables. 

Como las funciones se almacenan con una referencia al código completo de la función, ¡podemos invocarlas incluso antes de la línea en la que las creamos!

![[hoisting4.gif]]
Cuando hacemos referencia a una variable declarada con la palabra clave `var` antes de su declaración, simplemente devolverá el valor por defecto con el que fue almacenada: ¡**`undefined`**! Sin embargo, esto a veces puede llevar a un comportamiento "inesperado". En la mayoría de los casos esto significa que la estás referenciando involuntariamente (probablemente no quieres que realmente tenga el valor de `undefined`)

![[hoisting5.gif]]
Para evitar poder referenciar accidentalmente una variable indefinida, como podríamos hacer con la palabra clave `var`, se lanza un `ReferenceError` cada vez que intentamos acceder a variables no inicializadas. La "zona" anterior a su declaración real se denomina [[Temporal dead zone (TDZ)]]: no se puede hacer referencia a las variables (¡esto incluye también a las clases ES6!) antes de su inicialización.

![[hoisting6.gif]]
Cuando el motor pasa por la línea en la que realmente declaramos las variables, los valores en memoria se sobrescriben con los valores con los que realmente las declaramos.

![[hoisting7.gif]]