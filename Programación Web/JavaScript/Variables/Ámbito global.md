En JavaScript, el ámbito global es el alcance de las variables que se declaran fuera de cualquier función. Las variables globales se pueden acceder desde cualquier parte del código, incluidas otras funciones, objetos y propiedades.

## **Declarar variables globales**

Para declarar una variable global, se puede utilizar la palabra clave `var`. Por ejemplo:

```js
// Variable global
var nombre = "Juan";
```

También se puede declarar una variable global sin usar la palabra clave `var`. Sin embargo, esto se considera una mala práctica, ya que puede causar errores y dificultar el mantenimiento del código.

## **Acceso a variables globales**

Para acceder a una variable global, se puede utilizar su nombre sin ningún modificador de alcance. Por ejemplo:

```js
// Variable global
var nombre = "Juan";

// Acceso a la variable global
console.log(nombre); // Juan
```

## **Ejemplos de ámbito global**

El ámbito global se puede utilizar para compartir datos entre funciones y objetos. Por ejemplo:

```js
// Variable global
var nombre = "Juan";

// Función que utiliza la variable global
function saludar() {
  console.log("Hola, " + nombre); // Hola, Juan
}

// Objeto que utiliza la variable global
var persona = {
  nombre: nombre,
  saludar: function() {
    console.log("Hola, " + nombre); // Hola, Juan
  }
};

saludar();
persona.saludar();
```

En este ejemplo, la variable `nombre` se declara globalmente. La función `saludar()` utiliza la variable `nombre` para saludar al usuario. El objeto `persona` también utiliza la variable `nombre` para almacenar el nombre de la persona.

## **Ventajas y desventajas del ámbito global**

### Ventajas:

- Simplifica el acceso a las variables.
- Permite compartir datos entre funciones y objetos.

### Desventajas:

- Puede hacer que el código sea más difícil de entender y mantener.
- Puede causar errores, si se accede a la misma variable con el mismo nombre desde diferentes ámbitos.

## **Conclusión**

El ámbito global es un concepto importante en JavaScript. Un buen conocimiento del ámbito global puede ayudar a escribir código más limpio y eficaz.

## **Consejos para utilizar el ámbito global**

- Utilice el ámbito global solo cuando sea necesario.
- Evite declarar variables globales sin usar la palabra clave `var`.
- Utilice nombres de variables descriptivos para facilitar el seguimiento del código.
- Utilice módulos para organizar el código y evitar conflictos de nombres.