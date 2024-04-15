En JavaScript, las variables son un concepto fundamental para el almacenamiento de datos. Sin embargo, es importante comprender cómo funciona el ámbito de las variables, ya que esto determina dónde y cómo se pueden acceder a ellas.

El ámbito de una variable se refiere al alcance de su visibilidad. En otras palabras, indica qué partes del código tienen acceso a la variable.

En JavaScript, existen dos tipos de ámbitos:

### [[Ámbito global]]

Las variables declaradas fuera de cualquier función tienen ámbito global. Esto significa que se pueden acceder a ellas desde cualquier parte del código.

### [[Ámbito local]]

Las variables declaradas dentro de una función tienen ámbito local. Esto significa que solo se pueden acceder a ellas desde dentro de la función en la que se declararon.

#### [[Ámbito de función]]

El ámbito de función es el alcance de las variables que se declaran dentro de una función.

### [[Ámbito de bloque]]

El ámbito de bloque es el alcance de las variables que se declaran dentro de un bloque. Los bloques se delimitan por llaves `{}`.

## **Ejemplo**

Consideremos el siguiente ejemplo:

```js
// Variable global
var nombre = "Juan";

// Función con ámbito local
function saludar() {
  // Variable local
  let apellido = "Pérez";

  console.log("Hola, " + nombre + " " + apellido);
}

saludar();
```

En este ejemplo, la variable `nombre` es global, por lo que se puede acceder a ella desde cualquier parte del código. La variable `apellido` es local a la función `saludar()`, por lo que solo se puede acceder a ella desde dentro de la función.

## **Conclusión**

El ámbito de las variables es un concepto fundamental en JavaScript. Un buen conocimiento del ámbito de las variables puede ayudar a evitar errores y a escribir código más limpio y eficaz.