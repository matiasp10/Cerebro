Cuando se nos dice de escribir un programa el primer problema es encontrar que es lo que realmente queremos que haga el mismo.
La segunda dificultad es que a veces el programa es demasiado grande para encararlo de una, esta se soluciona fragmentando el programa en pequeñas partes funcionales.
Desde una vaga formacion del problema a una solucion bien estructurada se le llama el diseño de programa sistematico.
usaremos el BSL (Basic Student Lenguage)

### Glosario

- **Abstracción** (verbo)  Abstraer significa tomar dos o más expresiones o funciones que son muy similares, y convertir esas diferencias en parámetros de una función abstracta de propósito más general. Las recetas Abstracción a partir de ejemplos y Abstracción a partir de comentarios de tipos cubren el diseño de funciones abstractas. También es posible diseñar tipos abstractos, pero no lo haremos en este curso.  
- **Acumulador**  Un acumulador es un parámetro que mantiene un registro de la información que estaba disponible anteriormente en una recursión estructural, a veces esa información se construye, o se acumula a través de la recursión. Un acumulador también puede ser una variable mutable usada con una construcción de bucle para lograr el mismo efecto.  
- **Tamaño arbitrario**  La información (o datos) de tamaño arbitrario es información (o datos) cuyo tamaño no se conoce en el momento de diseñar el programa. Un "jugador con un nombre y un número de camiseta" no tiene un tamaño arbitrario, es un dato compuesto con dos partes. Pero "todos los jugadores de la liga" tiene un tamaño arbitrario porque no sabemos de antemano cuántos jugadores habrá.
- **Argumento**  Un argumento es un valor que se pasa a una función o a una operación primitiva cuando es llamada. Los argumentos son los valores que resultan de evaluar los operandos en la llamada a la función o primitiva. 
- **Datos atómicos**  Los datos atómicos son una forma de datos que no pueden descomponerse en piezas de datos más pequeñas. [Véase Datos atómicos no disociables].  
- **Retroceso**  En una búsqueda de retroceso, el recorrido se realiza primero por una rama del árbol (o grafo). Si esa rama falla, la búsqueda a lo largo de esa rama produce un valor de fallo especial, como false, y la función invocadora busca entonces en la siguiente rama. De este modo, la búsqueda retrocede hasta el nodo más cercano del árbol y sigue la siguiente rama.
- **Booleano**  Boolean es un tipo primitivo que sólo consta de dos valores: verdadero y falso.  
- **BST**  Un BST, o árbol de búsqueda binario, es una estructura de datos utilizada para almacenar datos que han sido ordenados de alguna manera. Binario significa que cada nodo tiene como máximo dos hijos. "Búsqueda" significa que los nodos están estructurados en un orden particular: para cualquier nodo n con una clave k, todos sus hijos con una clave menor que k están en la sub-rama izquierda. Todos sus hijos con una clave mayor que k están en la subrama derecha. "Árbol" describe el aspecto que tendría esta estructura si se dibujara en papel.  
- **Closure**  Una clausura es una función definida localmente en la que el cuerpo de la función utiliza un parámetro de la definición de la función que la encierra. El cierre puede definirse con local o lambda, pero debe definirse dentro de otra función. En el ejemplo siguiente, la función de ayuda bigger? es un cierre.![[Pasted image 20240111221102.png]]
- **Comentario**  En BSL, todo el texto de una línea después de ; es un comentario. Es ignorado por BSL, y está destinado a comunicar a los lectores humanos algo importante sobre el programa.  
- **Compuesto**  Los datos compuestos son un único elemento de datos que está formado por más de un valor relacionado, como el nombre, el apellido y la edad de una persona. En este curso los datos compuestos se crean utilizando define-struct.  
- **Constante**  Una constante es un valor con nombre definido mediante define. Se llama constante porque una vez definida nunca cambia.  
- **Datos**  Datos es el sustantivo masivo para los valores en nuestros programas, incluyendo números, cadenas, imágenes, listas y datos compuestos. En el diseño de programas tomamos una serie de decisiones sobre cómo representar la información como datos. [Véase Definiciones de datos.]
- **Definición de datos**  Una definición de datos describe un plan para representar información del dominio del programa utilizando datos dentro del programa. Una definición de datos incluye un comentario de tipo que describe cómo formar el nuevo tipo de datos; una interpretación que describe cómo los datos representan información en el dominio del programa; ejemplos del nuevo tipo de datos y una plantilla dirigida por datos para funciones que consumen un único argumento del nuevo tipo de datos. Las definiciones de datos se diseñan utilizando la receta Cómo diseñar datos. [Ver Definiciones de Datos].  
- **Grafo acíclico dirigido**  Un grafo acíclico dirigido (DAG) es un grafo dirigido que no contiene ciclos. En otras palabras, es imposible empezar en un nodo, seguir las aristas del grafo y visitar el mismo nodo más de una vez.  
- **Grafo dirigido**  Un grafo dirigido es un grafo en el que las aristas entre los nodos tienen una única dirección.  
- **Enumeración**  Forma de definición de datos en la que la información del dominio del programa consiste en un número fijo de valores distintos. [Véase Enumeración.]
- **Evaluar**  En BSL, la ejecución de un programa se realiza evaluando expresiones para producir valores. 
- **Expresión**  Una expresión es un elemento de un programa que se evalúa para producir un valor. 
- **Función**  Las funciones en los programas son muy similares a las funciones en matemáticas. En matemáticas, a una función f(x) se le puede pasar un valor para x, y producirá un resultado basado en ese valor. Las funciones en los programas actúan de la misma manera. Tienen un nombre (en el ejemplo de matemáticas este nombre era "f ") y uno o más parámetros (en el ejemplo de matemáticas, el parámetro era "x"). Las funciones también tienen un cuerpo, que es una expresión que se evalúa para producir el valor resultante de la función. [Véase Definiciones de funciones.]  
- **Gráfico**  Un grafo es un conjunto de nodos y un conjunto de aristas tales que cada arista une dos nodos.
- **Función auxiliar**  En el diseño de una función compleja a menudo es útil diseñar subfunciones que la función principal pueda llamar para hacer parte de su trabajo. Estas subfunciones se denominan a veces funciones auxiliares.  
- **Imagen**  Imagen es un tipo primitivo de datos que representa una imagen, como el resultado de una función de imagen incorporada o una imagen copiada y pegada. [Véase Cadenas e imágenes.]  
- **Entero**  Entero es un tipo primitivo de datos que representa cualquier número entero positivo o negativo (... -2, -1, 0, 1, 2 ...).  
- **Itemización**  Forma de definición de datos en la que los datos se componen de dos o más subclases, en la que al menos una de las subclases no es un valor distinto. [Véase Itemización.]  
- **Lambda**  Las expresiones lambda permiten crear funciones anónimas (o sin nombre). Son convenientes cuando es necesario pasar una función como argumento a otra función.
- **Lista**  Una lista es una estructura de datos que representa una lista de elementos. Si no hay nada en la lista, su valor está vacío, mientras que si hay datos en la lista (digamos los números 1 2 3), el valor sería (cons 1 (cons 2 (cons 3 vacío))). Los conses son un tipo de datos compuestos: El constructor es cons, se puede acceder a los distintos elementos de la lista utilizando los selectores first y rest, y hay predicados disponibles como cons? y empty?  
- **Itemización de datos mixtos**  Una itemización de datos mixta es aquella en la que al menos dos de las subclases están representadas por datos de tipos diferentes. [Véase Itemización.]  
- **Variable mutable**  Una variable mutable es una variable cuyo valor puede modificarse después de haber sido definida. Las variables mutables no se utilizan en la Parte 1 del curso.  
- **Natural**  Natural es un dato de tipo primitivo que representa cualquier número entero no negativo (0, 1, 2, 3...).
- **Número**  Número es un tipo primitivo de datos que representa cualquier número, incluyendo 0, fracciones, números decimales y números inexactos. Por ejemplo, 1, -5, 3.4, 134.9853957 y #i1.4142135623730951 son todos Números. 
- **Operando**  Las expresiones que siguen al nombre de la función en una expresión de llamada a función (o al nombre del operador en una expresión de llamada primitiva) se denominan operandos.
- **Operador**  El lenguaje BSL proporciona operadores primitivos para operar con datos primitivos. Incluyen +, -, string-append, substring, image-width y muchos otros.
- **Parámetro**  Un parámetro es un identificador (o nombre) utilizado en una declaración de función que representa el valor cambiante, o la variable. El parámetro o parámetros aparecen entre paréntesis justo después del nombre de la función. Dentro del cuerpo de la función, los parámetros representan los argumentos cada vez que se llama a la función.
  (define (bulb c)                  ;In this function definition, c
  (color 40 "solid" c))           ;is the only parameter of the function.
                                  ;The body of the function is itself a primitive call
                                  ;to the primitive operator color. The call has 3 operands.
  
