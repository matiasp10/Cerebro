Sean $g$ y $f$ _funciones_, la composición de $g$ con $f$ , denotada por $f ◦ g$ (se lee **”g compuesta con f ”**) es la función cuyo dominio es el conjunto 

$$
\huge A = \left\{x ∈ D_g : g(x) ∈ D_f \right\}
$$

cuya regla de correspondencia es $\large (f ◦ g)(x) = f(g (x))$.

![[funciones6|600|center]]

Aquí suponemos que $g$ tiene dominio en $X$ y rango en $Y$ y $f$ tiene dominio en $Y$ y rango en $Z$, entonces $f ◦ g$ tiene dominio en $X$ y rango en $Z$. El dominio de $f ◦ g$ son los elementos de $X$ cuya imagen $g (x)$ está en $D_f$ .

> [!example] Ejemplo
> ![[funciones7|500|center]]
> Para este ejemplo $\large A = {x ∈ D_g : g(x) ∈ D_f } = {2, 3}$, Luego tenemos
> $$
> \huge (f ◦ g) (2) = f(g (2)) = f (0) = 6, (f ◦ g) (3) = 8
> $$
> 
> Observemos que $\large (f ◦ g) (1)$ y $\large (f ◦ g) (4)$ no están definidas.

> [!example] Ejemplo
> Consideremos las funciones $f, g : \mathbb{R} → \mathbb{R}$ definidas por $f(x) = x + 1$ y $g(x) = x^2$ , entonces
> $$
> \huge (f ◦ g)(x) = f(g(x)) = f(x^2 ) = x^2 + 1
> $$
> y
> $$
> \huge (g ◦ f)(x) = g(f(x)) = g(x + 1) = (x + 1)^2
> $$

Observemos que $f ◦ g \neq g ◦ f$, en general la igualdad no es válida.

> [!hint] Teorema
> Si $f$ $g$ y $h$ son funciones. Se verifica:
> - $(f ◦ g) ◦ h = f ◦ (g ◦ h)$
> - $I ◦ f = f ◦ I$, donde $I$ es la función identidad
> - $(f + g) ◦ h = f ◦ h + g ◦ h$
> - $(fg) ◦ h = (f ◦ h)(g ◦ h)$


https://www.superprof.es/apuntes/escolar/matematicas/calculo/funciones/composicion-de-funciones.html
http://agrega.juntadeandalucia.es/repositorio/04022015/7b/es-an_2015020413_9134142/composicin_de_funciones.html#:~:text=En%20%C3%A1lgebra%20abstracta%2C%20una%20funci%C3%B3n,aplica%20finalmente%20la%20funci%C3%B3n%20restante.