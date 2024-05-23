---
tags:
  - FPL
---
**La estructura general de un programa** define la organización del código y la forma en que se ejecutan las instrucciones. Existen diferentes tipos de estructuras de programa, cada una con sus propias características, ventajas y desventajas.

# Estructura Monolítica

- **Características:**
    - Todo el código se encuentra en un único bloque.
    - No existen módulos ni divisiones en unidades más pequeñas.
    - El alcance de las variables es global, es decir, todas las variables son visibles desde cualquier parte del programa.
- **Ejemplo:** COBOL
- **Ventajas:**
    - Simple y fácil de entender para principiantes.
- **Desventajas:**
    - **Difícil de mantener y modificar:** Al no existir módulos, realizar cambios en una parte del código puede afectar a todo el programa.
    - **Propagación de errores:** Si hay un error en una parte del código, puede afectar a todo el programa, dificultando su localización y corrección.
    - **Código poco reutilizable:** Las partes del código no se pueden reutilizar fácilmente en otros programas.
    - **Baja modularidad:** El programa no está dividido en módulos independientes, lo que dificulta su organización y comprensión.

# Estructura de Bloques Chatos

- **Características:**
    - El programa se divide en un programa principal y un conjunto de subprogramas separados.
    - Los subprogramas no pueden contener otros subprogramas.
    - Existen dos tipos de alcance:
        - **Local:** Limitado al subprograma donde se declara la variable.
        - **Global:** Visible desde cualquier parte del programa.
- **Ejemplo:** C, Fortran
- **Ventajas:**
    - **Mayor modularidad:** El programa se divide en módulos independientes, lo que facilita su organización y comprensión.
    - **Mejora la mantenibilidad:** Los cambios en un subprograma no afectan al resto del programa.
    - **Facilita la reutilización de código:** Los subprogramas se pueden reutilizar en otros programas.
- **Desventajas:**
    - **No permite la anidación de subprogramas:** Limita la estructura y la organización del código.
    - **Dificultad para manejar dependencias entre subprogramas:** Si un subprograma necesita acceder a datos de otro subprograma, la comunicación debe realizarse a través del programa principal, lo que puede complicar el diseño.

# Estructura de Bloques Anidados

- **Características:**
    - Similar a la estructura de bloques chatos, pero permite la anidación de subprogramas.
    - Existen tres tipos de alcance:
        - **Local:** Limitado al bloque donde se declara la variable.
        - **No local:** Visible desde los bloques anidados superiores.
        - **Global:** Visible desde cualquier parte del programa.
- **Ejemplo:** Algol, JavaScript
- **Ventajas:**
    - **Mayor flexibilidad:** Permite crear estructuras de programa más complejas y organizadas.
    - **Mejora la modularidad:** Facilita la división del programa en módulos independientes y jerarquizados.
    - **Facilita el manejo de dependencias entre subprogramas:** Los subprogramas anidados pueden acceder directamente a los datos de sus subprogramas padres.
- **Desventajas:**
    - **Mayor complejidad:** La anidación de subprogramas puede dificultar la comprensión del código, especialmente para principiantes.
    - **Riesgo de circularidades:** Si un subprograma llama a otro que lo llama a su vez, se puede crear una dependencia circular que genere errores.

___

**En resumen, la elección de la estructura general de un programa depende del tamaño, la complejidad y las necesidades del proyecto. La estructura monolítica es simple pero poco flexible, mientras que las estructuras de bloques chatos y anidados ofrecen mayor modularidad y flexibilidad, pero también aumentan la complejidad del código.**

**Recuerda que la correcta elección y utilización de la estructura de programa es fundamental para escribir código organizado, mantenible, reutilizable y eficiente.**