---
sticker: emoji//1f47d
---
Un curso titulado "Lenguajes de programación" puede significar muchas cosas diferentes. Para nosotros, significa la oportunidad de aprender los conceptos fundamentales que aparecen de una forma u otra en casi todos los lenguajes de programación. 

También tendremos una idea de cómo estos conceptos "encajan" para proporcionar lo que los programadores necesitan en un lenguaje. Y utilizaremos diferentes lenguajes para ver cómo pueden adoptar enfoques complementarios para representar estos conceptos. Todo esto está pensado para convertirte en un mejor desarrollador de software, en cualquier lenguaje.

Mucha gente diría que este curso "enseña" los 3 lenguajes ML (en la Parte A), Racket (en la Parte B), y Ruby (Parte C), pero es una mala descripción. Utilizaremos estos lenguajes para aprender varios paradigmas y conceptos porque son adecuados para ello. Si nuestro objetivo fuera sólo para que sea lo más productivo posible en estos tres lenguajes, el material del curso sería muy diferente. Dicho esto, ser capaz de aprender nuevos lenguas y reconocer las similitudes y diferencias entre ellas es un objetivo importante.

La mayor parte del curso utilizará **programación funcional** (tanto ML como Racket son lenguajes funcionales), que inmutables (sin sentencias de asignación) y funciones, especialmente funciones que toman y devuelven otras funciones. Como discutiremos más adelante en la Parte C, la programación funcional hace algunas cosas exactamente lo contrario de la programación orientada a objetos, pero también tiene muchas similitudes. La programación funcional es no sólo es un enfoque muy potente y elegante, sino que aprenderlo te ayuda a entender mejor todos los estilos de programación.

[[Programación funcional]]

___
## [[S1 - Expresiones ML y enlaces de variables|Expresiones ML y enlaces de variables]]

## [[S1 -  Enlaces de variables en ML sintaxis, semántica y tipos|Enlaces de variables en ML: Sintaxis, semántica y tipos]]

## [[S1 - Enlaces de funciones|Enlaces de funciones en ML: definición, sintaxis, tipos, evaluación y llamadas]]

## [[S1 - Pares y tuplas en ML|Pares y tuplas en ML: definición, sintaxis, tipos, acceso a sus elementos y ejemplos]]

## [[S1 - Listas|Listas en ML: definición, tipos, sintaxis, funciones y ejemplos]]

## Revisión

Se ha logrado un gran avance en los componentes centrales de ML:

- **Tipos:** enteros, booleanos, unidad, tuplas de tipos compuestos (`t1*…*tn`), listas de tipos compuestos (`t1*…*tn->t`) 
- Los tipos pueden "anidar" (cada `t` mencionado anteriormente puede ser en sí mismo un tipo compuesto). 
- **Variables, entornos y expresiones básicas:** Conceptos fundamentales para definir y almacenar datos, así como realizar operaciones sobre ellos. 
- **Funciones:** 
	- **Definir:** `fun x0 (x1:t1, …, xn:tn) = e` 
	- Define una función con nombre `x0` que toma `n` parámetros: `x1` del tipo `t1`, ..., `xn` del tipo `tn`, y devuelve un valor del tipo `e`.
	- **Usar:** `e0 (e1, …, en)` - Aplica la función `e0` a los argumentos `e1`, ..., `en` (del tipo correspondiente a los parámetros definidos). 
- **Tuplas:** 
	- **Crear:** `(e1, …, en)` 
	- Crea una tupla con elementos `e1`, ..., `en`.
	- **Usar:** `#1 e`, `#2 e`, … 
	- Accede a elementos individuales de la tupla: `#1` para el primero, `#2` para el segundo, etc. 
- **Listas:** 
	- **Crear:** `[]`, `e1::e2` 
	- Crea una lista vacía (`[]`) o una lista con el elemento inicial `e1` seguido del resto de la lista `e2`. 
	- **Usar:** `null e`, `hd e`, `tl e` 
	- Comprueba si la lista está vacía (`null`), obtiene el primer elemento (`hd`) o el resto de la lista (`tl`).
- 



## [[S1 - Expresiones let en ML|Expresiones let en ML: sintaxis, verificación de tipos, evaluación, ejemplos y recomendaciones]]

## [[S1 - Opciones|Opciones]]


## Ausencia de mutación y sus ventajas

