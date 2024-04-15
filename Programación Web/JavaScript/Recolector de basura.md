Dentro de las Ciencias de Computación, el recolector de basura, o garbage collector en inglés (GC), es un mecanismo implícito de gestión de memoria. Esta herramienta fue inventada por John McCarthy a finales de los años 50 del pasado siglo como una solución automática a la gestión manual de memoria para el lenguaje Lisp.

> [!quote]- John McCarthy (1927 – 2011)
> También conocido como Tío John McCarthy, fue un prominente informático que recibió el Premio Turing en 1971 por sus importantes contribuciones en el campo de la Inteligencia Artificial. Padre de dicho término, desarrolló la familia de lenguajes de programación Lisp, influenció de forma significativa el desarrollo del lenguaje ALGOL y es también considerado como el primero en utilizar el concepto de cloud computing.

# Fundamento

Todo lenguaje de programación de bajo nivel requiere de una cantidad de memoria para trabajar. En esta memoria, cedida por el Sistema Operativo, cada programa debe ser capaz ubicar los objetos que está manejando en tiempo de ejecución, monitorizar su estado, reciclarlos cuando ya no son necesarios e, idealmente, compactar el espacio resultante para optimizar el rendimiento.

La gestión de dicha memoria, dependiendo del lenguaje, puede ser de dos tipos: manual o automática.

## Gestión manual

La **gestión manual de memoria**, es aquella donde se asignan y liberan los recursos de memoria de forma explícita. Esto significa que es el _desarrollador_ quien debe administrar los registros asignando memoria a sus objetos mediante **punteros** y liberarlos cuando ya no sean necesarios.

> [!quote] Puntero
> En Ciencias de la Computación, un puntero es un objeto del lenguaje de programación cuyo valor se refiere a (o «apunta a») otro valor almacenado en una dirección de memoria diferente.

Hasta mediados de los años 90, pese a que ya se habían introducidos modelos automáticos (como el caso de Lisp), la mayoría de lenguajes utilizados en la industria requerían de este tipo de gestión de memoria.

Algunos de estos, aún populares a día de hoy (en según qué ámbitos), son: C, C++, Pascal, Ensamblador, Fortran o Prolog.

## Gestión automática

La **gestión automática de memoria**, también denominada gestión implícita, es aquella donde las tareas de reserva, monitorización y reciclaje son llevadas a cabo _por el propio sistema_ sin la intervención del programador. Es en este escenario donde el Recolector de Basura se encarga de identificar y eliminar la memoria ocupada por objetos que ya no están en uso por el programa (conociéndose a esta memoria residual como ‘basura’).

Desde mediados de los noventa, este sistema ha ido creciendo en popularidad a raíz del lenguaje Java, extendiendo su paradigma a los más recientes como Ruby, JavaScript, Swift o GO.

# Funcionamiento del recolector de basura

Como ya se ha indicado, el propósito del recolector es _monitorizar la memoria reservada del sistema_ para detectar cuándo ésta ya no es necesaria y, eventualmente, **liberarla** para devolverla al SO (sistema operativo) o al pool del propio programa.

> [!quote] Pool
> Un pool o fondo en informática es un conjunto de recursos inicializados que se mantienen listos para su uso, en lugar de ser asignados y destruidos bajo demanda.

En los lenguajes de alto nivel, cuando un programa es compilado, se incluyen de forma predeterminada las subrutinas que constituyen el propio recolector. De este modo, el sistema ya cuenta con las herramientas necesarias para ejecutar periódicamente el procedimiento de optimización de forma desatendida y automática.

Será durante esa ejecución cuando el recolector se encargue de recorrer los espacios de memoria definidos por el lenguaje evaluando las referencias de los objetos que la ocupan.

