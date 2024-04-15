[[Introducción a la algorítmica y programación.]]

Es una descripción breve y concisa, debe escribirse en dos a tres renglones. Debe ser lo suficientemente claro, preciso y completo. Cuando el sistema es demasiado extenso, puede acompañarse de objetivo general, objetivos particulares y el alcance al que se pretende llegar en cada versión del sistema.

Sin embargo, en caso de tener un planteamiento concreto sobre futuras características que pueda llegar a desarrollar el producto, este puede ser un buen momento para especificar el alcance futuro. Escribirlo bajo este apartado le da la posibilidad al equipo de desarrollo, la posibilidad de contemplar requisitos adicionales para que la solución pueda extenderse con facilidad en posteriores revisiones.

Generalmente, construir una primera versión de un sistema puede llegar a ser tardado, y en algunas ocasiones las restricciones de presupuesto o de tiempo son un factor muy importante para posponer la creación de un sistema más completo.

El personal que se dedica a la programación de un sistema de cómputo no tiene que ser experta en todos los temas, el planteamiento del problema debe realizarse en el lenguaje que se utiliza en el contexto de los requerimientos, es decir: en el dominio del problema. Con la finalidad de establecer un puente de comunicación entre el cliente (quien solicita el sistema) y el equipo de desarrollo (quien realiza el sistema), comúnmente se agrega un glosario con términos relacionados con el problema: conceptos, roles, acciones, fórmulas, relaciones, etc.

En el planteamiento del sistema, debe quedarle muy claro al cliente y al desarrollador qué se espera como productos finales, qué insumos deberán entregarse al desarrollador, cómo se mostrarán los resultados, quiénes intervendrán en la solución, los tiempos de entrega, los mecanismos de verificación de avance, los roles de las personas o sistemas que interactuarán, la forma como se recaba y reporta la información y cómo se desea que se entregue, los costos y en su caso las penalizaciones por incumplimiento de cada parte (en tiempo o en dinero).

Aunque no se entrega en el documento de análisis, el encargado de solicitar los requerimientos debe ser capaz de visualizar la lógica del sistema, es decir, cuáles son las interrelaciones que se realizarán y qué es lo que se necesita mínimamente como entrada para llegar a la solución requerida.

### Ejemplo

#### Definición

Calcule el área de un triángulo a partir de conocer su base y altura.

#### Objetivo general

Diseñe una clase que modele distintos triángulos, conteniendo los atributos y métodos necesarios para almacenar asignar y recuperar la información de cada uno de ellos.

#### Objetivos particulares

Diseñe una especialización de la clase para modelar triángulos equiláteros a partir de la clase original (la base, y la altura guardan una relación de proporcionalidad).

#### Requerimientos no funcionales

El programa se desarrollará para un entorno que sólo una persona lo utilizará cada vez (monousuario).

#### Glosario

Un triángulo es una figura geométrica que se compone y delimita por las líneas que unen a tres puntos no colineales. Si una de esas líneas se coloca de forma horizontal, suele nombrarse como la “base del triángulo” (b), a partir de ahí hasta el punto que no forma la base se traza una línea perpendicular, la distancia de la base a dicho punto se conoce como la altura del triángulo (h).

<img
  src="https://portalacademico.cch.unam.mx/sites/default/files/glosario-triangulo.png"
  alt="triangulo"
/>
Así, el área (a) se calcula utilizando la siguiente fórmula:

$$
\huge area = {b.h\over2}
$$

Dónde:

• a es el área del triángulo.
• b es la longitud de la base.
• h es la longitud de la altura.

#### Alcance actual y futuro

Alcance actual: Se calculará únicamente el área si se conocen los valores del área y de la altura, no se manejarán unidades, no se dibujará en pantalla. Solo se solicitan los datos y se muestra el resultado.

Alcance futuro: Se podrá incluir en un formulario, se podrá dibujar en la pantalla, por el momento no se calculará a partir de conocer tres puntos en el espacio o conocer la longitud de tres segmentos de recta.

<img
  src="https://portalacademico.cch.unam.mx/sites/default/files/alcance-actual-futuro.png"
  alt="alcance"
/>

#### Documentación y rubrica de evaluación

Todos los puntos anteriores y lo que se desarrolle en cada etapa de la solución deberá documentarse y verificarse por alguien más del equipo de desarrollo y ser validado con el cliente (quien solicita el programa o sistema de cómputo).