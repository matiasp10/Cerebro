La propiedad **globalThis** contiene el valor _global_ **this**, que suele ser similar al objeto global.

# Descripción 

Históricamente, acceder al objeto global ha requerido una sintaxis diferente en diferentes entornos JavaScript. En la web puedes usar `window`, `self`, o `frames` - pero en Web Workers solo funciona `self`. En *Node.js* ninguno de estos funciona, y en su lugar debes utilizar `global`. La palabra clave **this** puede usarse dentro de funciones que se ejecuten en modo no estricto, pero esto será indefinido en módulos y dentro de funciones que se ejecuten en modo estricto. También puedes usar `Function('return this')()`, pero los entornos que deshabilitan `eval()`, como CSP en los navegadores, impiden el uso de `Function` de esta forma.

La propiedad `globalThis` proporciona una forma estándar de acceder al valor global `this` (y, por tanto, al propio objeto global) en distintos entornos. A diferencia de propiedades similares como `window` y `self`, está garantizado que funciona en contextos de `window` y `non-window`. De esta forma, puedes acceder al objeto global de forma consistente sin tener que saber en qué entorno se está ejecutando el código. Para ayudarte a recordar el nombre, sólo recuerda que en el ámbito global el valor *this* es *globalThis*.

> [!note] Nota
> `globalThis` es generalmente el mismo concepto que el objeto `global` (es decir, añadir propiedades a `globalThis` las convierte en variables globales) - este es el caso de los navegadores y Node - pero a los hosts se les permite proporcionar un valor diferente para `globalThis` que no esté relacionado con el objeto `global`.

