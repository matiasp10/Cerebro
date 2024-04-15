> [!definition]
> Sean $E$ y $F$ dos expresiones aritméticas y $x$ una variable en $E$. Sustituir $x$ por la expresión $F$ en $E$, significa reemplazar $x$ por $F$ en todas las ocurrencias de la variable $x$ en la expresión $E$. Esta operación da como resultado una nueva expresión aritmética que denotaremos $E [x := F]$.

Veamos a continuación algunos ejemplos:

> [!example]
> Si $E = (x + y)$ y sustituimos y por la expresión $F = (2 · z)$ entonces $E [y := F] = (x + (2 · z)) = x + 2 · z$. Observemos que hemos quitado los paréntesis, utilizando las reglas de precedencia ya mencionadas.

> [!example]
> Si $E = x$ y $F = (2 + z)$ entonces $E [x := F] = (2 + z) = 2 + z$. Esto último también puede expresarse así: $x [x := F] = 2 + z$.

> [!definition]
> La sustitución simultánea de una lista x de variables $x1, x2, . . . , xn$ por una lista $F$ de expresiones $F1, F2, . . . Fn$, que notaremos $E [x := F]$ se realiza mediante el reemplazo de la variable $x$ por las expresiones en $F$ cada una de ellas encerradas entre paréntesis, siguiendo como regla de correspondencia el orden y el número de variables.

> [!example]
> Si $E = x + z$, $F = z + 1$ y $G = 4$ entonces 
> $$E [x, z := F, G] = ((z + 1) + (4)) = z + 5$$
> o también 
> $$(x + z) [x, z := z + 1, 4] = ((z + 1) + (4)) = z + 5$$

> [!example]
> Es posible sustituir sucesivamente, por ejemplo 
> $$(x + z) [x := z + 1] [z := 4] = ((z + 1) + z) [z := 4] = ((4) + 1) + (4) = 9 $$
> Observemos que el resultado no es el mismo que en el caso de sustitución simultánea.

> [!example]
> Es posible sustituir una variable que no aparece en la expresión, en este caso dicha variable es ignorada, es decir
> $$(x + z) [x, w := z + 1, 4] = ((z + 1) + z) = 2z + 1$$

>[!hint] Convención
>La sustitución tiene mayor jerarquía que cualquier otra operación, es decir tiene precedencia sobre operaciones entre expresiones.
>

Por lo tanto en caso de que el orden deba alterarse, es necesario el uso de paréntesis, por ejemplo
$$x + z [x, z := z + 1, 4] = x + (z [x, z := z + 1, 4]) = x + (4) = x + 4$$
si quisiéramos realizar la sustitución indicada arriba en la expresión $E = x + z$, deberíamos utilizar paréntesis como se hizo en el ejemplo 6.

> [!info] Observación
> Es importante no confundir una sustitución con una evaluación. La primera consiste en el reemplazo de variables por expresiones, obteniendo así nuevas expresiones, la segunda en cambio obtiene un valor de una expresión a partir del estado determinado de cada una de las variables de la expresión.
> 

[[Sustitución y variables ocultas]]
[[La sustitución como regla de inferencia]]
[[Igualdad y sustitución. Regla de Leibniz]]
[[La regla de Leibniz y la evaluación de funciones]]
[[Razonando con la Regla de Leibniz]]
[[La sentencia de asignación]]