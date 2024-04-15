La mayoría de la gente piensa en "números" y "operaciones con números" cuando oye "aritmética". "Operaciones con números" significa sumar dos números para obtener un tercero, restar un número de otro, determinar el máximo común divisor de dos números y muchas cosas más. Si no nos tomamos la aritmética demasiado al pie de la letra, podemos incluir incluso el seno de un ángulo, el redondeo de un número real al entero más próximo, etc.

El lenguaje BSL soporta Números y aritmética sobre ellos. Como se discutió en el Prólogo, una operación aritmética como + se usa así:

```sml
(+ 3 4)
```

es decir, en forma de notación prefija. 

BSL ofrece una amplia variedad de operaciones aritméticas, incluyendo:

- Suma `(+)`
- Resta `(-)`
- Multiplicación `(*)`
- División `(/)`
- Valor absoluto `(abs)`
- Máximo común divisor `(gcd)`
- Seno `(sin)`
- Redondeo `(floor, ceiling)`
- Y muchas más

Puedes encontrar una lista completa de las operaciones disponibles en la documentación de BSL. [Documentacion](https://docs.racket-lang.org/htdp-langs/beginner.html)

Digamos que necesitas calcular el seno de un ángulo; prueba con

```sml
> (sin 0)
0
```

y úsalo felizmente para siempre. Allí encontrará que, además de las operaciones, el BSL también reconoce los nombres de algunos números muy utilizados, por ejemplo, pi y e.

> [!info] e
> Puede que conozcas e por el cálculo. Es un número real, cercano a 2,718, llamado **"constante de Euler"**.

BSL soporta diferentes tipos de números, incluyendo:

- **Naturales** (números enteros positivos)
- **Enteros** (números positivos, negativos y cero)
- **Racionales** (números que pueden expresarse como fracciones)
- **Reales** (números con decimales)
- **Complejos** (números con una parte real y una parte imaginaria)
 
Suponemos que ha oído hablar de todos menos del último. Si no es así, no se preocupe; aunque los números complejos son útiles para todo tipo de cálculos, un principiante no tiene por qué conocerlos.

Una distinción verdaderamente importante se refiere a la **precisión de los números**. Por ahora, es importante entender que BSL distingue entre **números exactos** y **números inexactos**. 

Cuando calcula con números exactos, _BSL preserva esta precisión siempre que es posible_. Por ejemplo, (`/ 4 6`) produce la fracción exacta `2/3`, que **DrRacket** puede representar como una fracción propia, una fracción impropia o un decimal mixto.

Algunas de las operaciones numéricas de BSL _no pueden producir un resultado exacto_. Por ejemplo, usar la operación **sqrt** en 2 produce un _número irracional_ que no puede describirse con un número finito de dígitos. Dado que los ordenadores tienen un tamaño finito y que BSL debe hacer caber de algún modo tales números en el ordenador, opta por _una aproximación_: `1.4142135623730951`. El prefijo `#i` advierte a los programadores de esta falta de precisión. Aunque la mayoría de los lenguajes de programación optan por reducir la precisión de esta manera, pocos lo anuncian y aún menos advierten a los programadores.

> [!note] "Numero"
> La palabra **"número"** se refiere a una _amplia variedad de números_, incluidos los números para contar, los números enteros, los números racionales, los números reales e incluso los números complejos. 
> Para la mayoría de los usos, se puede equiparar **Number** con la recta numérica de la escuela primaria, aunque en ocasiones esta traducción es demasiado imprecisa. Si queremos ser precisos, utilizaremos las palabras adecuadas: Entero, Racional, etc. Incluso podemos refinar estas nociones utilizando términos estándar como `PositiveInteger`, `NonnegativeNumber`, `NegativeNumber`, etc.

____
## Ejercicio 1

Añade las siguientes definiciones para `x` e `y` al área de definiciones de **DrRacket**:

```sml
(define x 3)
(define y 4)
```

Imagina que `x` e `y` son las coordenadas de un punto cartesiano. Escribe una expresión que calcule la distancia de este punto al origen, es decir, un punto con las coordenadas `(0,0)`.
El resultado esperado para estos valores es `5`, pero tu expresión debería producir el resultado correcto incluso después de cambiar estas definiciones.

Por si no has tomado cursos de geometría o por si has olvidado la fórmula que encontraste allí, el punto `(x,y)` tiene la distancia

$$
\large \sqrt{x^2 + y^2}
$$

desde el origen. Al fin y al cabo, te estamos enseñando a diseñar programas, no a ser geómetra.

Para desarrollar la expresión deseada, lo mejor es hacer clic en EJECUTAR y experimentar en el área de interacciones. La acción EJECUTAR le dice a **DrRacket** cuáles son los valores actuales de `x` e `y` para que pueda experimentar con expresiones que involucren `x` e `y`:

```bsl
> x
3

> y
4

> (+ x 10)
13

> (* x y)
12
```

Una vez que tengas la expresión que produce el resultado correcto, cópiala del área de interacciones al área de definiciones.
Para confirmar que la expresión funciona correctamente, cambia `x` a `12` e `y` a `5`, luego haz clic en EJECUTAR. El resultado debería ser `13`.

### Soluciones 

```bsl
(define x 3)
(define y 4)

(sqrt(+(* x x)(* y y)))
```
