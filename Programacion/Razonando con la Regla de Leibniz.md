La regla de Leibniz nos permite sustituir iguales por iguales en una expresión sin cambiar el valor de la expresión. Esto nos provee un método para demostrar que dos expresiones son iguales. En este método, el formato que utilizaremos será el siguiente:
$$ = E [z:= X] <X = Y> E[z := Y] $$
La primera y la última línea corresponden a la expresión de igualdad de la conclusión en la regla de Leibniz, la explicación entre los signos `< >` corresponde a la premisa $X = Y$ . Aquí ilustramos la regla de Leibniz para el problema enunciado en el Capítulo 0 sobre las manzanas de Juan y María. Recordemos el modelo asociado al problema:
$$m = 2j \ \ {y} \ \ m/2 = 2 · (j − 1)$$
entonces
$$ = m / 2 = 2 . (j - 1) < m = 2 . j > 2 . j / 2 = 2 . (j - 1) $$En este caso $E$ es la expresión $z/2 = 2 · (j − 1)$, $X$ es $m$ e $Y$ es $2 · j$. Veamos otro ejemplo de aplicación de (1.5). Supongamos que sabemos que la siguiente expresión es un teorema:
$$
2 · x/2 = x
$$
el siguiente cálculo utiliza las reglas (1.5) y (1.1):
$$
	= 2.j/ 2 = 2.(j-1) < (1.17) con x := j > j = 2.(j-1)
$$
Estamos usando Leibniz con la premisa $2 · j/2 = j$. Podemos usar esta premisa sólo en el caso de que se trate de un teorema, pero suponemos que (1.7) lo es y entonces por (1.1), resulta que $(2 · x/2 = x) [x := j]$ es también un teorema. Si el uso de la sustitución es suficientemente obvio, como en este caso, podemos abreviar la explicación entre `< >`, del siguiente modo:
$$
2.j/2 = 2.(j-1) <2.x /2 = x> j = 2 . (j-1)
$$
También podemos agregar un comentario aclaratorio después de un guion así:
$$
< 2.x / 2 = x - \rm{el\ simbolo \ "/" \ significa \ "divide \ a"}>
$$
Cualquier demostración que involucre una sucesión de aplicaciones de la regla de Leibniz, tendrá la siguiente forma:

$E_0$ = < Argumento a favor de $E_0 = E_1$, usando Leibniz >
$E_1$ = < Argumento a favor de $E_1 = E_2$, usando Leibniz >
$E_2$ = < Argumento a favor de $E_2 = E_3$, usando Leibniz >
$E_3$ = Los pasos individuales $E_0 = E_1$, $E_1 = E_2$ y $E_2 = E_3$ y la transitividad (regla (1.4)), demuestran que $E_0 = E_3$.
