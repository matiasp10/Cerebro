Las tablas hash son una estructura de datos que permite crear una lista de valores emparejados, por lo tal, se puede recuperar un determinado valor usando la llave de ese valor para el índice, que se pone en la tabla de antemano.

Una tabla hash transforma una llave en un índice entero, usando una función hash, el índice decidirá dónde almacenar el par llave/valor en la memoria:

![[Pasted image 20230525203011.png]]

Normalmente se utiliza una tabla hash por su rapidez en las operaciones de búsqueda, inserción y eliminación:

#### HASH TABLE TIME COMPLEXITY IN BIG O NOTATION

| Algorithm | Average | Worst case |
| --------- | ------- | ---------- |
| Space     | O(n)    | O(n)       |
| Search    | O(1)    | O(n)       |
| Insert    | O(1)    | O(n)       |
| Delete    | O(1)    | O(n)       |

## Cómo usar las tablas hash con clases objetos y Map en JavaScript

El ejemplo más común de una tabla hash en JavaScript es el tipo de datos `Object`, donde se puede emparejar el valor de la propiedad del objeto, con una llave que encuentra aquella propiedad.

En el siguiente ejemplo, la llave `Nathan` se empareja con el valor del número de teléfono `"555-0182"` y la llave `Jane` se empareja con el valor `"315-0322"`:

```js
let obj = {
  Nathan: "555-0182",
  Jane: "315-0322"
}
```

Objetos en JavaScript son claros ejemplos de implementación de una tabla Hash

El tipo `Object` de JavaScript es un tipo especial de implementación de tabla hash por dos razones:

- Tiene propiedades añadidas por la clase `Object`. Las llaves que introduzcas pueden entrar en conflicto y sobrescribir las propiedades por defecto heredadas de la clase.
- El tamaño de la tabla hash no es rastreado. Es necesario contar manualmente cuántas propiedades son definidas por el programador en lugar de ser heredadas del prototipo.

