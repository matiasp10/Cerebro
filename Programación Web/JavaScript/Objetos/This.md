Es común que un método de objeto necesite acceder a la información almacenada en el objeto para cumplir su tarea.

Por ejemplo, el código dentro de `user.sayHi()` puede necesitar el nombre del usuario `user`.

**Para acceder al objeto, un método puede usar la palabra clave `this`.**

El valor de `this` es el objeto “_antes del punto_”, el usado para llamar al método.

Por ejemplo:
```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // "this" es el "objeto actual"
    alert(this.name);
  }

};

user.sayHi(); // John
```

Aquí durante la ejecución de `user.sayHi()`, el valor de `this` será `user`.

Técnicamente, también es posible acceder al objeto sin `this`, haciendo referencia a él por medio de la variable externa:

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(user.name); // "user" en vez de "this"
  }

};
```

…Pero tal código no es confiable. Si decidimos copiar `user` a otra variable, por ejemplo `admin = user` y sobrescribir `user` con otra cosa, entonces accederá al objeto incorrecto.

Eso queda demostrado en las siguientes líneas:
```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert( user.name ); // lleva a un error
  }

};

let admin = user;
user = null; // sobrescribimos para hacer las cosas evidentes

admin.sayHi(); // TypeError: No se puede leer la propiedad 'name' de null
```

Si usamos `this.name` en vez de `user.name` dentro de `alert`, entonces el código funciona.

# "This" no es vinculado

En JavaScript, la palabra clave `this` se comporta de manera distinta a la mayoría de otros lenguajes de programación. Puede ser usado en cualquier función, incluso si no es el método de un objeto.

No hay error de sintaxis en el siguiente ejemplo:

```js
function sayHi() {
  alert( this.name );
}
```

El valor de `this` es _evaluado durante el tiempo de ejecución_, dependiendo del contexto.

Por ejemplo, aquí la función es asignada a dos objetos diferentes y tiene diferentes “this” en sus llamados:

```js
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// usa la misma función en dos objetos
user.f = sayHi;
admin.f = sayHi;

// estos llamados tienen diferente "this"
// "this" dentro de la función es el objeto "antes del punto"
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (punto o corchetes para acceder al método, no importa)
```

La regla es simple: si `obj.f()` es llamado, entonces `this` es `obj` durante el llamado de `f`. Entonces es tanto `user` o `admin` en el ejemplo anterior.

> [!hint] Llamado sin un objeto: `this == undefined`
> Podemos incluso llamar la función sin un objeto en absoluto:
> ```js
> function sayHi() {
>   alert(this);
> }
>   
> sayHi(); // undefined
> ```
> En este caso `this` es `undefined` en el modo estricto. Si tratamos de acceder a `this.name`, habrá un error.
> 
> En modo no estricto el valor de `this` en tal caso será el [[Global object]]. Este es un comportamiento histórico que `"use strict"` corrige.
> 
> Usualmente tal llamado es un error de programa. Si hay `this` dentro de una función, se espera que sea llamada en un _contexto de objeto_.

> [!warning] Las consecuencias de un `this` desvinculado
> Si vienes de otro lenguaje de programación, probablemente estés habituado a la idea de un "_`this` vinculado_", donde los método definidos en un objeto siempre tienen `this` referenciando ese objeto.
> 
> En JavaScript `this` es “_libre_”, su valor es evaluado al momento de su llamado y no depende de dónde fue declarado el método sino de cuál es el objeto “_delante del punto_”.
> 
> El concepto de `this` evaluado en tiempo de ejecución tiene sus pros y sus contras. Por un lado, una función puede ser reusada por diferentes objetos. Por otro, la mayor flexibilidad crea más posibilidades para equivocaciones.

# Las funciones flecha no tienen `this`

Las funciones de flecha son especiales: ellas no tienen su “propio” `this`. Si nosotros hacemos referencia a `this` desde tales funciones, esta será tomada desde afuera de la función “_normal_”.

Por ejemplo, aquí `arrow()` usa `this` desde fuera del método `user.sayHi()`:

```js
let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // Ilya
```

Esto es una característica especial de las funciones de flecha, útil cuando no queremos realmente un `this` separado sino tomarlo de un contexto externo.

Saber mas de las: [[Funciones flecha]]