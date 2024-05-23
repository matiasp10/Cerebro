---
tags:
  - FPL
---
**Alcance y visibilidad** son dos conceptos fundamentales en la programación que determinan **dónde y cómo se pueden utilizar las entidades (variables, funciones, etc.) dentro de un programa**. Comprender estos conceptos es crucial para escribir código claro, organizado y eficiente.
___
# Alcance

> [!info] Definición
> Es la **porción del programa** en la que una entidad es **visible** y puede ser **referenciada**. En otras palabras, es el conjunto de sentencias donde la entidad tiene un **significado**.

- **Tipos de alcance:**
    - **Estático:** Las referencias a entidades se resuelven en **tiempo de compilación**. El compilador analiza el código y determina qué entidad se asocia a cada referencia según la estructura del programa. Los lenguajes con alcance estático son más **fáciles de leer**, **confiables** y **rápidos de ejecutar**. Ejemplos: C, Pascal, Java.
    - **Dinámico:** Las referencias a entidades se resuelven en **tiempo de ejecución**. El lenguaje determina la entidad asociada a cada referencia en base al **estado actual del programa** y al **flujo de ejecución**. Los lenguajes con alcance dinámico son más **flexibles**, pero pueden ser **más difíciles de entender** y **más lentos**. Ejemplos: Lisp, Smalltalk, Python.

# Visibilidad

> [!info] Definición
> Indica si una entidad es **visible** en una sentencia específica. En otras palabras, si la entidad puede ser **utilizada** en esa sentencia.

- **Relación con el alcance:** Una entidad es visible dentro de su **alcance** e invisible fuera de él.
- **Tipos de visibilidad:**
    - **Local:** Una entidad con **alcance local** solo es visible dentro de la unidad de código donde se declara (por ejemplo, una función o un bloque).
    - **Global:** Una entidad con **alcance global** es visible desde cualquier parte del programa.
    - **No local:** Una entidad con **alcance no local** es visible desde una unidad de código, pero no está declarada en esa unidad. Se declara en una unidad "padre" y puede ser accesible desde la unidad "hija" a través de mecanismos específicos del lenguaje.

# Ejemplos de alcance y visibilidad

## Ejemplo 1: Alcance estático en C

```C
int x = 10; // Entidad global (visible en todo el programa)

void funcion1() {
  int y = 20; // Entidad local de funcion1 (visible solo dentro de funcion1)
  printf("x = %d\n", x); // Acceso a entidad global
  printf("y = %d\n", y); // Acceso a entidad local
}

void funcion2() {
  printf("x = %d\n", x); // Acceso a entidad global
}

int main() {
  funcion1();
  funcion2();
  return 0;
}
```

En este ejemplo:

- La variable `x` tiene **alcance global** y es visible en todas las funciones y en el `main`.
- La variable `y` tiene **alcance local** en la función `{C}funcion1` y solo es visible dentro de esa función.

## Ejemplo 2: Alcance dinámico

```python
def funcion_externa():
  variable_global = 10  # Entidad global

  def funcion_interna():
    print(variable_global)  # Acceso a entidad global

  funcion_interna()

funcion_externa()
```

En este ejemplo:

1. La variable `variable_global` se declara dentro de la función `funcion_externa` y tiene un **alcance global**.
2. La función `funcion_interna` se define dentro de `funcion_externa` y tiene un **alcance local**.
3. Dentro de `funcion_interna`, se imprime la variable `variable_global`.

> [!seealso]- Ver mas
> 1. Cuando se llama a `{python}funcion_externa()`, se crea un **entorno de ejecución** para esa función.
> 2. Dentro del entorno de `{python}funcion_externa()`, se declara la variable `{python}variable_global` y se le asigna el valor 10.
> 3. Se define la función `{python}funcion_interna()` dentro del mismo entorno de `{python}funcion_externa()`.
> 4. Cuando se llama a `{python}funcion_interna()`, se crea un nuevo **entorno de ejecución** anidado dentro del entorno de `{python}funcion_externa()`.
> 5. Al intentar imprimir la variable `{python}variable_global` dentro de `{python}funcion_interna()`, el intérprete **busca primero** la variable en el **entorno actual** de `{python}funcion_interna()`.
> 6. Como no se encuentra la variable en el entorno actual, el intérprete **sube un nivel** en la jerarquía de entornos y busca la variable en el entorno de `{python}funcion_externa()`.
> 7. En el entorno de `{python}funcion_externa()`, se encuentra la variable `{python}variable_global` y se utiliza su valor (10) para la impresión.

# Importancia del alcance y la visibilidad

- **Organización del código:** Permitir la modularidad y la separación de preocupaciones, dividiendo el código en unidades con entidades propias.
- **Control de acceso:** Evitar conflictos de nombres y garantizar que las entidades solo sean utilizadas desde las unidades de código para las que fueron diseñadas.
- **Legibilidad:** Facilitar la comprensión del código al saber dónde y cómo se pueden utilizar las entidades.

# Búsqueda de declaraciones de variables

En lenguajes con **alcance estático**, como Ada, C y C++, el compilador realiza un análisis del código para determinar la **declaración correspondiente** a cada referencia a una variable. Este proceso se lleva a cabo de la siguiente manera:

1. **Búsqueda local:** El compilador **primero busca la declaración de la variable** dentro de la unidad de código (bloque, función, etc.) **donde aparece la referencia**.
2. **Búsqueda en antepasados estáticos:** Si la variable no se encuentra en la unidad de código actual, el compilador **revisa los antepasados estáticos** de esa unidad. Los antepasados estáticos son las unidades de código que contienen a la unidad actual (padre estático, abuelo estático, etc.).
3. **Declaración global:** Si la variable no se encuentra en ninguno de los antepasados estáticos, el compilador busca una **declaración global**. Las variables globales son aquellas declaradas fuera de cualquier unidad de código y son visibles desde cualquier parte del programa.

# Antepasado estático y grado de anidamiento

- **Antepasado estático:** Es un subprograma que contiene a otro subprograma en el código fuente.
- **Grado de anidamiento:** Es el nivel en el que se encuentra un subprograma y representa la cantidad de antepasados estáticos que tiene. El bloque principal tiene un grado de anidamiento de 0 ya que no tiene antepasados estáticos.

___

**En resumen, el alcance y la visibilidad son conceptos fundamentales para la programación que permiten escribir código organizado, confiable, eficiente y fácil de entender. Comprender los diferentes tipos de alcance y visibilidad es esencial para dominar un lenguaje de programación y escribir código de alta calidad.**

**Recuerda que la elección entre alcance estático y dinámico depende de las características del lenguaje y las necesidades del proyecto.**