Por ejemplo, el prototipo [[Object()]] tiene el método [[Object()#Object.prototype.hasOwnProperty()|hasOwnProperty()]] que permite comprobar si una propiedad es heredada:

```js
const obj = {};
obj.nombre = "Nathan";

console.log(obj.hasOwnProperty("nombre")); // true
```

Ejemplo de llamada, para conocer si heredo una determinada llave en JavaScript

JavaScript no bloquea un intento de sobrescribir el método `hasOwnProperty()`, lo que puede causar un error como este:

```js
const obj = {};
obj.nombre = "Nathan";
obj.hasOwnProperty = true; // Aca se modifico para que fuera un valor bool no una función

console.log(obj.hasOwnProperty("nombre")); 
// Error: obj.hasOwnProperty no es una función
// JavaScript object inherited property gets overwritten
```

Para solucionar estas deficiencias, JavaScript creó otra implementación de la estructura de datos de la tabla hash que se llama `Map`.

Al igual que `Object`, `Map` permite almacenar pares llave-valor dentro de la estructura de datos. Aquí hay un ejemplo de `Map` en acción:

```js
const colleccion = new Map();

colleccion.set("Nathan", "555-0182");
colleccion.set("Jane", "555-0182");

console.log(colleccion.get("Nathan")); // 555-0182
console.log(colleccion.size); // 2
```

A diferencia del tipo `Object`, `Map` requiere que utilices los métodos `set()` y `get()` para definir y recuperar cualquier valor de par de llaves que quieras añadir a la estructura de datos.

Tampoco se pueden sobrescribir las propiedades heredadas de la clase `Map`. Por ejemplo, el siguiente código intentó sobrescribir el valor de la propiedad `size` a `false`:

```js
const colleccion = new Map();

colleccion.set("Nathan", "555-0182");
colleccion["size"] = false;

console.log(colleccion.get("size")); // undefined
console.log(colleccion.size); // 1
```

La propiedades de Map no se pueden sobrescribir

Como puedes ver en el código anterior, no puedes añadir una nueva entrada al objeto `Map` sin utilizar el método `set()`.

La estructura de datos `Map` también es iterable, lo que significa que se puede hacer un bucle sobre los datos de la siguiente manera:

```js
const miMap = new Map();

miMap.set("Nathan", "555-0182");
miMap.set("Jane", "315-0322");

for (let [llave, valor] of miMap) {
  console.log(`${llave} = ${valor}`);
}
```

Ahora que has aprendido cómo JavaScript implementa las Tablas Hash en forma de estructuras de datos `Object` y `Map`, vamos a ver cómo puedes crear tu propia implementación de la Tabla Hash.

## Cómo implementar una estructura de datos tipo tabla hash en JavaScript

Aunque JavaScript ya tiene dos implementaciones de tablas hash, escribir tu propia implementación de tablas hash es una de las preguntas más comunes en las entrevistas de JavaScript.

Puedes implementar una tabla hash en JavaScript en tres pasos:

- Crear una clase `TablaHash` con propiedades iniciales de `tabla` y `tamano`.
- Añadir una función `hash()` para transformar las llaves en índices.
- Añade los métodos `set()` y `get()` para añadir y recuperar pares llave/valor de la tabla.

Bien, empecemos por crear la clase `TablaHash`. El código siguiente creará una tabla con un arreglo de tamaño `127`:

```js
class TablaHash {
  constructor() {
    this.tabla = new Array(127);
    this.tamano = 0;
  }
}
```

TablaHash con propiedades iniciales

Todos sus pares llave/valor se almacenarán dentro de la propiedad de la `tabla`.

### Cómo escribir un método hash()

A continuación, hay que crear el método `hash()` que aceptará un valor `llave` y lo transformará en un índice.

Una forma sencilla de crear el hash sería sumar el código ASCII de los caracteres de la clave utilizando el método `charCodeAt()` como sigue. Observe que el método se nombra con `_` para indicar que es una función privada de la clase:

```js
_hash(llave) {
  let hash = 0;
  for (let i = 0; i < llave.length; i++) {
    hash += llave.charCodeAt(i);
  }
  return hash;
}
```

Función hash para retornar un indice

Como la clase `TablaHash` solo tiene 127 espacios, esto significa que el método `_hash()` debe devolver un número entre `0 y 127`.

Para asegurarse de que el valor del hash no excede el tamaño del espacio, es necesario utilizar el operador módulo como se muestra a continuación:

```js
_hash(llave) {
  let hash = 0;
  for (let i = 0; i < llave.length; i++) {
    hash += llave.charCodeAt(i);
  }
  return hash % this.tabla.tamano;
}
```

Módulo para evitar que se exceda del tamaño

Ahora que tienes el método `_hash()` completado, es el momento de escribir los métodos `set()` y `get()`.

### Cómo escribir el método set()

Para establecer el par llave/valor en tu tabla hash, necesitas escribir un método `set()` que acepte `(llave, valor)` como parámetros:

- El método `set()` llamará al método `_hash()` para obtener el valor del `índice`.
- El par `[llave, valor]` se asignará a la `tabla` en el `índice` especificado.
- Entonces, la propiedad de `tamaño` se incrementará en uno.

```js
set(llave, valor) {
  const indice = this._hash(llave);
  this.tabla[indice] = [llave, valor];
  this.tamano++;
}
```

Método set para tabla Hash

Ahora que el método `set()` está completo, vamos a escribir el método `get()` para recuperar un valor por su clave.

### Cómo escribir el método get()

Para obtener un determinado valor de la tabla hash, es necesario escribir un método `get()` que acepte un valor `llave` como parámetro:

- El método llamará al método `_hash()` para recuperar de nuevo el `índice` de la tabla.
- Devuelve el valor almacenado en la `tabla[índice]`.

```js
get(llave) {
  const indice = this._hash(llave);
  return this.tabla[indice];
}
```

Método get para tabla Hash

De este modo, el método `get()` devolverá el par `llave/valor` o `undefined` cuando no haya ningún par llave/valor almacenado en el `índice` especificado.

Hasta aquí todo bien. Vamos a añadir otro método para eliminar el par llave/valor de la tabla hash a continuación.

### Cómo escribir el método remover()

Para eliminar un par llave/valor de la tabla hash, es necesario escribir un método `remover()` que acepte un valor `llave` como parámetro:

- Recuperar el `índice` correcto mediante el método `_hash()`.
- Comprueba si la `tabla[índice]` tiene un valor verdadero y la propiedad `length` es mayor que cero. Asigna el valor `undefined` al `índice` correcto y decrementa la propiedad de `tamaño` en uno si es así.
- Si no, simplemente devuelve `false`

```js
remover(llave) {
  const indice = this._hash(llave);

  if (this.tabla[indice] && this.tabla[indice].length) {
    this.tabla[indice] = undefined;
    this.tamano--;
    return true;
  } else {
    return false;
  }
}
```

Método remover para tabla Hash

Con esto, ya tienes un método `remover()` que funciona. Veamos si la clase `Tabla Hash` funciona correctamente.

## Cómo testear la implementación de la tabla hash

Es hora de probar la implementación de la Tabla hash. Aquí está el código completo para la implementación de la Tabla hash de nuevo:

```js
class TablaHash {
  constructor() {
    this.tabla = new Array(127);
    this.tamano = 0;
  }

  _hash(llave) {
    let hash = 0;
    for (let i = 0; i < llave.length; i++) {
      hash += llave.charCodeAt(i);
    }
    return hash % this.tabla.length;
  }

  set(llave, valor) {
    const indice = this._hash(llave);
    this.tabla[indice] = [llave, valor];
    this.tamano++;
  }

  get(llave) {
    const objetivo = this._hash(key);
    return this.table[objetivo];
  }

  remover(llave) {
    const indice = this._hash(llave);

    if (this.tabla[indice] && this.tabla[indice].length) {
      this.tabla[indice] = [];
      this.tamano--;
      return true;
    } else {
      return false;
    }
  }
}
```

Implementación de tabla Hash en JavaScript

Para probar la clase `TablaHash`, voy a crear una nueva instancia de la `clase` y establecer algunos pares llave/valor como se muestra a continuación. Los pares llave/valor de abajo son solo valores numéricos arbitrarios emparejados con nombres de países sin ningún significado especial:

```js
const ht = new TablaHash();
ht.set("Canada", 300);
ht.set("France", 100);
ht.set("Spain", 110);
```

Prueba del método TablaHash set()

A continuación, vamos a intentar recuperarlos mediante el método `get()`:

```js
console.log(ht.get("Canada")); // [ 'Canada', 300 ]
console.log(ht.get("France")); // [ 'France', 100 ]
console.log(ht.get("Spain")); // [ 'Spain', 110 ]
```

Prueba del método TablaHash get()

Por último, intentemos eliminar uno de estos valores con el método `remover()`:

```js
console.log(ht.remover("Spain")); // true
console.log(ht.get("Spain")); // undefined
```

Prueba del método TablaHash remove()

Muy bien, todos los métodos funcionan como se esperaba. Intentemos otra inserción con una nueva instancia de `TablaHash` y recuperemos esos valores:

```js
const ht = new TablaHash();

ht.set("Spain", 110);
ht.set("ǻ", 192);

console.log(ht.get("Spain")); // [ 'ǻ', 192 ]
console.log(ht.get("ǻ")); // [ 'ǻ', 192 ]
```

Hash Table index collision 

¡Uy! Parece que nos hemos metido en un problema. 😨

## Cómo manejar la colisión en los índices

A veces, la función hash de una tabla hash puede devolver el mismo número de `índice`. En el caso de prueba anterior, la cadena `"España"` y `"ǻ"` **devuelven ambas el mismo valor** `hash` porque el número `507` es la suma del código ASCII de ambas.

El mismo valor `hash` hará que el índice colisione, sobrescribiendo la entrada anterior con la nueva.

En este momento, los datos almacenados en nuestra implementación de la tabla hash tienen el siguiente aspecto:

```js
[
    [ "Spain", 110],
    [ "France", 100]
]
```

Datos almacenados en la tabla Hash

Para manejar la colisión del número de `índice`, es necesario almacenar el par llave/valor en un segundo arreglo para que el resultado final sea el siguiente:

```js
[
    [
        [ "Spain", 110 ],
        [ "ǻ", 192 ]
    ],
    [
        ["France", 100]
    ],
]
```

Datos almacenados en un segundo array

Para crear el segundo arreglo, hay que actualizar el método `set()` para que lo haga:

- Busque en la `tabla[índice]` y realice un bucle sobre los valores del arreglo.
- Si la llave en uno de los arreglos es igual a la `llave` pasada al método, reemplaza el valor en el índice `1` y detiene cualquier ejecución posterior con la sentencia `return`.
- Si no se encuentra ninguna `llave` que coincida, añade un nuevo arreglo de llave-valor al segundo arreglo.
- Si no, inicializa un nuevo arreglo y coloca el par llave/valor en el `índice` especificado.
- Cada vez que se llama a un método `push()`, se incrementa la propiedad `tamaño` en uno.

El código completo del método `set()` será el siguiente:

```js
set(llave, valor) {
  const indice = this._hash(llave);
  if (this.tabla[indice]) {
    for (let i = 0; i < this.tabla[indice].length; i++) {
      // Encuentra llave-valor en el arreglo
      if (this.tabla[indice][i][0] === llave) {
        this.table[indice][i][1] = valor;
        return;
      }
    }
    // No encontrado, añade un nuevo llave valor
    this.tabla[indice].push([llave, valor]);
  } else {
    this.tabla[indice] = [];
    this.tabla[indice].push([llave, valor]);
  }
  this.tamano++;
}
```

Método set() completo

A continuación, actualizamos el método `get()` para que también compruebe el arreglo de segundo nivel con un bucle `for` y devuelva el par llave/valor correcto:

```js
get(llave) {
  const objetivo = this._hash(llave);
  if (this.tabla[llave]) {
    for (let i = 0; i < this.tabla.length; i++) {
      if (this.tabla[objetivo][i][0] === llave) {
        return this.tabla[objetivo][i][1];
      }
    }
  }
  return undefined;
}
```

Método get() completo

Por último, hay que actualizar el método `remover()` para que haga un bucle sobre el array de segundo nivel y elimine el array con el valor de la `llave` correcta utilizando el método `splice()`:

```js
remover(llave) {
  const indice = this._hash(llave);

  if (this.tabla[indice] && this.tabla[indice].length) {
    for (let i = 0; i < this.tabla.length; i++) {
      if (this.tabla[indice][i][0] === llave) {
        this.tabla[indice].splice(i, 1);
        this.tamano--;
        return true;
      }
    }
  } else {
    return false;
  }
}
```

Método remover() completo

Con esto, tu clase `TablaHash` podrá evitar cualquier colisión de números de índice y almacenar el par llave/valor dentro del arreglo de segundo nivel.

Como extra, vamos a añadir un método `mostrar` que mostrará todos los pares llave/valor almacenados en la tabla hash. Solo tienes que utilizar el método `forEach()` para iterar sobre la tabla y `map()` los valores a una cadena como se muestra a continuación:

```js
mostrar() {
  this.tabla.forEach((valores, indice) => {
    const valEncadenados = valores.map(
      ([llave, valor]) => `[ ${llave}: ${valor} ]`
    );
    console.log(`${indice}: ${valEncadenados}`);
  });
}
```

Método mostar() completo

Aquí está el código completo de la clase `TablaHash` de nuevo con el caso previsto de colisiones aplicada para su referencia:

```js
class TablaHash {
  constructor() {
    this.tabla = new Array(127);
    this.tamano = 0;
  }

  _hash(llave) {
    let hash = 0;
    for (let i = 0; i < llave.length; i++) {
      hash += llave.charCodeAt(i);
    }
    return hash % this.tabla.length;
  }

  set(llave, valor) {
    const indice = this._hash(llave);
    this.tabla[indice] = [llave, valor];
    this.tamano++;
  }

  get(llave) {
    const objetivo = this._hash(key);
    return this.table[objetivo];
  }

  remover(llave) {
    const indice = this._hash(llave);

    if (this.tabla[indice] && this.tabla[indice].length) {
      this.tabla[indice] = [];
      this.tamano--;
      return true;
    } else {
      return false;
    }
  }
    
  mostrar() {
     this.tabla.forEach((valores, indice) => {
      const valEncadenados = valores.map(
      	([llave, valor]) => `[ ${llave}: ${valor} ]`
      );
      console.log(`${indice}: ${valEncadenados}`);
    });
  }
}
```

Implementación completa de la clase HashTable

Puedes probar la implementación creando una nueva instancia de `TablaHash` y haciendo algunas inserciones y eliminaciones:

```js
const ht = new TablaHash();

ht.set("France", 111);
ht.set("Spain", 150);
ht.set("ǻ", 192);

ht.mostrar();
// 83: [ France: 111 ]
// 126: [ Spain: 150 ],[ ǻ: 192 ]

console.log(ht.tamano); // 3
ht.remover("Spain");
ht.mostrar();
// 83: [ France: 111 ]
// 126: [ ǻ: 192 ]
```

Otro test TablaHash

Ahora no hay colisión dentro de la instancia de `TablaHash`. ¡Buen trabajo!

## Conclusión

En este tutorial, has aprendido ¿qué es una tabla hash?... y cómo JavaScript la utiliza para crear la estructura de datos `Object` y `Map`.

También has aprendido cómo implementar tu propia clase `TablaHash` y cómo evitar que los índices clave de la tabla hash colisionen utilizando la técnica de encadenamiento.

Utilizando una estructura de datos tabla hash, podrás crear un arreglo asociativo con operaciones rápidas de búsqueda, inserción y borrado 😉 .