Uno de los conceptos claves para comprender el funcionamiento es el de [[Objetos#Referencias de objetos|Referencia]].

> [!hint] Referencia
> Dentro del contexto de gestión de memoria, se dice que un objeto referencia a otro si el primero tiene acceso al segundo (ya sea de forma implícita o explícita).

Otro concepto es el de **objeto atómico** ("leaf object")

> [!hint] Objeto atómico
> Un objeto atómico es aquel que no hace referencia a ningún otro objeto. En un lenguaje tipado, el compilador a menudo puede determinar en tiempo de compilación que ciertos tipos pueden ser representados unívocamente como objetos atómicos. Normalmente éstos son de un tipo escalar o un tipo vectorial de escalares con magnitud limitada.

Dicho de otro modo, **aquel objeto que por su naturaleza solo puede contener un valor y no referenciar a otro, se denomina atómico**.

# Algoritmo de recolección de basura

La implementación del recolector de basura puede variar de un lenguaje de programación a otro, al igual que de una biblioteca a otra. Esto posibilita diferentes aproximaciones o algoritmos, cada una con sus ventajas e inconvenientes.

> [!quote] David Flanagan, JavaScript, The Definitive Guide.
> La literatura sobre el recolector de basura es extensa y muy técnica; el procedimiento actual para la recolección es un aspecto específico de cada implementación, por lo que puede variar entre los diferentes lenguajes.

Pese a estas diferencias prácticas, podemos agrupar los principales algoritmos de recolección en dos familias teóricas principales: **el conteo de referencias y el marcado**.

# Conteo de referencias

> [!warning] Nota
> A día de hoy, se considera **obsoleto y en desuso**. Ni JavaScript, ni la mayoría de lenguajes modernos utilizan este algoritmo.

El **conteo de referencias** (o Reference Counting) es la técnica más sencilla para identificar direcciones de memoria que no están actualmente en uso. El proceso realiza una administración automática de la memoria al mantener una contabilidad en cada objeto, normalmente en su cabecera, de cuántas referencias apuntan al mismo.

Si un objeto, o dirección de memoria, _no está siendo referenciado por ningún otro_, se considera que no está en uso y, por tanto, puede ser __liberado__.

En la nomenclatura propia de la gestión de memoria, decimos que un objeto referenciado por al menos otro es un _objeto vivo_, en oposición a aquel no referenciado y que denominamos _objeto muerto_.

Este planteamiento presenta una serie de __desventajas__:

- El campo del objeto que se utiliza para llevar el conteo posee un _tamaño limitado_ y, por lo tanto, el sistema puede colapsar si el número de referencias posibles a dicho objeto es ilimitado.
- El recuento de referencia _implica una operación en cada modificación de un puntero_, lo que aumenta el tamaño del código, la demanda de ancho de banda de memoria, y puede derivar en una grave penalización de rendimiento (especialmente en entornos multihilo donde las actualizaciones de conteo de referencia requieren sincronización).
- Cada objeto necesita un _tamaño ligeramente mayor_ para almacenar el recuento de referencia.
- Si alguno de los objetos forma parte de una estructura de datos __cíclicos__, siempre tendrá un _recuento de referencia distinto de cero_ y, por lo tanto, no podrán ser reciclados cuando ya no sean necesarios.

## Ciclos

En programación, nos referimos a ciclos cuando una _serie de objetos se referencian entre sí creando un bucle cerrado_. Al conjunto de referencias mutuas se le conoce como **Referencia Circular** (Circular reference).

> [!hint] Referencias circulares
> Las referencias circulares aparecen en programación cuando una pieza de código requiere el resultado de otra, pero ese código necesita, a su vez, el resultado de la primera.


> [!info] Referencia circular
> ![[Pasted image 20230218211944.png|center]]
> Ejemplo de referencia circular (en rojo)

Como revela la anterior ilustración, si un objeto X contiene una referencia a un objeto Y, y ese objeto Y contiene una referencia al objeto X, ambos objetos forman un conjunto mutuamente dependiente. Aunque todo el conjunto quede en desuso y no sea necesario en el programa, su conteo de referencias siempre mostrará al menos una dependencia, por lo que el recolector no puede actuar sobre él.

Para lidiar con los problemas enumerados anteriormente, los sistemas de gestión evolucionaron con algoritmos más complejos y precisos. Y es así como llegamos a las soluciones modernas, derivadas todas ellas en mayor o menor medida de la familiar de algoritmos que trataremos a continuación: el de marcado y barrido.

# Marcado y barrido: Mark-Sweep

A día de hoy, todos los recolectores de basura modernos basan su funcionamiento en alguna variante de los algoritmos Mark-Sweep.

En esencia, este algoritmo realiza dos operaciones básicas. La primera, debe ser capaz de ‘marcar’ qué objetos son inalcanzables y la segunda, debe poder ‘barrer’ la memoria que ya no es necesaria para devolverla nuevamente al programa.

## Fase de marcado

La fase de marcado (‘Mark‘) se basa en los conceptos de ‘alcance‘ y ‘raíz‘ tomando todos los valores de un entorno y determinando si son o no accesibles por el programa.

Los objetos se agrupan así en accesibles (directa o indirectamente) e innaccesibles. Ambos términos se corresponden con los ya mecionados objetos ‘vivos’ y ‘muertos’ respectivamente.

> [!cite] Objetos accesibles directa e indirectamente
> Los objetos que un programa puede acceder directamente son aquellos que han sido referenciados por las variables globales (conocidas éstas últimas como raíces), mientras que los objetos indirectamente accesibles son aquellos referenciados por algún otro objeto accesible (directa o indirectamente).

> [!info] Marcado de objetos a partir de una raiz
> ![[Pasted image 20230219004748.png|center]]

El marcado sobre un objeto indicando si está o no vivo, puede realizarse de dos formas: con un bit asociado en la propia memoria reservada del objeto que sirve de marca (_Bit Mark_), o utilizando un mapeado a modo de diccionario (_Bitmap Marking_).

### Bit de marca (bit mark)

La **marca de bit** (también llamada _One-bit_ o _Bit Mark_) es una variante del conteo de referencias tradicional donde se utiliza un indicador (_flag_) de un bit asociado al puntero del objeto para indicar si éste tiene al menos una referencia apuntándole. Si eliminamos una referencia a un objeto marcado, el sistema debe volver a escanear su raíz para actualizar dicha marca.

### Mapeado de bits (bitmap marking)

En los recolectores de tipo _Mark-Sweep_, un **marcado de tipo bitmap** es una técnica en la que se almacena la correspondiente marca de bit de un objeto en un rango de memoria separado que constituye un diccionario. Esto favorece la identificación de cada referencia así como diversos sistemas de caché al evitar al sistema recorrer cada página de memoria para alterar un bit directamente en el objeto marcado.

## Fase de barrido

Una vez el sistema ha trazado el alcance de todos los objetos desde la raíz, el siguiente paso es eliminar aquellos que han quedado aislados y que, por tanto, son considerados como desechables. Esa labor le corresponde a esta segunda fase de barrido (o ‘_Sweep_‘).

> [!cite] Barrido
> El barrido es la segunda fase dentro de un sistema de gestión Mark-Sweep. En ella, se realiza una transferencia secuencial (dirección-orden) sobre la memoria para reciclar aquellos bloques que permanecen sin marcar. Como paso previo, el barrido normalmente reúne todos estos bloques en una o más listas libres.

> [!hint] Resultado de un barrido tras la recoleccion
> ![[Pasted image 20230219010359.png|center]]

### Compactacion

Un aspecto a tener en cuenta es que tras el reciclaje de objetos la memoria del sistema puede terminar muy fragmentada ralentizado con ello futuras asignaciones. Es por ello que muchos gestores realizan en esta fase de barrido un compactado de la memoria reduciendo con ello los espacios vacíos entre registros y mejorando el rendimiento posterior del recolector.

Dicho de otro modo, **la compactación es el proceso de mover y reubicar los objetos vivos para eliminar el espacio muerto que ha podido quedar entre ellos.**

> [!hint] Proceso de compactado tras el barrido
> ![[Pasted image 20230219010556.png|center]]

# Gestión de memoria en JS

JavaScript posee además la característica de que dispone de varias implementaciones sobre un mismo estándar, en este caso, ECMAScript. La lista de motores es muy amplia, lo que implica que también un número igual de _implementaciones del recolector de basura_.

## Modelo de objetos

Los tipos de datos primitivos no pueden referenciar a ningun otro valor. En un grafo de objetos, estos valores **son siempre atómicos**, y ello significa que no tienen descendientes ocupando así el último elemento de cada rama.

En este esquema, solo puede existir un tipo de contenedor: el objeto principal (`Object`). En JavaScript, **este objeto actúa como raíz**, siendo de él del que parten todas las relaciones con el resto de valores.

> [!info] Modelo de objetos JS
> ![[Pasted image 20230219101116.png|center]]
> 
> - **Raíz**: marcada con el punto _azul_, se corresponde con el _Objeto principal_. Este objeto puede referirse al objeto léxico global o a una clausura. Por ejemplo, el objeto window.
> - **Valores de objeto**: indicados mediante puntos _rojos_, estos valores se corresponden con _objetos definidos explícitamente_ (por ejemplo, funciones).
> - **Valores escalares**: indicados con puntos _verdes_, estos son las _primitivas inmutables_ del lenguaje y, por tanto, último extremo de cada nodo. Estos valores serían por ejemplo las cadenas, números o booleanos.

## Lógica de asignación de memoria

Pequeños ejemplos que muestran la lógica de asignación

```js
// Reserva de memoria para un número (Number)
let num = 12345;
 
// Reserva de memoria para dos números (Number)
let [ num1, num2 ] = [ 1, 2 ];
 
// Reserva de memoria para dos números (Number) y un array (Object)
let [ a, b, ...rest ] = [ 1, 2, 3, 4, 5 ];
 
// Reserva de memoria para una cadena (String)
let str = 'Hello World'; // Reserva para cadena (String)
 
// Reserva de memoria para un objeto (Object) y sus valores
let obj = {
    x: 12345,           // Reserva para número (Number)
    y: 'Hello World',   // Reserva para cadena (String)
    z: x => x * 2       // Reserva para una función (Object)
};
 
// Reserva de memoria para un array (Object)
let arr = [ 35, 25, 10, 45, 3 ];
 
// Reserva de memoria para una función (Object)
let fn = ( x ) => x * 2;    // Los argumentos de una función, también
                            // reservan memoria según su tipo de datos.
 
// Reserva de memoria para una función utilizada como expresión (Object)
arr.sort( ( a, b ) => a - b );  // a y b reservan memoria para sendos números (Number)
 
// Reserva de memoria para un objeto Date (Object)
let d = new Date();
```

### Asignaciones por referencia

En JavaScript, cuando asignamos a una variable el valor de un array o un objeto ya definido previamente, estamos creando una _referencia_ a dicho valor. Dicho de otro modo, no estamos copiando/clonando un objeto, sino apuntando a la dirección de memoria donde está almacenado su valor.

Es debido a esta referencia que el sistema no reserva memoria para dicho tipo, sino que únicamente se limita a crear un _puntero_:

```js
let arr = [ 1, 2, 3, 4, 5 ], // Reserva de memoria para un array (Object)
    copyArr = arr;           // NO se reserva memoria para un array.
                             // Se guarda solo el puntero a su referencia

let obj = {                  // Reserva de memoria para un objeto (Object)
    foo: 'Hello World'       // Reserva de memoria para una cadena (String)
},
    copyObj = obj            // NO se reserva memoria para un objeto
                             // Se guarda solo el puntero a su referencia
```

Con el ejemplo de una cadena (`String`), la cosa puede variar. Las primitivas son inmutables (una vez creadas no pueden ser modificadas), pero sí pueden construirse nuevos valores partiendo de otros previamente definidos. En este caso, será el sistema (y la lógica de su implementación) el que decida si un valor derivado debe copiarse como un objeto nuevo o únicamente como un puntero relacionado:

```js
let str = 'La donna e mobile',      // Reserva de memoria para una cadena (String)
 
    newStr = str.substr( str, 8 );  // El sistema puede NO reservar memoria para
                                    // una cadena (String), sino solo un puntero
                                    // para el rango [ 0, 8 ] del original
```

Cuando en lugar de copiar por referencia forzamos una clonación, el sistema sí reserva la memoria necesaria para un nuevo objeto:

```js
let arr = [ 1, 2, 3, 4, 5 ],        // Reserva de memoria para un array (Object)
    cloneArr = arr.slice();         // Reserva de memoria para un array (Object)
 
let obj = {                         // Reserva de memoria para un objeto (Object)
    foo: 'Hello World'              // Reserva de memoria para una cadena (String)
},
    objCopy = Object.assign( {}, obj ); // Reserva de memoria para un objeto y sus propiedades
```

## Lógica de reciclaje de memoria

Cabe aclarar que, como en cualquier lenguaje, el objetivo del recolector de basura es la de _liberar memoria que actualmente no está en uso por parte del programa_. Para ello, la lógica con la que el sistema marca si un valor es o no reciclable, radica en determinar si existe una ruta desde la raíz hasta dicho valor.

> [!info] Grafo de valores huérfanos
> ![[Pasted image 20230220173920.png|center]]
> 
> En el recuadro negro se observan valores huérfanos que pueden pasar a ser reciclados.

## Algoritmo mark-sweep

Todos los recolectores Javascript utilizan en la actualidad la metodología _Mark-Sweep_ para gestionar su memoria.

Este conjunto de procedimientos se dividen en dos sub procesos o etapas que son los que dan nombre al sistema: la fase de marcado (_mark_) y la de barrido (_sweep_).

### Fase de marcado

Vista ya la lógica de asignación en Javascript, recordamos cómo cada vez que creamos un objeto se reserva un espacio de memoria según el tipo de datos necesario. De forma paralela, se asigna también una marca para monitorizar su alcanzable desde el objeto raíz (bien se trate del [[Scope o alcance#Global scope|Objeto global]], o del [[Scope o alcance#Local scope|Scope de función]]).

El recolector puede así recorrer de forma periódica todo el listado de variables en un entorno dado, marcando cada valor que es referido por estas variables. Si una de estas referencias es un objeto (`Object`) o un array (internamente tratado también como un `Object`), se marca de forma recursiva cada una de sus propiedades (para los primeros) o elementos (para el segundo).

Al escanear cada nodo de forma recursiva, el recolector puede localizar (y marcar) cada valor unitario que es alcanzable, desechando aquellos que quedan sin marca y que se identifican por tanto como basura.

Para realizar este proceso y monitorización de las marcas, los motores de JavaScript modernos implementan una tabla sobre la que se realiza el mapeado (el _Bitmap Marking_ que ya analizamos más arriba).

> [!info] Bitmap marking
> ![[Pasted image 20230220191358.png|center]]

Dependiendo de la implementación, cada motor Javascript actuará de una forma diferente aunque todos responden, como veremos a continuación, **a un modelo generacional**. Esto quiere decir que si un objeto es referenciado por otro, su valor promociona entre distintos espacios pre establecidos. Sucesivos recorridos del recolector determinarán el ciclo de vida de estos valores según el espacio que ocupan: aquellos objetos que continúan siendo referenciados en el tiempo constituirán los espacios permanentes mientras que los huérfanos, se preparan en otros perecederos para posterior reciclaje.

Con las marcas establecidas y los objetos debidamente ubicados en su espacio correspondiente, se procede con la siguiente etapa del algoritmo: el barrido.

### Fase de barrido

En este sub proceso, el recolector tiene información sobre todos los objetos dentro de un determinado ámbito, ya sea este el objeto léxico global, o el scope de una función.

Revisando así los espacios reservados, el sistema conoce por un lado qué objetos han sido marcados como ‘inalcanzables’ (reciclables), mientras que por otro, sabe qué objetos permanecen vivos (compactables).

La división de la memoria en estos espacios independientes, permite al recolector trabajar de forma eficiente sin necesidad de recorrer todo el árbol de nodos a cada iteración.

Aquellos valores (células o celdas según la terminología de cada motor) que habiten las tablas establecidas por el sistema como inalcanzables pueden ser liberadas devolviéndose así la memoria al sistema operativo (SO) o a la piscina de memoria libre (reservada) del navegador (si procede). Al mismo tiempo, las tablas vivas pueden ser compactadas eliminándose el espacio muerto entre objetos y optimizando con ello el rendimiento posterior de la aplicación.

## Diferencias entre motores

http://www.etnassoft.com/2016/11/16/guia-definitiva-del-recolector-de-basura-en-javascript/

## Limitaciones actuales

Encontramos algunas limitaciones que son independientes al conjunto de algoritmos con el que trabaje.

El principal problema radica en que el proceso para determinar si un determinado registro de memoria es necesario o no para el sistema, es indecible. Dicho de otro modo, **no puede resolverse de forma unívoca mediante un algoritmo**.

> [!note] Problema indecible
> En teoría de la computabilidad y en teoría de la complejidad computacional, un problema indecidible es un problema de decisión para el cual es imposible construir un algoritmo que siempre conduzca a una respuesta de sí o no correcta.
> 
> ![[Pasted image 20230220191950.png|center]]
> Ejemplo clásico de problema indecible: Problema del domino por Hao Wang

Como consecuencia de esta restricción, las recolecciones de basura implementan sólo soluciones parciales. Es por ello que lenguajes de bajo nivel (como C o C++) apuestan por una gestión manual de memoria, más eficiente y precisa a priori, frente a los lenguajes modernos de alto nivel que liberan al desarrollador de esta carga mediante su gestión automática (y por tanto, sujeta a errores).

## Memory leaks (fugas de memoria) en JS

Podemos evitar el cometer errores que entorpezcan la gestión de memoria por parte del sistema. Si bien escribir un código amigable no es estrictamente necesario siempre que sigamos las buenas prácticas y contemos con una estrategia, sí lo es el evitar esos descuidos que terminan en fugas de memoria.

El ciclo de trabajo para gestionar en memoria en JS:
- Reservar la memoria necesaria cuando se crea un objeto
- Utilizarla (sub procesos de lectura y escritura)
- Liberar la memoria una vez ya no es necesaria

Las fugas de memoria se producen cuando falla el último paso de los anteriores y, por lo tanto, ésta _no se libera_.

> [!quote]- Sebastián Peyrott, 4 Types of Memory Leaks in JavaScript and How to Get Rid Of Them
> En esencia, una fuga de memoria puede definirse como una memoria que ya no es necesaria para la aplicación, pero que por algún motivo, no es devuelta al sistema operativo o a la piscina de memoria libre disponible.

Habiendo ya visto cómo trabaja el algoritmo _Mark-Sweep_, los principales errores en los que podemos caer durante un desarrollo son los relacionados, no ya con el conteo de referencias sobre cada objeto, sino con esa ruta que une la raíz del sistema con cada uno de nuestros objetos declarados en un grafo.

> [!hint] Fuga de memoria observada en las chrome dev tools
> ![[Pasted image 20230220192448.png|center]]

Todo lo anterior, traducido a términos habituales para los programadores, serían los problemas derivados de:

### Variables globales accidentales

En Javascript, la creación accidental de variables globales fue un problema histórico hasta la llegada de las herramientas de calidad de código (los llamados _linters_) o la inclusión del modo estricto.

Con anterioridad (y aún hoy fuera del modo estricto), toda variable que no era declarada de forma explícita, pasaba a ser una propiedad del objeto léxico global.

Este comportamiento interno de Javascript conlleva que toda variable iniciada sin declarar en un determinado scope, pasa a formar parte del global de la aplicación:

```js
let foo = ( x ) => {    // Reserva de memoria para una función (Object)
    result = x * 2;     // Variable 'result' no declarada
 
    return result;
};
```

En el caso anterior, `result` no ha sido declarado dentro del scope de la función `foo`. Eso obliga al intérprete a declarar esa variable como _global_, sacándola de su scope. El ejemplo equivale a lo siguiente:

```js
var result;
 
let foo = ( x ) => {
    result = x * 2;
 
    return result;
};
```

o también:

```js
let foo = ( x ) => {
    window.result = x * 2;
 
    return result;
};
```

Pensemos ahora que la función `foo` no es referenciada desde ninguna parte de nuestro programa siendo así que el recolector la marque como ‘inalcanzable’. Sin embargo, aunque para nosotros la memoria reservada para `foo` ya no es útil, `result` mantiene una referencia a su cuerpo y, para el algoritmo, **ésta continúa en uso y no debe ser purgada**.

Este problema tiene dos soluciones: si la no declaración de la variable es accidental, basta con hacerlo en su correspondiente scope. Si por el contrario es intencionada, una vez que el valor ya no sea necesario, deberíamos eliminarlo/anularlo:

```js
foo();  // Utilizamos nuestra función
 
// Una vez hemos utilizado el resultado y no lo volvemos a necesitar
window.result = null;
```

Si bien una variable global con un valor simple asociado como la del ejemplo no es una fuga de memoria importante, hay que pensar en escenarios donde ‘result’ puede almacenar gran cantidad de datos: una caché, una respuesta dada por un servidor en forma de JSON o estructura DOM, etc.

### Acciones periódicas y callbacks olvidadas

Las acciones periódicas son otro foco habitual de fugas de memoria en arquitecturas modernas de tipo SPA(Single-page application).

Una muestra podría ser un temporizador que refresca datos en pantalla de forma periódica mediante llamadas a servidor:

```js
let chartData = getChartData(),
    chartDataContainer = document.getElementById( 'chartDataContainer' );
 
setInterval( () => {
    let liveChart = chartDataContainer.querySelector( '.liveCharts' );
 
    printData( charData, liveChart );
}, 1000 );
```

Aquí el problema potencial reside en que las variables fuera del intervalo (`chartData` y `chartDataContainer`), deberían anularse una vez que ya no sean necesarias. De lo contrario, aunque estas se eliminen, permanecerán en memoria mientras sean requeridas por el cuerpo del intervalo.

Además de lo anterior, tenemos una referencia a un elemento DOM (`chartDataContainer`) que puede quedar en algún punto del programa obsoleto. Si este nodo fuera eliminado, o sobrescrito por otro (escenarios habituales en aplicaciones modernas), el sistema no puede liberar la memoria que está ocupando porque la variable `chartDataContainer` continúa manteniendo su referencia al tiempo que es requerida por `setInterval`. Es necesario que el intervalo se detenga de forma programática para que el recolector evalúe sus términos y actúe.

#### Observables

Un tema relacionado con el anterior son los observables que establecemos sobre elementos DOM.

Resulta habitual asociar funciones (_callbacks_) a determinadas acciones sobre elementos que, al igual que en el punto anterior, pueden quedar obsoletas.

Un ejemplo al respecto:
```js
let myBtn = document.getElementById( 'save' ),
 
    saveForm = () => {
        /*
         * Acciones necesarias para guardar un formulario
         * ...
         */
        console.info( 'Form saved!' );
    };
 
myBtn.addEventListener( 'click', saveForm );
 
// Eliminamos el elemento en algún momento del programa
myBtn.parentNode.removeChild( myBtn );
```

Fácilmente puede verse aquí cómo cuando eliminamos el botón de nuestra supuesta aplicación, el observador continúa manteniendo su referencia.

A pesar de lo que nos pueda sugerir la intuición, los navegadores modernos pueden lidiar con este problema. Actualmente, el árbol DOM está integrado dentro de las tablas de observación que el recolector evalúa, por lo que en teoría, es capaz de detectar que un observable ha quedado huérfano u obsoleto cuando su objeto de referencia deja de ser alcanzable desde la raíz.

Para reforzar este comportamiento, **bibliotecas de terceros como jQuery anulan automáticamente los observables** cuando el elemento sobre el que hacen referencia es eliminado (siempre a través de los métodos propios de jQuery).

Obsérvese este fragmento del código original de jQuery:

```js
function remove( elem, selector, keepData ) {
    var node,
        nodes = selector ? jQuery.filter( selector, elem ) : elem,
        i = 0;
 
    for ( ; ( node = nodes[ i ] ) != null; i++ ) {
        if ( !keepData && node.nodeType === 1 ) {
            jQuery.cleanData( getAll( node ) );
        }
 
        if ( node.parentNode ) {
            if ( keepData && jQuery.contains( node.ownerDocument, node ) ) {
                setGlobalEval( getAll( node, "script" ) );
            }
            node.parentNode.removeChild( node );
        }
    }
 
    return elem;
}
```

La línea clave es:

```js
jQuery.cleanData( getAll( node ) );
```

Donde se llama al método que anula los eventos asociados al elemento eliminado:

```js
var cleanData = function( elems ) {
    /* ... */
    jQuery.removeEvent( elem, type, data.handle );
};
```
