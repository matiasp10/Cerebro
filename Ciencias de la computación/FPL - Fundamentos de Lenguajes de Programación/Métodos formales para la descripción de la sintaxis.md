
En el ámbito de la informática, las **gramáticas libres de contexto (GFC)** y la **Forma Backus-Naur (BNF)** son herramientas fundamentales para describir la sintaxis de los lenguajes de programación. Estas formalidades permiten definir de manera precisa y rigurosa las estructuras válidas que pueden formar parte del lenguaje, facilitando tanto su comprensión como su análisis.

# Gramáticas libres de contexto (GFC)

Introducidas por Noam Chomsky a mediados de la década de 1950, las **GFC** proporcionan un marco teórico para especificar la sintaxis de lenguajes formales. Se componen de un conjunto de reglas de producción que definen cómo se pueden combinar símbolos para generar cadenas válidas del lenguaje.

Las reglas de producción de una **GFC** tienen la siguiente forma:

```
Símbolo_no_terminal -> Símbolo1 | Símbolo2 | ... | SímboloN
```

Donde:

- **Símbolo_no_terminal:** Representa un _elemento abstracto del lenguaje_ que puede ser descompuesto en otros símbolos.
- **Símbolo1, Símbolo2, ..., SímboloN:** Representan _símbolos terminales o no terminales_, que pueden ser combinados de diversas maneras.

La principal característica de las **GFC** es que las sustituciones de símbolos no terminales se realizan de forma **libre de contexto**. Esto significa que _la decisión de reemplazar un símbolo no terminal por su correspondiente cadena no depende del contexto en el que se encuentra dicho símbolo_.

# Forma Backus-Naur (BNF)

La **BNF** es una notación específica para representar GFC. Fue desarrollada por John Backus en la década de 1950 como parte del trabajo de diseño del lenguaje de programación Backus-Naur Form (**BNF**).

La **BNF** utiliza una sintaxis similar a la de las expresiones regulares, pero con extensiones para manejar la recursividad y la ambigüedad inherentes a las **GFC**. Las producciones de BNF se escriben de la siguiente manera:

```
<nombre_regla> --> <expresión>
```

Donde:

- `<nombre_regla>`: Representa el _nombre de la regla_, que usualmente corresponde a un símbolo no terminal.
- `<expresión>`: Representa una _secuencia de símbolos terminales y no terminales_, combinados mediante operadores de concatenación (`|`), repetición (`*`, `+`) y opcionalidad (`?`).

___

# Fundamentos

En el mundo de la informática, la **Forma Backus-Naur (BNF)** se utiliza como un **metalenguaje** para definir la **sintaxis** de los lenguajes de programación. Esto significa que BNF es un lenguaje que se emplea para _describir la estructura y las reglas que conforman un lenguaje de programación específico_.

## Abstracciones y reglas

BNF funciona mediante la creación de **abstracciones** para representar las diferentes estructuras sintácticas del lenguaje. Estas abstracciones, a menudo simbolizadas entre paréntesis angulares (`< >`), se combinan en **reglas** que definen cómo se pueden construir expresiones válidas en el lenguaje.

### Ejemplo: asignación en JAVA

Consideremos una simple sentencia de asignación en Java: `total = subtotal1 + subtotal2`. Para representar esta estructura sintáctica en BNF, podemos utilizar la siguiente regla:

```BNF
<asignacion> --> <variable> = <expresion>
```

En esta regla:

- `<asignacion>` es la abstracción que representa la sentencia de asignación completa.
- `<variable>` representa un identificador de variable válido en Java.
- ` = ` es el símbolo literal ` = `.
- `<expresion>` representa una expresión Java válida, que puede incluir operadores, variables y constantes.

La regla indica que una sentencia de asignación válida está formada por una variable, seguida del símbolo ` = `, y luego una expresión.

## Símbolos terminales y no terminales

Las reglas de BNF se componen de dos tipos de símbolos:

