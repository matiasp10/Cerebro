En ML, los programas son secuencias de enlaces. Ya hemos visto los enlaces de variables; ahora nos centraremos en los **enlaces de funciones**, que permiten definir y usar funciones.
___
## Definición de funciones

Una función es similar a un método en Java: **se llama con argumentos y tiene un cuerpo que produce un resultado**. A diferencia de los métodos, no hay clases ni declaraciones de retorno.

### Ejemplo

```sml
fun pow (x:int, y:int) = (* solo correcto para y >= 0 *)
  if y = 0
  then 1
  else x * pow(x, y - 1)
```

Esta función calcula `x^y` suponiendo que `y ≥ 0`.

## Sintaxis

La sintaxis de un enlace de función es:

```sml
fun x0 (x1 : t1, ..., xn : tn) = e
```

Donde:

- `x0` es el **nombre de la función**.
- `x1`, ..., `xn` son los **nombres de los argumentos**.
- `t1`, ..., `tn` son los **tipos de los argumentos**.
- `e` es la **expresión que define el cuerpo de la función**.

## Comprobación de tipos

Para verificar el tipo de una función:

1. Se **verifica el tipo** del cuerpo `e` en un _entorno estático_ que incluye:
    - Todos los enlaces anteriores.
    - `x1` a `t1`, ..., `xn` a `tn`.
    - `x0` a `t1 * ... * tn -> t`.
2. El tipo de la función es `t1 * ... * tn -> t`.

## Evaluación

La evaluación de un enlace de función es simple:

- La función _se añade al entorno como un valor_.
- `x0` se _añade al entorno dinámico_ con el tipo `t1 * ... * tn -> t`.

## Llamadas a funciones

La sintaxis de una llamada a función es:

```sml
e0 (e1, ..., en)
```

Donde:

- `e0` es la **expresión que devuelve la función**.
- `e1`, …, `en` son los **argumentos de la función**.

## Reglas de tipado

1. `e0` debe tener un **tipo similar** a `t1 * ... * tn -> t`.
2. `ei` debe tener el **tipo `ti`** para `1 ≤ i ≤ n`.

## Reglas de evaluación

1. Se evalúa `e0` a `v0`.
2. Se evalúan `e1`, ..., `en` a `v1`, ..., `vn`.
3. Se comprueba que `v0` es una función.
4. Se evalúa el cuerpo de la función en un entorno que incluye:
    - El entorno donde se definió la función.
    - `x1` a `v1`, ..., `xn` a `vn`.

## Ejemplo

```sml
fun pow (x:int, y:int) = (* solo correcto para y >= 0 *)
  if y = 0
  then 1
  else x * pow(x, y - 1)

fun cube (x:int) =
  pow(x, 3)

val ans = cube(4)
```

Este código produce un entorno donde `ans` es 64.

## Puntos clave

- Los **_enlaces_** de funciones **definen funciones con nombre, argumentos y un cuerpo**.
- La **_sintaxis_** de las funciones incluye el **nombre, los tipos de los argumentos y la expresión del cuerpo**.
- La **_comprobación de tipos_** verifica que **la expresión del cuerpo tenga el tipo correcto**.
- La **_evaluación_** de una función **crea un nuevo entorno con los argumentos**.
- Las llamadas a funciones **evalúan la expresión de la función en un entorno adecuado**.