La semántica denotacional es el método formal más riguroso y ampliamente conocido para describir el significado de los programas. Se _basa sólidamente en la teoría de funciones recursivas_.

## Construcción de una Especificación de Semántica Denotacional

El proceso de construir una especificación de semántica denotacional para un lenguaje de programación implica _definir para cada entidad del lenguaje tanto un objeto matemático como una función que mapea instancias de esa entidad del lenguaje a instancias del objeto matemático_. Al ser los objetos rigurosamente definidos, modelan el significado exacto de sus entidades correspondientes. La dificultad de este método radica en la creación de los objetos y las funciones de mapeo. Se denomina denotacional porque _los objetos matemáticos denotan el significado de sus entidades sintácticas correspondientes_.

## Funciones de Mapeo en la Semántica Denotacional

Las funciones de mapeo de una especificación de semántica denotacional de un lenguaje de programación, al igual que todas las funciones en matemáticas, tienen un dominio y un rango. El **dominio** es la _colección de valores_ que son parámetros legítimos para la función; el **rango** es la _colección de objetos_ a los que se mapean los parámetros. En la semántica denotacional, el dominio se llama **dominio sintáctico**, ya que son las estructuras sintácticas las que se mapean. El rango se llama **dominio semántico**.

## Relación con la Semántica Operacional

En la **semántica operacional**, las construcciones de los lenguajes de programación se _traducen en construcciones más simples_, que se convierten en la base del significado de la construcción. En la **semántica denotacional**, las construcciones de los lenguajes de programación se _mapean a objetos matemáticos_, ya sea conjuntos o, con mayor frecuencia, funciones. Sin embargo, a diferencia de la semántica operacional, _la semántica denotacional no modela el procesamiento computacional paso a paso de los programas_.

# Ejemplos de semántica denotacional 

## Representaciones de Números Binarios

Utilizamos una construcción de lenguaje muy simple, las representaciones de cadenas de caracteres de números binarios. La sintaxis de dichos números binarios se puede describir mediante las siguientes reglas gramaticales:

```
<bin_num> → '0' 
		  | '1' 
		  | <bin_num> '0' 
		  | <bin_num> '1'
```

El **dominio sintáctico** de la función de mapeo para números binarios es el _conjunto de todas las representaciones de cadenas de caracteres de números binarios_. 
El **dominio semántico** es el _conjunto de números decimales no negativos_, simbolizado por _`N`_. 

Para describir el significado de los números binarios utilizando la semántica denotacional, _asociamos el significado real_ (un número decimal) _con cada regla que tiene un solo símbolo terminal en su lado derecho_. La función semántica, llamada `Mbin`, mapea los objetos sintácticos, como se describe en las reglas gramaticales anteriores, a los objetos en _`N`_, el conjunto de números decimales no negativos. La función `Mbin` se define de la siguiente manera:

```
Mbin('0') = 0
Mbin('1') = 1
Mbin(<bin_num> '0') = 2 * Mbin(<bin_num>)
Mbin(<bin_num> '1') = 2 * Mbin(<bin_num>) + 1
```

## Representaciones de Números Decimales

Un ejemplo similar se puede dar para describir el significado de los literales decimales sintácticos. En este caso, el **dominio sintáctico** es el _conjunto de representaciones de cadenas de caracteres de números decimales_. El **dominio semántico** es una vez más _el conjunto `N`_.

```
<dec_num> → '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9' | 
	<dec_num> ('0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9')
```

Las **asignaciones denotacionales** para estas reglas de sintaxis son:

```
Mdec('0') = 0, Mdec('1') = 1, Mdec('2') = 2, ..., Mdec('9') = 9
Mdec(<dec_num> '0') = 10 * Mdec(<dec_num>)
Mdec(<dec_num> '1') = 10 * Mdec(<dec_num>) + 1
...
Mdec(<dec_num> '9') = 10 * Mdec(<dec_num>) + 9
```

# El Estado de un Programa

En la semántica denotacional, el estado de un programa se representa formalmente como una función de estado, que mapea variables a sus valores correspondientes.

Sea $Σ$ el conjunto de todos los posibles estados de un programa. Un estado $𝑠∈Σ$ se define como una función parcial:

$$𝑠:𝑉→𝑉⊥$$

Donde:

- $V$ es el conjunto de todas las variables del programa
- $𝑉_⊥=𝑉∪{⊥}$ es el conjunto de todos los valores posibles, incluyendo el valor especial $⊥$ que representa una variable indefinida.

Así, un estado $𝑠$ es un conjunto de pares ordenados $(𝑥,𝑣)$ donde $𝑥∈𝑉$ es una variable y $𝑣∈𝑉⊥​$ es su valor correspondiente en ese estado.

Sea $VARMAP:𝑉×Σ→𝑉⊥$​ una función que, dado un estado $𝑠$ y una variable $𝑥$, devuelve el valor $𝑣$ asociado a $𝑥$ en ese estado, o $⊥$ si $𝑥$ está indefinida.

Formalmente:

$$VARMAP(𝑥,𝑠)=𝑠(𝑥)$$

La mayoría de las funciones de mapeo semántico en la semántica denotacional son funciones que toman un estado de entrada y producen un estado de salida, reflejando los cambios de estado producidos por la ejecución de un programa o construcción del lenguaje.

>[!tip] Semántica denotacional vs semántica operacional
>La **semántica denotacional** utiliza el _estado del programa_ para describir el significado, mientras que la **semántica operacional** utiliza el _estado de una máquina_. 
>
>La diferencia clave entre la semántica operacional y la semántica denotacional es que los cambios de estado en la **semántica operacional** están _definidos por algoritmos codificados_, escritos en algún lenguaje de programación, mientras que en la **semántica denotacional**, los cambios de estado están _definidos por funciones matemáticas_.

