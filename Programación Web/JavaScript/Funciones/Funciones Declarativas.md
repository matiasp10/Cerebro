Una función declarativa consta de la palabra clave _`function`_, seguida de:

- El _nombre_ de la función.
- Una _lista de parámetros de la función_, entre paréntesis y separados por comas.
- Las _declaraciones de JavaScript que definen la función_, encerradas entre llaves, `{ ... }`.

Por ejemplo, el siguiente código define una función simple llamada `square` ("cuadrado"):

```js
function square(number) {
  return number * number;
}
```

La función `square` toma un parámetro, llamado `number`. La función consta de una declaración que dice devuelva el parámetro de la función (es decir, `number`) multiplicado por sí mismo. La instrucción `return` especifica el valor devuelto por la función:

```js
return number * number;
```

Los _parámetros primitivos_ (como un `number`) se pasan a las funciones **por valor**; el valor se pasa a la función, pero si la función cambia el valor del parámetro, **este cambio no se refleja globalmente ni en la función que llama**.

Si pasas un _objeto_ (es decir, un valor no primitivo, como `Array` o un objeto definido por el usuario) como parámetro y la función cambia las propiedades del objeto, ese cambio es visible fuera de la función, como se muestra en el siguiente ejemplo:

```js
function myFunc(theObject) {
  theObject.make = 'Toyota';
}

var mycar = { make: 'Honda', model: 'Accord', year: 1998 };
var x, y;

x = mycar.make; // x obtiene el valor "Honda"

myFunc(mycar);
y = mycar.make; // y obtiene el valor "Toyota"
                // (la propiedad make fue cambiada por la función)
```
