Una función de orden superior es una función que toma una o más funciones como argumentos, o devuelve una función como resultado.
___
Hay varios tipos diferentes de funciones de orden superior como map y reduce. Hablaremos de ellas más adelante en este tutorial. Pero antes de eso vamos a profundizar en lo que son las funciones de orden superior.

```js
// Callback function, passed as a parameter in the higher order function
function callbackFunction(){
    console.log('I am  a callback function');
}

// higher order function
function higherOrderFunction(func){
    console.log('I am higher order function')
    func()
}

higherOrderFunction(callbackFunction);
```

En el código anterior `higherOrderFunction()` es un HOF porque le estamos pasando una función callback como parámetro.  
  
El ejemplo anterior es bastante simple, ¿verdad? Así que vamos a ampliarlo y ver cómo se puede utilizar HOFs para escribir código más conciso y modular.
## ¿Cómo funcionan? 

Supongamos que quieres escribir una función que calcule el área y el diámetro de un círculo. Como principiante, la primera solución que nos viene a la mente es escribir cada función por separado para calcular el área o el diámetro.

```js
const radius = [1, 2, 3];

// function to calculate area of the circle
const calculateArea =  function (radius) {
    const output = [];
    for(let i = 0; i< radius.length; i++){
        output.push(Math.PI * radius[i] * radius[i]);
    }
    return output;
}

// function to calculate diameter of the circle
const calculateDiameter =  function (radius) {
    const output = [];
    for(let i = 0; i< radius.length; i++){
        output.push(2 * radius[i]);
    }
    return output;
}

console.log(calculateArea(radius));
console.log(calculateDiameter(radius))
```

Pero, ¿te has dado cuenta del problema con el código anterior? ¿No estamos escribiendo casi la misma función una y otra vez con una lógica ligeramente diferente? Además, las funciones que hemos escrito no son reutilizables, ¿verdad?  
  
Entonces, veamos cómo podemos escribir el mismo código usando HOFs:

```js
const radius = [1, 2, 3];

// logic to clculate area
const area = function(radius){
    return Math.PI * radius * radius;
}

// logic to calculate diameter
const diameter = function(radius){
    return 2 * radius;
}

// a reusable function to calculate area, diameter, etc
const calculate = function(radius, logic){ 
    const output = [];
    for(let i = 0; i < radius.length; i++){
        output.push(logic(radius[i]))
    }
    return output;
}

console.log(calculate(radius, area));
console.log(calculate(radius, diameter));
```

Ahora, como puedes ver en el código anterior, sólo hemos escrito una única función `calculate()` para calcular el área y el diámetro del círculo. Sólo tenemos que escribir la lógica y pasarla a `calculate()` y la función hará el trabajo.  
  
El código que hemos escrito usando HOFs es conciso y modular. Cada función está haciendo su propio trabajo y no estamos repitiendo nada aquí. 

Supongamos que en el futuro queremos escribir un programa para calcular la circunferencia del círculo. Podemos simplemente escribir la lógica para calcular la circunferencia y pasarla a la función `calculate()`.

```js
const circumeference = function(radius){
    return 2 * Math.PI * radius;
}

console.log(calculate(radius, circumeference));
```
## Cómo utilizar funciones de alto orden

Las funciones de orden superior pueden utilizarse de varias formas.  
  
Al trabajar con matrices, puede utilizar las funciones `map()`, `reduce()`, `filter()` y `sort()` para manipular y transformar los datos de una matriz.  
  
Cuando se trabaja con objetos, se puede utilizar la función `Object.entries()` para crear una nueva matriz a partir de un objeto.  
  
Cuando se trabaja con funciones, se puede utilizar la función `compose()` para crear funciones complejas a partir de otras más simples.