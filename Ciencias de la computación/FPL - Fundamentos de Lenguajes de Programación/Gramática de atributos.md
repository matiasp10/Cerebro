Una **_gramática de atributos_** es un dispositivo utilizado para describir más de la estructura de un lenguaje de programación de lo que se puede describir con una gramática libre de contexto. Una gramática de atributos _es una extensión de una gramática libre de contexto_. La extensión permite describir convenientemente ciertas reglas del lenguaje, como la compatibilidad de tipos. Antes de definir formalmente la forma de las gramáticas de atributos, debemos aclarar el concepto de semántica estática.

# Semántica estática

Hay algunas características de la estructura de los lenguajes de programación que son difíciles de describir con BNF, y algunas que son imposibles. 
Como ejemplo de una regla sintáctica difícil de especificar con BNF, considere las reglas de compatibilidad de tipos. En Java, por ejemplo, no se puede asignar un valor de coma flotante a una variable de tipo entero, aunque lo contrario sea legal. Aunque esta restricción puede especificarse en BNF, requiere símbolos no terminales y reglas adicionales. Si todas las reglas de tipado de Java se especificaran en BNF, la gramática se haría demasiado grande para ser útil, porque el tamaño de la gramática determina el tamaño del analizador sintáctico.

Como ejemplo de una regla sintáctica que no puede especificarse en BNF, considere la regla común de que todas las variables deben declararse antes de ser referenciadas. Se ha demostrado que esta regla no puede especificarse en BNF.

Estos problemas ejemplifican las categorías de reglas del lenguaje denominadas **reglas de semántica estática**. La semántica estática de un lenguaje _sólo está relacionada indirectamente con el significado de los programas durante la ejecución_; más bien tiene que ver con las formas legales de los programas (sintaxis más que semántica). Muchas reglas de la semántica estática de un lenguaje establecen sus restricciones de tipo. La semántica estática se llama así porque _el análisis necesario para comprobar estas especificaciones puede hacerse en tiempo de compilación_.

Debido a los problemas de describir la semántica estática con BNF, se ha ideado una variedad de mecanismos más potentes para esa tarea. Uno de estos mecanismos, las **gramáticas de atributos**, fue diseñado por **_Knuth_** (1968a) para describir tanto la sintaxis como la semántica estática de los programas.

Las gramáticas de atributos son un enfoque formal tanto para describir como para comprobar la corrección de las reglas semánticas estáticas de un programa. _Aunque no siempre se utilizan de manera formal en el diseño de compiladores, los conceptos básicos de las gramáticas de atributos se utilizan, al menos informalmente, en todos los compiladores_ (véase Aho et al., 1986).

# Conceptos básicos

Las gramáticas de atributos **_son gramáticas libres_** de contexto a las que se han añadido _atributos_, _funciones de cálculo de atributos_ y _funciones de predicado_. 

- **Atributos:** Son valores asociados a símbolos _terminales_ y _no terminales_ de la gramática. Se comportan como variables a las que se les asigna un valor durante el análisis sintáctico.

- **Funciones de cálculo de atributos:** También llamadas funciones semánticas, se asocian a reglas gramaticales. Definen cómo se calculan los valores de los atributos en función de los valores de otros atributos y símbolos en la derivación.

- **Funciones de predicado:** Están asociadas a reglas gramaticales y establecen las restricciones semánticas que deben cumplirse para que la regla sea válida.

# Definición

Una gramática de atributos es una gramática con las siguientes características adicionales:

## Atributos

- Cada símbolo gramatical `X` tiene un conjunto de atributos `A(X)`.
- `A(X)` se divide en dos conjuntos disjuntos: `S(X)` (atributos sintetizados) e `I(X)` (atributos heredados).
- Los **atributos sintetizados** se _propagan hacia arriba en el árbol de análisis sintáctico_.
- Los **atributos heredados** se _propagan hacia abajo y a través del árbol_.

## Funciones semánticas

- Cada regla gramatical tiene un conjunto de funciones semánticas.
- Las funciones semánticas calculan los valores de los atributos.
- Para una regla `X0 S X1 c Xn` los atributos sintetizados de `X0` se calculan con funciones de la forma `S(X0) = f(A(X1), c , A(Xn))`.
- Para una regla `Xj, 1 ... j ... n` los atributos heredados de los símbolos se calculan con funciones de la forma `I(Xj) = f(A(X0), c , A(X(j-1)))`. Esta forma impide que un atributo heredado dependa de sí mismo o de atributos situados a la derecha en el árbol de análisis sintáctico.

