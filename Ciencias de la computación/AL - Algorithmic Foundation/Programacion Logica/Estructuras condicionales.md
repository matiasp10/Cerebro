Se ejecuta una acción si se cumple una condición. Esto permite modificar el orden de ejecución de las sentencias según el resultadode una expresión que se evalúa. El tipo de dato del resultado de la condición debe ser de tipo lógico. 

Las estructuras condicionales se clasifican en: simples, dobles y múltiples.

### Condicional simple

Evalúa una expresión lógica (condición). Si esta es verdadera, ejecuta las sentencias especificadas a continuación de la palabra reservada entonces; si es falsa, no realiza ninguna acción y continúa con el flujo del algoritmo.

```
si <condición> entonces
sentencia 1
sentencia 2
fin-si
```

![[condicionalsimple|center]]
### Condicional doble

Evalúa una expresión lógica (condición). Si esta es verdadera, ejecuta las sentencias que se encuentran a continuación de la palabra reservada entonces (rama verdadera), pero si la condición resulta ser falsa, entonces se ejecutan las sentencias especificadas a continuación de la palabra reservada si-no (rama falsa).

```
si <condición> entonces
sentencia 1
si-no
sentencia 1
fin-si
```

![[Condicional doble|center]]
### Condicional múltiple

La estructura condicional múltiple es utilizada cuando se debe elegirentre más de dos alternativas de acuerdo con el valor de una variable. Evalúa una expresión (condición) que puede resultar en N valores distintos. Según el resultado de la expresión, se ejecutarán las sentencias definidas para el valor que se ha obtenido.

```
según-sea <expresión> hacer
caso A: sentencia A1
caso B: sentencia B1
caso N: sentencia N1
si-no:
sentencia X1
fin-según
```

Esta expresión requiere que la variable que se evalúa sea de tipo entero o carácter. La aplicación de la sentencia si-no es opcional y debe ser utilizada cuando necesitamos ejecutar un conjunto de acciones en el caso de que el resultado de la variable no sea igual a ninguno de los valores especificados en las sentencias caso.

![[Condicionales multiples|center|700]]