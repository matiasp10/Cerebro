En lugar de especificar directamente el significado de un programa, la **semántica axiomática** _especifica lo que se puede demostrar sobre el programa_. 

Uno de los posibles usos de las especificaciones semánticas es demostrar la corrección de los programas. En la semántica axiomática, no hay un modelo del estado de una máquina o programa ni un modelo de los cambios de estado que tienen lugar durante la ejecución del programa. 

El significado de un programa se basa en las relaciones entre las variables y constantes del programa, que son las mismas para cada ejecución del programa. 

La semántica axiomática tiene dos aplicaciones distintas: _verificación de programas_ y _especificación de semántica de programas_.

La semántica axiomática se define en conjunto con el desarrollo de un enfoque para demostrar la corrección de programas. Estas pruebas de corrección, cuando se pueden construir, demuestran que un programa realiza la computación descrita por su especificación. 

En una prueba, cada declaración de un programa está precedida y seguida por una expresión lógica que especifica restricciones sobre las variables del programa. Estas restricciones, en lugar de todo el estado de una máquina abstracta (como en la semántica operacional), se utilizan para especificar el significado de la declaración. 
La notación utilizada para _describir restricciones_, de hecho, el lenguaje de la semántica axiomática, es el _cálculo de predicados_. Aunque las expresiones booleanas simples suelen ser adecuadas para expresar restricciones, en algunos casos no lo son. 

Cuando la semántica axiomática se utiliza para especificar formalmente el significado de una declaración, el significado se define por el efecto de la declaración en las afirmaciones sobre los datos afectados por la declaración.

# Aserciones 

Las expresiones lógicas utilizadas en la semántica axiomática se denominan predicados o aserciones. Una aserción que precede inmediatamente a una declaración de programa describe las restricciones sobre las variables del programa en ese punto. Una aserción que sigue inmediatamente a una declaración describe las nuevas restricciones sobre esas variables (y posiblemente otras) después de la ejecución de la declaración. Estas aserciones se denominan, respectivamente, **precondición** y **postcondición** de la declaración. Para dos declaraciones adyacentes, la postcondición de la primera sirve como precondición de la segunda. Desarrollar una descripción axiomática o una prueba de un programa dado requiere que cada declaración en el programa tenga tanto una precondición como una postcondición.

Se examina el punto de vista de que las precondiciones para las declaraciones se calculan a partir de las postcondiciones dadas, aunque también es posible considerarlas en el sentido opuesto. Se asume que todas las variables son de tipo entero. Como ejemplo simple, se considera la siguiente declaración de asignación y la postcondición:

```
sum = 2 * x + 1 {sum > 1}
```

Una posible precondición para esta declaración es `{x > 10}`.

En la semántica axiomática, el significado de una declaración específica se define por su precondición y su postcondición, las cuales especifican precisamente el efecto de ejecutar la declaración. 

La verificación de programas es una aplicación común de las descripciones axiomáticas de los lenguajes.

# Precondición mas débil

La precondición más débil es la menos restrictiva que garantizará la validez de la postcondición asociada. Por ejemplo, en la declaración y postcondición dada en la Sección de aserciones, `{x > 10}`, `{x > 50}` y `{x > 1000}` son todas precondiciones válidas. La más débil de todas las precondiciones en este caso es `{x > 0}`.

Si la precondición más débil se puede calcular a partir de la postcondición más general para cada tipo de declaración de un lenguaje, entonces los procesos utilizados para calcular estas precondiciones proporcionan una descripción concisa de la semántica de ese lenguaje. Además, se pueden construir pruebas de corrección para programas en ese lenguaje. Una prueba de programa se inicia utilizando las características de los resultados de la ejecución del programa como la postcondición de la última declaración del programa. Esta postcondición, junto con la última declaración, se utiliza para calcular la precondición más débil para la última declaración. Esta precondición se utiliza luego como postcondición para la penúltima declaración. Este proceso continúa hasta llegar al inicio del programa. En ese punto, la precondición de la primera declaración establece las condiciones bajo las cuales el programa calculará los resultados deseados. Si estas condiciones están implícitas en la especificación de entrada del programa, se verifica que el programa sea correcto.

Una regla de inferencia es un método para inferir la verdad de una afirmación en función de los valores de otras afirmaciones. La forma general de una regla de inferencia es la siguiente:

```
(S1, S2, c, Sn) / S
```

Esta regla establece que si `S1, S2, ..., y Sn` son verdaderos, entonces se puede inferir la verdad de `S`. La parte superior de una regla de inferencia se llama antecedente; la parte inferior se llama consecuente.

Un axioma es una afirmación lógica que se asume como verdadera. Por lo tanto, un axioma es una regla de inferencia sin antecedente. Para algunas declaraciones de programas, el cálculo de una precondición más débil a partir de la declaración y una postcondición es simple y puede especificarse mediante un axioma. Sin embargo, en la mayoría de los casos, la precondición más débil solo se puede especificar mediante una regla de inferencia.

Para utilizar la semántica axiomática con un lenguaje de programación dado, ya sea para pruebas de corrección o para especificaciones formales de semántica, debe existir un axioma o una regla de inferencia para cada tipo de declaración en el lenguaje.

# Declaración de asignación

En la semántica axiomática, la precondición y postcondición de una declaración de asignación son fundamentales para definir su significado. La precondición representa el estado inicial necesario para que la declaración se ejecute correctamente, mientras que la postcondición describe el estado final que debe cumplirse después de la ejecución.