- **Símbolos terminales:** Representan los elementos básicos del lenguaje, como palabras clave, operadores, identificadores y literales. Estos símbolos se escriben tal cual, sin ninguna notación especial.
- **Símbolos no terminales:** Representan abstracciones de nivel superior, como `<asignacion>`, `<variable>` o `<expresion>`. Estos símbolos se escriben entre paréntesis angulares (`< >`).

En la regla de asignación anterior, `<variable>`, ` = ` y `<expresion>` son símbolos no terminales, mientras que ` = ` es un símbolo terminal.

## Definiciones recursivas y reglas múltiples

Las abstracciones de **BNF** pueden definirse de forma **recursiva**, es decir, _una abstracción puede ser utilizada en la definición de sí misma_. Esto permite describir estructuras sintácticas anidadas y repetitivas.

Además, una abstracción puede tener **múltiples definiciones**, lo que significa que _puede representarse de diferentes maneras en el lenguaje_. Esto permite capturar la flexibilidad de la sintaxis del lenguaje.

## Potencia y aplicaciones de BNF

A pesar de su simplicidad, **BNF** es un lenguaje lo suficientemente **potente** como para describir la mayoría de las estructuras sintácticas de los lenguajes de programación modernos. Permite especificar:

- Listas de construcciones similares
- El orden de las construcciones
- Estructuras anidadas
- Precedencia y asociatividad de operadores

Debido a su capacidad descriptiva, BNF se utiliza en diversas aplicaciones, como:

- **Diseño de lenguajes de programación:** Definir la sintaxis precisa del lenguaje para su implementación.
- **Análisis sintáctico:** Desarrollar herramientas que analizan el código fuente y verifican su validez sintáctica.
- **Traducción de lenguajes:** Crear compiladores o intérpretes que traducen código de un lenguaje a otro.
- **Especificación de protocolos:** Definir la sintaxis de protocolos de comunicación para asegurar una comunicación clara.

# Describir listas

En el ámbito de la informática, las **listas** son estructuras de datos que permiten almacenar una secuencia de elementos del mismo tipo. La sintaxis para describir listas en la **Forma Backus-Naur (BNF)**, un metalenguaje utilizado para definir la sintaxis de lenguajes de programación, presenta algunas particularidades debido a la ausencia del símbolo elipsis (`...`) en BNF.

## Recursión para representar listas

Para describir listas en BNF, se emplea la técnica de **recursión**. Una regla se considera recursiva cuando el símbolo no terminal del lado izquierdo (LHS) de la regla aparece también en el lado derecho (RHS) de la misma. Esta técnica permite representar listas de longitud variable sin necesidad del símbolo elipsis.

### Ejemplo: Lista de identificadores

Consideremos la siguiente regla BNF para definir una lista de identificadores:

```
<ident_list> --> identifier
              | identifier, <ident_list>
```

En esta regla:

- `<ident_list>` representa la abstracción que simboliza una lista de identificadores.
- `identifier` representa un identificador válido en el lenguaje de programación.
- La coma (`,`) es un símbolo terminal que separa los identificadores de la lista.

La regla indica que una `<ident_list>` puede estar formada por:

1. Un único `identifier`.
2. Un `identifier` seguido de una coma (`,`) y otra instancia de `<ident_list>`.

Esta definición recursiva permite representar listas de identificadores de cualquier longitud. Por ejemplo:

- `x` es una `<ident_list>` válida.
- `x, y` es una `<ident_list>` válida.
- `x, y, z` es una `<ident_list>` válida.

La **recursión** ofrece una forma concisa y elegante de describir listas en **BNF**, capturando la estructura repetitiva de estas estructuras de datos. Además, permite manejar listas de cualquier longitud sin necesidad de especificar manualmente cada caso posible.

Sin embargo, la recursión _puede generar ambigüedad en la sintaxis_, especialmente cuando se trata de listas anidadas o estructuras más complejas. En estos casos, es posible que se necesiten técnicas adicionales para garantizar una definición clara y precisa de la sintaxis.

# Gramáticas y derivaciones


