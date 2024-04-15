El método global `structuredClone()` crea un **clon profundo** de un valor dado utilizando el _algoritmo de clon estructurado_.

El método también permite transferir [[Objetos transferibles]] en el valor original en lugar de clonarlos en el nuevo objeto. Los objetos transferidos se separan del objeto original y se adjuntan al nuevo objeto; ya no son accesibles en el objeto original.

# Sintaxis

```js
structuredClone(value)
structuredClone(value, options)
```

# Parámetros

## value
El objeto a clonar. Puede ser cualquier [[Algoritmo de clonado estructurado#Tipos soportados|Tipos soportados]].

## options `Optional`
Un objeto con las siguientes propiedades:

### transfer
Un Array de objetos transferibles que se moverán en lugar de clonarse al objeto devuelto.

# Valor devuelto
El valor devuelto es una copia en profundidad del valor original.

# Excepciones
## DataCloneError `DOMException`
Lanzada si alguna parte del valor de entrada no es serializable.

# Ejemplo

```js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = structuredClone(user);

alert( user.sizes === clone.sizes ); // false, objetos diferentes

// ahora user y clone están totalmente separados
user.sizes.width = 60;    // cambia una propiedad de un lugar
alert(clone.sizes.width); // 50, no están relacionados
```

También soporta referencias circulares, cuando una propiedad de objeto referencia el objeto mismo (directamente o por una cadena de referencias).

Por ejemplo:
```js
let user = {};
// hagamos una referencia circular
// user.me referencia user a sí mismo
user.me = user;

let clone = structuredClone(user);
alert(clone.me === clone); // true
```

Por ejemplo, cuando un objeto tienen una propiedad “function”:

```js
// error
structuredClone({
  f: function() {}
});
```

_Las propiedades de función no están soportadas._

