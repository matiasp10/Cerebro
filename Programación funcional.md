---
tags:
  - "#CS"
  - ver
---
Es un paradigma de programación declarativa basado en el uso de **verdaderas funciones matemáticas**.

La programación funcional tiene sus raíces en el cálculo **_lambda_**, un sistema formal desarrollado en los años 1930 para investigar la naturaleza de las funciones, la naturaleza de la computabilidad y su relación con la recursión.

Los lenguajes de programación funcional, especialmente los puramente funcionales, han sido enfatizados en el _ambiente académico_ y no tanto en el desarrollo comercial o industrial. Sin embargo, lenguajes de programación funcional como **Lisp** (Scheme, Common Lisp, etc.), **Erlang**, **Rust**, **Objective** **Caml**, **Scala**, **F#** y **Haskell**, también han sido utilizados en aplicaciones comerciales e industriales. También es utilizada en la industria a través de lenguajes de dominio específico como **R** (estadística), **Mathematica** (cómputo simbólico), **J** y **K** (análisis financiero). Los lenguajes de uso específico usados comúnmente como **SQL** y **Lex/Yacc**, utilizan algunos elementos de programación funcional, especialmente al procesar valores mutables. Las **hojas de cálculo** también pueden ser consideradas lenguajes de programación funcional.

Otros lenguajes de programación no están diseñados específicamente para seguir un estilo funcional, sin embargo lo ofrecen como _alternativa_. Por ejemplo, **Perl**, [[JavaScript]] y Python fueron diseñados con capacidades de programación funcional, además de incorporar otros paradigmas.

## Utilidad

La programación funcional se caracteriza por _dividir la mayor cantidad posible de tareas en funciones_, de esta forma estas tareas pueden ser usadas por otras funciones con diferentes objetivos.

El objetivo es conseguir lenguajes expresivos y _matemáticamente elegantes_, en los que no sea necesario bajar al nivel de la máquina para describir el proceso llevado a cabo por el programa, y evitar el concepto de _estado_ del cómputo. La secuencia de computaciones llevadas a cabo por el programa se rige única y exclusivamente por la _reescritura_ de definiciones más amplias a otras cada vez más concretas y definidas.

Este paradigma, por no contener datos mutables, se caracteriza por ser _usado para el manejo de información y no para la creación o modificación de la misma_.

## Características

Los programas escritos en un lenguaje funcional están **constituidos únicamente por definiciones de funciones**, entendiendo estas no como subprogramas clásicos de un lenguaje imperativo, sino como **funciones puramente matemáticas**, en las que se verifican ciertas propiedades como la transparencia referencial (el significado de una expresión depende únicamente del significado de sus subexpresiones), y por tanto, la carencia total de efectos colaterales.

Otras características propias de estos lenguajes son la no existencia de asignaciones de variables y la falta de construcciones estructuradas como la secuencia o la iteración (lo que obliga en la práctica a que todas las repeticiones de instrucciones se lleven a cabo por medio de _funciones recursivas_).

Existen dos grandes categorías de lenguajes funcionales: los **_funcionales puros_** y los **_híbridos_**. La diferencia entre ambos es que los lenguajes funcionales híbridos son menos dogmáticos que los puros, al admitir conceptos tomados de los lenguajes imperativos, como las secuencias de instrucciones o la asignación de variables. En contraste, los lenguajes funcionales puros tienen una mayor potencia expresiva, conservando a la vez su transparencia referencial, algo que no se cumple siempre con un lenguaje funcional híbrido.

### Funciones de primera clase y de orden superior

Funciones de orden superior **son funciones que pueden tomar otras funciones como argumentos o devolverlos como resultados**. En cálculo , un ejemplo de una función de orden superior es el operador diferencial $d \ / \ dx$ , que devuelve la derivada de una función $f$.

Las funciones de orden superior _están estrechamente relacionadas con las funciones de primera clase_ en las cuales las funciones de orden superior y las funciones de primera clase pueden recibir como argumentos y resultados otras funciones. La distinción entre los dos es sutil: "de orden superior", describe **un concepto matemático de funciones que operan sobre otras funciones**, mientras que la "primera clase" es un _término informático que describe las entidades del lenguaje de programación que no tienen ninguna restricción de su utilización_ (por lo tanto funciones de primera clase pueden aparecer en cualquier parte del programa que otras entidades de primer nivel como los números pueden, incluidos como argumentos a otras funciones y como sus valores de retorno).

