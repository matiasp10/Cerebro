En la sección previa vimos como la sustitución interactúa con la igualdad, ahora veremos una correspondencia entre la sustitución y la sentencia de asignación que permitirá a los programadores razonar con asignaciones. Supongamos E una expresión y un estado de sus variables, ejecutar la sentencia de asignación
$$
x := E
$$
significa evaluar la expresión E en ese estado y guardar el resultado en x. La asignación x := E se lee “el valor de E se asigna a x.” 
La ejecución de la asignación (1.8) en un estado, guarda en x el valor de E en ese estado, alterando entonces el estado de x. Por ejemplo, supongamos que un estado consiste en la lista (v, 5), (w, 4), (x, 8) y consideremos la asignación v := v + w, el valor de la expresión v + w en ese estado es 9 y la ejecución de v := v + w guarda 9 en v, con lo cual el estado cambia a (v, 9), (w, 4), (x, 8). 
La manera de ejecutar una asignación es tan importante como la manera de razonar sobre sus efectos. Por ejemplo, a partir de la precondición de una asignación, ¿cómo podemos determinar la correspondiente poscondición? O también, desde la poscondición, podríamos determinar una adecuada precondición? Recordemos que en el Capítulo 0, introducimos los conceptos de pre y poscondición para un proceso en general, ahora diremos que la precondición de una sentencia o instrucción es una afirmación sobre el estado de las variables de un programa para el cual la sentencia puede ser ejecutada, mientras que la poscondición es una afirmación sobre el estado de las variables una vez ejecutada la asignación. El modo usual de indicar la precondición y la poscondición de una sentencia S es
$$
\{P\}\ S \ \{Q\}
$$
donde P es la precondición y Q es la poscondición correspondientes a S. Esta notación es conocida como tripleta de Hoare, debido a que fue C.A.R. Hoare quien introdujo la notación que permitiría a los lenguajes de programación definir los términos bajo los cuales puede determinarse que un programa es correcto respecto de sus especificaciones en lugar de probar su efectividad mediante ejecuciones sucesivas.

Por ejemplo,
$$
\{x = 0\} x := x + 1 \{x > 0\}
$$
es una tripleta de Hoare que resultará válida si y sólo si la ejecución de la asignación x := x+ 1 en cualquier estado en que x es 0 termina en un estado en el que x > 0. Aquí mostramos otros dos ejemplos de tripletas de Hoare válidas para la asignación x := x + 1:
$$
\{x > 5\} x := x + 1 \{x > 0\}
$$
$$
\{x + 1 > 0\} x := x + 1 \{x > 0\}
$$
La tripleta de Hoare
$$
\{x = 5\} x := x + 1 \{x = 7\}
$$
no es válida, porque la ejecución de $x := x + 1$ en un estado en el cual $x = 5$ no termina en un estado en el cual $x = 7$. La siguiente es una definición esquemática de tripleta de Hoare válida para una asignación $x := E$ en términos de sustitución:

> [!definition]
> Dada una asignación $x := E$, para cualquier poscondición $R$, una adecuada precondición es $R [x := E]$, es decir
> $$
> \{R [x := E]\} x := E \{R\}
> $$

