El concepto de función fue introducida en **matemáticas** por Leibniz.

Sean X, Y conjuntos. Una función es una correspondencia de los elementos de X con los elementos de Y tal que a cada $x ∈ X$ le corresponde un y solamente un elemento de Y.

> [!INFO] Ejemplo
> Sea X un conjunto de personas, Y = Z, (recuerde Z es el conjunto de enteros). Consideremos la siguiente correspondencia entre estos dos conjuntos: A cada persona de X le corresponde su edad. Claramente esta correspondencia es una función.

> [!INFO] Ejemplo
> Sea X = N, Y un conjunto de familias de cierta comunidad. Consideremos la siguiente correspondencia: A cada número de n ∈ N le corresponde una familia de Y con exactamente n miembros. Esta correspondencia en general no es una función pues pueden existir familias con el mismo número de miembros.

> [!question] Problema
> Si X es el conjunto de todas las familias y Y = N ¿es función la siguiente correspondencia?: A cada familia le corresponde el número de miembros de la familia.

Para denotar una función usaremos letras como f, g u otra letra. Si x ∈ X y a x le corresponde y ∈ Y , y la letra usada es f escribiremos

$$
	\huge f(x) = y \ ó \ x \ \underrightarrow{f} \ y
$$
y diremos que la “imagen” de x por la función f es f(x).

![[funciones1|center]]

Para decir que f es una función de X en Y escribiremos $\large f : X → Y$ , el conjunto X se llamará **dominio de f** y se denotará con **$Df$** , el conjunto Y se llamará **codominio de f** y se denotará con $Cf$ . Los valores de $y ∈ Y$ tales que son imágenes de algún $x ∈ X$ forman el conjunto que se llamará **rango de f** y se denotará con $Rf$, es claro que $R_f ⊂ C_f$ . Gráficamente:

![[funciones2|center]]

Observemos que ningún elemento del dominio de una función puede carecer de imagen. Finalmente observemos que una función $f : X → Y$ consta de tres partes:

1. El conjunto X llamado **dominio**. 
2. El conjunto Y llamado **codominio**. 
3. Una regla que permita asociar, de modo bien determinado (único) un elemento $x ∈ X$ con un elemento $\large y = f(x) ∈ Y$.

> [!abstract]- Definición formal de función
> Formalmente una función se define de la siguiente manera: 
> Sean X,Y conjuntos. Una función f de X en Y denotado por $f : X → Y$ es el conjunto de pares ordenados 
> $$\huge f = {(x, f (x)) : x ∈ Df }$$ 
> tales que:
> - Para todo $x ∈ X$, existe un $y ∈ Y$ tal que $f (x) = y$.
> - Para cualesquiera $x_0$, $x_1 ∈ X$, si $x_0 = x_1$ entonces $f (x_0) = f (x_1)$. 
>
>Observemos que $f ⊂ X × Y$ , además claramente: $(x, y) ∈ f$ significa $y = f(x)$.

> [!INFO] Ejemplo
> Sea $P$ el conjunto de todos los polígonos del plano, $\mathbb{R}$ el conjunto de números reales $y f : P → \mathbb{R}$ una función que asocia a cada polígono $x$ en $P$ su área $f(x)$.

> [!INFO] Ejemplo
> Sea $\mathbb{R}^+$ el conjunto de los reales positivos, $C$ el conjunto de cuadrados en el plano. $f : \mathbb{R}^+ → C$ es la correspondencia que a cada $x ∈ \mathbb{R}^+$ le hace corresponder un cuadrado en $C$ tal que su área sea $x$. Es claro que $f$ no puede ser función pues por ejemplo para $x = 1$ se tienen varios cuadrados como imagen como se muestra a continuación.
> 
> ![[funciones3|center]]
> 
> Del gráfico $f(1)$ es el cuadrado con vértices (0,0), (1,0), (1,1), (0,1), pero también $f(1)$ puede ser el cuadrado con vértices (0,2), (1,2), (1,3), (0,3) pues ambos cuadrados tienen área igual a 1.

> [!INFO] Ejemplo
> Sean $X = Y = \mathbb{R}$, considérese la función que asigna a cada elemento $x$ de $X$ el elemento $x^2$ de $Y$ , entonces tenemos $f(x) = x^2$ para cada $x ∈ \mathbb{R}$. El gráfico en coordenadas cartesianas es:
> ```functionplot
> ---
> title: 
> xLabel: 
>yLabel: 
>bounds: [-10,10,-10,10]
>disableZoom: false
> grid: true
> ---
>  f(x) = x^2
> ```