Las funciones de orden superior permiten la aplicación parcial, una técnica en la que se aplica una función a sus argumentos uno a la vez, con cada aplicación devolver una nueva función que acepta el siguiente argumento. Esto le permite a uno expresar, por ejemplo, la función sucesor como el operador de suma aplicada parcialmente al número natural uno.

```javascript
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11];

function filterOdd(arr) {
  const filteredArr = [];
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] % 2 !== 0) {
      filteredArr.push(arr[i]);
    }
  }
  return filteredArr;
}
console.log(filterOdd(arr));

// Salida:
// [ 1, 3, 5, 7, 9, 11 ]
```

```javascript
const numbers = [1,2,3,4,5];
const squaredNumbers = numbers.map(function(num){
	return num * num
});

// Output: [1, 4, 9, 16, 25]
```

### Funciones puras

Las **_funciones puramente funcionales_** (o expresiones) _no tienen efectos secundarios_ (memoria o E/S). Esto significa que las funciones puras tienen varias propiedades útiles, muchas de las cuales pueden ser utilizadas para optimizar el código:

- Si **no se utiliza el resultado de una expresión pura**, _se puede eliminar sin afectar a otras expresiones_.

- Si una función pura **se llama con parámetros que no causan efectos secundarios**, _el resultado es constante con respecto a la lista de parámetros_ (a veces llamada transparencia referencial), es decir, si la función pura se llama de nuevo con los mismos parámetros, el mismo resultado será devuelto (esto puede habilitar las optimizaciones de almacenamiento en caché).

- Si **no hay una dependencia de datos entre dos expresiones puras**, entonces _su orden puede ser invertido, o pueden llevarse a cabo en paralelo_ y que no pueda interferir con los otros.

- **Si el lenguaje no permite efectos secundarios**, entonces _cualquier estrategia de evaluación se puede utilizar_, lo que da la libertad al compilador para reordenar o combinar la evaluación de expresiones en un programa (por ejemplo, usando la poda).

La mayoría de los compiladores de [[Lenguaje imperativo|lenguajes imperativos]] _detectan funciones puras automáticamente y realizan la eliminación de subexpresiones comunes_. Sin embargo no siempre es posible detectarlo en bibliotecas pre-compiladas, porque por norma general no dan esta información. Esto provoca que no se puedan realizar optimizaciones que podrían aplicar a dichas funciones externas. 
Algunos compiladores, como **gcc**, añaden palabras claves adicionales para que el programador marque explícitamente como puras aquellas funciones externas que proceda, de modo que se le apliquen las optimizaciones pertinentes. **Fortran 95** también permite declarar funciones "puras".

### Recursividad

Iterar en los lenguajes funcionales es normalmente llevado a cabo mediante recursividad. Las funciones recursivas se invocan a sí mismas, permitiendo que una operación se realice una y otra vez hasta alcanzar el caso base. Aunque algunas recursividades requieren el mantenimiento de una pila, la recursividad mediante una cola puede ser reconocida y optimizada mediante un compilador dentro del mismo código utilizado, para implementar las iteraciones en un lenguaje imperativo. El estándar del esquema del lenguaje requiere implementaciones para conocer y optimizar la recursividad mediante una cola. La optimización de la recursividad mediante una cola puede ser implementada transformando el programa a un estilo de pase de continuidad durante la compilación, entre otros enfoques.

Los patrones comunes de recursividad pueden ser factorizados usando funciones comunes más grandes, con “catamorfismos” y “anamorfismos” (pliegues y despliegues), siendo estos los ejemplos más evidentes. Tal y como las mayores funciones más comunes tienen un rol análogo para construir estructuras de control se tienen los iteradores en los lenguajes imperativos.

