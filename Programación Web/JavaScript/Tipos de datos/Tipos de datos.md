Cada vez que tengas un valor, caerá en 1 de los tipos de datos en JavaScript. Podemos almacenar un valor de cualquier tipo dentro de una variable.

Los lenguajes de programación que permiten estas cosas, como JavaScript, se denominan “[[Lenguajes dinamicamente tipados|dinamicamente tipados]]”, lo que significa que allí hay tipos de datos, pero las variables no están vinculadas rígidamente a ninguno de ellos.

- [[Primitivos]]
- [[Objetos]]

## Operador typeof

El operador `typeof` devuelve el tipo de dato del operando. Es útil cuando queremos procesar valores de diferentes tipos de forma diferente o simplemente queremos hacer una comprobación rápida.

La llamada a `typeof x` devuelve una cadena con el nombre del tipo:

```js
typeof undefined // "undefined"

typeof 0 // "number"

typeof 10n // "bigint"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"

typeof Math // "object"  (1)

typeof null // "object"  (2)

typeof alert // "function"  (3)
```

1. **Math** es un objeto incorporado que proporciona operaciones matemáticas.
2. El resultado de typeof null es "object". Esto está oficialmente reconocido como un _error de comportamiento de typeof_ que proviene de los primeros días de JavaScript y se mantiene por compatibilidad. Definitivamente null no es un objeto. Es un valor especial con un tipo propio separado.
3. El resultado de typeof alert es "**function**" porque alert es una función. Las funciones pertenecen al tipo objeto. Pero typeof las trata de manera diferente, devolviendo _function_. Además proviene de los primeros días de JavaScript. Técnicamente dicho comportamiento es incorrecto, pero puede ser conveniente en la práctica.

> [!info]- Sintaxis de typeof(x)
> Se puede encontrar otra sintaxis en algún código: **typeof(x)**. Es lo mismo que **typeof x**.
> 
> Para ponerlo en claro: typeof es un _operador_, no una función. Los paréntesis aquí no son parte del operador typeof. Son del tipo usado en agrupamiento matemático.
> 
> Usualmente, tales paréntesis contienen expresiones matemáticas tales como (2 + 2), pero aquí solo tienen un argumento (x). Sintácticamente, permiten evitar el espacio entre el operador typeof y su argumento, y a algunas personas les gusta así. 
> 
> Algunos prefieren typeof(x), aunque la sintaxis typeof x es mucho más común. 