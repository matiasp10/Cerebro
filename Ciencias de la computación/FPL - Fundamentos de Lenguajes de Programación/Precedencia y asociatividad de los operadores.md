
El orden en que se evalúan los operadores en una expresión que contiene varios de ellos es crucial para determinar el resultado final. Para evitar ambigüedades y garantizar que todos los programadores interpreten las expresiones de la misma manera, los lenguajes de programación definen reglas de **precedencia de operadores** y **asociatividad**.

# Precedencia

- **Determina qué operador se evalúa primero.**
- Los operadores con mayor precedencia se evalúan antes que los de menor precedencia.
- Si hay varios operadores con la misma precedencia, la **asociatividad** define el orden de evaluación.

Por ejemplo, en la expresión `x + y * z`, si la multiplicación (`*`) tiene mayor precedencia que la suma (`+`), se evaluará primero la multiplicación (`y * z`), y luego se sumará el resultado a `x`.

El orden correcto se especifica utilizando símbolos no terminales separados para representar los operandos de los operadores que tienen diferente precedencia. Esto requiere símbolos no terminales adicionales y algunas reglas nuevas. En lugar de utilizar `<expr>` para los dos operandos de + y * , podríamos utilizar tres no terminales para representar los operandos, lo que permite a la gramática forzar diferentes operadores a diferentes niveles en el árbol de análisis sintáctico. Si `<expr>` es el símbolo raíz de las expresiones, + puede ser forzado a la parte superior del árbol de análisis haciendo que `<expr>` genere directamente sólo operadores +, utilizando el nuevo no terminal, `<term>`, como operando derecho de +. A continuación, podemos definir `<term>` para generar operadores * , utilizando `<term>` como operando izquierdo y un nuevo no terminal, `<factor>`, como operando derecho. Ahora, * siempre estará más abajo en el árbol de análisis sintáctico, simplemente porque está más lejos del símbolo de inicio que + en cada derivación.

```
<assign> → <id> = <expr>
<id> → A | B | C
<expr> → <expr> + <term>
	   | <term>
<term> → <term> * <factor>
	   | <factor>
<factor> → ( <expr> )
	   | <id> 
```

```
<assign> => <id> = <expr>
		 => A = <expr>
		 => A = <expr> + <term>
		 => A = <term> + <term>
		 => A = <factor> + <term>
		 => A = <id> + <term>
		 => A = B + <term>
		 => A = B + <term> * <factor>
		 => A = B + <factor> * <factor>
		 => A = B + <id> * <factor>
		 => A = B + C * <factor>
		 => A = B + C * <id>
		 => A = B + C * A
```

# Asociatividad

- **Indica en qué dirección se evalúan los operadores con la misma precedencia.**
- De izquierda a derecha o de derecha a izquierda.

Cuando una expresión incluye dos operadores que tienen la misma precedencia (como suelen tener `*` y `/`)-por ejemplo, `A / B * C`-se requiere una regla semántica para especificar cuál debe tener _precedencia_. Esta regla se denomina **_asociatividad_**.

Como en el caso de la precedencia, una gramática de expresiones puede implicar correctamente la asociatividad de operadores. Considere el siguiente ejemplo de una sentencia de asignación:

```
A = B + C + A
```

![[Drawing 2024-04-24 14.51.04.excalidraw]]

En este árbol sintáctico se muestra el operador de adición izquierdo por debajo del operador de adición derecho.
Este es el orden correcto si se supone que la suma es _asociativa izquierda_, que es lo típico. En la mayoría de los casos, la asociatividad de la suma en un ordenador es irrelevante. En matemáticas, la suma es asociativa, lo que significa que los órdenes de evaluación asociativo izquierdo y derecho significan lo mismo. Es decir, (A + B) + C = A + (B + C). 
Sin embargo, la _suma de coma flotante en un ordenador no es necesariamente asociativa_. Por ejemplo, supongamos que los valores de coma flotante almacenan siete dígitos de precisión.
La _resta y la división no son asociativas_, ni en matemáticas ni en un ordenador. Por lo tanto, una correcta asociatividad puede ser esencial para una expresión que contenga cualquiera de ellas.

Cuando una regla gramatical tiene su LHS que también aparece al principio de su RHS, se dice que la regla es **recursiva izquierda**. 
Esta recursividad izquierda _especifica la asociatividad izquierda_. Por ejemplo, la recursividad izquierda de las reglas de la gramática del ejemplo anterior hace que tanto la suma como la multiplicación sean asociativas por la izquierda. 
Por desgracia, la recursividad izquierda impide el uso de algunos algoritmos importantes de análisis sintáctico. Cuando se van a utilizar dichos algoritmos, la gramática debe modificarse para eliminar la recursividad izquierda. Esto, a su vez, impide que la gramática especifique con precisión que ciertos operadores son asociativos izquierdos. Afortunadamente, _la asociatividad a la izquierda puede ser impuesta por el compilador_, aunque la gramática no lo dicte.

En la mayoría de los lenguajes que lo proporcionan, _el operador de exponenciación es asociativo a la derecha_. Para indicar la asociatividad a la derecha, se puede utilizar la **recursividad a la derecha**. Una regla gramatical es recursiva por la derecha si el LHS aparece en el extremo derecho del RHS. Como por ejemplo:

```
<factor> → <exp> ** <factor>
	     |<exp>
<exp> → ( <expr> )
	  |id
```

podría utilizarse para describir la exponenciación como un operador asociativo a la derecha.

