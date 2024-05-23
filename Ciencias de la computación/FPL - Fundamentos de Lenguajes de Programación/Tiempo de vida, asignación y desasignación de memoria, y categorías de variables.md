# Tiempo de vida

El tiempo de vida de una entidad en programación se refiere al _intervalo de tiempo durante el cual la entidad está ligada a un área de almacenamiento específico_. En otras palabras, es el **período en el que la entidad existe y puede ser utilizada por el programa**.

- **Nacimiento:** La entidad "_nace_" cuando se liga a una celda de memoria. Esto ocurre cuando se declara y se le asigna un valor inicial.

- **Muerte:** La entidad "muere" cuando se desliga de la celda de memoria. Esto ocurre cuando la entidad ya no se necesita y se libera el espacio de memoria que ocupaba.


En el caso de las variables, el tiempo de vida depende de su tipo y alcance:

- **Variables locales:** Su tiempo de vida está limitado al bloque de código en el que se declaran. Nacen cuando se entra en el bloque y mueren cuando se sale del mismo.

- **Variables globales:** Su tiempo de vida abarca toda la ejecución del programa. Nacen cuando se inicia el programa y mueren cuando este termina.


## Asignación y desasignación de memoria

- **Asignación:** Es el proceso de obtener una celda de memoria de un grupo de celdas disponibles para almacenar una entidad. Esta operación se realiza generalmente mediante la declaración y asignación inicial de una variable.

- **Desasignación:** Es el proceso de devolver una celda de memoria a un grupo de celdas disponibles para su posterior reutilización. Esta operación se realiza cuando la entidad ya no se necesita y se libera el espacio de memoria que ocupaba.


## Categorías de variables

Existen diferentes categorías de variables en función de su comportamiento en cuanto a la asignación y desasignación de memoria, y su tiempo de vida:

### 1. Variables estáticas

- **Características:**
    
    - Se ligan a una celda de memoria antes de la ejecución del programa y permanecen ligadas durante toda la ejecución.
    - Su tipo y tamaño se definen durante la compilación.
    - Son sensibles a la historia, es decir, retienen los valores de los módulos ejecutados anteriormente.
- **Ventajas:**
    
    - Eficiencia: Al estar cargadas en memoria, se accede a ellas rápidamente.
- **Desventajas:**
    
    - Falta de flexibilidad: No permiten recursividad.
    - Desperdicio de memoria: Si no se utilizan durante la ejecución, ocupan memoria innecesariamente.

#### Ejemplos

- Variables de FORTRAN, COBOL.
- Variables declaradas `static` en C y C++.

### 2. Variables dinámicas en pila

- **Características:**
    
    - La ligadura de almacenamiento se produce cuando se alcanza la ejecución de la declaración.
    - Se eliminan automáticamente al salir del bloque de código en el que se declararon.
- **Ventajas:**
    
    - Permiten la recursividad.
    - No desperdician memoria, ya que se alocan y desaloca conforme aparecen las variables.
- **Desventajas:**
    
    - Costo de tiempo en asignación y desasignación.
    - Los subprogramas no son sensibles a la historia.
    - Acceso ineficiente (direccionamiento indirecto).

#### Ejemplos

- La mayoría de las variables locales en lenguajes como Java, C++, Python, etc.

### 3. Variables dinámicas en heap explícito

- **Características:**
    
    - Se alocan y desaloca memoria manualmente durante la ejecución, utilizando directivas explícitas (como `new` y `delete` en C++).
    - Se referencian mediante punteros o referencias.
    - La ligadura del tipo es estática, mientras que el espacio se gestiona dinámicamente.
- **Ventajas:**
    
    - Ofrecen una gestión de almacenamiento dinámico flexible.
- **Desventajas:**
    
    - Ineficientes en términos de rendimiento.

#### Ejemplos

- Objetos en Java.
- Objetos dinámicos en C++ (`new` y `delete`).

### 4. Variables dinámicas en heap implícito

- **Características:**
    
    - Se alocan y desaloca memoria automáticamente mediante sentencias de asignación.
    - El tipo y el espacio se asignan en tiempo de ejecución.
- **Ventajas:**
    
    - Flexibilidad: Son útiles para definir listas, árboles, etc.
- **Desventajas:**
    
    - Ineficientes, ya que todos los atributos son dinámicos.
    - No confiables, por la posible pérdida de detección de errores.

#### Ejemplos

- Todas las variables de APL.
- Strings y arrays en PERL, JavaScript y PHP.