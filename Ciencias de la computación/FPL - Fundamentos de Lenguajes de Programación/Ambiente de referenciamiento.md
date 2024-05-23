---
tags:
  - FPL
---
**El ambiente de referenciamiento**, también conocido como **entorno de ejecución**, es un concepto fundamental en la programación que define el **contexto en el que se ejecuta una unidad de código** (por ejemplo, un subprograma o una función). Este contexto incluye el conjunto de **entidades** (variables, funciones, etc.) a las que se puede hacer referencia desde la unidad y los **valores** asociados a esas entidades.

# Componentes del ambiente de referenciamiento

1. **Entidades:** Son los elementos básicos del ambiente, como variables, funciones, parámetros, tipos de datos, etc. Cada entidad tiene un **nombre** que la identifica y una **ligadura** que la asocia a un valor o a otra entidad.
2. **Ligaduras:** Son las **conexiones** entre los nombres de las entidades y sus valores o definiciones. Las ligaduras pueden ser **estáticas** (establecidas en tiempo de compilación) o **dinámicas** (establecidas en tiempo de ejecución).
3. **Alcance:** Es la **extensión** dentro del código en la que una entidad es visible y accesible. El alcance puede ser **local** (limitado a una unidad de código específica) o **global** (visible desde cualquier parte del programa).

# Tipos de ambientes de referenciamiento

- **Ambiente local:** Es el conjunto de entidades **declaradas dentro de una unidad de código** y que solo son **visibles** desde esa unidad. El alcance de las entidades locales es **limitado** a la unidad donde se declaran.

- **Ambiente global/No local:** Es el conjunto de entidades **declaradas fuera de una unidad de código** pero que son **visibles** desde esa unidad. El alcance de las entidades globales es **mayor** que el de las entidades locales y abarca todo el programa o un módulo específico.

# Relación entre ambientes y alcance

Las **reglas de alcance** determinan cómo una unidad de código accede a las entidades de su ambiente de referenciamiento. Estas reglas varían según el lenguaje de programación, pero en general siguen los siguientes principios:

- **Prioridad del alcance local:** Si una entidad con el mismo nombre se declara tanto en el ambiente local como en el global, la referencia dentro de la unidad se resuelve a la entidad del **alcance local**.
- **Acceso a entidades globales:** Para acceder a una entidad global desde una unidad de código, se debe utilizar un **mecanismo específico** proporcionado por el lenguaje, como prefijos o modificadores especiales.
- **Alcance de las funciones:** Las funciones también tienen su propio ambiente local, que incluye las variables y parámetros declarados dentro de la función.

# Importancia del ambiente de referenciamiento

El ambiente de referenciamiento es crucial para la **correcta ejecución de un programa** por las siguientes razones:

- **Permite la organización modular del código:** Al separar las entidades en ambientes locales y globales, se facilita la organización del código y se evita la **ambigüedad** en los nombres de las entidades.
- **Controla el acceso a las entidades:** Las reglas de alcance garantizan que las entidades solo sean accesibles desde las unidades de código para las que fueron diseñadas, lo que mejora la **seguridad** y la **modularidad** del programa.
- **Facilita la reutilización de código:** Las entidades declaradas en ambientes globales pueden ser reutilizadas por diferentes unidades de código, lo que promueve la **modularidad** y la **eficiencia** del programa.

___
**En resumen, el ambiente de referenciamiento es un concepto fundamental en la programación que define el contexto en el que se ejecutan las unidades de código y controla el acceso a las entidades. Las reglas de alcance y las ligaduras juegan un papel crucial en la organización modular del código, la seguridad y la reutilización del código.**

**Recuerda que la comprensión del ambiente de referenciamiento es esencial para escribir código claro, organizado y eficiente.**