(bulb (string-append "r" "ed"))   ;In this function call expression 
                                  ;(string-append "r" "ed") is the operand
                                  ;When the function call is evaluated,
                                  ;"red" is the argument.

- **Predicado**  Función o primitiva que produce un valor booleano. [Véase booleanos y expresiones if].  
- **Primitiva**  Una primitiva es un bloque de construcción básico proporcionado por BSL que usamos cuando diseñamos nuestros programas. BSL proporciona datos primitivos y operaciones primitivas sobre los datos.
- **Dominio del programa**  El dominio de un programa es el objeto o la naturaleza del problema. Así, en un sistema de nóminas, el dominio del programa incluye conceptos como empleados y salarios, etc. En un sistema de transporte público, incluiría conceptos como paradas de autobús, rutas y horarios. El enfoque SPD, y en particular las recetas HtDD y HtDW, hacen hincapié en centrarse en el dominio del problema (salarios y nóminas) antes que en el dominio de la solución (Número, Entero, etc.). [Véase Definición de datos].  
- **Propósito**  Un propósito es un comentario que se escribe cuando se diseña una función y que explica en palabras lo que se supone que debe producir la función. Intente que los propósitos no superen los 78 caracteres, pero sea específico.
- **Recursión**  Cuando una función se llama a sí misma decimos que la función es recursiva. Cuando un comentario de tipo se refiere a sí mismo, decimos que el tipo implica autorreferencia. Ambas son formas de recursividad.  
- **Selector**  Un selector es una función que se utiliza en datos compuestos para "seleccionar" (u obtener los valores de) los distintos campos de los datos. El nombre del selector consiste en el nombre de la estructura de datos seguido de un guión y, a continuación, el nombre del campo al que accede el selector El argumento del selector debe ser el dato compuesto específico para el que se desea acceder al campo. Por ejemplo, con una definición de datos como ![[Pasted image 20240111221536.png]] Entonces, para un gato c, las expresiones serían (cat-x c) para obtener la coordenada x del gato y (cat-y c) para obtener la coordenada y del gato.
- **Firma**  Una firma es la primera línea escrita en el diseño de una función. Es un comentario que especifica los tipos de argumentos que consumirá la función, así como qué tipo de datos produce la función.  
- **Cadena**  Una cadena es un tipo de dato primitivo formado por símbolos "encadenados". Las cadenas siempre van entre comillas dobles "así". Es importante tener en cuenta que si se escriben números dentro de una cadena, se trata de una cadena y no de un número. "123" no tiene el valor de ciento veintitrés, ya que es una Cadena, mientras que 123 sí tiene el valor de ciento veintitrés, ya que es un Número. [Véase Cadenas e imágenes].  
- **Stub**  Un stub es una versión simulada de una función que especifica el nombre propio de la función y el parámetro(s), pero donde el cuerpo de la función es simplemente un valor del tipo de retorno propio. Consulte la página Funciones HtD para obtener más información sobre los stubs.
- **Plantilla**  Una plantilla describe la estructura básica o columna vertebral de la función independientemente de sus detalles. Las plantillas basadas en datos se basan en el tipo de datos que consume la función. Otros tipos de plantillas se basan en saber algo sobre la estructura básica del cálculo que realizará la función. La idea de la plantilla es permitirnos escribir rápidamente lo que sabemos sobre la definición de la función "antes de llegar a los detalles".  
- **Comentario de tipo**  Un comentario de tipo es un comentario en una definición de datos que define cómo se forma el nuevo tipo de datos. [Véase Atómico No Distinto].  
- **Valor**  Un valor es un elemento de datos, como 1, "foo", etc.

### Expresiones

```
(<primitive><expresion>...)
```

### Evaluación 

1° regla: regla de los primitivos

### Strings e Images

string-append
string-length
substring

require 2htdp/image

(circle 10 "solid" "red")

above
overlay