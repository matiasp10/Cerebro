Las expresiones `let` permiten introducir _**vinculaciones temporales**_ dentro de una expresión. Es decir, puedes definir nombres locales y asignarles valores, y luego usar esos nombres dentro de la expresión principal. Las vinculaciones solo tienen efecto dentro del bloque delimitado por `in` y `end`.
# Sintaxis

- `let b1 b2 … bn in e end`
    - `b1`, `b2`, ..., `bn` son las _vinculaciones_.
    - Cada vinculación puede ser:
        - Una _definición de variable_ (`x = e1`).
        - Una _definición de función_ (`f = fun (x) -> e2`).
    - `e` es la _expresión principal_.

# Verificación de tipos

Se realiza en un _entorno estático que incluye las vinculaciones definidas previamente_. Esto **permite usar nombres de vinculaciones anteriores dentro de las posteriores** y dentro de la expresión principal.

# Evaluación

1. Se **evalúan las vinculaciones** (de izquierda a derecha) y se **asocian los valores a los nombres**.
2. Se **evalúa la expresión principal en un entorno dinámico que incluye las vinculaciones evaluadas**.

# Ejemplo

```sml
let x = 3 + 4 in
 let y = x * 2 in
  x + y
end
```

## Explicación

1. Se calcula `3 + 4` y se asigna el valor 7 a `x`.
2. Se calcula `x * 2` usando el valor de `x` (7) y se asigna el valor 14 a `y`.
3. Se evalúa `x + y` usando los valores de `x` (7) y `y` (14), lo que resulta en 21.

# Ejemplos adicionales

## Función con variable local

```sml
fun silly1 (z : int) =
 let val x = if z > 0 then z else 34
	 val y = x+z+9
 in
	 if x > y then x*2 else y*y
 end
```

## Expresiones `let` anidadas

```sml
fun silly2 () =
 let val x = 1
 in
	 (let val x = 2 in x+1 end) +
	 (let val y = x+2 in y+1 end)
 end
```

# Recomendaciones

- Prefiera **funciones pequeñas y enfocadas para mejorar la legibilidad**.
- Use `let` de **manera moderada y evite el sombreado innecesario de variables**.
- Usar `let` para definir variables locales que se usan en un corto bloque de código.

# Alcance de las expresiones `let`

Las expresiones `let` en SML permiten definir **vinculaciones locales** dentro de una expresión. Esto significa que puedes crear variables y funciones que solo son accesibles dentro del bloque delimitado por `in` y `end`.

## Novedades del alcance

Las expresiones `let` en SML introducen un concepto clave: el **alcance**. Las características principales del alcance son:

- **Las vinculaciones solo son accesibles dentro del bloque `let`:** Las variables y funciones definidas dentro de un `let` _no son accesibles fuera del mismo_.
- **Acceso a las definiciones anteriores:** Las vinculaciones definidas dentro de un `let` _pueden acceder a las definiciones previas dentro del mismo_ `let`.
- **Sombreado:** Si se define una variable con el mismo nombre que una variable anterior, la nueva definición **oculta** la anterior dentro del bloque `let`.

### Ejemplo

```sml
let x = 3
in
 let y = x * 2
 in
  x + y
end
```

En este ejemplo:

- La variable `x` se define en el primer `let`, por lo que _solo está disponible dentro de ese bloque y el segundo_ `let`.
- La variable `y` se define en el segundo `let`, por lo que _solo está disponible dentro de ese bloque_.
- La expresión `x + y` puede acceder a _ambas variables ya que están dentro de su alcance_.

# Ventajas de las expresiones `let`

- **Modularidad:** Permiten dividir el código en bloques más pequeños y manejables.
- **Legibilidad:** Ayudan a mejorar la claridad del código al nombrar variables locales.
- **Eficiencia:** Se pueden usar para evitar cálculos repetidos al almacenar resultados intermedios.

# Ejemplos adicionales

#### Función con variable local

```sml
fun silly1 (z : int) =
 let val x = if z > 0 then z else 34
	 val y = x+z+9
 in
	 if x > y then x*2 else y*y
 end
```

#### Expresiones `let` anidadas

```sml
fun silly2 () =
 let val x = 1
 in
	 (let val x = 2 in x+1 end) +
	 (let val y = x+2 in y+1 end)
 end
```

# Enlaces locales

Las expresiones `let` no solo permiten definir variables locales, sino también **enlaces locales**. Un enlace puede ser una variable, una función o cualquier otro tipo de valor.

