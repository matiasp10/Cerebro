## ¿Qué es JavaScript? Breve historia

**JavaScript** (también conocido como ECMAScript) nació como un sencillo lenguaje de programación para navegadores. En el momento de su invención, se esperaba que se utilizara para pequeños fragmentos de código incrustados en una página web: escribir más de unas pocas docenas de líneas de código habría sido algo inusual. Por eso, los primeros navegadores ejecutaban este tipo de código con bastante lentitud. Con el tiempo, sin embargo, JS se hizo cada vez más popular y los desarrolladores web empezaron a utilizarlo para crear experiencias interactivas.  
  
Los desarrolladores de navegadores respondieron a este mayor uso de JS optimizando sus motores de ejecución (compilación dinámica) y ampliando lo que se podía hacer con él (añadiendo API), lo que a su vez hizo que los desarrolladores web lo utilizaran aún más. En los sitios web modernos, el navegador ejecuta con frecuencia aplicaciones que abarcan cientos de miles de líneas de código. Este es el largo y gradual crecimiento de "la web", que empezó como una simple red de páginas estáticas y evolucionó hasta convertirse en una plataforma para aplicaciones ricas de todo tipo.  
  
Además, JS se ha hecho lo suficientemente popular como para utilizarse fuera del contexto de los navegadores, por ejemplo implementando servidores JS mediante node.js. La naturaleza "ejecutable en cualquier lugar" de JS lo convierte en una opción atractiva para el desarrollo multiplataforma. Hoy en día hay muchos desarrolladores que sólo utilizan JavaScript para programar toda su pila.  
  
En resumen, tenemos un lenguaje que se diseñó para usos rápidos, y luego creció hasta convertirse en una herramienta completa para escribir aplicaciones con millones de líneas. Cada lenguaje tiene sus peculiaridades - rarezas y sorpresas, y el humilde comienzo de JavaScript hace que tenga muchas de ellas. Algunos ejemplos:

- El operador de igualdad de JavaScript (` == `) fuerza a sus operandos, lo que provoca un comportamiento inesperado:

```js
if ("" == 0) {
  // It is! But why??
}
if (1 < x < 3) {
  // True for *any* value of x!
}
```

- JavaScript también permite acceder a propiedades que no están presentes:

```js
const obj = { width: 10, height: 15 };
// Why is this NaN? Spelling is hard!
const area = obj.width * obj.heigth;
```

La mayoría de los lenguajes de programación lanzan un error cuando se producen este tipo de errores, algunos lo hacen durante la compilación, antes de que se ejecute ningún código. Cuando se escriben programas pequeños, estas peculiaridades son molestas pero manejables; cuando se escriben aplicaciones con cientos o miles de líneas de código, estas sorpresas constantes son un grave problema.
## TypeScript: Un comprobador estático de tipos

Antes dijimos que algunos lenguajes no permitirían que esos programas con errores se ejecutaran en absoluto. Detectar errores en el código sin ejecutarlo se conoce como comprobación estática. Determinar qué es un error y qué no lo es basándose en los tipos de valores sobre los que se opera se conoce como comprobación estática de tipos.  

TypeScript comprueba si hay errores en un programa antes de ejecutarlo, y lo hace basándose en los tipos de valores, lo que lo convierte en un comprobador de tipos estático. Por ejemplo, el último ejemplo anterior tiene un error debido al tipo de obj. Aquí está el error que TypeScript encontró:

```ts error:3
const obj = { width: 10, height: 15 };
const area = obj.width * obj.heigth;
// Property 'heigth' does not exist on type '{ width: number; height: number; }'. Did you mean 'height'?
```

### Un superconjunto tipado de JavaScript

Pero, ¿Cómo se relaciona TypeScript con JavaScript?
#### Sintaxis

TypeScript es un lenguaje que es un superconjunto de JavaScript: Por lo tanto, la sintaxis de JS es TS legal. La sintaxis se refiere a la forma en que escribimos el texto para formar un programa. Por ejemplo, este código tiene un error de sintaxis porque le falta un ):

```ts error:2
let a = (4
// ')' expected.
```

TypeScript no considera ningún código JavaScript como un error debido a su sintaxis. Esto significa que puedes tomar cualquier código JavaScript que funcione y ponerlo en un archivo TypeScript sin preocuparte de cómo está escrito exactamente.
#### Tipos

Sin embargo, TypeScript es un superconjunto tipado, lo que significa que añade reglas sobre cómo se pueden usar los diferentes tipos de valores. El error anterior sobre obj.heigth no era un error de sintaxis: es un error de uso de algún tipo de valor (un tipo) de forma incorrecta.  
  
Como otro ejemplo, esto es código JavaScript que puedes ejecutar en tu navegador, y registrará un valor:

```ts
console.log(4 / []);
```

Este programa sintácticamente legal registra Infinity. TypeScript, sin embargo, considera la división de un número por un array como una operación sin sentido, y emitirá un error:

```ts error:2
console.log(4 / []);
// The right-hand side of an arithmetic operation must be of type 'any', 'number', 'bigint' or an enum type.
```

Es posible que realmente tuvieras la intención de dividir un número por un array, tal vez sólo para ver qué pasa, pero la mayoría de las veces, sin embargo, se trata de un error de programación. El comprobador de tipos de TypeScript está diseñado para permitir que los programas correctos pasen mientras se detectan tantos errores comunes como sea posible. (Más adelante, aprenderemos sobre los ajustes que puedes utilizar para configurar el grado de rigor con el que TypeScript comprueba tu código).  
  
Si mueves algún código de un archivo JavaScript a un archivo TypeScript, puede que veas errores de tipo dependiendo de cómo esté escrito el código. Estos pueden ser problemas legítimos con el código, o TypeScript siendo demasiado conservador. A lo largo de esta guía demostraremos cómo añadir varias sintaxis de TypeScript para eliminar tales errores.

#### Comportamiento en tiempo de ejecución

TypeScript es también un lenguaje de programación que conserva el comportamiento en tiempo de ejecución de JavaScript. Por ejemplo, dividir por cero en JavaScript produce Infinito en lugar de lanzar una excepción en tiempo de ejecución. Como principio, TypeScript nunca cambia el comportamiento en tiempo de ejecución del código JavaScript.  
  
Esto significa que si pasas código de JavaScript a TypeScript, está garantizado que se ejecute de la misma manera, incluso si TypeScript piensa que el código tiene errores de tipo.  
  
Mantener el mismo comportamiento en tiempo de ejecución que JavaScript es una promesa fundamental de TypeScript porque significa que puedes hacer fácilmente la transición entre los dos lenguajes sin preocuparte de sutiles diferencias que podrían hacer que tu programa dejara de funcionar.
#### Tipos borrados

A grandes rasgos, una vez que el compilador de TypeScript ha terminado de comprobar tu código, borra los tipos para producir el código "compilado" resultante. Esto significa que una vez que tu código es compilado, el código JS plano resultante no tiene información de tipos.  
  
Esto también significa que TypeScript nunca cambia el comportamiento de tu programa basándose en los tipos inferidos. La conclusión es que, aunque puede que veas errores de tipo durante la compilación, el sistema de tipos en sí mismo no influye en cómo funciona tu programa cuando se ejecuta.  
  
Por último, TypeScript no proporciona ninguna biblioteca adicional en tiempo de ejecución. Tus programas usarán la misma biblioteca estándar (o bibliotecas externas) que los programas JavaScript, así que no hay que aprender ningún marco de trabajo adicional específico de TypeScript.