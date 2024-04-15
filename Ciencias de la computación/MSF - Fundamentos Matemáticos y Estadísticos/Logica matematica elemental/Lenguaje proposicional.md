La **lógica proposicional** o **lógica de orden cero** es un sistema formal cuyos elementos más simples representan proposiciones, y cuyas constantes lógicas, llamadas conectivas lógicas, representan operaciones sobre proposiciones, capaces de formar otras proposiciones de mayor complejidad. La lógica proposicional trata con sistemas lógicos que carecen de cuantificadores, o variables interpretables como entidades. En lógica proposicional si bien no hay signos para variables de tipo entidad, sí existen signos para variables proposicionales (es decir, que pueden ser interpretadas como proposiciones con un valor de verdad definido), de ahí el nombre proposicional. La lógica proposicional incluye además de variables interpretables como proposiciones simples signos para conectivas lógicas, por lo que dentro de este tipo de lógica puede analizarse la inferencia lógica de proposiciones a partir de proposiciones, pero sin tener en cuenta la estructura interna de las proposiciones más simples.

Considérese el siguiente argumento:

1. Mañana es miércoles o mañana es jueves.
2. Mañana no es jueves.
3. Por lo tanto, mañana es miércoles.

Es un argumento válido. Quiere decir que es imposible que las premisas (1) y (2) sean verdaderas y la conclusión (3) falsa.

Sin embargo, a pesar de que el argumento sea válido, esto no quiere decir que la conclusión sea verdadera. En otras palabras, si las premisas son falsas, entonces la conclusión también podría serlo. Pero si las premisas son verdaderas, entonces la conclusión también lo es. La validez del argumento no depende del significado de las expresiones _«mañana es miércoles»_ ni _«mañana es jueves»_, sino de la estructura misma del argumento. Estas premisas podrían cambiarse por otras y el argumento permanecería válido. Por ejemplo:


1. Hoy está soleado o está nublado.
2. Hoy no está nublado.
3. Por lo tanto, hoy está soleado.

La validez de los dos argumentos anteriores depende del significado de las expresiones _«o»_ y _«no»_. Si alguna de estas expresiones se cambia por otra, entonces los argumentos podrían dejar de ser válidos. Por ejemplo, considérese el siguiente argumento inválido:

1. Ni está soleado ni está nublado.
2. No está nublado.
3. Por lo tanto, está soleado.

Estas expresiones como _«o»_ y _«no»_, de las que depende la validez de los argumentos, se llaman **conectivas lógicas**. En cuanto a expresiones como _«está nublado»_ y _«mañana es jueves»_, lo único que importa de ellas es que tengan un valor de verdad. Es por esto que se las reemplaza por simples letras, cuya intención es simbolizar una expresión con valor de verdad cualquiera. A estas letras se las llama variables proposicionales, y en general se toman del alfabeto latino, empezando por la letra p (de _«proposición»_) luego q, r, s, etc. Es así que los dos
primeros argumentos de esta sección se podrían reescribir así:

1. p o q.
2. No q.
3. Por lo tanto, p.

Y el tercer argumento, a pesar de no ser válido, se puede reescribir así:

1. Ni p ni q
2. No q
3. Por lo tanto, p

### Conectivas lógicas

A continuación hay una tabla que despliega todas las conectivas lógicas que ocupan a la lógica proposicional, incluyendo ejemplos de su uso en el lenguaje natural y los símbolos que se utilizan para representarlas en lenguaje formal.


| Conectiva            | Expresión en el lenguaje natural | Ejemplo                                      | Símbolo |
| -------------------- | -------------------------------- | -------------------------------------------- | ------- |
| Negación             | no                               | No esta lloviendo                            | ¬       |
| Conjunción           | y                                | Esta lloviendo y esta nublado                | ⋀       |
| Disyunción           | o                                | Esta lloviendo o esta soleado                | ⋁       |
| Condicional material | si...entonces                    | Si esta soleado, entonces es de día          | →       |
| Bicondicional        | si y solo si                     | Esta nublado si y solo si hay nubes visibles | ↔       |
| Disyunción opuesta   | ni...ni                          | Ni esta soleado ni esta nublado              | ↓       |
| Disyunción exclusiva | o bien...o bien                  | O bien esta soleado, o bien esta nublado     |↮|