En el ámbito de la informática, las **gramáticas libres de contexto (GFC)** y la **Forma Backus-Naur (BNF)** son herramientas fundamentales para definir la sintaxis de lenguajes formales. Las **_derivaciones_**, un proceso que transforma cadenas de símbolos siguiendo las reglas gramaticales, juegan un papel crucial en la comprensión del funcionamiento de estas gramáticas.

> [!info] Concepto
> Una **derivación** en una GFC representa una secuencia de pasos que transforman una cadena inicial en una cadena final, aplicando las reglas de producción de la gramática. Esta secuencia se inicia con un símbolo no terminal especial, denominado **símbolo inicial** o **axioma**, y termina en una cadena formada únicamente por símbolos terminales.

## Pasos de una derivación

Cada paso de una derivación implica la **sustitución** de un símbolo no terminal por su correspondiente **lado derecho (RHS)** en una regla de producción. La sustitución se realiza siguiendo estas reglas:

- El símbolo no terminal debe estar presente en la cadena actual.
- La sustitución debe realizarse por completo, es decir, no se pueden realizar sustituciones parciales.
- El orden de las sustituciones no afecta al resultado final de la derivación.

## Ejemplo de una derivación 

En una gramática para un lenguaje de programación completo, el _símbolo de inicio_ representa un programa completo y a menudo se denomina `<program>`. La gramática simple que se muestra en el ejemplo se utiliza para ilustrar las derivaciones.

```
<program> → begin <stmt_list> end
<stmt_list> → <stmt>
			| <stmt> ; <stmt_list>
<stmt> → <var> = <expression>
<var> → A | B | C
<expression> → <var> + <var>
			 | <var> – <var>
			 | <var>
```

El lenguaje descrito por la gramática del ejemplo sólo tiene una forma de sentencia: _asignación_. Un programa consta de la palabra especial `begin`, seguida de una **lista de sentencias separadas por punto y coma**, seguida de la palabra especial `end`. Una expresión es una única variable o dos variables separadas por un operador + o -. Los únicos nombres de variables en este lenguaje son A, B y C.

A continuación se presenta una derivación de un programa en este lenguaje:

```
<program> => begin <stmt_list> end
		  => begin <stmt> ; <stmt_list> end
		  => begin <var> = <expression> ; <stmt_list> end
		  => begin A = <expression> ; <stmt_list> end
		  => begin A = <var> + <var> ; <stmt_list> end
		  => begin A = B + <var> ; <stmt_list> end
		  => begin A = B + C ; <stmt_list> end
		  => begin A = B + C ; <stmt> end
		  => begin A = B + C ; <var> = <expression> end
		  => begin A = B + C ; B = <expression> end
		  => begin A = B + C ; B = <var> end
		  => begin A = B + C ; B = C end
```

Esta derivación, como todas las derivaciones, comienza con el símbolo de inicio, en este caso `<program>`. El símbolo => se lee "_deriva_". Cada cadena sucesiva de la secuencia se deriva de la cadena anterior _sustituyendo uno de los no-terminales por una de las definiciones de ese no-terminal_. Cada una de las cadenas de la derivación, incluido `<program>`, se denomina **forma sentencial**.

En esta derivación, el no terminal sustituido es siempre el no terminal situado más a la **izquierda** de la forma sentencial anterior. Las derivaciones que utilizan este orden de sustitución se denominan **derivaciones del extremo izquierdo**. La derivación continúa hasta que la forma sentencial no contiene ningún no-terminal. Esa forma sentencial, compuesta sólo de terminales o lexemas, es la _frase generada_.

Además de más a la izquierda, una derivación puede estar más a la derecha o en un orden que no sea ni más a la izquierda ni más a la derecha. _El orden de las derivaciones no afecta al lenguaje generado por una gramática_.

Eligiendo RHS (derivaciones del extremo derecho) como alternativas de reglas con las que sustituir los no terminales en la derivación, se pueden generar distintas frases en el lenguaje. Eligiendo exhaustivamente todas las combinaciones de opciones, se puede generar todo el lenguaje. Este lenguaje, como la mayoría de los demás, es _infinito_, por lo que no se pueden generar todas las sentencias del lenguaje en un tiempo finito.