La mayoría de los lenguajes de programación funcional de propósito general permiten la recursividad sin restricciones y superan el test de Turing, lo que hace que el programa que se interrumpe no pueda tomar una decisión, lo que puede causar una falta de solidez en el razonamiento ecuacional y generalmente requiere introducir inconsistencia dentro de la lógica expresada por los tipos del sistema del lenguaje. Algunos lenguajes de propósito especial como Coq permiten tan solo recursividad bien fundamentada y tienen una normalización fuerte(cálculos no finalizados pueden ser expresados tan solo con flujos de valores infinitos llamados codata) En consecuencia, estos lenguajes fallan el test de Turing y declarar funciones ciertas en ellos es imposible, pero pueden declarar una amplia clase de cálculos interesantes mientras evitan los problemas producidos por la recursividad sin restricciones. La programación funcional limitada a la recursividad bien construida con unas cuantas restricciones más se llama programación funcional total.

### Evaluación estricta frente a la no estricta

Los lenguajes funcionales pueden ser clasificados por el hecho de usar evaluación estricta(eager) o no estricta(lazy), conceptos que hacen referencia a cómo los argumentos de las funciones son procesados cuando una expresión está siendo evaluada. La diferencia técnica está en la notación semántica de las expresiones que contienen cálculos fallidos o divergentes. Bajo la evaluación estricta, la evaluación de cualquier término que contenga un sub-término fallido hará que este sea de por sí fallido.

Por ejemplo, la expresión:

```javascript
print length([2+1, 3*2, 1/0, 5-4])
```

fallará bajo evaluación estricta por la división por cero en el tercer elemento de la lista. Utilizando evaluación no estricta, el tamaño de la función devolverá un valor de 4( por ejemplo el número de elementos de la lista) ya que evaluar esto no afectará al estar evaluando los que componen la lista. En resumen, la evaluación estricta evalúa por completo los argumentos a menos que sus valores requieran evaluar la propia función que se llama a sí misma.

La implementación de la estrategia común para evaluación no estricta en los lenguajes funcionales es la de reducción mediante un grafo. La evaluación no estricta es utilizada por defecto en multitud de lenguajes funcionales puros, incluidos Miranda, Clean y Haskell.

Hughes (1984) defendía la evaluación no estricta como un mecanismo para mejorar la modularidad de los programas a través de la separación de tareas, a partir de la implementación de productores y consumidores de flujos de datos de forma fácil e independiente. Launchbury (1993) describe algunas dificultades que tenía la evaluación no estricta, particularmente al analizar los requisitos de almacenamiento de los programas, y propone una semántica operacional para ayudar durante el análisis. Harper (2009) propone incluir ambas técnicas (evaluación estricta y no estricta) en el mismo lenguaje, utilizando los tipos del sistema del lenguaje para distinguirlas.

### Sistemas de tipos

Especialmente desde el desarrollo de inferencia de tipos Hindley - Milner en la década de 1970, los lenguajes de programación funcionales han tendido a utilizar el cálculo lambda con tipos, en comparación con el cálculo lambda sin tipos utilizado en Lisp y sus variantes (tales como el lenguaje scheme).2​

El uso de tipos de datos algebraicos y la coincidencia de patrones hace que la manipulación de estructuras de datos complejas convenientes y expresivos, la presencia de comprobaciones estrictas de tipos en tiempo de compilación hace que los programas sean más fiables, mientras que la inferencia de tipos libera al programador de la necesidad de declarar manualmente los tipos para el compilador.

Algunos lenguajes funcionales orientados a la investigación, tales como Coq, Agda, Cayenne y Epigram se basan en la teoría de tipos intuicionista, que permite a los tipos a depender de los términos. Estos tipos se denominan tipos dependientes. Se ha demostrado que estos sistemas de tipos sofisticados son tan expresivos que sus respectivos problemas de inferencia de tipos dejan de ser decidibles. Los tipos dependientes pueden expresar proposiciones arbitrarias en la lógica de predicados intuicionista. Este resultado se conoce como isomorfismo de Curry-Howard, y convierte a la programación funcional con una teoría de tipos intuicionista o equivalente en una forma de escribir pruebas matemáticas formales, de las que un compilador puede generar código certificado. Si bien estos lenguajes son principalmente de interés en la investigación académica (incluyendo las matemáticas formalizadas), han comenzado a ser utilizados en la ingeniería también. Compcert es un compilador para un subconjunto del lenguaje de programación C que está escrito en Coq y el cual se verificó formalmente. Una forma limitada de tipos dependientes llamados tipos de datos algebraicos generalizados (GADTs) puede ser implementado de una manera que ofrece algunos de los beneficios de la programación dependiente, evitando la mayor parte de su inconveniencia. GADTs están disponibles en el Glasgow Haskell Compiler, en OCaml (desde la versión 4.00) y en Scala y se han propuesto como adiciones a otros lenguajes, incluyendo Java y C#.

