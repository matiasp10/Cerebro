Las **listas** son una estructura de datos fundamental en ML que **permite agrupar un número variable de elementos del mismo tipo**. Son más flexibles que los pares y las tuplas porque su longitud no está predeterminada.

# Definición

- La lista vacía se escribe `[]` y tiene el tipo `'a list` para cualquier tipo `'a`.
- Una lista no vacía con `n` elementos se escribe `[v1, v2, ..., vn]`, donde cada `vi` es un valor de tipo `'a`.
- También se puede construir una lista con la expresión `e1 :: e2`, donde:
    - `e1` se evalúa a un valor de tipo `'a`.
    - `e2` se evalúa a una lista de valores de tipo `'a`.
    - El resultado es una nueva lista que comienza con el valor de `e1` seguido de todos los elementos de `e2`.

# Funciones sobre listas

ML proporciona algunas funciones básicas para trabajar con listas:

- `null`: Devuelve `true` si **la lista está vacía** y `false` si no.
- `hd`: Devuelve **el primer elemento de la lista** (excepción si está vacía).
- `tl`: Devuelve **la cola de la lista** (excepción si está vacía).

## Ejemplos de funciones que usan listas

```sml
fun sum_list (xs : int list) =
  if null xs then 0 else hd(xs) + sum_list(tl xs)

fun countdown (x : int) =
  if x = 0 then [] else x :: countdown(x - 1)

fun append (xs : int list, ys : int list) =
  if null xs then ys else (hd xs) :: append(tl xs, ys)
```

# Funciones recursivas y listas

Las funciones que trabajan con listas a menudo son **recursivas**, ya que la longitud de la lista puede ser desconocida. El proceso de escribir una función recursiva sobre listas implica:

- **Caso base:** _Definir la respuesta para una lista vacía_.
- **Caso recursivo:** _Expresar la respuesta para una lista no vacía_ en términos de la respuesta para el resto de la lista (la cola).

## Combinando pares y listas

Se pueden combinar pares y listas de forma flexible. Por ejemplo:

```sml
fun sum_pair_list (xs : (int * int) list) =
  if null xs then 0 else #1(hd xs) + #2(hd xs) + sum_pair_list(tl xs)

fun firsts (xs : (int * int) list) =
  if null xs then [] else (#1(hd xs)) :: (firsts(tl xs))

fun seconds (xs : (int * int) list) =
  if null xs then [] else (#2(hd xs)) :: (seconds(tl xs))

fun sum_pair_list2 (xs : (int * int) list) =
  (sum_list (firsts xs)) + (sum_list (seconds xs))
```

# Reutilización de código y abstracción

Las funciones sobre listas se pueden reutilizar para crear soluciones más complejas. En el ejemplo anterior, `sum_pair_list2` reutiliza `firsts` y `seconds` para evitar duplicar código.