## Cálculo de la precondición

La precondición, denotada como $P$, de una declaración de asignación $x = E$ con postcondición $Q$ se calcula reemplazando todas las instancias de $x$ en $Q$ por la expresión $E$. Por ejemplo, si tenemos la declaración $a = b / 2 - 1$ con postcondición $a < 10$, la precondición más débil se obtiene al sustituir $b / 2 - 1$ por $a$ en la postcondición, resultando en $b < 22$ como precondición.

## Regla de consecuencia

Para utilizar la semántica axiomática en pruebas, se emplea la regla de consecuencia. Esta regla establece que si la afirmación lógica ${P} S {Q}$ es verdadera, y las implicaciones $P' \rightarrow P$ y $Q \rightarrow Q'$ se cumplen, entonces se puede inferir que ${P'} S {Q'}$. En otras palabras, la regla de consecuencia permite debilitar la postcondición y fortalecer la precondición.

## Ejemplo de aplicación

Consideremos la afirmación lógica ${x > 3} x = x - 3 {x > 0}$. Al aplicar el axioma de asignación, se demuestra que la precondición ${x > 3}$ es válida. En otro caso, si tenemos ${x > 5} x = x - 3 {x > 0}$, aunque la precondición dada no coincide con la producida por el axioma, se reconoce que ${x > 5}$ implica ${x > 3}$.La regla de consecuencia se utiliza para formalizar estas inferencias, permitiendo fortalecer precondiciones y debilitar postcondiciones en el proceso de prueba. Esta herramienta es esencial para garantizar la corrección y validez de los programas en el contexto de la semántica axiomática.

# Secuencias

En la semántica axiomática, la precondición más débil para una secuencia de declaraciones no puede ser descrita por un axioma, ya que depende de los tipos particulares de declaraciones en la secuencia. En este caso, la precondición solo se puede describir mediante una regla de inferencia.

## Regla de inferencia para secuencias

Sean S1 y S2 declaraciones de programa adyacentes. Si S1 y S2 tienen las siguientes pre- y postcondiciones:

```
{P1} S1 {Q1} 
{Q1} S2 {Q2}
```

Entonces, la regla de inferencia para la secuencia S1; S2 es:
$$\frac{\{P1\} S1 \{Q1\}, \{Q1\} S2 \{Q2\}}{\{P1\} S1, S2 \{Q2\}
}$$
Es decir, la precondición más débil para la secuencia S1; S2 es la precondición P1 de la primera declaración S1.

## Ejemplo

Supongamos que tenemos las siguientes declaraciones de asignación:

```
𝑥1=𝐸1 
𝑥2=𝐸2
```

Aplicando la regla de inferencia, tenemos:

$$\{(𝑄3_{𝑥2→𝐸2})𝑥1→𝐸1\}𝑥1=𝐸1\{𝑄3𝑥_{2→𝐸2}\}$$
$$\{𝑄3_{𝑥2→𝐸2}\}𝑥2=𝐸2\{𝑄3\}$$

Por lo tanto, la precondición más débil para la secuencia x1 = E1; x2 = E2 con postcondición Q3 es:
$$\{(𝑄3_{𝑥2→𝐸2})_{𝑥1→𝐸1}\}$$
Otro ejemplo:

```
y = 3 * x + 1; 
x = y + 3; 
{x < 10}
```

La precondición para la segunda asignación es `y < 7`, que se usa como postcondición para la primera asignación. Calculando la precondición de la primera asignación:

```
3 * x + 1 < 7 
x < 2
```

Por lo tanto, `{x < 2}` es la precondición más débil tanto para la primera asignación como para la secuencia completa.

# Selección

A continuación, consideramos la regla de inferencia para las declaraciones de selección, cuya forma general es:

```
if B then S1 else S2
```

Consideramos solo selecciones que incluyen cláusulas `else`. La regla de inferencia es:
$$\frac{\{B \ and\ P\} S1 \{Q\}, \{(not\ B)\ and\ P\} S2\{Q\}}{\{P\} \text{ if B then S1 else S2} \{Q\}}$$
Esta regla indica que las declaraciones de selección deben ser probadas tanto cuando la expresión de control booleana es verdadera como cuando es falsa. La primera afirmación lógica sobre la línea representa la cláusula `then`; la segunda representa la cláusula `else`. Según la regla de inferencia, necesitamos una precondición `P` que pueda ser utilizada en la precondición tanto de la cláusula `then` como de la cláusula `else`.

Consideremos el siguiente ejemplo de cálculo de la precondición utilizando la regla de inferencia para selecciones. La declaración de selección de ejemplo es:

```
if x > 0 then     
	y = y - 1 
else     
	y = y + 1
```

Supongamos que la postcondición, `Q`, para esta declaración de selección es `{y > 0}`. Podemos utilizar el axioma para la asignación en la cláusula `then`:

```
y = y - 1 {y > 0}
```

Esto produce `{y - 1 > 0}` o `{y > 1}`. Esto se puede utilizar como la parte `P` de la precondición para la cláusula `then`. Ahora aplicamos el mismo axioma a la cláusula `else`:

```
y = y + 1 {y > 0}
```

lo cual produce la precondición `{y + 1 > 0}` o `{y > -1}`. Dado que ` {y > 1} => {y > -1} `, la regla de consecuencia nos permite usar `{y > 1}` como la precondición de toda la declaración de selección.