En la lógica proposicional, las conectivas lógicas se tratan como funciones de verdad. Es decir, como funciones que toman conjuntos de valores de verdad y devuelven valores de verdad. Por ejemplo, la conectiva lógica _«no»_ es una función que si toma el valor de verdad V, devuelve F, y si toma el valor de verdad F, devuelve V. Por lo tanto, si se aplica la función «no» a una letra que represente una proposición falsa, el resultado será algo verdadero. Si es falso que «está lloviendo», entonces será verdadero que «no está lloviendo». El significado de las conectivas lógicas no es nada más que su comportamiento como funciones de verdad. Cada conectiva lógica se distingue de las otras por los valores de verdad que devuelve frente a las distintas combinaciones de valores de verdad que puede recibir. Esto quiere decir que el significado de cada conectiva lógica puede ilustrarse mediante una tabla que despliegue los valores de verdad que la función devuelve frente a todas las combinaciones posibles de valores de verdad que puede recibir.

## Negacion

| 𝟇   | ¬𝟇  |
| --- | --- |
| F   | V   |
| V   | F    |

## Conjunción

| 𝟇   | 𝝍   | 𝟇 ⋀ 𝝍 |
| --- | --- | ----- |
| V   | V   | V     |
| F   | V   | F     |
| V   | F   | F     |
| F   | F   | F      |

## Disyunción

| 𝟇   | 𝝍   | 𝟇 ⋁ 𝝍 |
| --- | --- | ----- |
| V   | V   | V     |
| F   | V   | V     |
| V   | F   | V     |
| F   | F   | F      |

## Condicional

| 𝟇   | 𝝍   | 𝟇 → 𝝍 |
| --- | --- | ----- |
| V   | V   | V     |
| F   | V   | V     |
| V   | F   | F     |
| F   | F   | V      |

## Bicondicional

| 𝟇   | 𝝍   | 𝟇 ↔ 𝝍 |
| --- | --- | ----- |
| V   | V   | V     |
| F   | V   | F     |
| V   | F   | F     |
| F   | F   | V      |

## Disyunción exclusiva

| 𝟇   | 𝝍   | 𝟇 ↮ 𝝍 |
| --- | --- | ----- |
| V   | V   | F     |
| F   | V   | V     |
| V   | F   | V     |
| F   | F   | F      |

# Límites de la lógica proposicional

La maquinaria de la lógica proposicional permite formalizar y teorizar sobre la validez de una gran cantidad de argumentos. Sin embargo, también existen argumentos que son intuitivamente válidos, pero cuya validez no se puede probar por la lógica proposicional. Por ejemplo, considérese el siguiente argumento:

1. Todos los hombres son mortales.
2. Sócrates es un hombre.
3. Por lo tanto, Sócrates es mortal.

Como este argumento no contiene ninguna de las conectivas «no», «y», «o», etc., según la lógica proposicional, su formalización será la siguiente:

1. p.
2. q.
3. Por lo tanto, r.

Pero esta es una forma de argumento inválida, y eso contradice nuestra intuición de que el argumento es válido. Para teorizar sobre la validez de este tipo de argumentos, se necesita investigar la estructura interna de las variables proposicionales. De esto se ocupa la lógica de primer orden. Otros sistemas formales permiten teorizar sobre otros tipos de argumentos. Por ejemplo la lógica de segundo orden, la lógica modal y la lógica temporal.

#### Semántica

Una interpretación para un sistema de lógica proposicional es una asignación de valores de verdad para cada variable proposicional, sumada a la asignación usual de significados para los operadores lógicos. A cada variable proposicional se le asigna uno de dos posibles valores de verdad: o V (verdadero) o F (falso). Esto quiere decir que si hay n variables proposicionales en el sistema, el número de interpretaciones distintas es de 2$^n$.

Partiendo de esto es posible definir una cantidad de nociones semánticas. Si A y B son fórmulas cualquiera de un lenguaje L, 𝐫 es un conjunto de fórmulas de L, y M es una interpretación de L, entonces:{' '}

- A es verdadera bajo la interpretación M si y sólo si M asigna el valor de verdad V a A.
- A es falsa bajo la interpretación M si y sólo si M asigna el valor de verdad F a A.
- A es una tautología (o una verdad lógica) si y sólo si para toda interpretación M, M asigna el valor de verdad V a A.
- A es una contradicción si y sólo si para toda interpretación M, M asigna el valor de verdad F a A.
- A es satisfacible (o consistente) si y sólo si existe al menos una interpretación M que asigne el valor de verdad V a A.
- 𝐫 es consistente si y sólo si existe al menos una interpretación que haga verdaderas a todas las fórmulas en 𝐫.
- A es una consecuencia semántica de un conjunto de fórmulas 𝐫 si y sólo si no existe interpretación en la que todas las fórmulas que pertenecen a 𝐫 sean verdaderas y A sea falsa. Cuando A es una consecuencia semántica de 𝐫 en un lenguaje L, se escribe: 𝐫 ⊨ L A.
- A es una verdad lógica si y sólo si A es una consecuencia semántica del conjunto vacío. Cuando A es una verdad lógica de un lenguaje L, se escribe: ⊨ L A.