## Funciones de predicado

- Cada regla gramatical tiene un conjunto (posiblemente vacío) de funciones de predicado.
- Las funciones de predicado son expresiones booleanas sobre la unión del conjunto de atributos `{A(X0), c , A(Xn)}` que verifican la semántica estática.
- Solo se permiten derivaciones válidas donde cada predicado sea verdadero.

## Árbol de análisis sintáctico atribuido

- Un árbol de análisis sintáctico con valores de atributos adjuntos a cada nodo.
- Los valores de los atributos se calculan después de construir el árbol sin atribuir.

# Atributos intrínsecos

Los atributos intrínsecos son un tipo especial de **atributos sintetizados** asociados a los **nodos hoja** de un árbol de análisis sintáctico en gramáticas de atributos. Se caracterizan por tener sus valores **determinados fuera del árbol**, es decir, no se calculan mediante las funciones semánticas dentro del árbol de análisis.

## Características

- Son atributos **sintetizados** porque _su valor se propaga hacia arriba en el árbol_ de análisis.
- Se encuentran en los **nodos hoja**, que son los nodos que no tienen hijos.
- Sus valores se obtienen de **fuentes externas** al árbol, como la tabla de símbolos o la entrada del usuario.
- Sirven como **información inicial** para el cálculo de otros atributos en el árbol.

## Ejemplo

En un analizador sintáctico de un lenguaje de programación, un atributo intrínseco podría ser el **tipo de una variable**. Este tipo se determina en la **declaración de la variable** y se almacena en la tabla de símbolos. Al analizar una expresión que utiliza la variable, el atributo intrínseco del nodo hoja que representa la variable se recupera de la tabla de símbolos y se utiliza para calcular los tipos de los nodos padre que representan la expresión completa.

## Proceso de cálculo

1. **Inicialización:** Se asignan valores a los atributos intrínsecos de los nodos hoja.
2. **Propagación:** Se aplican las funciones semánticas para calcular los valores de los atributos sintetizados de los nodos no hoja, utilizando los valores de los atributos heredados y de los nodos hijos.
3. **Actualización:** Los valores de los atributos sintetizados se actualizan en cada nodo hasta llegar a la raíz del árbol.

# Ejemplo

```
 1. Syntax rule: <assign> → <var> = <expr>
 Semantic rule: <expr>.expected_type ← <var>.actual_type
 
 2. Syntax rule: <expr> → <var>[2] + <var>[3]
 Semantic rule: <expr>.actual_type ←
				 if (<var>[2].actual_type = int) and
 (<var>[3].actual_type = int)
					 then int
				 else real
				 end if
 Predicate: <expr>.actual_type == <expr>.expected_type
 
 3. Syntax rule: <expr> → <var>
 Semantic rule: <expr>.actual_type ← <var>.actual_type
 Predicate: <expr>.actual_type == <expr>.expected_type
 
 4. Syntax rule: <var> → A | B | C
 Semantic rule: <var>.actual_type ← look-up(<var>.string)
```

## Símbolos

- `<var>`: Representa un identificador de variable.
- `<expr>`: Representa una expresión aritmética.
- `int`: Tipo entero.
- `real`: Tipo real.
- `A`, `B`, `C`: Nombres de variables.

## Atributos

- `<var>.actual_type`: Tipo actual de la variable (`int` o `real`).
- `<expr>.expected_type`: Tipo esperado para la expresión (`int` o `real`).
- `<expr>.actual_type`: Tipo real calculado de la expresión (`int` o `real`).
- `<var>.string`: Nombre de la variable como cadena de caracteres.

## Funciones semánticas

- `look-up(<var>.string)`: Busca el tipo de la variable con nombre `<var>.string` en la tabla de símbolos y lo devuelve.

## Funciones de predicado

- `<expr>.actual_type == <expr>.expected_type`: Verifica si el tipo real de la expresión coincide con el tipo esperado.

## Reglas