# Eficiencia

Las expresiones `let` se pueden usar para evitar cálculos repetidos. Al almacenar el resultado de un cálculo en una variable local, se puede evitar recalcularlo cada vez que se necesita.

# Ejemplos adicionales

#### Función con función local

```sml
fun silly3 (z : int) =
 let fun f (x : int) = x + z
 in
	 f(3) + f(4)
 end
```

#### Expresiones `let` para evitar cálculos repetidos

```sml
fun sum_list (xs : int list)
```

# Funciones anidadas en expresiones `let`

Las expresiones `let` en SML permiten definir **vinculaciones temporales**, incluyendo **funciones**, dentro de una expresión. Esta capacidad ofrece varias ventajas en cuanto a modularidad, alcance local y reutilización de código.

## Ventajas de las funciones anidadas

- **Modularidad:** Permiten dividir el código en bloques más pequeños y manejables, encapsulando la lógica relacionada con un área específica.
- **Alcance local:** Las funciones anidadas solo son accesibles dentro del bloque `let` donde se definen, evitando posibles conflictos de nombres y asegurando un uso preciso y contextual.
- **Reutilización:** Si una función es necesaria en varios lugares del código, definirla dentro de un `let` común permite reutilizarla sin necesidad de duplicar código.

## Cuándo usar funciones anidadas

- **Funciones "ayudantes":** Si una función solo se usa dentro de otra para una tarea específica, definirla como anidada puede mejorar la organización y legibilidad del código. Estas funciones tienen un alcance local y no se pueden llamar desde afuera, evitando conflictos de nombres.
- **Funciones "poco reutilizables":** Si una función es poco probable que se use en otras partes del código, definirla como anidada evita crear funciones innecesarias que aumentan la complejidad.
- **Funciones temporales:** Si una función solo se necesita en una parte específica del código y es probable que cambie o desaparezca en el futuro, definirla como anidada puede mantener el código modular y adaptable.
### Ejemplo

```sml
let square (x : int) = x * x
in
 let y = square(5)
 in
  y + 1
end
```

En este ejemplo:

- Se define la función `square` dentro del `let` externo.
- La función solo está disponible dentro del bloque `let`.
- Se calcula el cuadrado de 5 y se suma 1 al resultado.

## Consideraciones de estilo

Si bien las funciones anidadas son útiles, es importante usarlas con moderación. Un exceso de anidamiento puede dificultar la legibilidad del código. Se recomienda:

- Preferir funciones pequeñas y bien definidas.
- Buscar un equilibrio entre modularidad y claridad.

### Ejemplo adicional

```sml
fun countup_from1 (x : int) =
 let fun count (from : int, to : int) =
	 if from = to
	 then to :: []
	 else from :: count(from+1,to)
 in
	 count (1,x)
 end
```

Este ejemplo muestra una función `countup_from1` que utiliza una función auxiliar `count` definida dentro de un `let` local.

## Mejora del estilo

Observamos que la función `count` no utiliza la variable `x`. En este caso, podemos mejorar el estilo definiendo `count` como una función local sin parámetros:

```sml
fun countup_from1_better (x : int) =
 let fun count (from : int) =
	 if from = x
	 then x :: []
	 else from :: count(from+1)
 in
	 count 1
 end
```

- Las funciones pueden utilizar vinculaciones del entorno en el que están definidas:
	- Vinculaciones de entornos "externos"
		- Como parámetros de la función externa
	- Vinculaciones anteriores en la expresión `let`
• Los parámetros innecesarios suelen ser un mal estilo de programación.
## Acceso a variables del entorno

Las funciones anidadas pueden acceder a las variables del entorno en el que se definen. Esto incluye:

- Variables del bloque `let` donde se define la función.
- Variables de bloques `let` externos, siempre que no haya un nombre oculto.

## Uso de parámetros vs. acceso al entorno

En general, se recomienda evitar el uso de parámetros innecesarios en las funciones. En la mayoría de los casos, es mejor acceder a las variables necesarias desde el entorno en el que se define la función.

### Ejemplo de función recursiva anidada

```sml
fun factorial (n : int) =
 let fun fact (n : int, acc : int) =
	 if n = 0
	 then acc
	 else fact(n-1, n*acc)
 in
	 fact(n, 1)
 end
```

En este ejemplo, la función `factorial` utiliza una función auxiliar recursiva `fact` para calcular el factorial de un número.

### Ejemplo de función de orden superior anidada

