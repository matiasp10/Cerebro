Los lenguajes de programación, al igual que los lenguajes naturales, se componen de un **conjunto de reglas** que definen cómo se forman las unidades válidas del lenguaje. Estas unidades, llamadas _sentencias o enunciados_, se construyen a partir de elementos más pequeños denominados **_lexemas_**. La sintaxis del lenguaje establece las normas para combinar estos lexemas de manera correcta y significativa.

# Simplicidad relativa de la sintaxis en lenguajes de programación

En comparación con la complejidad de la sintaxis en los lenguajes naturales, como el inglés, _la sintaxis de los lenguajes de programación suele ser relativamente simple_. Esto se debe a que los lenguajes de programación están diseñados con un propósito específico: la ejecución de instrucciones para realizar tareas informáticas. Su estructura está optimizada para la claridad y la precisión, evitando la ambigüedad y la complejidad que caracterizan a los lenguajes naturales.

# Componentes de la sintaxis

1. **Lexemas:** Los lexemas son las _unidades básicas e indivisibles de un lenguaje de programación_. Son los "bloques de construcción" fundamentales, como palabras clave, operadores, identificadores y literales. Cada lexema tiene un significado propio y representa un elemento específico del lenguaje.

2. **Tokens:** Los tokens son _categorías o grupos de lexemas_ que comparten características similares. Por ejemplo, el token "`identificador`" puede incluir lexemas como "`variable1`", "`funcion_suma`" o "`clase_principal`". Cada token representa una clase de lexemas relacionados.

3. **Reglas sintácticas:** Las reglas sintácticas definen _cómo se pueden combinar los lexemas y tokens para formar unidades de lenguaje válidas_, como expresiones, sentencias y programas completos. Estas reglas establecen la estructura y organización correctas de los elementos del lenguaje.

Considerando el siguiente ejemplo en **JAVA**:

```java
index = 2 * count + 17;
```

Los lexemas y tokens de esta declaración son:

| Lexemas | Tokens      |
| ------- | ----------- |
| index   | identifier  |
| =       | equal_sign  |
| 2       | int_literal |
| *       | mult_op     |
| count   | identifier  |
| +       | plus_op     |
| 17      | int_literal |
| ;       | semicolon   |

# Especificación de la sintaxis

Las descripciones formales de la sintaxis de los lenguajes de programación se suelen realizar utilizando herramientas como las **gramáticas formales** o **BNF** (Backus-Naur Form). Estas herramientas proporcionan un método riguroso y preciso para definir las reglas sintácticas del lenguaje, permitiendo una representación clara y comprensible de su estructura.
