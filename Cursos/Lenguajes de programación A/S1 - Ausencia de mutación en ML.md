En **ML**, existe una característica fundamental que se destaca: la **ausencia de mutación**. Esto significa que no es posible modificar el contenido de un enlace, una tupla o una lista una vez que se han creado. Permíteme explicarte con más detalle:

1. **Inmutabilidad de datos**:
    
    - Si tenemos una variable `x` que corresponde a una lista de pares, como por ejemplo `[(3, 4), (7, 9)]`, en un entorno dado, esa lista siempre estará asociada a `x`. No existe una sentencia de asignación que cambie `x` para que apunte a una lista diferente.
    - Aunque podríamos introducir un nuevo enlace (variable) que haga sombra a `x`, esto no afectaría a ningún código que busque la `x` “original” en ese entorno.
    - Además, no hay ninguna sentencia que permita modificar la cabeza o la cola de una lista, ni cambiar el contenido de una tupla.
2. **Ventajas de la inmutabilidad**:
    
    - Esta característica es poderosa. ¿Por qué? Porque cuando escribes código en un lenguaje que no permite la mutación, puedes confiar en que ningún otro código alterará tus datos de manera inesperada.
    - La inmutabilidad es una de las principales contribuciones de la **programación funcional**. Algunas ventajas clave son:
        - **Robustez**: Tus datos permanecen consistentes y no se corrompen accidentalmente.
        - **Facilidad de razonamiento**: Al no preocuparte por cambios inesperados, puedes concentrarte en la lógica de tu programa.
        - **Facilita el paralelismo**: Los datos inmutables son más seguros para operaciones concurrentes.
3. **Compartir y utilizar alias**:
    
    - En este contexto, nos enfocaremos en una ventaja específica: la inmutabilidad hace que compartir y utilizar **alias** (múltiples referencias a los mismos datos) sea irrelevante.
    - En lenguajes donde los datos son mutables, compartir referencias puede ser peligroso, ya que un cambio en un lugar afecta a todas las referencias. Pero con datos inmutables, no hay riesgo de efectos secundarios inesperados.

```sml
fun sort_pair (pr : int*int) =
	if (#1 pr) < (#2 pr)
	then pr
	else ((#2 pr), (#1 pr))
```

En esta función llamada “sort_pair”, se toma un par de enteros como argumento (`pr`). Veamos cómo funciona:

1. **Comparación de los elementos del par**:
    
    - Primero, comparamos si el primer elemento del par (`#1 pr`) es menor que el segundo elemento (`#2 pr`).
    - Si es cierto (la condición `then`), simplemente devolvemos el mismo par (`pr`).
2. **Intercambio de elementos en caso contrario**:
    
    - Si la condición no se cumple (la condición `else`), creamos un nuevo par con los elementos intercambiados.
    - Es decir, el primer elemento del nuevo par es el segundo elemento del par original (`#2 pr`), y el segundo elemento del nuevo par es el primer elemento del par original (`#1 pr`).

Ahora, consideremos el siguiente fragmento de código:

```sml
val x = (3, 4)
val y = sort_pair x
```

Aquí, hemos creado un par `(3, 4)` y lo hemos asignado a la variable `x`. Luego, llamamos a la función `sort_pair` con `x` como argumento y asignamos el resultado a la variable `y`.

**¿Son `x` e `y` alias para el mismo par?**

- La respuesta es que **no podemos determinarlo con certeza**.
- En el contexto del aprendizaje automático, no existe una estructura que pueda afirmar si `x` e `y` son alias o no.
- Sin embargo, no hay motivos para preocuparse por la posibilidad de que lo sean.
- Si pudiéramos realizar mutaciones (cambios en los datos), la situación sería diferente.
- Imagina que pudiéramos decidir: “modificar el segundo elemento del par al que `x` está vinculado, para que contenga el número 5 en lugar de 4”.
- En ese caso, nos preguntaríamos si el número 2 ahora sería 4 o 5.

Eso es más eficiente que esta versión, que crearía otro par con exactamente el mismo contenido:

```sml
fun sort_pair (pr : int*int) =
	if (#1 pr) < (#2 pr)
	then (#1 pr, #2 pr)
	else ((#2 pr),(#1 pr))
```