Es decir, la precondición se calcula a partir de la asignación y la poscondición. Como ejemplo consideremos la asignación $x := x + 1$ y la poscondición $x > 4$. De acuerdo a la definición anterior la expresión $E$ es $x + 1$ y $R$ es $x > 4$. Concluimos entonces que una precondición para una tripleta de Hoare válida es $(x > 4) [x := x + 1]$ que resulta $x + 1 > 4$. Aquí damos más ejemplos de la aplicación de la definición 1.19 para obtener tripletas de Hoare válidas:
$$
\{x + 1 > 5\} x := x + 1 \{x > 5\}
$$
$$
\{x^2 > x^2 · y\} x := x 2 \{x > x · y\}
$$
La propia definición de la pre y poscondición que ya vimos podría hacernos suponer que la poscondición debería calcularse desde la precondición y de ese modo considerar como una definición de tripleta de Hoare válida $\{R\} x := E \{R [x := E]\}$. Sin embargo, podríamos obtener usando esta regla incorrecta la tripleta $\{x = 0\} x := 2 \{(x = 0) [x := 2]\}$, que es inválida porque una vez finalizada la asignación, el estado no satisface la poscondición. Ahora vamos a ver porqué la definición (1.19) es consistente con la ejecución de la asignación $x := E$. Supongamos un programa con un estado inicial s y un estado final s 0 . Vamos a demostrar que $R [x := E]$ tiene el mismo valor en el estado s que el que tiene R en el estado s 0 . Observemos que $R [x := E]$ y R son exactamente lo mismo salvo que, cada ocurrencia de x en R fue reemplazada por E en $R [x := E]$. Ahora, la ejecución de x := E guarda en x el valor de la expresión E evaluada en el estado s, luego de la asignación el valor de E en el estado s es igual al valor de x en el estado s 0 y como el resto de las variables que no son x tienen el mismo estado en s como en s 0 , sigue que la ejecución comenzó en un estado en donde $R [x := E]$ tiene el valor true y termina en un estado donde R tiene el valor true. En algunos lenguajes de programación, la sentencia de asignación se extiende a la múltiple asignación
$$
x1, x2, . . . , xn := E1, E2, . . . , En
$$
donde las variables xi son todas distintas y Ei son expresiones. La múltiple asignación se ejecuta del siguiente modo; primero se evalúan todas las expresiones Ei , lo cual da como resultado valores que llamaremos vi , luego se asignan v1 a x1, v2 a x2, . . . , vn a xn. Observemos que todas las asignaciones se realizan una vez que se han evaluado todas las expresiones. Por ejemplo:

$x, y := y, x$ intercambia las variables $x$ e $y$
x, i := 0, 0 guarda 0 en x e i
i, x := i + 1, x + i agrega 1 a i y agrega i a x
x, i := x + i, i + 1 agrega i a x y agrega 1 a i

Notemos que los dos últimos ejemplos en la tabla son idénticos. La definición (1.19) puede reformularse para múltiple asignación, simplemente considerando x como una lista de variables y E como una lista de expresiones, con lo cual la múltiple asignación puede definirse en términos de sustitución simultánea. Veamos ahora ejemplos de tripletas de Hoare válidas para múltiple asignación, donde la precondición está dada por (1.19):
$$
\{y > x\} x, y := y, x \{x > y\}
$$
$$
\{x + i = 1 + 2 + . . . + (i + 1 − 1)\} x, i := x + i, i + 1 \{x = 1 + 2 + . . . + (i − 1)\}
$$
$$
\{x + i = 1 + 2 + . . . + (i + 1 − 1)\} i, x := i + 1, x + i \{x = 1 + 2 + . . . + (i − 1)\}
$$
las precondiciones de los dos últimos ejemplos son idénticas, aún cuando las variables y las expresiones en la asignación aparecen en diferente orden. Observemos además que en ambos ejemplos, la precondición y la poscondición coinciden (después de restar a ambos miembros i en la precondición), cuando esto ocurre se dice que la precondición se mantiene por ejecución de la asignación o equivalentemente, la asignación preserva la precondición. 
Veamos ahora la diferencia entre múltiple asignación y asignación sucesiva, consideremos:
$$
x, y := x + y, x + y
$$
$$
x := x + y; y := x + y
$$
en el estado inicial (x, 2) y (y, 3) la ejecución de la múltiple asignación de arriba cambia el estado de x e y al valor 5, mientras que la asignación sucesiva cambia el estado de x a 5 y el estado de y a 8. Con lo cual no resultan ser iguales. La precondición que establece la definición (1.19) para el caso de múltiple asignación toma la forma:
$$
\{R [x, y := E, F]\} x, y := E, F \{R\}
$$
mientras que en el caso de asignación sucesiva resulta
$$
\{R [y := F] [x := E]\} x := E; y := F \{R\}
$$
en este caso la definición se usa para conseguir la precondición de la segunda asignación que resulta la poscondición de la primera, luego la definición se aplica una vez más para conseguir la precondición de la primera asignación. 
Ya vimos que $R [y := F] [x := E]$ no es lo mismo en general que $R [x := E] [y := F]$, con lo cual no es sorprendente que estas dos asignaciones tengan efectos distintos.