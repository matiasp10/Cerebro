La creación de una _descripción concisa pero comprensible de un lenguaje de programación es una tarea compleja_ pero fundamental para su éxito. Si bien ejemplos como **ALGOL 60** y **ALGOL 68** demuestran la utilidad de las descripciones formales concisas, la complejidad de su notación dificultó su comprensión y limitó su adopción. Por otro lado, lenguajes con definiciones simples pero informales pueden derivar en múltiples dialectos, generando confusión entre los usuarios.

El desafío de describir un lenguaje de programación radica en la diversidad de usuarios que deben comprenderlo: **evaluadores iniciales**, **implementadores** y **usuarios**. 
**_Los evaluadores iniciales_**, generalmente miembros de la organización que desarrolla el lenguaje, son cruciales para su refinamiento durante el proceso de diseño. La claridad de la descripción es esencial para un ciclo de retroalimentación efectivo.

Los **_implementadores del lenguaje_** necesitan comprender cómo se forman las expresiones, sentencias y unidades de programa, así como su comportamiento durante la ejecución. La exhaustividad y precisión de la descripción del lenguaje son fundamentales para facilitar su trabajo.

Finalmente, los **_usuarios_** del lenguaje deben poder codificar soluciones informáticas consultando un manual de referencia. Si bien los libros de texto y cursos también juegan un papel importante, los manuales son la fuente de información oficial sobre el lenguaje.

Al igual que los lenguajes naturales, los lenguajes de programación se estudian en dos aspectos: _sintaxis_ y _semántica_. La sintaxis define la forma de las expresiones, sentencias y unidades de programa, mientras que la semántica define su significado. Un ejemplo de sintaxis es la sentencia `while` de Java:

```java
while (boolean_expr) statement
```

La semántica de esta sentencia indica que la sentencia `statement` se ejecuta si el valor actual de la expresión booleana es verdadero. De lo contrario, el control del programa continúa después de la construcción `while`. Luego, el control vuelve implícitamente a la expresión booleana para repetir el proceso.

Si bien **la sintaxis y la semántica se suelen analizar por separado**, están estrechamente relacionadas. En un lenguaje de programación bien diseñado, _la semántica debería derivarse directamente de la sintaxis_, es decir, la apariencia de una expresión debería sugerir claramente su propósito.

Describir la sintaxis suele ser más sencillo que describir la semántica, ya que _existe una notación concisa y universalmente aceptada para la sintaxis_, mientras que para la semántica aún no se ha desarrollado una notación estandarizada.

En resumen, crear una descripción clara y precisa de un lenguaje de programación es un desafío crucial para su éxito. Al considerar las necesidades de los diferentes usuarios y abordar tanto la sintaxis como la semántica de manera efectiva, se puede garantizar que el lenguaje sea comprensible, implementable y utilizable.