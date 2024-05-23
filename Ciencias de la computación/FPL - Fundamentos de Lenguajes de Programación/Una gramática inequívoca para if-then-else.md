Las reglas BNF para una sentencia `if-then-else` de Ada son las siguientes:

```
<if_stmt> → if <logic_expr> then <stmt>
			if <logic_expr> then <stmt> else <stmt>
```

Si además tenemos `<stmt> → <if_stmt>`, esta gramática es ambigua. La forma sentencial que ilustra esta ambigüedad es

```
if <logic_expr> then if <logic_expr> then <stmt> else <stmt>
```

Considere el siguiente ejemplo de esta construcción:

```
if done == true
	 then if denom == 0
		 then quotient = 0;
		 else quotient = num / denom;
```

El problema es que si utilizamos el siguiente árbol sintáctico como base para la traducción, la cláusula `else` se ejecutaría cuando `done` no es verdadero, lo que probablemente no era lo que pretendía el autor de la construcción.

![[Drawing 2024-04-24 15.28.19.excalidraw|600]]

A continuación desarrollaremos una gramática inequívoca que describa esta sentencia `if`. La regla para las construcciones `if` en muchos idiomas es que una cláusula `else`, cuando está presente, _se empareja con la más cercana anterior no emparejada_ `then`.

Por lo tanto, no puede haber una sentencia `if` sin `else` entre un `then` y su `else` coincidente. Por lo tanto, para esta situación, las sentencias deben distinguirse entre las que coinciden y las que no coinciden, donde las sentencias que no coinciden son `ifs` sin `else` y todas las demás sentencias coinciden.

El problema de la gramática anterior es que trata todas las sentencias como si tuvieran el mismo significado sintáctico, es decir, como si todas coincidieran.

_Para reflejar las distintas categorías de enunciados, deben utilizarse distintas abstracciones, o no terminales_. A continuación se presenta una gramática inequívoca basada en estas ideas:

```
<stmt> → <matched> | <unmatched>
<matched> → if <logic_expr> then <matched> else <matched>
		  |any non-if statement
<unmatched> → if <logic_expr> then <stmt>
		    | if <logic_expr> then <matched> else <unmatched>
```

Sólo hay un árbol de análisis sintáctico posible, utilizando esta gramática, para la siguiente forma sentencial:

![[Drawing 2024-04-24 15.43.47.excalidraw|600]]

```
if <logic_expr> then if <logic_expr> then <stmt> else <stmt>
```