```sml
fun map (f : int -> int, xs : int list) =
 let fun mapi (i : int, xs : int list) =
	 if null xs
	 then []
	 else f(i) :: mapi(i
```

# Evitar la recursividad repetida

```sml
fun bad_max (xs : int list) =
	 if null xs
	 then 0 (* horrible style; fix later *)
	 else if null (tl xs)
	 then hd xs
	 else if hd xs > bad_max (tl xs)
	 then hd xs
	 else bad_max (tl xs)
let x = bad_max [50,49,…,1]
let y = bad_max [1,2,…,50]
```

El código `bad_max` es un ejemplo de cómo **no** escribir código eficiente. La función realiza llamadas recursivas innecesarias, lo que puede llevar a un rendimiento terrible para listas grandes.

## Analicemos el problema

- La función `bad_max` calcula el máximo de una lista de enteros.
- La función realiza llamadas recursivas a sí misma para calcular el máximo de la cola de la lista.
- **Problema:** La función calcula el máximo de la cola de la lista **dos veces** en cada llamada recursiva.

## Ejemplo

Supongamos que queremos calcular el máximo de la lista `[1, 2, 3, 4, 5]`.

- La primera llamada recursiva calcula el máximo de la cola `[2, 3, 4, 5]`.
- La segunda llamada recursiva calcula el máximo de la cola `[3, 4, 5]`.
- **Problema:** La función calcula el máximo de la cola `[3, 4, 5]` **dos veces**: una vez en la primera llamada recursiva y otra vez en la segunda llamada recursiva.

### Rápido vs Inusable

```sml
if hd xs > bad_max (tl xs)
then hd xs
else bad_max (tl xs)
```

- **Rápido:** Este enfoque podría parecer más rápido inicialmente. Compara la cabeza con el máximo en la cola **solo una vez** por llamada recursiva.
- **Inutilizable:** Sin embargo, teniendo en cuenta la ineficiencia de `bad_max`, este enfoque se vuelve inutilizable para listas grandes. Los cálculos repetidos dentro de `bad_max` ralentizarían significativamente el proceso.
## Solución

Podemos usar una expresión `let` para evitar calcular el máximo de la cola de la lista dos veces. La idea es almacenar el resultado de la primera llamada recursiva en una variable local y luego usarla en la segunda llamada recursiva.

## Código mejorado

```sml
fun good_max (xs : int list) =
	if null xs
	then 0 (* horrible style; fix later *)
	else if null (tl xs)
	then hd xs
	else
		let val tl_ans = good_max (tl xs)
		in
			if hd xs > tl_ans
			then hd xs
			else tl_ans
		end
```

## Explicación

- La variable local `tl_ans` almacena el resultado de la llamada recursiva `good_max (tl xs)`.
- La segunda llamada recursiva usa la variable `tl_ans` para evitar calcular el máximo de la cola de la lista dos veces.

![[langprogfastvsunusable|center|700]]
## Las Matemáticas No Mienten

Imagínate que la lógica condicional y las llamadas a `hd`, `null` y `tl` dentro de una llamada a `bad_max` tardan aproximadamente de 10 a 7 segundos. En ese caso:

- `bad_max [50,49,…,1]` tomaría 50 x 10-7 segundos, aproximadamente 0.35 segundos.
- Pero `bad_max [1,2,…,50]` tardaría la exorbitante cifra de 1.12 x 10^8 segundos, ¡más de 3.5 años!
- Y para `bad_max [1,2,…,55]`, el tiempo de ejecución superaría un siglo entero.

Comprar un ordenador más rápido no te salvará.

La clave está en **evitar el trabajo repetitivo que, a su vez, podría generar más trabajo repetitivo, y así sucesivamente**. Aquí es donde resulta **esencial guardar los resultados de las llamadas recursivas en variables locales**.
#### Matemática eficiente

```sml
fun good_max (xs : int list) =
	 if null xs
	 then 0 (* horrible style; fix later *)
	 else if null (tl xs)
	 then hd xs
	 else
		 let val tl_ans = good_max(tl xs)
		 in
			 if hd xs > tl_ans
			 then hd xs
			 else tl_ans
		 end
```
#### RAPIDO vs rápido

```sml
(* RAPIDO *)
let val tl_ans = good_max(tl xs)
in
	 if hd xs > tl_ans
	 then hd xs
	 else tl_ans
end

(* rapido *)
if hd xs > bad_max (tl xs)
then hd xs
else bad_max (tl xs)
```

![[langprogfastvsfast|700|center]]