En ML, no hay forma de cambiar el contenido de un enlace, una tupla o una lista. Si x corresponde a algún valor como la lista de pares lista de pares `[(3,4),(7,9)]` en algún entorno, entonces x siempre se asignará a esa lista en ese entorno. No hay ninguna sentencia de asignación que cambie x a una lista diferente. (Puede introducir un nuevo binding que haga sombra a x, pero eso no afectará a ningún código que busque la x "original" en un entorno). No existe ninguna sentencia de asignación que permita cambiar la cabeza o la cola de una lista. Y no hay ninguna sentencia que permita cambiar el contenido de una tupla. Así que tenemos construcciones para construir datos compuestos y acceder a las piezas, pero no hay construcciones para mutar los datos que hemos construido.

Se trata de una función realmente potente. Puede que esto le sorprenda: ¿cómo puede un idioma que no tiene algo ser una característica? Porque si no existe tal característica, cuando escribes tu código puedes confiar en que ningún otro código hará algo que haga que tu código sea incorrecto, incompleto o difícil de usar. otro código haga algo que pueda hacer que tu código sea incorrecto, incompleto o difícil de usar. Tener datos inmutables es probablemente la "no característica" más importante que un lenguaje puede tener, y es una de las principales contribuciones de la programación funcional. contribuciones de la programación funcional.

Si bien los datos inmutables presentan diversas ventajas, en este contexto nos centraremos en una en particular: hacen que compartir y utilizar alias se vuelva irrelevante. Es pertinente reconsiderar dos ejemplos previos antes de seleccionar Java (o cualquier otro lenguaje en el que los datos mutables sean la norma y las declaraciones de asignación sean frecuentes).

```
fun sort_pair (pr : int*int) =
	if (#1 pr) < (#2 pr)
	then pr
	else ((#2 pr),(#1 pr))
```

En la función "sort_pair", se procede de manera inequívoca a construir y retornar un nuevo par en la rama "else". No obstante, en la rama "then", se opta por retornar ya sea una copia del par referenciado por "pr" o un alias, de acuerdo a las preferencias del llamante.

```
val x = (3,4)
val y = sort_pair x
```

¿Ahora x e y serían alias para el mismo par? La respuesta es que no se puede determinar con certeza: no existe ninguna estructura en el aprendizaje automático que pueda afirmar si x e y son alias o no, y no hay motivos para preocuparse acerca de la posibilidad de que lo sean. Si tuviéramos la capacidad de llevar a cabo mutaciones, el panorama sería distinto. Supongamos que pudiéramos decidir: "modificar la segunda parte del par, al cual x está vinculado, para que contenga el número 5 en lugar de 4". En este escenario nos surgiría la pregunta de si el número 2 ahora sería 4 o 5.

En caso de que tengas curiosidad, esperaríamos que el código anterior creara alias: al devolver pr, la función sort_pair devolvería un alias a su argumento. Eso es más eficiente que esta versión, que crearía otro par con exactamente el mismo contenido:

```sml
fun sort_pair (pr : int*int) =
	if (#1 pr) < (#2 pr)
	then (#1 pr, #2 pr)
	else ((#2 pr),(#1 pr))
```

