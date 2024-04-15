## Sintaxis

La sintaxis se refiere a las **_reglas que definen cómo se escribe un programa en un lenguaje de programación específico_**. Es la estructura formal del código, que define cómo se combinan los símbolos y palabras clave para crear expresiones y declaraciones válidas.

## Semántica

La semántica se refiere al significado de un programa. Es lo que el programa realmente hace cuando se ejecuta. La semántica incluye:

- **Comprobación de tipos:** Se verifica que el programa esté escrito correctamente y que los tipos de datos de las expresiones sean compatibles.
- **Evaluación:** Se define cómo se calculan los valores de las expresiones y cómo se ejecutan las instrucciones.

### Ejemplo

```python
x + y
```

Sin embargo, la semántica de la expresión depende de los tipos de `x` e `y`. Si `x` e `y` son números, la expresión se evalúa como la suma de sus valores. Si `x` e `y` son cadenas, la expresión se evalúa como la concatenación de sus valores.
## Sintaxis

Un enlace de variable en ML se escribe de la siguiente forma:

```sml
val x = e;
```

Donde:

- `val` es una **_palabra clave_** que indica que se está definiendo una variable.
- `x` es el **_nombre de la variable_** que se está definiendo.
- `e` es una expresión que define el **_valor inicial de la variable_**.
- El **_punto y coma_** es opcional en un archivo, pero necesario en el bucle **leer-evaluar-imprimir** para indicar el final del enlace.

## Semántica

La semántica de un enlace de variable se divide en dos partes:

- **_Comprobación de tipo:_** Se **verifica que la expresión** `e` tenga un **tipo válido**. El tipo de la variable `x` se establece como el tipo de la expresión `e`. Esta verificación se realiza utilizando el _"entorno estático actual"_, que es el _conjunto de tipos de las variables definidas anteriormente_.
- **_Evaluación:_** Se **calcula el valor de la expresión** `e` y se asigna a la variable `x`. Esta evaluación se realiza utilizando el _"entorno dinámico actual"_, que es el _conjunto de valores de las variables definidas anteriormente_.

## Tipos

- **_Valor:_** Una _expresión que no tiene más cálculo que realizar_. Por ejemplo, 17 es un valor.
- **_Expresión:_** _Cualquier construcción válida del lenguaje que puede ser evaluada para obtener un valor_. **No todas las expresiones son valores**. Por ejemplo, 8+9 es una expresión, pero no un valor.

**Ejemplo:**

```sml
val x = 17;
val y = x + 5;
```

En este ejemplo:

- El enlace `val x = 17;` define una variable `x` con el valor 17.
- El enlace `val y = x + 5;` define una variable `y` con el valor 22 (17 + 5).

___
Es cierto que las descripciones de programas de ML (bindings, expresiones, tipos, valores, entornos) pueden sonar abstractas al principio. Sin embargo, son la base fundamental para construir un lenguaje preciso y conciso. Vamos a desmitificar estas definiciones con ejemplos concretos:
### Constantes enteras

- **Sintaxis:** Una _secuencia de dígitos_, como "123" o "4567".
- **Comprobación de tipo:** Siempre tienen tipo `int`, sin importar el entorno estático.
- **Evaluación:** Se _evalúan a sí mismas_, es decir, el valor de "123" es 123 en cualquier entorno dinámico. Son **valores**.
### Adición

- **Sintaxis:** Se escribe como `e1 + e2`, donde `e1` y `e2` _son expresiones_.
- **Comprobación de tipo:** Solo se verifica si `e1` y `e2` tienen tipo `int` _en el mismo entorno estático_. Si no, no se comprueba el tipo.
- **Evaluación:** Se evalúan `e1` y `e2` a `v1` y `v2` respectivamente. El resultado es la suma de `v1` y `v2`.

### Variables

- **Sintaxis:** Una _secuencia de letras_, guiones bajos, etc., como "x" o "suma".
- **Comprobación de tipo:** Se busca el tipo de la variable en el _entorno estático actual_.
- **Evaluación:** Se busca el valor de la variable en el _entorno dinámico actual_.

### Condicionales

- **Sintaxis:** Se escribe como `{sml}if e1 then e2 else e3`, donde `e1`, `e2` y `e3` son _expresiones_.
- **Comprobación de tipo:** Se verifica que `e1` sea de tipo `bool` y que `e2` y `e3` tengan el mismo tipo. El tipo de la expresión completa es el tipo de `e2` y `e3`.
- **Evaluación:** Se evalúa `e1`. Si es verdadero, se evalúa `e2`. Si es falso, se evalúa `e3`. El resultado de la evaluación completa es el resultado de evaluar `e2` o `e3`.

### Constantes booleanas

- **Sintaxis:** `true` o `false`.
- **Comprobación de tipo:** Siempre tienen tipo `bool`, sin importar el entorno estático.
- **Evaluación:** Se _evalúan a sí mismas_, es decir, el valor de `true` es `true` en cualquier entorno dinámico. Son **valores**.

### Comparación menor que

- **Sintaxis:** Se escribe como `e1 < e2`, donde `e1` y `e2` son expresiones.
- **Comprobación de tipo:** Solo se verifica si `e1` y `e2` tienen tipo `int` en el mismo _entorno estático_. Si no, no se comprueba el tipo.
- **Evaluación:** Se evalúan `e1` y `e2` a `v1` y `v2` respectivamente. El resultado es `true` si `v1` es menor que `v2`, y `false` en caso contrario.


> [!tip]- Siempre que aprendas una nueva construcción en un lenguaje de programación, pregúntate
> 
> 1. **¿Cuál es la sintaxis?**
> 2. **¿Cuáles son las reglas de comprobación de tipos?**
> 3. **¿Cuáles son las reglas de evaluación?**
> 
> Al comprender estas tres preguntas, estarás mejor preparado para usar la construcción correctamente y escribir código preciso y eficiente.

## Uso de `use`

La palabra clave `use` en ML se utiliza para _incluir bindings (enlaces) desde un archivo externo en el entorno actual_. Esto permite organizar el código en módulos y reutilizar definiciones de variables y funciones.

```sml
use "foo.sml";
```

El comando anterior _incluye todos los bindings del archivo_ `foo.sml` en el entorno actual. El tipo de la expresión `use` es `unit` y su valor es `()`, el único valor de tipo `unit`. Sin embargo, el efecto principal de la expresión `use` es cargar las definiciones del archivo `foo.sml`.

## Inmutabilidad de las variables

En ML, las variables son **_inmutables_** una vez que se les asigna un valor. Un **binding** _crea una asociación entre un nombre de variable y un valor_. Una vez que se crea un binding, no se puede modificar el valor asociado a la variable.

```sml
val x = 8 + 9;
```

El binding anterior crea una variable `x` con el valor 17. En el entorno actual, `x` siempre se referirá a este valor. No hay una "sentencia de asignación" en ML para cambiar el valor de una variable.

Es posible _crear un nuevo binding con el mismo nombre que una variable existente_, pero esto **crea un nuevo entorno en el que la nueva variable oculta la anterior** (shadowing).

```sml
val x = 19;
```

El binding anterior crea una **nueva variable** `x` con el valor 19 en un **nuevo entorno**. En este entorno, `x` se refiere a 19, mientras que en el entorno anterior `x` se refiere a 17.

La inmutabilidad de las variables es una característica importante de ML que ayuda a evitar errores y facilita el razonamiento sobre el comportamiento del programa.