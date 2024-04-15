Los métodos de **transformación de objetos a _arrays_** sirven para obtener la información de las propiedades, sus valores o ambas.

## Obtener los pares de valor de un objeto en un _array_

`Object.entries()` devuelve un _array_ con las _entries_ en forma `[propiedad, valor]` del objeto enviado como argumento.

```js
const usuario = {
    name: "Andres",
    email: "andres@correo.com",
    age: 23
}

Object.entries(usuario) 
/* 
[
  [ 'name', 'Andres' ],
  [ 'email', 'andres@correo.com' ],
  [ 'age', 23 ]
]  
*/
```

## Obtener las propiedades de un objeto en un _array_

`Object.keys()` devuelve un _array_ con las propiedades _(keys)_ del objeto enviado como argumento.

```js
const usuario = {
    name: "Andres",
    email: "andres@correo.com",
    age: 23
}

Object.keys(usuario) 
// [ 'name', 'email', 'age' ]
```

## Obtener los valores de un objeto en un _array_

`Object.values()` devuelve un _array_ con los valores de cada propiedad del objeto enviado como argumento.

```js
const usuario = {
    name: 'Andres',
    email: "andres@correo.com",
    age: 23
}

Object.values(usuario) 
// [ 'Andres', 'andres@correo.com', 23 ]
```

## Rellenar un _string_ o _padding_

El _padding_ consiste en rellenar un `string` por el principio o por el final, con el carácter especificado, repetido hasta que complete la longitud máxima.

Este método recibe dos argumentos:

-   La longitud máxima a rellenar, incluyendo el `string` inicial.
-   El `string` para rellenar, por defecto, es un espacio.

Si la longitud a rellenar es menor que la longitud del `string` actual, entonces no agregará nada.

### Método _padStart_

El método `padStart` completa un `string` con otro `string` **en el inicio** hasta tener un total de caracteres especificado.

```js
'abc'.padStart(10) // "       abc"
'abc'.padStart(10, "foo") // "foofoofabc"
'abc'.padStart(6,"123465") // "123abc"
'abc'.padStart(8, "0") // "00000abc"
'abc'.padStart(1) // "abc"
```

### Método _padEnd_

El método `padEnd` completa un `string` con otro `string` **en el final** hasta tener un total de caracteres especificado.

```js
'abc'.padEnd(10) // "abc       "
'abc'.padEnd(10, "foo") // "abcfoofoof"
'abc'.padEnd(6, "123456") // "abc123"
'abc'.padEnd(1) // "abc"
```

## _Trailing commas_

Las _trailing commas_ consisten en comas al final de objetos o _arrays_ que faciliten añadir nuevos elementos y evitar errores de sintaxis.

```js
const usuario = {
    name: 'Andres',
    email: "andres@correo.com",
    age: 23, //<-- Trailing comma
}

const nombres = [
    "Andres",
    "Valeria",
    "Jhesly", //<-- Trailing comma
 ]
```

### Asincronismo

En ECMAScript 2017 o ES8 fue añadida una **nueva forma de manejar el asincronismo** en JavaScript mediante funciones asíncronas.

## Cómo utilizar funciones asíncronas

La función asíncrona se crea mediante la palabra reservada `async` y retorna una promesa.

```js
async function asyncFunction () {...}

const asyncFunction = async () => { ... } 
```

La palabra reservada `await` significa que **espera hasta que una promesa sea resuelta** y solo funciona dentro de una función asíncrona. Los bloques `try / catch` sirven para manejar si la promesa ha sido resuelta o rechazada.

```js
async function asyncFunction () {
  try {
    const response = await promesa()
    return response
  } catch (error) {
    return error
  }
}
```

¿Cuál es la mejor forma de manejar promesas, `then` o `async / await`? Ambas son muy útiles, manejar ambas te hará un mejor desarrollador.