Crear el nuevo par (#1 pr, #2 pr) es un mal estilo, ya que pr es más simple y funcionará igual de bien. Sin embargo, en lenguajes con mutación, los programadores hacen copias como esta todo el tiempo, exactamente para evitar alias donde hacer una asignación usando una variable como x provoca cambios inesperados al usar otra variable como y. En ML, ningún usuario de sort_pair puede saber si devolvemos un nuevo par o no.

Nuestro segundo ejemplo es nuestra elegante función para la concatenación de listas:

```
fun append (xs : int list, ys : int list) =
if null xs
then ys
else (hd xs) :: append(tl xs, ys)
```

Podemos hacer una pregunta similar: ¿La lista devuelta comparte algún elemento con los argumentos? De nuevo, la respuesta no importa porque ningún llamador puede saberlo. Y de nuevo la respuesta es sí: construimos una nueva lista que "reutiliza" todos los elementos de ys. Esto ahorra espacio, pero sería muy confuso si alguien pudiera modificar ys más tarde. Ahorrar espacio es una buena ventaja de los datos inmutables, pero también lo es simplemente no tener que preocuparse de si las cosas están alias o no al escribir algoritmos elegantes.

De hecho, tl en sí mismo introduce felizmente aliasing (aunque no se puede saber): devuelve (un alias a) la cola de la lista, que siempre es "barata", en lugar de hacer una copia de la cola de la lista, que es "cara" para listas largas.

El ejemplo de append es muy similar al ejemplo de sort_pair, pero es aún más convincente porque es difícil hacer un seguimiento del aliasing potencial si tienes muchas listas de longitudes potencialmente grandes. Si concateno `[1,2]` a `[3,4,5]`, obtendré alguna lista `[1,2,3,4,5]`, pero si alguien más tarde puede cambiar la lista `[3,4,5]` a `[3,7,5]`, ¿sigue siendo la lista concatenada `[1,2,3,4,5]` o ahora es `[1,2,3,7,5]`?

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
## Los Componentes de un Lenguaje de Programación

Ahora que hemos aprendido suficiente ML para escribir algunas funciones y programas simples con él, podemos enumerar las "piezas" esenciales necesarias para definir y aprender cualquier lenguaje de programación:

- **Sintaxis:** ¿Cómo se escriben las distintas partes del lenguaje? Imagínala como el conjunto de reglas que gobiernan cómo formar oraciones con sentido en el lenguaje natural. Ejemplos: palabras clave, identificadores, operadores, puntuación y el orden en que estos elementos se pueden combinar.
- **Semántica:** ¿Qué significan las distintas características del lenguaje? Por ejemplo, ¿cómo se evalúan las expresiones? Ejemplos: cómo se evalúan las expresiones, cómo se comprueban los tipos y el flujo de control (toma de decisiones e iteración) de tu programa.
- **Idiomas:** ¿Cuáles son los enfoques comunes para usar las características del lenguaje para expresar cálculos? Ejemplos: recursión para tareas como recorrer árboles, funciones de orden superior para la modularidad, patrones de programación funcional para código declarativo y estructuras de datos como listas y árboles.
- **Bibliotecas:** ¿Qué se ha escrito ya para ti? ¿Cómo se hacen cosas que no podrías hacer sin el soporte de bibliotecas (como acceder a archivos)? Ejemplos: bibliotecas estándar para entrada/salida, redes, manipulación de cadenas, operaciones matemáticas, interfaces gráficas de usuario (GUI) y más.
- **Herramientas:** ¿Qué hay disponible para manipular programas en el lenguaje (compiladores, bucles de lectura-evaluación-impresión, depuradores, ...)? Ejemplos: compiladores para traducir tu código a instrucciones ejecutables por la máquina, intérpretes para ejecutar código línea por línea, depuradores para identificar y corregir errores, editores de código para escribir y editar código, y entornos de desarrollo integrado (IDE) que combinan estas herramientas.

Si bien las bibliotecas y herramientas son esenciales para ser un programador eficaz (para evitar reinventar soluciones disponibles o hacer las cosas manualmente de forma innecesaria), este curso no se centra mucho en ellas. Esto puede dar la impresión errónea de que estamos utilizando lenguajes "tontos" o "poco prácticos", pero las bibliotecas y herramientas son simplemente menos relevantes en un curso sobre las similitudes y diferencias conceptuales de los lenguajes de programación.
## Más expresiones booleanas y de comparación

### Operaciones Booleanas

**Operadores lógicos:**

- `e1 andalso e2`:
    
    - **Verificación de tipos:** `e1` y `e2` deben tener tipo `bool`.
    - **Evaluación:**
        - Si el resultado de `e1` es `false`, devuelve `false`.
        - Si el resultado de `e1` es `true`, devuelve el resultado de `e2`.

- `e1 orelse e2`:
    - **Verificación de tipos:** `e1` y `e2` deben tener tipo `bool`.
    - **Evaluación:**
        - Si el resultado de `e1` es `true`, devuelve `true`.
        - Si el resultado de `e1` es `false`, devuelve el resultado de `e2`.

- `not e1`:
    - **Verificación de tipos:** `e1` debe tener tipo `bool`.
    - **Evaluación:**
        - Si el resultado de `e1` es `true`, devuelve `false`.
        - Si el resultado de `e1` es `false`, devuelve `true`.

**Sintaxis alternativa:**

- Muchos lenguajes usan `&&` para `andalso`, `||` para `orelse` y `!` para `not`.
- En SML, `&&` y `||` no existen y `!` tiene un significado diferente.

**Evaluación en cortocircuito:**

- `andalso` y `orelse` no son funciones verdaderas, sino que utilizan la evaluación en cortocircuito. Esto significa que la evaluación de `e2` solo se realiza si es necesaria para determinar el resultado final (dependiendo del resultado de `e1`).
- `not` es una función predefinida en SML.

**Estilo con valores booleanos:**

- El lenguaje no necesita operadores especiales como `andalso`, `orelse` y `not`. Se pueden expresar las mismas operaciones usando condicionales `if`:

```sml
(* e1 andalso e2 *)
if e1 then e2 else false

(* e1 orelse e2 *)
if e1 then true else e2

(* not e1 *)
if e1 then false else true
```

- Usar estas formas más concisas generalmente se considera un mejor estilo de programación.

**Mal uso de los condicionales:**

- Evitar construcciones innecesarias como:

```sml
(* just say e (!!!) *)
if e then true else false
```

- Esta expresión siempre devuelve `true` y se puede simplificar a `e`.
### Comparaciones

**Operadores de comparación:**

Para comparar valores enteros, SML dispone de los siguientes operadores:

- ` = `: Igualdad
- `<>`: Desigualdad
- `>`: Mayor que
- `<`: Menor que
- `>=`: Mayor o igual que
- `<=`: Menor o igual que

**Ten cuidado con los mensajes de error:**

Es posible que te encuentres con mensajes de error inesperados al usar estos operadores. Esto se debe a que algunos de ellos se pueden utilizar con otros tipos de datos además de los enteros. Aquí te lo explicamos:

- `>`, `<`, `>=`, `<=`: Estos operadores se pueden usar con números reales, pero no con la comparación de un entero y un real (por ejemplo, `1 int > 1 real` provocará un error).
- ` = `, `<>`: Estos operadores se pueden usar con cualquier "tipo de igualdad", pero no con números reales. (No te preocupes por los "tipos de igualdad" por ahora, se abordarán más adelante).

En resumen, **utiliza los operadores de comparación con cuidado y sé consciente de con qué tipos de datos son compatibles**.
## Un Beneficio Clave de los Datos Inmutables en SML

**Sin mutación: una característica valiosa**

Hasta ahora, hemos cubierto todas las características que necesitas (y deberías usar) para la tarea 1. Ahora aprenderás sobre una "no-característica" muy importante.

¿Cómo puede ser importante la falta de una característica? La no-mutación te permite saber cosas que otros códigos no te dirán sobre tu código y los resultados que produce.

Un aspecto y contribución importante de la programación funcional es la **incapacidad de asignar valores nuevos (mutar) a variables o partes de tuplas y listas**. (Esto es algo muy importante)

**No se puede saber si copias o alias**

```sml
fun sort_pair (pr : int * int) =
  if #1 pr < #2 pr
  then pr
  else (#2 pr, #1 pr)

fun sort_pair (pr : int * int) =
  if #1 pr < #2 pr
  then (#1 pr, #2 pr)
  else (#2 pr, #1 pr)
```

En SML, estas dos implementaciones de `sort_pair` son indistinguibles. Pero solo porque las tuplas son inmutables. La primera es un mejor estilo: más simple y evita crear una nueva tupla en la rama `then`.

En lenguajes con datos compuestos mutables, ¡estas funciones serían diferentes!

**Supongamos que tuviéramos mutación...**

```sml
val x = (3, 4)
val y = sort_pair x
somehow mutate #1 x to hold 5
val z = #1 y
```

• ¿Qué es `z`?

- Dependería de cómo implementamos `sort_pair`. 
- Tendríamos que decidir cuidadosamente y documentar `sort_pair`.

Pero sin mutación, podemos implementar la función de "cualquier manera". Ningún código puede distinguir entre alias y copias idénticas.

• No necesitas pensar en el alias: concéntrate en otras cosas. 
• Puedes usar alias, que ahorran espacio, sin peligro.

**Un ejemplo aún mejor**

```sml
fun append (xs : int list, ys : int list) =
  if null xs
  then ys
  else hd (xs) :: append (tl(xs), ys)

val x = [2, 4]
val y = [5, 3, 0]
val z = append(x,y)

(no se puede saber,
pero es el primero)
```

**ML vs. lenguajes imperativos**

• En ML, creamos alias todo el tiempo sin pensar en ello porque es imposible saber dónde hay alias.

- Ejemplo: `tl` es constante; no copia el resto de la lista.
- Así que no te preocupes y céntrate en tu algoritmo.

• En lenguajes con datos mutables (por ejemplo, Java), los programadores están obsesionados con el alias y la identidad de los objetos.

- ¡Tienen que estarlo! para que las asignaciones posteriores afecten las partes correctas del programa.
- A menudo es crucial hacer copias en los lugares correctos.

**En resumen:**

Los datos inmutables te liberan de preocuparte por los alias y la mutación, permitiéndote:

- Diseñar funciones más simples y claras.
- Evitar errores relacionados con la mutación inesperada.
- Razonar más fácilmente sobre el comportamiento de tu código.
- Aprovechar la potencial optimización de estructuras inmutables.
## ML vs. Lenguajes Imperativos: El Peligro de la Mutación (Ejemplo en Java)

**SML vs. Lenguajes con Datos Mutables:**

- En SML, creamos alias todo el tiempo sin pensarlo, ya que es imposible saber dónde hay alias.
    - Ejemplo: `tl` es constante; no copia el resto de la lista.
    - Así que no te preocupes y céntrate en tu algoritmo.
- En lenguajes con datos mutables (como Java), los programadores están obsesionados con los alias y la identidad de los objetos.
    - ¡Tienen que estarlo! para que las asignaciones posteriores afecten las partes correctas del programa.
    - A menudo es crucial hacer copias en los lugares correctos.

**Ejemplo de Error por Mutación en Java:**

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
			 ... // acceso permitido: usarlo
			 return;
		  }
		}
		throw new IllegalAccessException();
	}
}
```

**El Problema:**

```java
p.getAllowedUsers()[0] = p.currentUser(); // Modifica el array devuelto por getAllowedUsers
p.useTheResource(); // Puede acceder al recurso indebidamente
```

**La Solución:**

```java
public String[] getAllowedUsers() {
 … return a copy of allowedUsers …
}
```

**La Importancia de la Inmutabilidad:**

En lenguajes imperativos como Java, la mutación (cambio del valor de una variable) puede generar errores sutiles y difíciles de detectar. El ejemplo anterior muestra cómo un usuario malintencionado podría explotar la mutación de un array devuelto por un método para obtener acceso no autorizado a un recurso.

En lenguajes funcionales como SML, los datos son inmutables, es decir, no se pueden modificar. Esto elimina la posibilidad de este tipo de errores y facilita el razonamiento sobre el comportamiento del código. En el ejemplo de SML, no es necesario preocuparse por si `getAllowedUsers` devuelve un alias o una copia del array, ya que el código no puede modificarlo de ninguna manera.

**En resumen:**

La inmutabilidad de los datos es una característica fundamental de la programación funcional que ofrece ventajas en cuanto a seguridad, claridad y razonamiento del código.
## Las Cinco Piezas del Aprendizaje de un Lenguaje de Programación

Este texto habla sobre los diferentes aspectos que necesitas comprender para aprender bien un lenguaje de programación.

**Las cinco piezas:**

1. **Sintaxis:** ¿Cómo se escriben las estructuras del lenguaje? (Por ejemplo, la forma de declarar variables, definir funciones, etc.)
2. **Semántica:** ¿Qué significado tienen los programas? (Reglas de evaluación que determinan el resultado de la ejecución).
3. **Idiomas:** ¿Cuáles son los patrones típicos para usar las características del lenguaje y expresar tus cálculos? (Formas comunes de programar para lograr cierto resultado).
4. **Bibliotecas:** ¿Qué funcionalidades básicas proporciona el lenguaje o un proyecto conocido? (Por ejemplo, acceso a archivos, estructuras de datos).
5. **Herramientas:** ¿Qué ofrecen las implementaciones del lenguaje para facilitar tu trabajo? (Por ejemplo, REPL, depurador, formateador de código, etc.).

**Puntos clave:**

- Estos cinco aspectos son independientes, pero todos son esenciales para ser un buen programador.
- Muchas personas confunden estos conceptos, lo que puede dificultar el aprendizaje.
- Este curso se centra en la semántica y los idiomas:
    - La sintaxis suele ser poco interesante, similar a memorizar hechos históricos.
    - Las bibliotecas y herramientas son importantes, pero se suelen aprender sobre la marcha.
    - Este curso se enfoca en comprender la semántica y cómo usarla para entender cualquier software y aplicar la forma correcta de programar (idiomas).
    - Al evitar bibliotecas y herramientas comunes, los lenguajes de este curso pueden parecer "extraños", pero cualquier lenguaje estudiado de esta manera lo parecería.

En resumen, para dominar un lenguaje de programación, no solo debes conocer la sintaxis, sino también comprender cómo funcionan los programas (semántica), qué formas de programación son comunes (idiomas) y cómo aprovechar las herramientas disponibles. Este curso te ayudará a enfocarte en los fundamentos esenciales para una comprensión profunda del mundo de la programación.

## Beneficios de la no mutación

Ahora ha cubierto todas las características que necesita (y debería usar) en hw1.
Ahora aprende una característica muy importante

- ¿Eh? ¿Cómo podría ser importante la falta de una característica?
- Cuando te permite saber cosas que otro código no hará con tu código y los resultados que produce tu código 
 
Un aspecto y contribución importante de la programación funcional: No poder asignar a (también conocido como mutar) variables o partes de tuplas y listas.

```sml
fun sort_pair (pr : int * int) =
	if #1 pr < #2 pr
	then pr
	else (#2 pr, #1 pr)
	
fun sort_pair (pr : int * int) =
	if #1 pr < #2 pr
	then (#1 pr, #2 pr)
	else (#2 pr, #1 pr)
```

En ML, estas dos implementaciones de `sort_pair` son indistinguibles

- Pero solo porque las tuplas son inmutables
- La primera tiene mejor estilo: es más simple y evita crear un nuevo par en la rama `then`.
- ¡En lenguajes con datos compuestos mutables, estos son diferentes!
### Supongamos tenemos una mutación 

```sml
val x = (3,4)
val y = sort_pair x
(* somehow mutate #1 x to hold 5 *)
val z = #1 y
```

![[Pasted image 20240301101456.png|center]]

- Que es Z?
	- Va a depender de como implementemos sort_pair
		- Tenemos que decidir cuidadosamente y documentar sort_pair
	- Pero si no tenemos mutación podemos elegir cualquier camino 

- Ningún código puede distinguir jamás entre alias y copias idénticas.
- No es necesario pensar en alias: céntrate en otras cosas.
- Puedes usar alias, lo que ahorra espacio, sin peligro.
### Un mejor ejemplo 

```sml
fun append (xs : int list, ys : int list) =
	 if null xs
	 then ys
	 else hd (xs) :: append (tl(xs), ys)

val x = [2,4]
val y = [5,3,0]
val z = append(x,y)
```

![[Pasted image 20240301101807.png|center]]
### ML vs. Lenguajes imperativos 

En ML, creamos alias todo el tiempo sin pensarlo porque es imposible saber dónde hay alias.

– Ejemplo: `tl` tiene un tiempo constante; no copia el resto de la lista.
– Así que no te preocupes y céntrate en tu algoritmo.

En lenguajes con datos mutables (por ejemplo, Java), los programadores
están obsesionados con el aliasamiento y la identidad de los objetos.

- ¡Tienen que estarlo! para que las asignaciones posteriores afecten
las partes correctas del programa.
- A menudo es crucial hacer copias en los lugares justos.
Ejemplo opcional de Java en el siguiente segmento.

[[Aliasing]]
## Un ejemplo en JAVA: "Java Mutation Bug"
### Java security nightmare (bad code)

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
### Necesitamos crear copias

El problema:

```java
p.getAllowedUsers()[0] = p.currentUser();
p.useTheResource();
```

La solución:

```java
public String[] getAllowedUsers() {
	 … return a copy of allowedUsers …
}
```

Referencia (alias) vs Copia, no importa si el código es inmutable.
## Las piezas del aprendizaje de una lengua

Cinco cosas diferentes
1. La sintaxis: ¿Cómo se escriben las construcciones del lenguaje?
2. Semántica: ¿Qué significan los programas? (Reglas de evaluación)
3. Modismos: ¿Cuáles son los patrones típicos de uso de las características del lenguaje para expresar su computación?
4. Bibliotecas: ¿Qué facilidades proporciona el lenguaje (o un proyecto) proporciona "de serie"? (Por ejemplo, acceso a archivos, estructuras de datos)
5. Herramientas: ¿Qué ofrecen las implementaciones del lenguaje para su trabajo? (Por ejemplo, REPL, depurador, formateador de código, ...)
- En realidad no forman parte del lenguaje

Se trata de 5 cuestiones distintas

- En la práctica, todas son esenciales para un buen programador.
- Mucha gente los confunde, pero no debería.

