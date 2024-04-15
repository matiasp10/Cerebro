El método `Object.assign()` copia **todas las propiedades enumerables de uno o más objetos fuente a un objeto destino**. Devuelve el objeto destino.

Las propiedades en el _objeto destino serán sobrescritas por las propiedades en las fuentes si tienen la misma clave_. Propiedades posteriores de las fuentes podrán sobrescribir las anteriores.

El método `Object.assign()` copia sólo las _propiedades enumerables_ y _propias del objeto origen_ a un objeto destino. Usa `[[Get]]` en el origen y `[[Set]]` en el destino, por lo que invocará los métodos de acceso y establecimiento (getters y setters). Por consiguiente asignará propiedades frente a sólo copiar o definir propiedades nuevas. Esto puede hacer que sea inadecuado para fusionar propiedades nuevas en un prototipo si los objetos fuente contienen métodos de acceso (getters). 

Para copiar definiciones de propiedades en prototipos, incluyendo su enumerabilidad, se deben usar `Object.getOwnPropertyDescriptor()` y `Object.defineProperty()`.

Tanto las propiedades **String** como **Symbol** son copiadas.

En caso de un error, por ejemplo si una propiedad es de solo lectura, se lanza un **TypeError**, y el objeto destino se mantendrá sin cambios.

Note que `Object.assign()` **no lanza excepciones** al encontrar en las fuentes propiedades _null_ o _undefined_.

# Sintaxis 

```js
Object.assign(objetivo, ...fuentes)
```

# Parámetros

## objetivo
El objeto destino.

## fuentes
Los objetos origen.

# Valor devuelto
El objeto destino.

# Ejemplos

Por ejemplo, tenemos el objeto user, agreguemos un par de permisos:

```js
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// copia todas las propiedades desde permissions1 y permissions2 en user
Object.assign(user, permissions1, permissions2);

// ahora es user = { name: "John", canView: true, canEdit: true }
alert(user.name); // John
alert(user.canView); // true
alert(user.canEdit); // true
```

Si la propiedad por copiar ya existe, se sobrescribe:

```js
let user = { name: "John" };

Object.assign(user, { name: "Pete" });

alert(user.name); // ahora user = { name: "Pete" }
```

También podemos usar Object.assign para hacer una clonación simple:

```js
let user = {
  name: "John",
  age: 30
};

let clone = Object.assign({}, user);

alert(clone.name); // John
alert(clone.age); // 30
```

Aquí, copia todas las propiedades de user en un objeto vacío y lo devuelve.