
```js
"key" in object
```

Por ejemplo:

```js
let user = { name: "John", age: 30 };

alert( "age" in user );    // mostrará "true", porque user.age sí existe
alert( "blabla" in user ); // mostrará false, porque user.blabla no existe
```

Nota que a la izquierda de in debe estar el nombre de la propiedad que suele ser un `string` entre comillas.

Si omitimos las comillas, significa que es una variable. Esta variable debe almacenar la clave real que será probada. Por ejemplo:

```js
let user = { age: 30 };

let key = "age";
alert( key in user ); // true, porque su propiedad "age" sí existe dentro del objeto
```

Pero… ¿Por qué existe el operador in? ¿No es suficiente comparar con `undefined`?

La mayoría de las veces las comparaciones con `undefined` funcionan bien. Pero hay un caso especial donde esto falla y aún así "_in_" funciona correctamente.

Es cuando existe una propiedad de objeto, pero almacena `undefined`:

```js
let obj = {
  test: undefined
};

alert( obj.test ); // es undefined, entonces... ¿Quiere decir realmente existe tal propiedad?

alert( "test" in obj ); //es true, ¡La propiedad sí existe!
```

En el código anterior, la propiedad `obj.test` técnicamente existe. Entonces el operador _in_ funciona correctamente.

Situaciones como esta suceden raramente ya que `undefined` no debe ser explícitamente asignado. Comúnmente usamos `null` para valores “desconocidos” o “vacíos”. Por lo que el operador in es un invitado exótico en nuestro código.

## Para recorrer el objeto

[[for...in]]