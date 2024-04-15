Los lenguajes de programación necesitan formas de construir datos complejos a partir de datos simples. En ML, los **pares** y las **tuplas** son dos herramientas fundamentales para este propósito.

____
# Pares

Un **par** es una estructura que **agrupa dos valores de cualquier tipo**. La sintaxis para crear un par es:

```sml
(e1, e2)
```

Donde:

- `e1` y `e2` son expresiones que se evalúan a los valores `v1` y `v2` respectivamente.
- El resultado es un par con el tipo `t1 * t2`, donde `t1` es el tipo de `v1` y `t2` es el tipo de `v2`.

## Acceso a los elementos de un par

Para acceder a los elementos de un par, se utilizan las expresiones especiales _`#1` y `#2`_.

- `#1 e` devuelve el **primer elemento** del par `e`.
- `#2 e` devuelve el **segundo elemento** del par `e`.

## Ejemplos

```sml
val p1 = (1, "Hola");
val x = #1 p1; (* x es 1 *)
val y = #2 p1; (* y es "Hola" *)

fun swap (pr : int*bool) =
  (#2 pr, #1 pr)

val p2 = swap(p1); (* p2 es ("Hola", 1) *)
```

# Tuplas

Las **tuplas** son una _generalización de los pares que permiten agrupar más de dos valores_. Una tupla con `n` elementos se define como:

```sml
(e1, ..., en)
```

Donde:

- `e1`, ..., `en` son **expresiones** que se evalúan a los valores `v1`, ..., `vn` respectivamente.
- El resultado es una tupla con el tipo `t1 * ... * tn`, donde `ti` es el tipo de `vi`.

## Acceso a los elementos de una tupla

Para acceder a los elementos de una tupla, se utilizan las expresiones _`#1`, `#2`, ..., `#n`_.

- `#i e` devuelve el **elemento `i` de la tupla `e`**.

## Ejemplos

```sml
val t1 = (7, 9, 11);
val x = #1 t1; (* x es 7 *)
val y = #2 t1; (* y es 9 *)
val z = #3 t1; (* z es 11 *)

fun div_mod (x : int, y : int) =
  (x div y, x mod y)

val (q, r) = div_mod(13, 4); (* q es 3 y r es 1 *)
```

# Anidamiento de pares y tuplas

Los pares y las tuplas **pueden anidarse entre sí**. Por ejemplo, la siguiente expresión es una tupla que contiene un par y un entero:

```sml
(7, (true, 9))
```

# Tipos de datos complejos

Los pares y las tuplas son **herramientas poderosas para construir tipos de datos complejos** a partir de tipos de datos simples. Esta flexibilidad es una de las características clave de los lenguajes de programación funcional como ML.