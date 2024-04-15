El primer uso que le daremos a la sustitución es la sustitución como regla de inferencia, es decir la utilizaremos como un mecanismo sintáctico para derivar “verdades”, o teoremas. Veremos más adelante la definición de teorema pero por ahora diremos que un teorema es una proposición verdadera. Recordemos que una regla de inferencia consiste en un mecanismo por el cual bajo el supuesto de verdad de expresiones llamadas premisas se deriva la veracidad de otra expresión llamada conclusión. Es decir, una regla de inferencia asegura que si las premisas son teoremas, la conclusión también será un teorema. Aquí adoptaremos un formato especial para las reglas de inferencia en general: las premisas se describirán mediante una lista, una bajo la otra y luego de trazar una línea se escribirá la conclusión. La regla de inferencia de la sustitución utiliza una expresión E, una lista de variables v, y la correspondiente lista de expresiones F, así tenemos
$$Sustitucion : {E \over E [v := F]}$$
esta regla asegura que si E es un teorema, entonces también E es un teorema después de haber reemplazado todas las ocurrencias de v por las correspondientes expresiones de F.

> [!example]
> Supongamos que la expresión E que corresponde $a x + y = y + x$, es un teorema, la regla (1.1) nos permite concluir que $b + 3 = 3 + b$ es también un teorema. Esta última expresión no es más que $E [x, y := b, 3]$.

> [!example]
> Supongamos que la expresión $2 · x/2 = x$ es un teorema, de acuerdo a (1.1) podemos concluir que $(2 · x/2 = x) [x := j]$ es un teorema o bien $2 · j/2 = j$ es un teorema.

Observemos que una regla de inferencia como la sustitución, es un esquema que representa una infinidad de reglas, una para cada combinación de la expresión $E$, la lista de variables $v$, y la lista de expresiones $F$, podríamos considerar a $E$ y $x$ del ejemplo anterior y $F : j + 5$ y tendríamos:

$$2 · x/2 = x \over (2 · x/2 = x) [x := j + 5]$$
o bien

$$2 · x/2 = x \over 2 · (j + 5) /2 = j + 5$$