> [!question] Problema
> Dar un ejemplo de una correspondencia de conjuntos que no sea función.
> > [!success]- Solución
> >  Sea $A = {a, b, c}$, $B = {u, v}$. Consideremos la correspondencia
> >  
> >  $\large a \longrightarrow u$
> >  $\large b \longrightarrow v$
> >  $\large c \longrightarrow u$
> >  $\large c \longrightarrow v$
> >  
> >  No puede ser función pues $f(c) = u$ y $f(c) = v$, así el elemento $c$ tendría dos imágenes, lo que no está de acuerdo con la definición de función.

> [!question] Problema
> Sea $X = {a, b, c, d, }$, $Y = {u, v, w}$, ¿es función la siguiente correspondencia?
> 
> ![[funciones4|center]]
> 
> > [!success]- Solución
> >  No puede ser función pues $d ∈ X$ no tiene imagen en $Y$ . Si asignamos $f(d) = w$ obtenemos:
> >  
> >  ![[funciones5|center]]
> >
> > que es una función. Intuitivamente observemos que **del codominio X no pueden salir “dos flechas”** de un mismo elemento, sin embargo **a un elemento de Y pueden llegarle ”más de una flecha”** sin perder la condición de función.

# Funciones especiales

[[Función identidad]]
[[Función constante|Funciones constantes]]
[[Función valor absoluto|Función valor absoluto]]
[[Función lineal|Función lineal]]
[[Función potencia|Función potencia]]
[[Función polinomial|Función polinomial]]
[[Función trigonométrica|Función trigonométrica]]
[[Función exponencial|Función exponencial]]
[[Función logarítmica|Función logarítmica]]
[[Función mayor entero|Función mayor entero]]
[[Función hiperbólica|Función hiperbólica]]

## Ejercicios funciones

[[Ciencias de la computación/MSF - Fundamentos Matemáticos y Estadísticos/Calculo I/Ejercicios|Ejercicios]]

# Operaciones con funciones

En esta sección se definen las siguientes operaciones: **suma**, **resta**, **producto**, **división** y **composición**. Antes de empezar con este tema se define la igualdad de funciones.

> [!tip] Igualdad de funciones
> Dos funciones $f$ y $g$ son iguales, lo que escribimos $f = g$ si tienen un mismo dominio $D$ y $f(x) = g(x)$ para todo $x ∈ D$.

[[Suma y resta|Suma y resta de funciones]]
[[Producto y división|Producto y división]]
[[Reciproco de una función|Reciproco de una función]]
[[Composición de funciones|Composición de funciones]]

## Ejercicios operaciones con funciones

[[Ejercicios operaciones con funciones|Ejercicios]]

# Propiedades de las funciones

[[Simetría|Simetría]]
[[Crecimiento|Crecimiento]]

# Transformaciones de las funciones

Imaginemos que inicialmente tenemos graficada una función cualquiera y luego observamos que ésta está trasladada de posición (ya sea horizontalmente o verticalmente), comprimida (o dilatada) y reflejada en torno a un eje. La aplicación de estos procesos anteriores a una función cualquiera, se llama **transformación de funciones**.

[[Traslación|Traslación]]
[[Escalamiento|Escalamiento]]
[[Reflexión|Reflexión]]

## Transformaciones consecutivas

> [!tip] 
> Cuando tengas que aplicar _varias transformaciones_ sobre una función **comienza por** aquellas que afectan al **eje _x_**, y **termina por** las que tengan que ver con el **eje _y_**. Si la función está en la forma:
> $$\huge g(x) = (-) \frac{a}{b}.f((-)\frac{c}{d}x±e)h$$
> Deberás _**comenzar las transformaciones del eje x** **por el desplazamiento horizontal**_ (_±e_), y _**terminar las transformaciones del eje y** **por el desplazamiento vertical**_ (_±h_). El resto de transformaciones las puedes realizar en el orden que quieras, siempre que las del eje _x_ precedan a las del eje _y_.

# Funciones inyectivas, sobreyectivas y biyectivas

https://ozonocentrodeestudios.files.wordpress.com/2012/10/documento-extrac3addo-11.pdf

[[Función inyectiva|Función inyectiva]]
[[Función sobreyectiva|Función sobreyectiva]]
[[Función biyectiva|Función biyectiva]]

# Funciones inversas

[[Funciones inversas|Funciones inversas]]