Crear el nuevo par (#1 pr, #2 pr) es un mal estilo, ya que pr es más simple y funcionará igual de bien. Sin embargo, en lenguajes con mutación, los programadores hacen copias como esta todo el tiempo, exactamente para evitar alias donde hacer una asignación usando una variable como x provoca cambios inesperados al usar otra variable como y. En ML, ningún usuario de `sort_pair` puede saber si devolvemos un nuevo par o no.

En resumen, en ML, esperaríamos que el código anterior creara **alias**: al devolver `pr`, la función `sort_pair` devuelve un alias a su argumento original. Esto es más eficiente que crear otro par con exactamente el mismo contenido, como se muestra en la segunda versión del código.

En lenguajes con mutación, los programadores a menudo hacen copias como la segunda versión para evitar problemas con alias. Pero en ML, ningún usuario de `sort_pair` puede saber si se devuelve un nuevo par o no, lo que demuestra la potencia de la inmutabilidad en la programación funcional.

El segundo ejemplo:

```sml
fun append (xs : int list, ys : int list) =
    if null xs
    then ys
    else (hd xs) :: append(tl xs, ys)
```

Aquí está lo que está sucediendo:

1. **Verificación de la lista `xs`**:
    
    - Primero, verificamos si la lista `xs` está vacía (`null xs`).
    - Si está vacía (la rama “then”), simplemente devolvemos la lista `ys`.
2. **Construcción de una nueva lista en caso contrario**:
    
    - Si la lista `xs` no está vacía (la rama “else”), creamos una nueva lista.
    - Agregamos el primer elemento de `xs` al frente de la lista resultante (`(hd xs)`).
    - Luego, llamamos recursivamente a `append` con la cola de `xs` y la lista `ys` como argumentos (`append(tl xs, ys)`).

Ahora, consideremos el siguiente fragmento de código:

```sml
val x = [3, 4]
val y = append(x, [7, 9])
```

Aquí hemos creado una lista `[3, 4]` y la hemos asignado a la variable `x`. Luego, llamamos a la función `append` con `x` y `[7, 9]` como argumentos y asignamos el resultado a la variable `y`.

**¿Comparten `x` e `y` algún elemento?**

- La respuesta es que **no podemos determinarlo con certeza**.
- En el contexto de ML, no existe una estructura que pueda afirmar si `x` e `y` comparten elementos o no.
- Sin embargo, no hay motivos para preocuparse por la posibilidad de que lo hagan.
- La función `append` crea una nueva lista que “reutiliza” todos los elementos de `ys`.
- Ahorrar espacio es una ventaja de los datos inmutables, pero también lo es simplemente no tener que preocuparse por alias al escribir algoritmos elegantes.

En resumen, la programación funcional y la inmutabilidad nos permiten concentrarnos en la lógica del programa sin preocuparnos por efectos secundarios inesperados. Aunque no podemos rastrear el aliasing en este caso, la potencia de la inmutabilidad radica en su simplicidad y robustez.

En el programa Java análogo, esta es una pregunta crucial, por lo que los programadores de Java deben obsesionarse con cuándo se usan las referencias a objetos antiguos y cuándo se crean objetos nuevos. Hay momentos en los que obsesionarse con el aliasing es lo correcto y momentos en los que evitar la mutación es lo correcto; la programación funcional te ayudará a mejorar en esto último.

Para un ejemplo final, el siguiente código Java es la idea clave detrás de un agujero de seguridad real en una biblioteca Java importante (y posteriormente corregida). Supongamos que estamos manteniendo los permisos de quién puede acceder a algo como un archivo en el disco. Está bien permitir que todos vean quién tiene permiso, pero claramente solo aquellos que tienen permiso pueden usar el recurso. Considere este código incorrecto (se omiten algunas partes si no son relevantes):

```java
class ProtectedResource {
	private Resource theResource = ...;
	private String[] allowedUsers = ...;
	public String[] getAllowedUsers() {
		return allowedUsers;
	}
	public String currentUser() { ... }
	public void useTheResource() {
		for(int i=0; i < allowedUsers.length; i++) {
			if(currentUser().equals(allowedUsers[i])) {
				... // access allowed: use it
				return;
			}
		}
		throw new IllegalAccessException();
	}
}
```

¿Puedes encontrar el problema? Aquí está: `getAllowedUsers` devuelve un alias al array `allowedUsers`, por lo que cualquier usuario puede obtener acceso haciendo `getAllowedUsers()[0] = currentUser()`. ¡Uy! Esto no sería posible si tuviéramos algún tipo de array en Java que no permitiera actualizar su contenido. En cambio, en Java a menudo tenemos que recordar hacer una copia. La siguiente corrección muestra un ciclo explícito para mostrar en detalle qué se debe hacer, pero un mejor estilo sería usar un método de biblioteca como `System.arraycopy` o métodos similares en la clase `Arrays`; estos métodos de biblioteca existen porque la copia de arrays es necesariamente común, en parte debido a la mutación.

```java
public String[] getAllowedUsers() {
	String[] copy = new String[allowedUsers.length];
	for(int i=0; i < allowedUsers.length; i++)
		copy[i] = allowedUsers[i];
	return copy;
}
```