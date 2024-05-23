**texto extraido del libro**
# Declaración de asignación

La precondición y postcondición de una declaración de asignación juntas definen precisamente su significado. Para definir el significado de una declaración de asignación, dada una postcondición, debe haber una forma de calcular su precondición a partir de esa postcondición.  

Sea $x = E$ una declaración de asignación general y $Q$ sea su postcondición.
Entonces, su precondición, $P$, está definida por el axioma.

$$P = Q_x\rightarrow E$$
Esto significa que P se calcula como Q con todas las instancias de x reemplazadas por E. Por ejemplo, si tenemos la declaración de asignación y la postcondición
$$ a = b / 2 - 1 {a < 10} $$
La precondición más débil se calcula sustituyendo `b / 2 - 1` por `a` en la postcondición `{a < 10}`, de la siguiente manera:

$$ b / 2 - 1 < 10 $$
$$ b < 22 $$
Por lo tanto, la precondición más débil para la declaración de asignación dada y la postcondición es `{b < 22}`. Recuerda que el axioma de asignación está garantizado de ser correcto solo en ausencia de efectos secundarios. Una declaración de asignación tiene un efecto secundario si cambia alguna variable que no sea su objetivo.
La notación habitual para especificar la semántica axiomática de una forma de declaración dada es:
$$\{P\} S \{Q\}$$
Donde P es la precondición, Q es la postcondición y S es la forma de declaración. En el caso de la declaración de asignación, la notación es:
$$ \{Q_{x \rightarrow E}\} x = E\{Q\} $$
Como otro ejemplo de cálculo de una precondición para una declaración de asignación, considere lo siguiente:
$$x = 2 * y - 3 \{x > 25\}$$
La precondición es calculada como:
$$ 2 * y - 3 > 25$$
$$y > 14$$
Entonces, $\{y > 14\}$ es la precondición más débil para esta declaración de asignación y postcondición.
Es importante tener en cuenta que la aparición del lado izquierdo de la declaración de asignación en su lado derecho no afecta el proceso de cálculo de la precondición más débil.
Por ejemplo, para
$$x = x + y - 3 \{x > 10\}$$
la condición mas débil es
$$x + y - 3 > 10$$
$$y > 13 - x$$
Recuerda que la semántica axiomática se desarrolló para probar la corrección de los programas. En ese sentido, es natural preguntarse cómo se puede usar el axioma para las declaraciones de asignación para probar algo. 

> [!note] ¿Cómo se puede usar el axioma para las declaraciones de asignación para probar algo?
> Una declaración de asignación dada, con una precondición y una postcondición, puede considerarse una afirmación lógica o un teorema. Si el axioma de asignación, al aplicarse a la postcondición y a la declaración de asignación, produce la precondición dada, entonces el teorema queda probado.

Por ejemplo, considera la siguiente afirmación lógica:
$$\{x > 3\} x = x - 3 \{x > 0\}$$
Utilizando el axioma de asignación en
$$x = x - 3 \{x > 0\}$$
Esto produce `{x > 3}`, que es la precondición dada. Por lo tanto, hemos probado la afirmación lógica de ejemplo. 
A continuación, considera la siguiente afirmación lógica:
$$\{x > 5\} x = x - 3 \{x > 0\}$$
En este caso, la precondición dada, `{x > 5}`, no es la misma que la afirmación producida por el axioma. Sin embargo, es evidente que `{x > 5}` implica `{x > 3}`.

Para utilizar esto en una prueba, se necesita una regla de inferencia, llamada regla de consecuencia. La forma de la regla de consecuencia es:
$$ \frac{\{P\} S \{Q\}, P' \rightarrow P, Q \rightarrow Q'}{\{P'\} S \{Q'\}}$$
El símbolo ` => ` significa "implica", y `S` puede ser cualquier declaración de programa. La regla se puede enunciar de la siguiente manera: Si la afirmación lógica `{P} S {Q}` es verdadera, la afirmación `P` implica la afirmación `P`, y la afirmación `Q` implica la afirmación `Q`, entonces se puede inferir que `{P} S {Q}`. En otras palabras, la regla de consecuencia dice que una postcondición siempre se puede debilitar y una precondición siempre se puede fortalecer. Esto es muy útil en las pruebas de programas. Por ejemplo, permite completar la prueba del último ejemplo de afirmación lógica anterior. Si dejamos que `P` sea `{x > 3}`, `Q` y `Q` sean `{x > 0}`, y `P` sea `{x > 5}`, tenemos:
$$\frac{\{x>3\}x = x–3\{x>0\},(x>5) \rightarrow \{x>3\},(x>0) \rightarrow (x>0)}{\{x>5\}x = x–3\{x>0\}}$$
El primer término del antecedente ({x > 3} x = x - 3 {x > 0}) se probó con el axioma de asignación. El segundo y tercer términos son obvios. Por lo tanto, mediante la regla de consecuencia, el consecuente es verdadero.