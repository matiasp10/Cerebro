En JavaScript, el ámbito de función es el alcance de las variables que se declaran dentro de una función. Las variables declaradas dentro de una función solo se pueden acceder desde dentro de esa función y de sus funciones anidadas.

## **Declarar variables en el ámbito de función**

Para declarar una variable en el ámbito de función, se puede utilizar la palabra clave `let` o `const`. La palabra clave `let` declara una variable local que se puede reasignar, mientras que la palabra clave `const` declara una variable local que no se puede reasignar.

```js
// Función con ámbito de función
function saludar() {
  // Variable local
  let nombre = "Juan";

  // Acceso a la variable local
  console.log(nombre); // Juan

  // Función anidada
  function despedirse() {
    // Acceso a la variable local del ámbito de función superior
    console.log(nombre); // Juan
  }

  // Llamada a la función anidada
  despedirse();
}

// Llamada a la función
saludar();
```

En este ejemplo, la variable `nombre` se declara localmente dentro de la función `saludar()`. Esto significa que solo se puede acceder a ella desde dentro de la función. La función `despedirse()` también puede acceder a la variable `nombre`, ya que se encuentra en el ámbito de función superior.

## **Ventajas y desventajas del ámbito de función**

### Ventajas:

- Mejora la legibilidad y la mantenibilidad del código.
- Evita errores, si se accede a la misma variable con el mismo nombre desde diferentes ámbitos.

### Desventajas:

- Puede hacer que el código sea más difícil de entender.
- Puede requerir más código para acceder a las variables.

## **Conclusión**

El ámbito de función es un concepto importante en JavaScript. Un buen conocimiento del ámbito de función puede ayudar a escribir código más limpio y eficaz.

## **Consejos para utilizar el ámbito de función**

- Utilice el ámbito de función siempre que sea posible.
- Utilice nombres de variables descriptivos para facilitar el seguimiento del código.
- Utilice módulos para organizar el código y evitar conflictos de nombres.

## **Shadowing**

El shadowing es un fenómeno que se produce cuando se declara una variable con el mismo nombre que una variable declarada anteriormente en un ámbito superior. En este caso, la variable declarada en el ámbito inferior oculta a la variable declarada en el ámbito superior.

```js
// Función con shadowing
function saludar() {
  // Variable global
  var nombre = "Juan";

  // Variable local
  let nombre = "Pedro";

  // Acceso a la variable local
  console.log(nombre); // Pedro
}

// Llamada a la función
saludar();
```

En este ejemplo, la variable `nombre` se declara globalmente. La función `saludar()` declara una variable local con el mismo nombre. Esto significa que la variable local oculta a la variable global.

## **Shadowing de variables globales**

El shadowing de variables globales es una práctica que se considera una mala práctica. Esto se debe a que puede causar confusión y errores.

## **Shadowing de variables locales**

El shadowing de variables locales es una práctica que se puede utilizar para fines específicos. Por ejemplo, se puede utilizar para reemplazar el valor de una variable local.

```js
// Función con shadowing de variables locales
function saludar() {
  // Variable local
  let nombre = "Juan";

  // Acceso a la variable local
  console.log(nombre); // Juan

  // Shadowing de la variable local
  nombre = "Pedro";

  // Acceso a la variable local
  console.log(nombre); // Pedro
}

// Llamada a la función
saludar();
```

En este ejemplo, la función `saludar()` declara una variable local `nombre` con el valor `Juan`. La función luego reemplaza el valor de la variable local con `Pedro`.