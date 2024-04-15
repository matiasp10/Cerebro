Para recorrer todas las claves de un objeto existe una forma especial de bucle: **for..in**.

```js
for (key in object) {
  // se ejecuta el cuerpo para cada clave entre las propiedades del objeto
}
```

Por ejemplo, mostremos todas las propiedades de user:

```js
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  // claves
  alert( key );  // name, age, isAdmin
  // valores de las claves
  alert( user[key] ); // John, 30, true
}
```

Nota que todas las construcciones “`for`” nos permiten _declarar variables_ para bucle dentro del bucle, como `let key` aquí.

Además podríamos usar otros nombres de variables en lugar de key. Por ejemplo, "`for (let prop in obj)`" también se usa bastante.

## Ordenamiento de un objeto

¿Los objetos están ordenados? Es decir, si creamos un bucle sobre un objeto, ¿obtenemos todas las propiedades en el mismo orden en el que se agregaron? ¿Podemos confiar en ello?

La respuesta corta es: “_ordenados de una forma especial_”: las propiedades de _números enteros se ordenan_, los demás aparecen en el _orden de la creación_. Entremos en detalle.

Como ejemplo, consideremos un objeto con códigos telefónicos:

```js
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "44": "Great Britain",
  // ..,
  "1": "USA"
};

for (let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```

El objeto puede usarse para sugerir al usuario una lista de opciones. Si estamos haciendo un sitio principalmente para el público alemán, probablemente queremos que 49 sea el primero.

Pero si ejecutamos el código, veremos una imagen totalmente diferente:

USA (1) va primero
Luego Switzerland (41) y así sucesivamente.
Los códigos telefónicos van en orden ascendente porque son números enteros. Entonces vemos 1, 41, 44, 49.

> [!hint]- Propiedades de números enteros 
> El término “**propiedad de números enteros**” aquí significa que _una cadena se puede convertir a y desde desde un entero sin ningún cambio_.
> 
> Entonces, “49” es un nombre de propiedad entero, porque cuando este se transforma a un entero y viceversa continúa siendo el mismo. Pero “+49” y “1.2” no lo son.

…Por otro lado, si las claves no son enteras, se enumeran en el orden de creación, por ejemplo:

```js
let user = {
  name: "John",
  surname: "Smith"
};
user.age = 25; // Se agrega una propiedad más

// Las propiedades que no son enteras se enumeran en el orden de creación
for (let prop in user) {
  alert( prop ); // name, surname, age
}
```

Entonces, para solucionar el problema con los códigos telefónicos, podemos “hacer trampa” haciendo que los códigos no sean enteros. Agregar un signo más "+" antes de cada código será más que suficiente.

```js
let codes = {
  "+49": "Germany",
  "+41": "Switzerland",
  "+44": "Great Britain",
  // ..,
  "+1": "USA"
};

for (let code in codes) {
  alert( +code ); // 49, 41, 44, 1
}
```






