Texto extraído del libro
# Secuencias

La precondición más débil para una secuencia de declaraciones no puede ser descrita por un axioma, porque la precondición depende de los tipos particulares de declaraciones en la secuencia. En este caso, la precondición solo se puede describir con una regla de inferencia. Sean S1 y S2 declaraciones de programa adyacentes. Si S1 y S2 tienen las siguientes pre- y postcondiciones:

```
{P1} S1 {Q1}  
{Q1} S2 {Q2}
```

La regla de inferencia para una secuencia de dos declaraciones es:

$$\frac{\{P1\} S1 \{P2\}, \{P2\} S2 \{P3\}}{\{P1\} S1, S2 \{P3\}
}$$

Entonces, para nuestro ejemplo, ` {P1} S1; S2 {P3}` describe la semántica axiomática de la secuencia `S1; S2`. La regla de inferencia establece que para obtener la precondición de la secuencia, se calcula la precondición de la segunda declaración. Esta nueva afirmación se usa entonces como la postcondición de la primera declaración, que a su vez se puede usar para calcular la precondición de la primera declaración, que también es la precondición de toda la secuencia. Si `S1` y `S2` son las declaraciones de asignación:
$$x1= E1$$
y
$$x2= E2$$
Entonces tenemos
$$\{P3_{x2 \rightarrow E2}\} x2 = E2 \{P3\}$$
$$\{(P3_{x2 \rightarrow E2})_{x1 \rightarrow E1}\} x1= E1 \{P3_{x2 \rightarrow E2}\}$$
Por lo tanto, la precondición más débil para la secuencia x1 = E1; x2 = E2 con postcondición P3 es $\{(P3_{x2 \rightarrow E2})_{x1 \rightarrow E1}\}$.

Por ejemplo, considera la siguiente secuencia y postcondición:

```
y = 3 * x + 1;
x = y + 3;
{x < 10}
```

La precondición para la segunda declaración de asignación es 
$$y < 7$$
la cual se utiliza como postcondición para la primera declaración. La precondición para la primera declaración de asignación ahora se puede calcular:

```
3 * x + 1 < 7  
x < 2  
```

Por lo tanto, `{x < 2}` es la precondición tanto de la primera declaración como de la secuencia de dos declaraciones.