1. **Asignación:**
    
    - Asigna el valor de la expresión `<expr>` a la variable `<var>`.
    - El tipo esperado de la expresión (`<expr>.expected_type`) se copia del tipo actual de la variable (`<var>.actual_type`).
        - Esto asegura compatibilidad de tipos en la asignación.

2. **Suma de variables:**
    
    - Define una expresión como la suma de dos variables con índices `[2]` y `[3]`. (La sintaxis específica con índices podría variar según la gramática).
    - El tipo real de la expresión (`<expr>.actual_type`) se calcula como:
        - `if`: Verifica si ambas variables son de tipo entero (`int`).
        - Si ambas son enteras, la expresión también es entera (`int`). (Función semántica implícita).
        - Si al menos una variable es real (`real`), la expresión completa se considera real (`real`). (Función semántica implícita).
    - **Predicado:** Verifica que el tipo real calculado (`<expr>.actual_type`) coincida con el tipo esperado (`<expr>.expected_type`).
        - Esto asegura consistencia de tipos en la suma.

3. **Variable como expresión:**
    
    - Una variable sola también se considera una expresión.
    - El tipo real de la expresión (`<expr>.actual_type`) se copia del tipo actual de la variable (`<var>.actual_type`).

4. **Tipo de variable:**
    
    - Define las posibles variables como `A`, `B`, y `C`.
    - El tipo actual de la variable (`<var>.actual_type`) se obtiene buscando su nombre (`<var>.string`) en la tabla de símbolos con la función `look-up`.
        - La tabla de símbolos debe estar definida previamente para almacenar los tipos de las variables.

## Análisis sintáctico

Supongamos la expresión `A = B[2] + C[3]`.

1. Se analiza la regla 1 (`<assign> → <var> = <expr>`).
2. Se verifica el tipo de `A` (`<var>.actual_type`) en la tabla de símbolos.
3. Se analiza la regla 2 (`<expr> → <var>[2] + <var>[3]`).
4. Se verifica el tipo de `B[2]` (`<var>[2].actual_type`) y `C[3]` (`<var>[3].actual_type`) en la tabla de símbolos.
5. Se aplica la función semántica para calcular `<expr>.actual_type` (entera si ambas variables son enteras, real si alguna es real).
6. Se aplica el predicado para verificar `<expr>.actual_type == <var>.actual_type`. Si no coinciden, se reporta un error de tipo.

## Resumen

Esta gramática de atributos permite verificar tipos en asignaciones y expresiones aritméticas simples. Mediante atributos, funciones semánticas y predicados, se garantiza la compatibilidad de tipos durante el análisis sintáctico, evitando errores en tiempo de ejecución.

# Calcular valores de atributos

El proceso de calcular los valores de los atributos del árbol se denomina decorar el árbol de análisis sintáctico. 

- Si todos los atributos son heredados se decora el árbol en orden descendente, de la raíz a las hojas. 
- Si todos los atributos son sintetizados se decora el árbol en orden ascendente, de las hojas a la raíz.
- Si tenemos atributos heredados y sintetizados no podemos decorar el árbol en una sola dirección. 

Por ejemplo la siguiente gramática con atributos sintetizados y heredados se puede decorar de la siguiente manera: 

```
1. <var>.actual_type ← look-up(A) (Regla 4)
2. <expr>.expected_type ← <var>.actual_type (Regla 1)
3. <var>[2].actual_type ← look-up(A) (Regla 4)
<var>[3].actual_type ← look-up(B) (Regla 4)
4. <expr>.actual_type ← either int or real (Regla 2)
5. <expr>.expected_type == <expr>.actual_type is either
 TRUE or FALSE (Regla 2)
```

En el siguiente árbol se observa el flujo de los valores de atributos para `A = A + B`.

![[figura37sintaxisysemantica|700]]

- Las líneas continuas se usan para el árbol de análisis sintáctico. 
- Las líneas discontinuas muestran el flujo de atributos del árbol.

En este otro árbol se muestran los valores finales de los atributos en los nodos (A se define como `real` y B como `int`).

![[fi38sintaxisysemantica|700]]

> [!warning] Evaluacion de las reglas sintacticas
> Evaluar las reglas semanticas es crucial para todos los compiladores.
> La principal dificultad de usar gramatica de atributos para toda la sintaxis y semantica de un lenguaje complejo actual es el tamaño.
> La gran cantidad de atributos y reglas necesarias lo hacen dificil de escribir y entender.