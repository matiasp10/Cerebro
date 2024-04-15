## El problema con `max` y valores especiales

En SML, la función `max` tradicionalmente devuelve 0 para una lista vacía. Esta solución tiene algunas desventajas:

- **Falta de claridad:** No se distingue claramente entre un valor máximo real y la ausencia de un valor.
- **Errores potenciales:** El uso de un valor especial como 0 puede generar errores si no se maneja correctamente en el código.
- **Falta de flexibilidad:** No es una solución extensible para otros tipos de datos.

## Opciones como solución

Las **opciones** en SML ofrecen una forma más elegante y robusta de manejar la ausencia de valores. Una opción puede ser `NONE` (vacía) o contener un valor de cualquier tipo `t`.

## Ventajas de las opciones:

- **Claridad:** Distinguen claramente entre la ausencia de un valor y un valor real.
- **Seguridad:** Previenen errores al evitar el uso de valores especiales.
- **Flexibilidad:** Se pueden usar con cualquier tipo de dato.

## Ejemplo con `better_max`

```sml
fun better_max (xs : int list) =
 if null xs
 then NONE
 else
	 let val tl_ans = better_max(tl xs)
	 in
		 if isSome tl_ans
			 andalso valOf tl_ans > hd xs
		 then tl_ans
		 else SOME (hd xs)
	 end
```

- **`NONE` para lista vacía:** Si la lista está vacía, la función devuelve `NONE` para indicar la ausencia de un valor máximo.
- **`SOME` para valor máximo:** Si la lista no está vacía, la función calcula el máximo y lo devuelve usando `SOME`.
## Ventajas de `better_max`

- **Claridad:** El uso de `NONE` deja claro que la función puede no encontrar un valor máximo.
- **Seguridad:** Se evita el uso de 0 como valor especial, lo que reduce la posibilidad de errores.
- **Flexibilidad:** La función puede trabajar con cualquier tipo de lista de enteros.

## Variación con `max_nonempty`

El código también presenta una variación con una función auxiliar `max_nonempty`:

```sml
fun better_max2 (xs : int list) =
	 if null xs
	 then NONE
	 else let (* ok to assume xs nonempty b/c local *)
			 fun max_nonempty (xs : int list) =
				 if null (tl xs)
				 then hd xs
				 else
					 let val tl_ans = max_nonempty(tl xs)
					 in
						 if hd xs > tl_ans
						 then hd xs
						 else tl_ans
					 end
		 in
			 SOME (max_nonempty xs)
		 end
```

- **Función local:** `max_nonempty` se define como una función local dentro de `better_max`.
- **Manejo de casos base:** Se encarga de calcular el máximo para listas no vacías.
- **Uso de `SOME`:** Devuelve el máximo usando `SOME` para indicar un valor presente.

### Ventajas de esta variación

- **Eficiencia:** Evita la creación innecesaria de opciones en cada llamada recursiva.
- **Modularidad:** Divide la lógica en dos funciones para mayor claridad.