### La programación funcional en lenguajes no funcionales

Es posible utilizar un estilo de programación funcional en lenguajes que tradicionalmente no se consideran lenguajes funcionales. Por ejemplo, tanto D y Fortran95 se apoyan explícitamente en funciones puras. Funciones de primera clase, se han añadido lentamente a los lenguajes principales. Por ejemplo, a principios de 1994, el apoyo a lambda, filtro, mapa, y reducir está en Python. Luego, durante el desarrollo de Python 3000, Guido van Rossum pidió la eliminación de estas características. Sin embargo, más tarde cambió de opinión, y solo la reducción fue eliminado, a pesar de que sigue siendo accesible a través de los módulos de biblioteca functools estándar. Funciones de primera clase también fueron introducidas en PHP 5.3, Visual Basic9, C#3.0 y C++11.

En Java, las clases anónimas a veces pueden ser utilizados para simular clausuras. Sin embargo, las clases anónimas no son siempre los reemplazos completos de las clausuras, ya que tienen capacidades más limitadas. Por ejemplo, Java 8, incluye expresiones lambda para reemplazar determinadas clases anónimas. Sin embargo, la presencia de excepciones con comprobaciones en este lenguaje puede desaconsejar el uso de programación funcional, ya que puede ser necesario para capturar las excepciones que se deben controlar para después volverlas a lanzar ellos (problema este que sin embargo no se produce en otros lenguajes sobre JVM que no tienen excepciones comprobadas, como es Scala).

Muchos patrones de diseño orientado a objetos se pueden expresar en términos de programación funcional por ejemplo : el patrón de estrategia simplemente dicta el uso de una función de orden superior, y el patrón de visitantes corresponde aproximadamente a un catamorfismo, o doble también conocido como reducir, comprimir, o inyectar, se refiere a una familia de funciones de orden superior que analiza una estructura de datos recursiva y se recombinan con el uso de una operación de combinación.

Del mismo modo, la idea de los datos inmutables de la programación funcional se incluye a menudo en lenguajes de programación imperativa, por ejemplo, la tupla de Python, que es una matriz inmutable.

## Ventajas de usar un paradigma funcional

Entre las ventajas que suelen citarse de usar un paradigma funcional en la programación de computadoras, están las siguientes:​

- Ausencia de efectos colaterales.
- Proceso de depuración menos problemático.
- Pruebas de unidades más confiables.
- Mayor facilidad para la ejecución concurrente.

### Simulación de estados

Hay tareas (como por ejemplo, el mantenimiento del saldo de una cuenta bancaria) que a menudo parecen implementadas con estados. La programación funcional pura actúa sobre esas tareas, tareas de entrada/salida de datos tales como entrada de datos por parte del usuario y mostrar resultados por pantalla, de una forma diferente.

El lenguaje de programación funcional Haskell lo implementa usando mónadas, estructura que representa cálculos que se describen como una secuencia de pasos, derivada de la teoría de categorías.

Las mónadas ofrecen una forma de abstraer ciertos tipos de patrones computacionales, incluyendo (pero no limitado a) el diseño de operaciones con estados cambiantes (y otras acciones secundarias tales como entrada/salida de datos) de una manera imperativa sin perder la pureza. Mientras las mónadas existentes pueden ser fáciles de aplicar en un programa usando las plantillas y ejemplos adecuados, muchos estudiantes tienen problemas para entenderlo conceptualmente, por ejemplo cuando se les pide definir nuevas mónadas. (lo que a veces resulta necesario para ciertos tipos de librerías).4​