Otro ejemplo de gramática para una parte de un lenguaje de programación típico.

```
<assign> → <id> = <expr>
<id> → A | B | C
<expr> → <id> + <expr>
	   | <id> * <expr>
	   | ( <expr> )
	   | <id>
```

La gramática del ejemplo describe sentencias de asignación cuyos lados derechos son expresiones aritméticas con operadores de multiplicación y suma y paréntesis. Por ejemplo, la sentencia

```
A = B * ( A + C )
```

es generado por la derivación LHS:

```
<assign> => <id> = <expr>
		 => A = <expr>
		 => A = <id> * <expr>
		 => A = B * <expr>
		 => A = B * ( <expr> )
		 => A = B * ( <id> + <expr> )
		 => A = B * ( A + <expr> )
		 => A = B * ( A + <id> )
		 => A = B * ( A + C )
```

# Desentrañando la Estructura de las Oraciones (Parsing trees)

En el ámbito de la lingüística computacional, los **árboles de sintaxis** (también conocidos como árboles de análisis sintáctico) juegan un papel fundamental en la comprensión de la estructura jerárquica de las oraciones. Estos diagramas jerárquicos representan la organización interna de las frases, revelando las relaciones entre sus componentes y la función que cada uno desempeña.

**Estructura de un Árbol de Sintaxis:**

- **Raíz:** El nodo superior representa el símbolo inicial de la gramática, que en el caso de oraciones suele ser el verbo principal.
- **Nodos Internos:** Etiquetados con símbolos no terminales, representan abstracciones gramaticales como sustantivos, verbos, adjetivos o frases.
- **Hojas:** Etiquetadas con símbolos terminales, representan los elementos más básicos de la oración, como palabras individuales o signos de puntuación.
- **Relaciones Jerárquicas:** Cada nodo interno tiene uno o más nodos hijos, que representan sus componentes subordinados. La posición relativa de los nodos refleja la estructura jerárquica de la oración.

Siguiendo el ejemplo anterior este seria el arbol sintactico de la sentencia `A = B * ( A + C )`

![[Pasted image 20240422211658.png]]

# Ambigüedad

Se dice que una gramática que genera una forma sentencial para la que hay **dos o más árboles de análisis sintáctico distintos es _ambigua_**. Consideremos la gramática mostrada en el siguiente ejemplo que es una variación del ejemplo anterior.

```
<assign> → <id> = <expr>
<id> → A | B | C
<expr> → <expr> + <expr>
	   | <expr> * <expr>
	   | ( <expr> )
	   | <id>
```

Esta gramática es ambigua porque la frase

```
A = B + C * A
```

tiene dos árboles de análisis distintos. La ambigüedad se debe a que la gramática especifica algo menos de estructura sintáctica. En lugar de permitir que el árbol de análisis sintáctico de una expresión crezca sólo a la derecha, esta gramática _permite el crecimiento tanto a la izquierda como a la derecha_.

![[Pasted image 20240422212632.png]]

La ambigüedad sintáctica de las estructuras del lenguaje es un problema porque _los compiladores suelen basar la semántica de esas estructuras en su forma sintáctica_. En concreto, el compilador elige el código que debe generarse para una sentencia examinando su árbol de análisis sintáctico. _Si una estructura de lenguaje tiene más de un árbol de análisis sintáctico, el significado de la estructura no puede determinarse de forma única_.

Hay otras características de una gramática que a veces son útiles para determinar si una gramática es ambigua. Entre ellas se encuentran las siguientes: 

- Si la gramática genera una frase con _más de una derivación a la izquierda_. 
- Si la gramática genera una frase con _más de una derivación a la derecha_.

_Algunos algoritmos de análisis sintáctico pueden basarse en gramáticas ambiguas_. Cuando un analizador sintáctico de este tipo encuentra una construcción ambigua, utiliza la información no gramatical proporcionada por el diseñador para construir el árbol de análisis sintáctico correcto. En muchos casos, una gramática ambigua puede reescribirse para que no sea ambigua, pero seguir generando el lenguaje deseado.