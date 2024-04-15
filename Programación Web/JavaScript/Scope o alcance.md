El concepto principal del manejo de memoria en JavaScript es **alcance**.

Puesto simple, los valores “_alcanzables_” son aquellos que se pueden _acceder_ o _utilizar_ de alguna manera: Se garantiza que serán conservados en la memoria.

1. Hay un conjunto base de __valores inherentemente accesibles__, que no se pueden eliminar por razones obvias.
    
    Por ejemplo:
    
    - La _función ejecutándose actualmente_, sus _variables locales_ y _parámetros_.
    - Otras _funciones_ en la cadena actual de _llamadas anidadas, sus variables y parámetros_.
    - _Variables Globales_
    - (Hay algunos otros internos también)
    
    Estos valores se llaman _raíces_.
    
2. Cualquier otro valor se considera accesible si se lo puede alcanzar desde una raíz por una referencia o por una cadena de referencias.
    
    Por ejemplo, si hay un objeto en una variable global, y ese objeto tiene una propiedad que hace referencia a otro objeto, este objeto también se considera accesible. Y aquellos a los que este objeto hace referencia también son accesibles. Ejemplos detallados a continuación.


Hay un proceso en segundo plano en el motor de JavaScript que se llama recolector de basura. Este proceso monitorea todos los objetos y elimina aquellos que se han vuelto inalcanzables.

# ¿Para que sirve?

Entender bien el concepto de `scope` nos ayudará a aumentar el nivel de _seguridad_ ya que delimita quienes tienen acceso y quienes no a determinadas partes de nuestro código, también nos facilitará en la _detección y disminución de errores_, por ende nuestro código será más robusto.

# Tipos de scope

## Global scope

Se dice que una variable se encuentra en el scope global cuando está declarada fuera de una función o de un bloque. Vamos a poder acceder a este tipo de variables desde _cualquier parte de nuestro código_, ya sea dentro o fuera de una función.

El objeto __window__ es un ejemplo de scope global. 

```js
var alfajor = "Guaymallen";
// El código escrito en esta parte va a poder acceder a alfajor.
function myFunction() {
  // El código escrito en esta parte también va a poder acceder a alfajor.
}
```

## Local scope

Las variables que definimos dentro de una función son variables locales, es decir se encuentran en el Scope local. Esto significa que este tipo de variables van a _vivir únicamente dentro de la función en donde las hayamos declarado_ y si intentamos accederlas fuera de ella, dichas variables no van a estar definidas.

Esto nos permite decidir si queremos una variable solo para una determinada función.

```js
// El código escrito en esta parte NO va a poder acceder a la variable alfajor.
function myFunction() {
  var alfajor= "Guaymallen";
  // El código escrito acá si puede.
}
```

## Global scope automático

Si asignamos un valor a una variable que no ha sido declarada, esta se convertirá automáticamente en una variable global.

```js
myFunction();
// El código en esta parte va a poder acceder a la variable alfajor.
function myFunction() {
  alfajor = "Jorgito";
}
```

## Scope de bloque

A diferencia del scope local este scope está limitado al bloque de código donde fue definida la variable. Desde ECMAScript 6 contamos con los keyword `let` y `const` los cuales nos permiten tener un scope de bloque, esto quiere decir que las variables solo van a _vivir dentro del bloque de código correspondiente_.

```js
if (true) {
    // este bloque if no crea un scope
    // la variable nombre es global por el uso de la keyword 'var'
    var nombre = 'Juan';
    // preferencias se encuentra en el scope local por el uso de la keyword 'let'
    let preferencias = 'Codear';
    // skills también es una scope local por el uso de la keyword 'const'
    const skills = 'Java';
}
console.log(nombre); // logs 'Juan'
console.log(preferencias); // Uncaught ReferenceError: preferencias is not defined
console.log(skills); // Uncaught ReferenceError: skills is not defined
```

## Scope léxico

El lexical scope significa que en un grupo anidado de funciones, las funciones internas tienen acceso a las variables y otros recursos de su ámbito padre. Esto significa que las funciones hijas están vinculadas léxicamente al contexto de ejecución de sus padres.

```js
function myFunction() {
    var nombre = 'Juan';
    // no podemos acceder a preferencias desde acá
    function parent() {
        // nombre si es accesible desde acá.
        // preferencias en cambio, no es accesible.
        function child() {           
 
            // tambien podemos acceder a nombre desde acá.
            var preferencias = 'Codear';
        }
    }
}
```