Otra forma en la que los lenguajes funcionales pueden simular estados es rodeando una estructura de datos que representa el estado actual como un parámetro para llamadas a funciones. En cada llamada a función, se crea una copia de esta estructura de datos que se diferencia con el resultado de la función. Esto se conoce como “estilo de paso de estado”.

Los lenguajes funcionales no puros normalmente incluyen métodos para gestionar el cambio de estado más directamente. Clojure por ejemplo, usa una gestión de referencias que pueden ser actualizadas aplicando funciones puras al estado actual. Este tipo de enfoque permite el cambio de estado, promoviendo el uso de funciones puras como la mejor forma de realizar cálculos.

Métodos alternativos como lógica de Hoare, el cual es un sistema formal con un conjunto de reglas lógicas que sirven para razonar con rigor acerca de la corrección de programas, y la singularidad han sido desarrollados para realizar un seguimiento de los efectos secundarios en los programas. Algunos lenguajes de investigación modernos usan sistemas de efectos para hacer explícita la presencia de efectos colaterales.

### Cuestiones de eficiencia

Los lenguajes de programación en este paradigma son típicamente menos eficientes en el uso de CPU y memoria que los lenguajes imperativos como pueden ser C y Pascal. Esto está relacionado con el hecho de que algunas estructuras de datos de tamaño indefinido como los vectores tienen una programación muy sencilla usando el hardware existente, el cual es una máquina de Turing bastante evolucionada. Se puede acceder muy eficientemente a las posiciones del array con CPUs con un alto grado de perfeccionamiento, haciendo pre búsquedas eficientemente a través de las memorias caché o manejado con instrucciones SIMD. Y no es fácil crear componentes homólogos inmutables de propósito general con la misma eficiencia. Para lenguajes puramente funcionales, el peor caso descendente es el logarítmico en el número de celdas de memoria usadas, porque las estructuras de memoria que cambian de tamaño pueden ser representadas por estructuras de datos puramente funcionales con tiempo de acceso logarítmico, como por ejemplo un árbol equilibrado. Sin embargo, tales retrasos no son universales. Para programas que realizan cálculos numéricos intensivos, los lenguajes funcionales tales como OCaml y Clean son algo más lentos que C. Para programas que manejan grandes matrices y bases de datos multidimensionales, los vectores de los lenguajes funcionales, como J y K, fueron diseñados optimizando su velocidad.

La inalterabilidad de los datos puede llevar en muchos casos a ejecuciones eficientes permitiendo al compilador hacer suposiciones que en un lenguaje imperativo resultarían arriesgadas, aumentando las probabilidades para la expansión en línea, que es una optimización del compilador que sustituye en el lugar de la llamada a una función con el cuerpo del destinatario de la llamada mejorando el uso del tiempo y espacio en tiempo de ejecución.

La evaluación perezosa es una estrategia de evaluación que retrasa el cálculo de una expresión hasta que su valor sea necesario, también puede mejorar la velocidad del problema, incluso asintóticamente, mientras que puede reducir la velocidad por un factor constante, sin embargo puede producir pérdidas de memoria si se usa de manera incorrecta. Launchbury 1993 discute de manera teórica los problemas relacionados con las pérdidas de memoria de evaluación perezosa, y O’Sullivan et al. 2008 da algunos consejos prácticos para el análisis y la solución de estos problemas. Sin embargo, las implementaciones más generales de evaluación perezosa hace un uso extensivo de código sin referencia y los datos llevan a cabo un funcionamiento pobre en los procesadores modernos con un alto grado de paralelismo y cachés multinivel, donde un fallo de caché puede producir un coste de cientos de ciclos de reloj.
# Flashcards

