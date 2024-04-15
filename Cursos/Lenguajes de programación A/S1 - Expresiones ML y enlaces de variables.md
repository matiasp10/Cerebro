Así que vamos a empezar a "aprender ML", pero de una manera que enseñe conceptos básicos de lenguajes de programación en lugar de simplemente "bajar algo de código que funcione".

Un programa **ML** se puede entender como una **_secuencia de enlaces_**. Cada enlace representa una operación o instrucción que se debe realizar.
## Ejecución y evaluación de enlaces

Antes de ejecutar un enlace, se _comprueba_ para verificar si es válido y si se puede ejecutar en el contexto actual. Si la comprobación es exitosa, el enlace se _evalúa_, lo que significa que se lleva a cabo la operación o instrucción que representa.
## Entorno estático vs dinámico 

El tipo de un enlace, si lo hay, depende de un **entorno estático**. _El entorno estático define el conjunto de tipos y variables disponibles para el programa_. Por ejemplo, en un programa Python, el entorno estático puede definir variables como `x` e `y` con tipos específicos como `int` y `str`.

Por otro lado, la forma en que se evalúa un enlace depende de un **entorno dinámico**. El entorno dinámico _contiene información sobre el estado actual del programa, como los valores de las variables y las funciones que se han llamado_.
## Entorno vs. contexto

El término **entorno** generalmente se refiere al **entorno dinámico**. Sin embargo, a veces **contexto** se usa como sinónimo de **entorno estático**.

### Ejemplo en Python

```python
x + y
```

El tipo de este enlace depende del **entorno estático**. Si `x` e `y` son de tipo `int`, el tipo del enlace será `int`.

La **forma en que se evalúa este enlace depende del entorno dinámico**. Si `x` tiene el valor 5 e `y` tiene el valor 10, el resultado de la evaluación del enlace será 15.