# Expresiones

Las expresiones son fundamentales en la mayoría de los lenguajes de programación. En este contexto, se asume que las expresiones no tienen efectos secundarios y son bastante simples: solo se utilizan los operadores `+` y `*`, con a lo sumo un operador por expresión. Los operandos son variables escalares enteras y literales enteros, sin paréntesis, y el valor de una expresión es un número entero.

La descripción BNF de estas expresiones es la siguiente:

```
<expr> → <dec_num> | <var> | <binary_expr>
<binary_expr> → <left_expr> <operator> <right_expr>
<left_expr> → <dec_num> | <var>
<right_expr> → <dec_num> | <var>
<operator> → + | *
```

En este contexto, el único error considerado es una variable con un valor indefinido. El dominio semántico para la especificación denotacional de estas expresiones es $Z ∪ {error}$, donde $Z$ es el conjunto de enteros y $error$ representa un valor de error.

La función de mapeo para una expresión dada $E$ y un estado $s$ se define de la siguiente manera. Se utiliza el símbolo $\Delta=$ para definir funciones matemáticas y el símbolo $=>$ para conectar la forma de un operando con su caso asociado. La notación de punto se emplea para referirse a los nodos hijos de un nodo. Por ejemplo, `<binary_expr>.<left_expr>` se refiere al nodo hijo izquierdo de `<binary_expr>`.

```
Me(<expr>, s) Δ= case <expr> of
				<dec_num>=>Mdec(<dec_num>, s)
				<var> =>if VARMAP(<var>, s) == undef
				then error
				else VARMAP(<var>, s)
				<binary_expr> =>
				if(Me(<binary_expr>.<left_expr>,s) == undef OR
				Me(<binary_expr>.<right_expr>, s) == undef)
				then error
				else if (<binary_expr>.<operator> == '+')
				then Me(<binary_expr>.<left_expr>, s) +
				Me(<binary_expr>.<right_expr>, s)
				else Me(<binary_expr>.<left_expr>, s) *
				Me(<binary_expr>.<right_expr>, s)
```

La función `Me(<expr>, s)` se define como un caso de selección que evalúa la expresión según su tipo:

- Si `<expr>` es un `<dec_num>`, se aplica la función `Mdec(<dec_num>, s)`.
- Si `<expr>` es una `<var>`, se verifica si la variable está definida en el estado s y se devuelve su valor.
- Si `<expr>` es un `<binary_expr>`, se evalúan recursivamente las expresiones izquierda y derecha y se aplica la operación correspondiente (`+` o `*`).

Esta definición formal permite evaluar expresiones simples de manera precisa y manejar errores relacionados con variables no definidas en un programa.

# Declaraciones de Asignación

En la semántica denotacional, una declaración de asignación se define como la evaluación de una expresión y la actualización del valor de la variable objetivo con el resultado de dicha evaluación. La función que define el significado de una declaración de asignación se denota como $Ma(x = E, s)$, donde

- $x$ es la variable a la que se le asigna el valor
- $E$ es la expresión que se evalúa
- $s$ es el estado del programa antes de la asignación

La función $Ma$ se define de la siguiente manera:

```
Ma(x = E, s) Δ= if Me(E, s) == error
	 then error
	 else s = {<i1, v1>, <i2, v2>, . . . , <in, vn>}, where
		 for j = 1, 2, . . . , n
			 if ij == x
				 then vj = Me(E, s)
				 else vj = VARMAP(ij, s)
```

Donde:

- $Me(E, s)$ es la función que evalúa la expresión $E$ en el estado $s$
- $\text{VARMAP}(i_j, s)$ es la función que obtiene el valor de la variable $i_j$ en el estado $s$.

# Bucles Lógicos con Prueba Previa

La representación de un bucle lógico con prueba previa parece ser simple a primera vista. Para facilitar la discusión, se asume la existencia de dos funciones de mapeo adicionales, `Msl` y `Mb`, que mapean listas de instrucciones y estados a estados, y expresiones booleanas a valores booleanos (o error), respectivamente. La función se define de la siguiente manera:

```
Ml (while B do L, s) Δ= if Mb(B, s) == undef
	 then error
	 else if Mb(B, s) == false
		 then s
		 else if Msl(L, s) == error
			 then error
			 else Ml (while B do L, Msl(L, s))
```

Donde:

- $Mb(B, s)$ es una función que evalúa la expresión booleana $B$ en el estado $s$ y devuelve su valor booleano o el valor especial $\text{undef}$ si hay un error.
- $Msl(L, s)$ es una función que ejecuta la lista de instrucciones $L$ en el estado $s$ y devuelve el nuevo estado resultante, o $\text{error}$ si hay un error.

La definición de $Ml$ es _recursiva_ y describe el significado del bucle de la siguiente manera:

1. Si la evaluación de la condición $B$ produce un error, el bucle también produce un error.
2. Si la evaluación de $B$ es falsa, el bucle termina y devuelve el estado $s$ actual.
3. Si la evaluación de $B$ es verdadera, se ejecuta la lista de instrucciones $L$ en el estado $s$ actual, y luego se llama recursivamente a $Ml$ con el nuevo estado resultante.
4. Si la ejecución de $L$ produce un error, el bucle también produce un error.

> [!summary] Objetos, Funciones y Semántica Denotacional
> La semántica denotacional permite definir formalmente el significado de los elementos sintácticos de un lenguaje de programación a través de objetos y funciones matemáticas.
> 
> Esto proporciona un marco riguroso para pensar en la programación, aunque las descripciones denotacionales pueden ser complejas y poco prácticas para los usuarios finales. Aun así, la semántica denotacional puede ser útil para el diseño de lenguajes, al identificar construcciones que pueden ser difíciles de entender.