- [[Programación funcional#Funciones de primera clase y de orden superior]]

¿Qué son las funciones de orden superior?::Son funciones que pueden tomar otras funciones como argumentos o devolverlas como resultados.

¿Qué son las funciones de primera clase?::Son funciones que pueden ser tratadas como cualquier otro valor del lenguaje, es decir, pueden ser almacenadas en variables, pasadas como argumentos y devueltas desde funciones.

¿Cuál es la diferencia entre funciones de orden superior y de primera clase?::La distinción es sutil. Las funciones de orden superior son un concepto matemático que describe funciones que operan sobre otras funciones, mientras que las funciones de primera clase son un término de informática que describe entidades del lenguaje de programación que no tienen restricciones en su uso.

¿Qué es la aplicación parcial?::Es una técnica en la que se aplica una función a sus argumentos uno a la vez, con cada aplicación devolviendo una nueva función que acepta el siguiente argumento.

¿Por qué son útiles las funciones de orden superior y de primera clase?::Permiten escribir código más conciso y reutilizable, y hacen que el código sea más fácil de entender y mantener.

¿En qué lenguajes de programación son comunes las funciones de orden superior y de primera clase?::Son comunes en lenguajes funcionales como Haskell y Lisp, pero también están disponibles en lenguajes imperativos como Python y JavaScript.

¿Cuáles son algunos ejemplos de funciones de orden superior en diferentes lenguajes de programación?::map (Python,JavaScript) filter (Python, JavaScript) reduce (Python, JavaScript) sort (Python, JavaScript) lambda (Python, JavaScript)

¿Cómo puedo aprender más sobre funciones de orden superior y de primera clase?::Hay muchos recursos disponibles en línea, como tutoriales, artículos y libros.

[[Programación funcional#Recursividad]]

¿Qué es la recursividad?::La recursividad es una técnica en la que una función se llama a sí misma, permitiendo resolver problemas complejos dividiéndolos en subproblemas más pequeños del mismo tipo.

¿Cómo se implementa la recursividad en lenguajes funcionales?::La recursividad se implementa directamente en lenguajes funcionales. La función recursiva se invoca a sí misma hasta llegar a un caso base que no requiere más llamadas.

¿Qué ventajas tiene la recursividad?
?
La recursividad ofrece las siguientes ventajas:
- Simplicidad: Permite expresar soluciones complejas de forma elegante y concisa.
- Modularidad: Divide el problema en subproblemas más pequeños y manejables.
- Reutilización: Permite reutilizar el código para resolver problemas similares.

¿Qué desventajas tiene la recursividad?
?
La recursividad tiene las siguientes desventajas:
- **Eficiencia:** Puede ser menos eficiente que la iteración en algunos casos.
- **Profundidad de pila:** Puede consumir mucha memoria si la profundidad de la recursión es grande.

¿Qué es la recursividad bien fundada?::La recursividad bien fundada es un tipo de recursividad en la que cada llamada recursiva se acerca a un caso base que no requiere más llamadas.

¿Qué lenguajes permiten la recursividad sin restricciones?::La mayoría de los lenguajes de programación funcional de propósito general, como Haskell y Lisp, permiten la recursividad sin restricciones.

¿Qué lenguajes permiten solo la recursividad bien fundada?::Algunos lenguajes de propósito especial, como Coq, solo permiten la recursividad bien fundada.

¿Qué es la programación funcional total?::La programación funcional total es un paradigma que restringe la recursividad a la recursividad bien fundada y otras restricciones para evitar problemas como la falta de solidez en el razonamiento ecuacional.

¿Cuáles son algunos ejemplos de patrones comunes de recursividad?
?
Algunos ejemplos de patrones comunes de recursividad son:
- **Factorización:** Extraer código común en funciones más grandes.
- **Catamorfismos:** Desplegar una estructura de datos en un valor.
- **Anamorfismos:** Construir una estructura de datos a partir de un valor.

¿Cómo se optimiza la recursividad en lenguajes imperativos?::La recursividad en lenguajes imperativos puede optimizarse mediante la transformación del código a un estilo de pase de continuidad durante la compilación.

¿Qué es el test de Turing?::El test de Turing es una prueba de la capacidad de una máquina para exhibir un comportamiento inteligente equivalente al de un humano.

¿Por qué algunos lenguajes fallan el test de Turing?::Algunos lenguajes fallan el test de Turing porque no permiten la recursividad sin restricciones, lo que limita su capacidad para simular el comportamiento humano.

¿Qué es la codata?::La codata es un tipo de dato que representa un flujo infinito de valores.

¿Qué es la programación funcional limitada?::La programación funcional limitada es un paradigma que restringe la recursividad a la recursividad bien fundada y otras restricciones para evitar problemas como la falta de solidez en el razonamiento ecuacional.