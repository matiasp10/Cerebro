### Entidades y ligaduras

Se denomina entidad a un elemento sobre el cual trabaja un programa. Esta posee atributos, los cuales están asociados a la entidad por el mecanismo de ligadura. Esta asociación se puede producir en tiempo de compilación (ligadura estática) o durante la ejecución del programa (ligadura dinámica). El momento en el cual se crea la ligadura o en el que se decidió su implementación se denomina tiempo de ligadura.

**Ligadura estática**: la asociación se produce antes de la ejecución del programa, por lo que puede darse en tiempo de compilación o de diseño.

Las características de este tipo de ligadura son:

- Menor flexibilidad.
- Mayor seguridad (detección temprana de errores).
- Mayor eficiencia.
- Aplicable a lenguajes compilados.

**Ligadura dinámica**: la asociación se produce durante la ejecución del programa, no puede realizarse en un paso anterior. Las características de este tipo de ligadura son:

- Mayor flexibilidad.
- Menor seguridad.
- Mayor costo de ejecución.
### Sintaxis y semántica

Los lenguajes de programación deben seguir ciertas _reglas que determinan la validez de las sentencias empleadas_. Este conjunto de reglas define la sintaxis del lenguaje de programación y están determinadas por las **reglas léxicas** (_definen el conjunto de caracteres y sus combinaciones validas_) y las **reglas sintácticas** (_definen las reglas de mayor complejidad, mediante la combinación de elementos léxicos_).

Dentro de los elementos de la sintaxis de un lenguaje mencionamos:

- alfabeto.
- identificadores.
- palabras reservadas.
- espacios en blanco.
- símbolos de operadores.
- expresiones.
- delimitadores de código.
- comentarios.

El significado que toma cada uno de los elementos de un lenguaje de programación de acuerdo al contexto define la semántica del lenguaje. La sintaxis no tiene en cuenta el contexto, mientras que la semántica sí lo hace. Las variables, los valores y las expresiones son algunos de los elementos principales de la semántica de un lenguaje de programación. Estos elementos tienen una semántica que indica cómo debe definírselos.