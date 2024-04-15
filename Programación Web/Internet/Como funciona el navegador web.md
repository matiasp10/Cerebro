Este completo manual sobre el funcionamiento interno de WebKit y Gecko es el resultado de una larga investigación de la desarrolladora israelí Tali Garsiel. Durante varios años, revisó todos los datos publicados sobre el funcionamiento interno de los navegadores y dedicó mucho tiempo a leer el código fuente de los mismos. Escribió:

> [!abstract] Tali Garsiel
> En los años en que IE dominaba el 90% no había mucho más que hacer que considerar el navegador como una "caja negra", pero ahora que los navegadores de código abierto tienen más de la mitad de la cuota de uso, es un buen momento para echar un vistazo bajo el capó del motor y ver qué hay dentro de un navegador web. Bueno, lo que hay dentro son millones de líneas de **C++**...

> [!cite] Paul Irish, Chrome Developer Relations
> Como desarrollador web, aprender los entresijos de las operaciones del navegador te ayudará a tomar mejores decisiones y a conocer las justificaciones de las mejores prácticas de desarrollo. Aunque se trata de un documento bastante extenso, te recomendamos que le dediques algo de tiempo; te garantizamos que te alegrarás de haberlo hecho.

# Introducción

Hoy en día se utilizan cinco grandes navegadores en los ordenadores de sobremesa: *Chrome*, *Internet Explorer*, *Firefox*, *Safari* y *Opera*. En los móviles, los principales navegadores son *Android Browser*, *iPhone*, *Opera Mini* y *Opera Mobile*, *UC Browser*, los navegadores *Nokia S40/S60* y *Chrome*, todos los cuales, salvo los navegadores Opera, se basan en **WebKit**. Daré ejemplos de los navegadores de código abierto Firefox y Chrome, y Safari (que es en parte de código abierto). Según las estadísticas de StatCounter (a junio de 2013) *Chrome, Firefox y Safari representan alrededor del 71%* del uso mundial de navegadores de escritorio. En móviles, *Android Browser, iPhone y Chrome constituyen alrededor del 54% del uso*.

# Funciones principales del navegador

La función principal de un navegador es **presentar el recurso web elegido, solicitándolo al servidor y mostrándolo en la ventana del navegador**. El recurso suele ser un documento HTML, pero también puede ser un PDF, una imagen u otro tipo de contenido. El usuario especifica la ubicación del recurso mediante un **URI** (Identificador Uniforme de Recursos).  
  
La forma en que el navegador interpreta y muestra los archivos HTML se especifica en las normas HTML y CSS. Estas especificaciones son mantenidas por la organización **W3C** (World Wide Web Consortium), que es la organización de estándares para la web. Durante años, los navegadores sólo cumplían una parte de las especificaciones y desarrollaban sus propias extensiones. Esto causaba graves problemas de compatibilidad a los autores de páginas web. Hoy, la mayoría de los navegadores se ajustan más o menos a las especificaciones.

Las *interfaces de usuario de los navegadores tienen mucho en común*. Entre los elementos comunes de la interfaz de usuario están:  
  
1. *Barra de direcciones* para insertar un URI
2. *Botones de retroceso y avance*  
3. Opciones de *marcadores*  
4. Botones *Actualizar y Detener para actualizar o detener la carga* de los documentos actuales  
5. Botón de *inicio* que te lleva a tu página de inicio  

Por extraño que parezca, la interfaz de usuario del navegador *no se especifica en ninguna especificación formal*, sino que procede de **buenas prácticas** conformadas a lo largo de años de experiencia y de navegadores que se imitan unos a otros. La especificación HTML5 no define los elementos de interfaz de usuario que debe tener un navegador, pero enumera algunos elementos comunes. Entre ellos están la barra de direcciones, la barra de estado y la barra de herramientas. Por supuesto, hay funciones exclusivas de cada navegador, como el gestor de descargas de Firefox.

# Estructura de alto nivel del navegador

Los principales **componentes** del navegador son:  
  
1. La **interfaz de usuario**: incluye la barra de direcciones, el botón atrás/adelante, el menú de marcadores, etc. Cada parte de la pantalla del navegador excepto la ventana donde se ve la página solicitada.  
2. El **motor del navegador**: gestiona las acciones entre la interfaz de usuario y el motor de renderizado.  
3. El **motor de renderizado**: responsable de mostrar el contenido solicitado. Por ejemplo, si el contenido solicitado es HTML, el motor de renderizado analiza HTML y CSS, y muestra el contenido analizado en la pantalla.  
4. **Networking**: para llamadas de red como peticiones HTTP, utilizando diferentes implementaciones para diferentes plataformas detrás de una interfaz independiente de la plataforma.  
5. **Interfaz de usuario backend**: Este componente utiliza los métodos de interfaz de usuario del sistema operativo subyacente. Se utiliza principalmente para dibujar widgets básicos (ventanas y cuadros combinados).
6. **Intérprete** de JavaScript. Se utiliza para analizar y ejecutar código JavaScript.  
7. **Almacenamiento de datos**. Se trata de una capa de persistencia. El navegador puede necesitar guardar todo tipo de datos localmente, como las cookies. Los navegadores también soportan mecanismos de almacenamiento como localStorage, IndexedDB, WebSQL y FileSystem.

![[Pasted image 20230808110914.png|center]]

Es importante tener en cuenta que navegadores como Chrome ejecutan múltiples instancias del motor de renderizado: una para cada pestaña. Cada pestaña se ejecuta en un proceso independiente.

# El motor de renderizado

La responsabilidad del motor de renderizado es... **Renderizar**, es decir, mostrar los contenidos solicitados en la pantalla del navegador.  
  
Por defecto, el motor de renderizado puede mostrar documentos **HTML** y **XML** e **imágenes**. Puede mostrar otros tipos de datos a través de plug-ins o extensiones; por ejemplo, mostrar documentos PDF utilizando un plug-in visor de PDF.

# Motores de renderizado

Los distintos navegadores utilizan motores de renderizado diferentes: Internet Explorer utiliza Trident, Firefox utiliza Gecko, Safari utiliza WebKit. Chrome y Opera (a partir de la versión 15) utilizan Blink, una bifurcación de WebKit.  

**WebKit** es un motor de renderizado de código abierto que comenzó siendo un motor para la plataforma Linux y fue modificado por Apple para ser compatible con Mac y Windows.

# El flujo principal

El **motor de renderizado** comenzará a obtener el contenido del documento solicitado desde la capa de red. Esto se hará normalmente en trozos de 8kB.  

Después de esto, este es el flujo básico del motor de renderizado:

![[Pasted image 20230808170725.png|center]]

1. El motor de renderizado **analiza la página HTML** solicitada en trozos, incluidos los archivos CSS externos y los elementos de estilo. A continuación, _los elementos HTML se convierten en nodos DOM_ para formar un "árbol de contenido" o "**árbol DOM**".  
2. Simultáneamente, el navegador también crea un _árbol de renderizado_ (**render tree**). Este árbol incluye tanto la información de estilo como las instrucciones visuales que definen el orden en que se mostrarán los elementos. El árbol de representación garantiza que el contenido se muestre en el orden deseado.  
3. Además, el árbol de renderizado pasa por el _proceso de maquetación_ (**Layout process**). Cuando se crea un árbol de renderizado, no se asignan los valores de posición o tamaño. Todo el proceso de cálculo de valores para evaluar la posición deseada se denomina proceso de disposición. En este proceso, a cada nodo se le asignan las coordenadas exactas. Esto garantiza que cada nodo aparezca en una posición exacta en la pantalla.  
4. El paso final es _pintar_ la pantalla, para lo cual se recorre el árbol de renderizado y se invoca el método `paint()` del renderizador, que pinta cada nodo en la pantalla utilizando la capa de fondo de la interfaz de usuario.

Es importante entender que se trata de un proceso gradual. Para mejorar la experiencia del usuario, el motor de renderizado intentará mostrar los contenidos en la pantalla lo antes posible. _No esperará hasta que todo el HTML esté analizado antes de empezar a construir y maquetar el árbol de renderizado_. Partes del contenido serán analizadas y mostradas, mientras el proceso continúa con el resto del contenido que sigue llegando de la red.

## Ejemplos

> [!cite] WebKit main flow
> ![[Pasted image 20230808170757.png|center]]

> [!cite] Mozilla's Gecko rendering engine main flow
> ![[Pasted image 20230808170806.png|center]]

Puedes ver que aunque WebKit y Gecko utilizan una terminología ligeramente diferente, el flujo es básicamente el mismo.  
  
Gecko llama "Árbol de marcos" al árbol de elementos formateados visualmente. Cada elemento es un marco. WebKit utiliza el término "Árbol de renderizado" y se compone de "Objetos de renderizado". WebKit utiliza el término "layout" para la colocación de elementos, mientras que Gecko lo llama "Reflow". "Adjuntar" es el término de WebKit para conectar los nodos DOM y la información visual para crear el árbol de renderizado. Una pequeña diferencia no semántica es que Gecko tiene una capa extra entre el HTML y el árbol DOM. Se llama "sumidero de contenido" y es una fábrica para crear elementos DOM.

## Parsing

_Analizar un documento_ significa **traducirlo a una estructura que el código pueda utilizar**. El resultado del análisis suele ser un árbol de nodos que representan la estructura del documento. Esto se llama árbol de análisis sintáctico o árbol sintáctico.  

Por ejemplo, analizar la expresión 2 + 3 - 1 podría devolver este árbol:

>[!quote] mathematical expression tree node
> ![[Pasted image 20230809103723.png|center|500]]
### Gramáticas  

El análisis sintáctico se basa en las reglas sintácticas a las que obedece el documento: _el lenguaje o formato en el que fue escrito_. Todo formato que se pueda analizar debe tener una gramática determinista compuesta por vocabulario y reglas sintácticas. Se denomina gramática libre de contexto. Los lenguajes humanos no son tales lenguajes y, por tanto, no pueden analizarse con las técnicas convencionales de análisis sintáctico.

### Lexer combination

El análisis sintáctico puede dividirse en dos subprocesos: _análisis léxico_ y _análisis sintáctico_.  
  
El **análisis léxico** es el <mark style="background: #FF5582A6;">proceso de descomponer la entrada en tokens</mark>. Los tokens son el vocabulario de la lengua: la colección de bloques de construcción válidos. En el lenguaje humano, está formado por todas las palabras que aparecen en el diccionario de ese idioma.

El **análisis sintáctico** es la <mark style="background: #BBFABBA6;">aplicación de las reglas sintácticas</mark> del lenguaje.  
  
Los analizadores sintácticos suelen dividir el trabajo entre dos componentes: el léxico (a veces llamado *tokenizador*), que se encarga de dividir la entrada en tokens válidos, y el analizador sintáctico, que se encarga de construir el árbol de análisis sintáctico analizando la estructura del documento según las reglas sintácticas del lenguaje.  
  
El **lexer** sabe cómo *eliminar los caracteres irrelevantes*, como los espacios en blanco y los saltos de línea.

> [!quote] from source document to parse trees
![[Pasted image 20230809104542.png|center]]

El proceso de análisis sintáctico es iterativo. Por lo general, *el analizador le pedirá al lexicógrafo un nuevo token e intentará que coincida con una de las reglas sintácticas*. Si una regla coincide, se añadirá un nodo correspondiente al token al árbol de análisis sintáctico y el analizador sintáctico pedirá otro token.  

Si ninguna regla coincide, el analizador almacenará el token internamente, y seguirá pidiendo tokens hasta que encuentre una regla que coincida con todos los tokens almacenados internamente. *Si no se encuentra ninguna regla, el analizador sintáctico lanzará una excepción*. Esto significa que el documento no era válido y contenía errores de sintaxis.

### Translation

En muchos casos, el árbol de análisis sintáctico no es el producto final. El análisis sintáctico se utiliza a menudo en la traducción: **transformar el documento de entrada a otro formato**. Un _ejemplo es la compilación_. El compilador que compila código fuente en código máquina primero lo analiza en un árbol de análisis sintáctico y luego traduce el árbol en un documento de código máquina.

>[!quote] compilation flow
>![[Pasted image 20230809104637.png|center]]

### Ejemplo

En la figura "mathematical expression tree node" construimos un árbol de análisis sintáctico a partir de una expresión matemática. Intentemos definir un lenguaje matemático sencillo y veamos el proceso de análisis sintáctico.

> [!note] Termino
> Nuestro lenguaje puede incluir números enteros, signos más y signos menos.

**Sintaxis**:  

1. Los elementos constitutivos de la sintaxis del lenguaje son las **expresiones, los términos y las operaciones**.  
2. Nuestro lenguaje puede **incluir cualquier número de expresiones**.  
3. Una expresión se define como un **"término" seguido de una "operación" seguida de otro término**.  
4. Una **operación es un signo más o un signo menos**.  
5. Un **término es un número entero o una expresión**.

Analicemos la entrada `2 + 3 - 1`.  
  
La primera subcadena que coincide con una regla es `2`: según la regla nº5 es un término. La segunda coincidencia es `2 + 3`: coincide con la tercera regla: un término seguido de una operación seguida de otro término. La siguiente coincidencia sólo se producirá al final de la entrada. `2 + 3 - 1` es una expresión porque ya sabemos que `2 + 3` es un término, así que tenemos un término seguido de una operación seguida de otro término. `2 + +` no coincidirá con ninguna regla y, por lo tanto, es una entrada no válida.

### Definiciones formales de vocabulario y sintaxis

El vocabulario suele expresarse mediante expresiones regulares.  
  
Por ejemplo, nuestro lenguaje se definirá como:

```
INTEGER: 0|[1-9][0-9]*  
PLUS: +  
MINUS: -
```

Como ves, los enteros se definen mediante una expresión regular.  
  
La sintaxis suele definirse en un formato llamado BNF. Nuestro lenguaje se definirá como:

```
expression := term operation term  
operation := PLUS | MINUS  
term := INTEGER | expression
```

Hemos dicho que un lenguaje puede ser analizado por analizadores sintácticos regulares si su gramática es una gramática libre de contexto. Una definición intuitiva de una gramática libre de contexto es una gramática que puede expresarse completamente en BNF. Para una definición formal, véase el artículo de Wikipedia sobre Gramática libre de contexto.

### Tipos de parsers

Hay dos tipos de analizadores sintácticos: los **descendentes** y los **ascendentes**. Una explicación intuitiva es que los analizadores descendentes examinan la estructura de alto nivel de la sintaxis e intentan encontrar una regla que coincida. Los analizadores sintácticos ascendentes comienzan con la entrada y la transforman gradualmente en reglas sintácticas, empezando por las reglas de bajo nivel hasta que se cumplen las de alto nivel.  
  
Veamos cómo analizarán nuestro ejemplo los dos tipos de analizadores sintácticos.  
  
El analizador sintáctico descendente partirá de la regla de nivel superior: identificará 2 + 3 como una expresión. A continuación, identificará 2 + 3 - 1 como una expresión (el proceso de identificación de la expresión evoluciona, coincidiendo con las demás reglas, pero el punto de partida es la regla de nivel superior).  
  
El analizador sintáctico ascendente escaneará la entrada hasta que coincida una regla. A continuación, sustituirá la entrada coincidente por la regla. Así sucesivamente hasta el final de la entrada. La expresión parcialmente coincidente se coloca en la pila del analizador sintáctico.

| Stack                | Input     |
|:-------------------- | --------- |
|                      | 2 + 3 - 1 |
| term                 | + 3 - 1   |
| term operation       | 3 - 1     |
| expression           | - 1       |
| expression operation | 1         |
| expression           | -         |

Este tipo de analizador sintáctico ascendente se denomina analizador shift-reduce, porque la entrada se desplaza hacia la derecha (imagina un puntero apuntando primero al inicio de la entrada y moviéndose hacia la derecha) y se reduce gradualmente a reglas sintácticas.

### Generación automática de analizadores sintácticos

Existen herramientas capaces de generar un analizador sintáctico. Les proporcionas la gramática de tu idioma -su vocabulario y reglas sintácticas- y ellos generan un analizador sintáctico que funciona. Crear un analizador sintáctico requiere un profundo conocimiento del análisis sintáctico y no es fácil crear un analizador sintáctico optimizado a mano, por lo que los generadores de analizadores sintácticos pueden ser muy útiles.  
  
WebKit utiliza dos generadores de parser bien conocidos: Flex para crear un lexer y Bison para crear un parser (puede que te los encuentres con los nombres Lex y Yacc). La entrada de Flex es un archivo que contiene definiciones de expresiones regulares de los tokens. La entrada de Bison son las reglas sintácticas del lenguaje en formato BNF.

## HTML Parser

La función del analizador HTML es convertir el código HTML en un árbol de análisis sintáctico.

### Definición de la gramática HTML

El vocabulario y la sintaxis de HTML se definen en especificaciones creadas por la organización W3C.

### No es una gramática libre de contexto

Como hemos visto en la introducción al análisis sintáctico, la sintaxis gramatical puede definirse formalmente utilizando formatos como BNF.  
  
Por desgracia, todos los temas convencionales de los analizadores sintácticos no se aplican a HTML (no los he mencionado sólo por diversión, se utilizarán para analizar CSS y JavaScript). HTML no puede definirse fácilmente mediante una gramática libre de contexto como la que necesitan los analizadores sintácticos.  
  
Existe un formato formal para definir HTML - DTD (Document Type Definition) - pero no es una gramática libre de contexto.  
  
Esto parece extraño a primera vista; HTML es bastante parecido a XML. Hay muchos analizadores XML disponibles. Existe una variante XML de HTML (XHTML), así que ¿Cuál es la gran diferencia?  
  
La diferencia es que el enfoque HTML es más "indulgente": permite omitir ciertas etiquetas (que se añaden implícitamente), omitir a veces las etiquetas de inicio o fin, etc. En general, se trata de un "lenguaje de programación". En general, es una sintaxis "suave", frente a la rígida y exigente de XML.  
  
Este detalle aparentemente insignificante supone una gran diferencia. Por un lado, ésta es la principal razón por la que HTML es tan popular: perdona los errores y facilita la vida al autor web. Por otro, dificulta la redacción de una gramática formal. En resumen, HTML no puede ser analizado fácilmente por los analizadores convencionales, ya que su gramática no es libre de contexto. Los analizadores XML no pueden analizar HTML.

### HTML DTD

La definición de HTML se realiza en un formato DTD. Este formato se utiliza para definir lenguajes de la familia SGML. El formato contiene definiciones para todos los elementos permitidos, sus atributos y jerarquía. Como hemos visto antes, el DTD de HTML no forma una gramática libre de contexto.  
  
Existen algunas variantes del DTD. El modo estricto se ajusta únicamente a las especificaciones, pero otros modos contienen soporte para el marcado utilizado por los navegadores en el pasado. El objetivo es la compatibilidad con contenidos anteriores. La DTD estricta actual se encuentra aquí: www.w3.org/TR/html4/strict.dtd

### DOM

El árbol de salida (el "árbol de análisis sintáctico") es un árbol de nodos de elementos y atributos DOM. DOM es la abreviatura de Document Object Model. Es el objeto de presentación del documento HTML y la interfaz de los elementos HTML con el mundo exterior, como JavaScript.  
  
La raíz del árbol es el objeto "Document".  
  
El DOM tiene una relación casi unívoca con el marcado. Por ejemplo:

```html
<html>
  <body>
    <p>
      Hello World
    </p>
    <div> <img src="example.png"/></div>
  </body>
</html>
```

Este marcado se traduciría al siguiente árbol DOM:

> [!quote] DOM tree of the example markup
> ![[Pasted image 20230809190511.png|center]]

Al igual que HTML, DOM está especificado por la organización W3C. Véase www.w3.org/DOM/DOMTR. Es una especificación genérica para manipular documentos. Un módulo específico describe elementos específicos de HTML. Las definiciones de HTML pueden encontrarse aquí: www.w3.org/TR/2003/REC-DOM-Level-2-HTML-20030109/idl-definitions.html.  
  
Cuando digo que el árbol contiene nodos DOM, quiero decir que el árbol está construido de elementos que implementan una de las interfaces DOM. Los navegadores utilizan implementaciones concretas que tienen otros atributos utilizados internamente por el navegador.

#### The parsing algorithm

Como hemos visto en las secciones anteriores, HTML no puede analizarse utilizando los analizadores normales de arriba abajo o de abajo arriba.  
  
Las razones son:  
  
1. La naturaleza indulgente del lenguaje.  
2. El hecho de que los navegadores tienen tolerancia a errores tradicional para soportar casos bien conocidos de HTML inválido.  
3. El proceso de análisis es reentrante. En otros lenguajes, el código fuente no cambia durante el análisis sintáctico, pero en HTML, el código dinámico (como los elementos de script que contienen llamadas a document.write()) puede añadir tokens adicionales, por lo que el proceso de análisis sintáctico modifica realmente la entrada.

Al no poder utilizar las técnicas habituales de análisis sintáctico, los navegadores crean analizadores personalizados para analizar HTML.  
  
El algoritmo de análisis sintáctico se describe detalladamente en la especificación HTML5. El algoritmo consta de dos etapas: tokenización y construcción del árbol.  
  
La tokenización es el análisis léxico, que analiza la entrada en tokens. Entre los tokens HTML se encuentran las etiquetas de inicio, las etiquetas de fin, los nombres de atributos y los valores de atributos.  
  
El tokenizador reconoce el token, se lo da al constructor del árbol y consume el siguiente carácter para reconocer el siguiente token, y así sucesivamente hasta el final de la entrada.

> [!quote] HTML parsing flow (taken from HTML5 spec)
> ![[Pasted image 20230809190626.png|center]]

### El algoritmo de tokenización

La salida del algoritmo es un token HTML. El algoritmo se expresa como una máquina de estados. Cada estado consume uno o más caracteres del flujo de entrada y actualiza el siguiente estado en función de esos caracteres. La decisión está influida por el estado actual de tokenización y por el estado de construcción del árbol. Esto significa que el mismo carácter consumido producirá resultados diferentes para el siguiente estado correcto, dependiendo del estado actual. El algoritmo es demasiado complejo para describirlo por completo, así que veamos un ejemplo sencillo que nos ayudará a entender el principio.

Ejemplo básico - tokenizar el siguiente HTML:

```html
<html>
  <body>
    Hello world
  </body>
</html>
```

El estado inicial es el "Estado de datos". Cuando se encuentra el carácter <, el estado cambia a "Estado de etiqueta abierta". Al consumir un carácter a-z se crea un "Token de etiqueta de inicio", el estado cambia a "Estado de nombre de etiqueta". Permanecemos en este estado hasta que se consume el carácter >. Cada carácter se añade al nuevo nombre del token. En nuestro caso el token creado es un token html.

Cuando se alcanza la etiqueta >, se emite el token actual y el estado cambia de nuevo al "Estado de datos". La etiqueta `<body>` será tratada por los mismos pasos. Hasta ahora se han emitido las etiquetas html y body. Ahora estamos de vuelta en el "Estado de datos". Consumir el carácter H de Hello world causará la creación y emisión de un token de carácter, esto continúa hasta que se alcanza el < de `</body>`. Emitiremos un carácter por cada carácter de Hola mundo.

Ahora estamos de vuelta en el "estado de etiqueta abierta". Al consumir la siguiente entrada / se creará un token de etiqueta final y pasaremos al "Estado de nombre de etiqueta". De nuevo permanecemos en este estado hasta llegar a >.Entonces se emitirá el nuevo token de etiqueta y volvemos al "Estado de datos". La entrada </html> será tratada como en el caso anterior.

> [!quote] Tokenizing the example input
> ![[Pasted image 20230809191126.png|center]]

#### Algoritmo de construcción del árbol

Cuando se crea el analizador sintáctico se crea el objeto Documento. Durante la etapa de construcción del árbol se modificará el árbol DOM con el Documento en su raíz y se le añadirán elementos. Cada nodo emitido por el tokenizador será procesado por el constructor del árbol. Para cada token, la especificación define qué elemento DOM es relevante para él y se creará para este token. El elemento se añade al árbol DOM, y también a la pila de elementos abiertos. Esta pila se utiliza para corregir los desajustes de anidamiento y las etiquetas no cerradas. El algoritmo también se describe como una máquina de estados. Los estados se denominan "modos de inserción".  
  
Veamos el proceso de construcción del árbol para la entrada de ejemplo:

```html
<html>
  <body>
    Hello world
  </body>
</html>
```

La entrada a la etapa de construcción del árbol es una secuencia de tokens procedentes de la etapa de tokenización. El primer modo es el "modo inicial". La recepción del token "html" provocará el paso al modo "antes de html" y el reprocesamiento del token en ese modo. Esto provocará la creación del elemento HTMLHtmlElement, que se anexará al objeto Document raíz.  
  
El estado cambiará a "before head". A continuación se recibe el token "body". Se creará implícitamente un elemento HTMLHeadElement aunque no tengamos un token "head" y se añadirá al árbol.

Ahora pasamos al modo "in head" y después a "after head". Se vuelve a procesar el token body, se crea e inserta un HTMLBodyElement y se pasa al modo "in body".  
  
Ahora se reciben los tokens de caracteres de la cadena "Hola mundo". El primero provocará la creación e inserción de un nodo "Texto" y los demás caracteres se añadirán a ese nodo.  
  
La recepción del token de fin de cuerpo provocará una transferencia al modo "after body". Ahora recibiremos la etiqueta html end que nos trasladará al modo "after after body". La recepción del token de fin de archivo finalizará el análisis sintáctico.

> [!quote] tree construction of example html
> ![[Pasted image 20230809191235.png|center]]

### Acciones al finalizar el parsing

En esta fase, el navegador marcará el documento como interactivo y comenzará a analizar los scripts que están en modo "diferido": aquellos que deben ejecutarse después de analizar el documento. El estado del documento pasará a ser "completo" y se disparará un evento "load".

### Tolerancia a errores de los navegadores

Nunca se produce un error de "Sintaxis no válida" en una página HTML. Los navegadores corrigen cualquier contenido no válido y siguen adelante.  
  
Tome este HTML como ejemplo:

```html
<html>
  <mytag>
  </mytag>
  <div>
  <p>
  </div>
    Really lousy HTML
  </p>
</html>
```

Debo de haber violado un millón de reglas ("mytag" no es una etiqueta estándar, anidamiento incorrecto de los elementos "p" y "div" y más), pero el navegador sigue mostrándolo correctamente y no se queja. Así que gran parte del código del analizador está corrigiendo los errores del autor del HTML.  
  
El tratamiento de errores es bastante consistente en los navegadores, pero sorprendentemente no ha formado parte de las especificaciones HTML. Al igual que los marcadores y los botones atrás/adelante, es algo que se ha desarrollado en los navegadores a lo largo de los años. Se sabe que hay construcciones HTML no válidas que se repiten en muchos sitios, y los navegadores intentan corregirlas de una manera conforme con otros navegadores.  
  
La especificación HTML5 define algunos de estos requisitos. (WebKit lo resume muy bien en el comentario al principio de la clase del analizador HTML).  
  
El analizador sintáctico analiza la entrada tokenizada en el documento, construyendo el árbol del documento. Si el documento está bien formado, analizarlo es sencillo.

#### `</br>` instead of `<br>`

Algunos sitios utilizan `</br>` en lugar de `<br>`. Para ser compatible con IE y Firefox, WebKit lo trata como `<br>`.  
  
El código:

```js
if (t->isCloseTag(brTag) && m_document->inCompatMode()) {
     reportError(MalformedBRError);
     t->beginTag = true;
}
```

Tenga en cuenta que la gestión de errores es interna: no se presentará al usuario.

#### Una mesa perdida

Una tabla perdida es una tabla dentro de otra tabla, pero no dentro de una celda de tabla.  
  
Por ejemplo:

```html
<table>
  <table>
    <tr><td>inner table</td></tr>
  </table>
  <tr><td>outer table</td></tr>
</table>
```

WebKit cambiará la jerarquía a dos tablas hermanas:

```html
<table>
  <tr><td>outer table</td></tr>
</table>
<table>
  <tr><td>inner table</td></tr>
</table>
```

El código:

```js
if (m_inStrayTableContent && localName == tableTag)
        popBlock(tableTag);
```

WebKit utiliza una pila para el contenido del elemento actual: sacará la tabla interior de la pila de la tabla exterior. Las tablas serán ahora hermanas.

#### Elementos de formulario anidados

En caso de que el usuario ponga un formulario dentro de otro formulario, se ignora el segundo formulario.  
  
El código:

```js
if (!m_currentFormElement) {
        m_currentFormElement = new HTMLFormElement(formTag,    m_document);
}
```

#### Una jerarquía de etiquetas demasiado profunda

El comentario habla por sí solo.

> [!hint] Un ejemplo
> www.liceo.edu.mx es un ejemplo de un sitio que alcanza un nivel de anidamiento de unas 1500 etiquetas, todas procedentes de un montón de `<b>`. Sólo permitiremos un máximo de 20 etiquetas anidadas del mismo tipo antes de ignorarlas todas juntas.

```js
bool HTMLParser::allowNestedRedundantTag(const AtomicString& tagName)
{

unsigned i = 0;
for (HTMLStackElem* curr = m_blockStack;
         i < cMaxRedundantTagDepth && curr && curr->tagName == tagName;
     curr = curr->next, i++) { }
return i != cMaxRedundantTagDepth;
}
```

#### Etiquetas html o body finales mal colocadas

Una vez más, el comentario habla por sí solo.

>[!hint] Soporte para HTML realmente roto
>Nunca cerramos la etiqueta body, ya que algunas estúpidas páginas web la cierran antes del final real del documento. Confiemos en la llamada end() para cerrar las cosas.

```js
if (t->tagName == htmlTag || t->tagName == bodyTag )
        return;
```

Así que cuidado, autores web: a menos que queráis aparecer como ejemplo en un fragmento de código de tolerancia a errores de WebKit, escribid un HTML bien formado.

## CSS Parsing

¿Recuerdas los conceptos de análisis sintáctico de la introducción? Pues bien, a diferencia de HTML, CSS es una gramática libre de contexto y puede analizarse utilizando los tipos de analizadores descritos en la introducción. De hecho, la especificación CSS define la gramática léxica y sintáctica de CSS.  
  
Veamos algunos ejemplos:  
  
La gramática léxica (vocabulario) está definida por expresiones regulares para cada token:

```
comment   \/\*[^*]*\*+([^/*][^*]*\*+)*\/
num       [0-9]+|[0-9]*"."[0-9]+
nonascii  [\200-\377]
nmstart   [_a-z]|{nonascii}|{escape}
nmchar    [_a-z0-9-]|{nonascii}|{escape}
name      {nmchar}+
ident     {nmstart}{nmchar}*
```

"ident" es la abreviatura de identificador, como el nombre de una clase. "name" es el id de un elemento (al que se hace referencia con "#" )  
  
La gramática sintáctica se describe en BNF.

```
ruleset
  : selector [ ',' S* selector ]*
    '{' S* declaration [ ';' S* declaration ]* '}' S*
  ;
selector
  : simple_selector [ combinator selector | S+ [ combinator? selector ]? ]?
  ;
simple_selector
  : element_name [ HASH | class | attrib | pseudo ]*
  | [ HASH | class | attrib | pseudo ]+
  ;
class
  : '.' IDENT
  ;
element_name
  : IDENT | '*'
  ;
attrib
  : '[' S* IDENT S* [ [ '=' | INCLUDES | DASHMATCH ] S*
    [ IDENT | STRING ] S* ] ']'
  ;
pseudo
  : ':' [ IDENT | FUNCTION S* [IDENT S*] ')' ]
  ;
```

Explicación:  
  
Un conjunto de reglas es esta estructura:

```js
div.error, a.error {
  color:red;
  font-weight:bold;
}
```

`div.error` y `a.error` son selectores. La parte dentro de las llaves contiene las reglas que son aplicadas por este conjunto de reglas. Esta estructura se define formalmente en esta definición:

```js
ruleset
  : selector [ ',' S* selector ]*
    '{' S* declaration [ ';' S* declaration ]* '}' S*
  ;
```

Esto significa que un conjunto de reglas es un selector u opcionalmente un número de selectores separados por una coma y espacios (S significa espacio en blanco). Un conjunto de reglas contiene llaves y dentro de ellas una declaración u, opcionalmente, varias declaraciones separadas por punto y coma. "declaración" y "selector" se definirán en las siguientes definiciones BNF.

### WebKit CSS parser

WebKit utiliza los generadores de analizadores Flex y Bison para crear analizadores automáticamente a partir de los archivos de gramática CSS. Como recordarás de la introducción al analizador sintáctico, Bison crea un analizador sintáctico shift-reduce de abajo a arriba. Firefox utiliza un analizador sintáctico descendente escrito manualmente. En ambos casos, cada archivo CSS se analiza en un objeto StyleSheet. Cada objeto contiene reglas CSS. Los objetos regla CSS contienen objetos selector y declaración y otros objetos correspondientes a la gramática CSS.

> [!quote] parsing CSS
> ![[Pasted image 20230810094535.png|center]]

## El orden de procesamiento de los scripts y las hojas de estilo

### Scripts

El modelo de la web es síncrono. Los autores esperan que los scripts se analicen y ejecuten inmediatamente cuando el analizador llega a una etiqueta `<script>`. El análisis del documento se detiene hasta que se ejecuta el script. Si el script es externo, primero hay que obtener el recurso de la red; esto también se hace de forma sincrónica, y el análisis se detiene hasta que se obtiene el recurso. Este fue el modelo durante muchos años y también se especifica en HTML4 y 5. Los autores pueden añadir el atributo "defer" a un script, en cuyo caso no detendrá el análisis del documento y se ejecutará una vez analizado el documento. HTML5 añade una opción para marcar el script como asíncrono, de modo que será analizado y ejecutado por un hilo diferente.

### Análisis especulativo

Tanto WebKit como Firefox realizan esta optimización. Mientras se ejecutan los scripts, otro hilo analiza el resto del documento y averigua qué otros recursos deben cargarse desde la red y los carga. De este modo, los recursos pueden cargarse en conexiones paralelas y se mejora la velocidad general. Nota: el analizador especulativo sólo analiza referencias a recursos externos como scripts externos, hojas de estilo e imágenes: no modifica el árbol DOM, eso se deja al analizador principal.

### Hojas de estilo

Por otro lado, las hojas de estilo tienen un modelo diferente. Conceptualmente parece que como las hojas de estilo no cambian el árbol DOM, no hay razón para esperarlas y detener el análisis del documento. Sin embargo, existe el problema de que los scripts solicitan información de estilo durante la fase de análisis del documento. Si el estilo no está cargado y analizado todavía, el script obtendrá respuestas erróneas y aparentemente esto ha causado muchos problemas. Parece ser un caso extremo, pero es bastante común. Firefox bloquea todos los scripts cuando hay una hoja de estilo que todavía se está cargando y analizando. WebKit bloquea los scripts sólo cuando intentan acceder a ciertas propiedades de estilo que pueden verse afectadas por hojas de estilo descargadas.

## Construcción del árbol de renderizado

Mientras se construye el árbol DOM, el navegador construye otro árbol, el árbol de renderizado. Este árbol contiene los elementos visuales en el orden en que se mostrarán. Es la representación visual del documento. El propósito de este árbol es permitir pintar los contenidos en su orden correcto.  
  
Firefox llama "marcos" a los elementos del árbol de renderizado. WebKit utiliza el término renderizador u objeto de renderizado.  
  
Un renderizador sabe cómo distribuirse y pintarse a sí mismo y a sus hijos.  
  
La clase RenderObject de WebKit, la clase base de los renderizadores, tiene la siguiente definición:

```js
class RenderObject{
  virtual void layout();
  virtual void paint(PaintInfo);
  virtual void rect repaintRect();
  Node* node;  //the DOM node
  RenderStyle* style;  // the computed style
  RenderLayer* containgLayer; //the containing z-index layer
}
```

Cada renderizador representa un área rectangular que suele corresponder a la caja CSS de un nodo, tal y como se describe en la especificación CSS2. Incluye información geométrica como anchura, altura y posición.  
  
El tipo de caja se ve afectado por el valor "display" del atributo de estilo relevante para el nodo (véase la sección de cálculo de estilo). Aquí está el código WebKit para decidir qué tipo de renderizador debe ser creado para un nodo DOM, de acuerdo con el atributo display:

```js
RenderObject* RenderObject::createObject(Node* node, RenderStyle* style)
{
    Document* doc = node->document();
    RenderArena* arena = doc->renderArena();
    ...
    RenderObject* o = 0;

    switch (style->display()) {
        case NONE:
            break;
        case INLINE:
            o = new (arena) RenderInline(node);
            break;
        case BLOCK:
            o = new (arena) RenderBlock(node);
            break;
        case INLINE_BLOCK:
            o = new (arena) RenderBlock(node);
            break;
        case LIST_ITEM:
            o = new (arena) RenderListItem(node);
            break;
       ...
    }

    return o;
}
```

También se tiene en cuenta el tipo de elemento: por ejemplo, los controles de formulario y las tablas tienen marcos especiales.  
  
En WebKit si un elemento quiere crear un renderizador especial, anulará el método `createRenderer()`. Los renderizadores apuntan a objetos de estilo que contienen información no geométrica.

### Relación del árbol de renderizado con el árbol DOM

Los renderizadores corresponden a elementos DOM, pero la relación no es uno a uno. Los elementos DOM no visuales no se insertarán en el árbol de renderizado. Un ejemplo es el elemento "head". Tampoco aparecerán en el árbol los elementos cuyo valor de visualización haya sido asignado a "none" (mientras que los elementos con visibilidad "hidden" sí aparecerán en el árbol).  
  
Hay elementos DOM que corresponden a varios objetos visuales. Suele tratarse de elementos con una estructura compleja que no puede describirse con un único rectángulo. Por ejemplo, el elemento "select" tiene tres renderizadores: uno para el área de visualización, otro para el cuadro de lista desplegable y otro para el botón. También cuando el texto se divide en varias líneas porque la anchura no es suficiente para una línea, las nuevas líneas se añadirán como renderizadores adicionales.  
  
Otro ejemplo de múltiples renderizadores es el HTML roto. Según la especificación CSS, un elemento en línea debe contener sólo elementos de bloque o sólo elementos en línea. En el caso de contenido mixto, se crearán renderizadores de bloque anónimos para envolver los elementos en línea.  
  
Algunos objetos de renderizado corresponden a un nodo DOM pero no en el mismo lugar del árbol. Los elementos flotantes y absolutamente posicionados están fuera de flujo, colocados en una parte diferente del árbol, y mapeados al marco real. Un marco marcador de posición es donde deberían haber estado.

> [!quote] The render tree and the corresponding DOM tree. The "Viewport" is the initial containing block. In WebKit it will be the "RenderView" object
> ![[Pasted image 20230810095952.png|center]]

#### El flujo de construcción del árbol

En Firefox, la presentación se registra como oyente de las actualizaciones del DOM. La presentación delega la creación del marco al `FrameConstructor` y el constructor resuelve el estilo (ver cálculo de estilo) y crea un marco.  
  
En WebKit el proceso de resolver el estilo y crear un renderizador se llama "attach". Cada nodo DOM tiene un método "attach". El attachment es síncrono, la inserción de un nodo en el árbol DOM llama al método "attach" del nuevo nodo.  
  
El procesamiento de las etiquetas html y body resulta en la construcción de la raíz del árbol de render. El objeto de renderizado raíz corresponde a lo que la especificación CSS llama el bloque contenedor: el bloque superior que contiene todos los demás bloques. Sus dimensiones son el viewport: las dimensiones del área de visualización de la ventana del navegador. Firefox lo llama ViewPortFrame y WebKit lo llama RenderView. Este es el objeto de renderizado al que apunta el documento. El resto del árbol se construye como una inserción de nodos DOM.  
  
Ver la especificación CSS2 sobre el modelo de procesamiento.

### Style Computation

Construir el árbol de renderizado requiere calcular las propiedades visuales de cada objeto de renderizado. Esto se hace calculando las propiedades de estilo de cada elemento.  
  
El estilo incluye hojas de estilo de diversos orígenes, elementos de estilo en línea y propiedades visuales en el HTML (como la propiedad "bgcolor"), que se traducen en propiedades de estilo CSS correspondientes.  
  
Los orígenes de las hojas de estilo son las hojas de estilo predeterminadas del navegador, las hojas de estilo proporcionadas por el autor de la página y las hojas de estilo del usuario, es decir, las hojas de estilo proporcionadas por el usuario del navegador (los navegadores le permiten definir sus estilos favoritos. En Firefox, por ejemplo, esto se hace colocando una hoja de estilo en la carpeta "Perfil de Firefox").  
  
El cálculo de estilos plantea algunas dificultades:

1. Los datos de estilo son una construcción muy grande, que contiene las numerosas propiedades de estilo, esto puede causar problemas de memoria.  
2. Encontrar las reglas coincidentes para cada elemento puede causar problemas de rendimiento si no se optimiza. Recorrer toda la lista de reglas de cada elemento para encontrar coincidencias es una tarea pesada. Los selectores pueden tener una estructura compleja que puede hacer que el proceso de búsqueda de coincidencias comience en un camino aparentemente prometedor que se demuestre inútil y haya que intentar otro camino.  
   
   Por ejemplo, este selector compuesto:
   
```css
div div div div{
...
}
```

Significa que las reglas se aplican a un `<div>` que es descendiente de 3 divs. Supongamos que desea comprobar si la regla se aplica a un determinado elemento `<div>`. Usted elige un determinado camino hacia arriba en el árbol para la comprobación. Es posible que tenga que recorrer el árbol de nodos hacia arriba sólo para descubrir que sólo hay dos divs y la regla no se aplica. A continuación, tendrá que probar otros caminos en el árbol.

3. La aplicación de las normas implica reglas en cascada bastante complejas que definen la jerarquía de las normas.

Veamos cómo afrontan los navegadores estos problemas:

### Sharing style data

Los nodos WebKit hacen referencia a objetos de estilo (RenderStyle). Estos objetos pueden ser compartidos por nodos en algunas condiciones. Los nodos son hermanos o primos y:  
  
1. Los elementos deben estar en el mismo estado del ratón (por ejemplo, uno no puede estar en :hover mientras que el otro no)  
2. Ninguno de los elementos debe tener id  
3. Los nombres de las etiquetas deben coincidir  
4. Los atributos de clase deben coincidir  
5. El conjunto de atributos asignados debe ser idéntico  
6. Los estados de enlace deben coincidir  
7. Los estados de foco deben coincidir  
8. Ninguno de los elementos debe estar afectado por selectores de atributos, entendiendo por afectado cualquier coincidencia de selector que utilice un selector de atributos en cualquier posición del selector.  
9. No debe haber ningún atributo de estilo en línea en los elementos.  
10. No debe haber ningún selector hermano en uso. WebCore simplemente lanza un interruptor global cuando se encuentra cualquier selector hermano y desactiva la compartición de estilos para todo el documento cuando están presentes. Esto incluye el selector + y selectores como :first-child y :last-child.

### Firefox rule tree

Firefox tiene dos árboles adicionales para facilitar el cálculo de estilos: el árbol de reglas y el árbol de contexto de estilos. WebKit también tiene objetos de estilo, pero no se almacenan en un árbol como el árbol de contexto de estilo, sólo el nodo DOM apunta a su estilo relevante.

> [!quote] Firefox style context tree.
> ![[Pasted image 20230810101435.png|center]]

Los contextos de estilo contienen valores finales. Los valores se calculan aplicando todas las reglas de concordancia en el orden correcto y realizando manipulaciones que los transforman de valores lógicos a valores concretos. Por ejemplo, si el valor lógico es un porcentaje de la pantalla, se calculará y transformará a unidades absolutas. La idea del árbol de reglas es realmente inteligente. Permite compartir estos valores entre nodos para evitar computarlos de nuevo. Esto también ahorra espacio.  
  
Todas las reglas coincidentes se almacenan en un árbol. Los nodos inferiores de una ruta tienen mayor prioridad. El árbol contiene todos los caminos para las coincidencias de reglas que se encontraron. El almacenamiento de las reglas se realiza de forma perezosa. El árbol no se calcula al principio para cada nodo, sino que cada vez que es necesario calcular el estilo de un nodo, las rutas calculadas se añaden al árbol.  
  
La idea es ver los caminos del árbol como palabras en un léxico. Supongamos que ya hemos calculado este árbol de reglas:

> [!quote] Computed rule tree.
> ![[Pasted image 20230810101459.png|center]]

Supongamos que necesitamos emparejar reglas para otro elemento en el árbol de contenido, y descubrimos que las reglas emparejadas (en el orden correcto) son B-E-I. Ya tenemos este camino en el árbol porque ya hemos calculado el camino A-B-E-I-L. Ahora tendremos menos trabajo que hacer.  
  
Veamos cómo el árbol nos ahorra trabajo.

### Division into structs

Los contextos de estilo se dividen en structs. Estos structs contienen información de estilo para una determinada categoría, como el borde o el color. Todas las propiedades de un struct son heredadas o no heredadas. Las propiedades heredadas son aquellas que, a menos que sean definidas por el elemento, se heredan de su padre. Las propiedades no heredadas (llamadas propiedades "reset") utilizan valores por defecto si no están definidas.  
  
El árbol nos ayuda almacenando en caché structs enteros (que contienen los valores finales calculados) en el árbol. La idea es que si el nodo inferior no proporciona una definición para una estructura, se puede utilizar una estructura almacenada en caché en un nodo superior.

### Computing the style contexts using the rule tree

Al calcular el contexto de estilo para un elemento determinado, primero calculamos una ruta en el árbol de reglas o utilizamos una ya existente. A continuación, empezamos a aplicar las reglas de la ruta para rellenar los structs de nuestro nuevo contexto de estilo. Empezamos por el nodo inferior de la ruta, el de mayor precedencia (normalmente, el selector más específico), y recorremos el árbol hasta llenar la estructura. Si no hay especificación para el struct en ese nodo de regla, entonces podemos optimizar mucho - subimos por el árbol hasta encontrar un nodo que lo especifique completamente y simplemente apuntamos a él - esa es la mejor optimización - se comparte todo el struct. Esto ahorra computación de valores finales y memoria.  
  
Si encontramos definiciones parciales subimos por el árbol hasta llenar la estructura.  
  
Si no encontramos ninguna definición para nuestra estructura entonces, en caso de que la estructura sea un tipo "heredado", apuntamos a la estructura de nuestro padre en el árbol de contexto. En este caso también conseguimos compartir structs. Si es un struct restablecido entonces se usarán los valores por defecto.  
  
Si el nodo más específico añade valores entonces necesitamos hacer algunos cálculos extra para transformarlo en valores reales. A continuación, almacenamos en caché el resultado en el nodo del árbol para que pueda ser utilizado por los hijos.  
  
En caso de que un elemento tenga un hermano que apunte al mismo nodo del árbol, el contexto de estilo completo puede ser compartido entre ellos.  
  
Veamos un ejemplo: Supongamos que tenemos este HTML

```html
<html>
  <body>
    <div class="err" id="div1">
      <p>
        this is a <span class="big"> big error </span>
        this is also a
        <span class="big"> very  big  error</span> error
      </p>
    </div>
    <div class="err" id="div2">another error</div>
  </body>
</html>
```

Y las siguientes reglas:

```css
div {margin: 5px; color:black}
.err {color:red}
.big {margin-top:3px}
div span {margin-bottom:4px}
#div1 {color:blue}
#div2 {color:green}
```

Para simplificar las cosas, digamos que sólo tenemos que rellenar dos estructuras: la estructura de color y la estructura de margen. La estructura de color sólo contiene un miembro: el color. La estructura de margen contiene los cuatro lados.  
  
El árbol de reglas resultante tendrá este aspecto (los nodos están marcados con el nombre del nodo: el número de la regla a la que apuntan):

> [!quote] The rule tree
> ![[Pasted image 20230810102255.png|center]]

El árbol contextual tendrá este aspecto (nombre del nodo: nodo de la regla al que apuntan):

> [!quote] The context tree
> ![[Pasted image 20230810103526.png|center]]

Supongamos que analizamos el HTML y llegamos a la segunda etiqueta `<div>`. Necesitamos crear un contexto de estilo para este nodo y rellenar sus estructuras de estilo.  
  
Haremos coincidir las reglas y descubriremos que las reglas coincidentes para el `<div>` son 1, 2 y 6. Esto significa que ya existe una ruta en el árbol que nuestro elemento puede usar y sólo necesitamos añadirle otro nodo para la regla 6 (nodo F en el árbol de reglas).  
  
Crearemos un contexto de estilo y lo pondremos en el árbol de contexto. El nuevo contexto de estilo apuntará al nodo F del árbol de reglas.  
  
Ahora tenemos que rellenar las estructuras de estilo. Empezaremos rellenando la estructura de margen. Dado que el último nodo de la regla (F) no se añade a la estructura de margen, podemos subir por el árbol hasta encontrar una estructura en caché calculada en una inserción de nodo anterior y utilizarla. La encontraremos en el nodo B, que es el nodo superior que especificaba reglas de margen.  
  
Tenemos una definición para la estructura color, así que no podemos usar una estructura en caché. Como el color tiene un atributo no necesitamos subir por el árbol para rellenar otros atributos. Calcularemos el valor final (convertir cadena a RGB, etc.) y almacenaremos en caché la estructura calculada en este nodo.

El trabajo con el segundo elemento `<span>` es aún más sencillo. Compararemos las reglas y llegaremos a la conclusión de que apunta a la regla G, como el span anterior. Como tenemos hermanos que apuntan al mismo nodo, podemos compartir todo el contexto de estilo y sólo apuntar al contexto del span anterior.  
  
Para los structs que contienen reglas que se heredan del padre, el almacenamiento en caché se realiza en el árbol de contexto (la propiedad de color es en realidad heredada, pero Firefox la trata como restablecida y la almacena en caché en el árbol de reglas).  
  
Por ejemplo, si añadimos reglas para fuentes en un párrafo:

```css
p {font-family: Verdana; font size: 10px; font-weight: bold}
```

Entonces el elemento párrafo, que es hijo del div en el árbol contextual, podría haber compartido la misma estructura de fuentes que su padre. Esto es así si no se especificaron reglas de fuente para el párrafo.  
  
En WebKit, que no tiene un árbol de reglas, las declaraciones coincidentes se recorren cuatro veces. Primero se aplican las propiedades no importantes de alta prioridad (propiedades que deben aplicarse primero porque otras dependen de ellas, como la visualización), luego las importantes de alta prioridad, luego las no importantes de prioridad normal y luego las reglas importantes de prioridad normal. Esto significa que las propiedades que aparecen varias veces se resolverán según el orden de cascada correcto. La última gana.  
  
Resumiendo: compartir los objetos de estilo (en su totalidad o algunos de los structs que contienen) resuelve los problemas 1 y 3. El árbol de reglas de Firefox también ayuda a aplicar las propiedades en el orden correcto.

### Manipular las reglas para un partido fácil

Existen varias fuentes de normas de estilo:

1. Reglas CSS, ya sea en hojas de estilo externas o en elementos de estilo.

    ```css
    p {color: blue}
    ```

2. Atributos de estilo en línea como

    ```html
    <p style="color: blue" />
    ```

3. Atributos visuales HTML (que se asignan a las reglas de estilo pertinentes)

    ```html
    <p bgcolor="blue" />
    ```

Los dos últimos son fácilmente emparejados con el elemento ya que posee los atributos de estilo y los atributos HTML pueden ser mapeados usando el elemento como clave.  
  
Como se ha indicado anteriormente en el número 2, la correspondencia de reglas CSS puede ser más complicada. Para resolver la dificultad, las reglas se manipulan para facilitar el acceso.  
  
Después de analizar la hoja de estilo, las reglas se añaden a uno de varios mapas hash, según el selector. Hay mapas por id, por nombre de clase, por nombre de etiqueta y un mapa general para todo lo que no encaje en esas categorías. Si el selector es un id, la regla se añadirá al mapa de id, si es una clase se añadirá al mapa de clases, etc.  
  
Esta manipulación hace que sea mucho más fácil hacer coincidir las reglas. No hay necesidad de mirar en cada declaración: podemos extraer las reglas relevantes para un elemento de los mapas. Esta optimización elimina más del 95 % de las reglas, de modo que ni siquiera es necesario tenerlas en cuenta durante el proceso de correspondencia(4.1).

Veamos por ejemplo las siguientes reglas de estilo:

```css
p.error {color: red}
#messageDiv {height: 50px}
div {margin: 5px}
```

La primera regla se insertará en el mapa de clases. La segunda en el mapa de id y la tercera en el mapa de etiquetas.  
  
Para el siguiente fragmento HTML;

```html
<p class="error">an error occurred</p>
<div id=" messageDiv">this is a message</div>
```

Primero intentaremos encontrar reglas para el elemento p. El mapa de clases contendrá una clave "error" bajo la cual se encuentra la regla para "p.error". El elemento div tendrá reglas relevantes en el mapa de id (la clave es el id) y en el mapa de etiquetas. Así que el único trabajo que queda es averiguar cuáles de las reglas extraídas por las claves coinciden realmente.  
  
Por ejemplo, si la regla para el elemento div era

```css
table div {margin: 5px}
```

seguirá extrayéndose del mapa de etiquetas, porque la clave es el selector situado más a la derecha, pero no coincidiría con nuestro elemento div, que no tiene un ancestro de tabla.  
  
Tanto WebKit como Firefox realizan esta manipulación.

### Aplicar las normas en el orden de cascada correcto

El objeto de estilo tiene propiedades correspondientes a cada atributo visual (todos los atributos CSS pero más genéricos). Si la propiedad no está definida por ninguna de las reglas coincidentes, algunas propiedades pueden ser heredadas por el objeto de estilo del elemento padre. Otras propiedades tienen valores por defecto.  
  
El problema comienza cuando hay más de una definición - aquí viene la orden en cascada para resolver el problema.

### Orden en cascada de las hojas de estilo

Una declaración para una propiedad de estilo puede aparecer en varias hojas de estilo, y varias veces dentro de una hoja de estilo. Esto significa que el orden de aplicación de las reglas es muy importante. Esto se denomina orden "en cascada". Según la especificación CSS2, el orden en cascada es (de menor a mayor):  
  
1. Declaraciones del navegador  
2. Declaraciones normales del usuario  
3. Declaraciones normales del autor  
4. Declaraciones importantes del autor  
5. Declaraciones importantes del usuario  

Las declaraciones del navegador son las menos importantes y el usuario anula al autor sólo si la declaración fue marcada como importante. Las declaraciones con el mismo orden se ordenarán por especificidad y luego por el orden en que se especifican. Los atributos visuales HTML se traducen a declaraciones CSS coincidentes . Se tratan como reglas de autor con prioridad baja.

### Especificidad

La especificidad del selector se define en la especificación CSS2 de la siguiente manera:  
  
1. cuenta 1 si la declaración de la que procede es un atributo 'style' en lugar de una regla con selector, 0 en caso contrario (= a)  
2. contar el número de atributos ID en el selector (= b)  
3. contar el número de otros atributos y pseudo-clases en el selector (= c)  
4. contar el número de nombres de elementos y pseudoelementos en el selector (= d)  
5. Concatenando los cuatro números a-b-c-d (en un sistema numérico con una base grande) se obtiene la especificidad.  
  
La base numérica que debe utilizar viene definida por el recuento más alto que tenga en una de las categorías.  
  
Por ejemplo, si a=14 puedes utilizar la base hexadecimal. En el improbable caso de que a=17 necesitará una base numérica de 17 dígitos. La última situación puede ocurrir con un selector como este: html body div div p... (17 etiquetas en tu selector... no es muy probable).  
  
Algunos ejemplos:

```css
 *             {}  /* a=0 b=0 c=0 d=0 -> specificity = 0,0,0,0 */
 li            {}  /* a=0 b=0 c=0 d=1 -> specificity = 0,0,0,1 */
 li:first-line {}  /* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 */
 ul li         {}  /* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 */
 ul ol+li      {}  /* a=0 b=0 c=0 d=3 -> specificity = 0,0,0,3 */
 h1 + *[rel=up]{}  /* a=0 b=0 c=1 d=1 -> specificity = 0,0,1,1 */
 ul ol li.red  {}  /* a=0 b=0 c=1 d=3 -> specificity = 0,0,1,3 */
 li.red.level  {}  /* a=0 b=0 c=2 d=1 -> specificity = 0,0,2,1 */
 #x34y         {}  /* a=0 b=1 c=0 d=0 -> specificity = 0,1,0,0 */
 style=""          /* a=1 b=0 c=0 d=0 -> specificity = 1,0,0,0 */
```

### Ordenar las normas

Una vez cotejadas las reglas, se ordenan según las reglas en cascada. WebKit utiliza la ordenación por burbujas para las listas pequeñas y la ordenación por fusión para las grandes. WebKit implementa la ordenación anulando el operador "`>`" para las reglas:

```js
static bool operator >(CSSRuleData& r1, CSSRuleData& r2)
{
    int spec1 = r1.selector()->specificity();
    int spec2 = r2.selector()->specificity();
    return (spec1 == spec2) : r1.position() > r2.position() : spec1 > spec2;
}
```

### Proceso gradual

WebKit utiliza una bandera que marca si se han cargado todas las hojas de estilo de nivel superior (incluyendo @imports). Si el estilo no está completamente cargado al adjuntar, se utilizan marcadores de posición y se marca en el documento, y se recalcularán una vez que se hayan cargado las hojas de estilo.

## Layout

Cuando el renderizador se crea y se añade al árbol, no tiene posición ni tamaño. El cálculo de estos valores se denomina layout o reflow.  
  
HTML utiliza un modelo de diseño basado en el flujo, lo que significa que la mayor parte del tiempo es posible calcular la geometría en una sola pasada. Los elementos que se encuentran más adelante "en el flujo" no suelen afectar a la geometría de los elementos que se encuentran antes "en el flujo", por lo que el diseño puede realizarse de izquierda a derecha y de arriba abajo a lo largo del documento. Hay excepciones: por ejemplo, las tablas HTML pueden requerir más de una pasada.  
  
El sistema de coordenadas es relativo al marco raíz. Se utilizan las coordenadas superior e izquierda.  
  
La maquetación es un proceso recursivo. Comienza en el renderizador raíz, que corresponde al elemento `<html>` del documento HTML. La maquetación continúa recursivamente a través de toda o parte de la jerarquía de marcos, calculando la información geométrica para cada renderizador que la requiera.  
  
La posición del renderizador raíz es 0,0 y sus dimensiones son el viewport - la parte visible de la ventana del navegador.  
  
Todos los renderizadores tienen un método "layout" o "reflow", cada renderizador invoca el método layout de sus hijos que necesitan layout.

### Sistema de bits sucios

Para no tener que hacer una maquetación completa por cada pequeño cambio, los navegadores utilizan un sistema de "bits sucios". Un renderizador que se modifica o añade se marca a sí mismo y a sus hijos como "sucios": necesitan maquetación.  
  
Hay dos banderas: "dirty" (sucio), y "children are dirty" (los hijos están sucios), que significa que aunque el propio renderizador esté bien, tiene al menos un hijo que necesita maquetación.

### Global and incremental layout

La maquetación puede activarse en todo el árbol de renderizado: es la maquetación "global". Esto puede ocurrir como resultado de:  
  
1. Un cambio de estilo global que afecta a todos los renderizadores, como un cambio de tamaño de fuente.  
2. Como resultado de un cambio de tamaño de la pantalla  

La maquetación puede ser incremental, sólo se maquetarán los renderizadores sucios (esto puede causar algunos daños que requerirán maquetaciones extra).  
  
La maquetación incremental se activa (de forma asíncrona) cuando los renderizadores están sucios. Por ejemplo, cuando se añaden nuevos renderizadores al árbol de renderizado después de que un contenido extra haya llegado de la red y se haya añadido al árbol DOM.

> [!quote] Incremental layout - only dirty renderers and their children are laid out
> ![[Pasted image 20230811112157.png|center]]

### Asynchronous and Synchronous layout

La maquetación incremental se realiza de forma asíncrona. Firefox pone en cola los "comandos de reflujo" para los diseños incrementales y un programador activa la ejecución por lotes de estos comandos. WebKit también dispone de un temporizador que ejecuta una maquetación incremental: se recorre el árbol y los renderizadores "sucios" se maquetan.  
  
Los scripts que solicitan información de estilo, como "offsetHeight", pueden activar la maquetación incremental de forma sincrónica.  
  
El diseño global se ejecutará normalmente de forma sincrónica.  
  
A veces, el diseño se activa como una llamada de retorno después de un diseño inicial porque algunos atributos, como la posición de desplazamiento, han cambiado.

### Optimizations

Cuando un diseño se activa mediante un "redimensionamiento" o un cambio en la posición del renderizador (y no en el tamaño), los tamaños de los renders se toman de una caché y no se recalculan...  
  
En algunos casos sólo se modifica un subárbol y la maquetación no comienza desde la raíz. Esto puede ocurrir en los casos en que el cambio es local y no afecta a su entorno - como el texto insertado en los campos de texto (de lo contrario, cada pulsación de tecla desencadenaría un diseño a partir de la raíz).

### The layout process

La disposición suele seguir el siguiente patrón:  
  
1. El renderizador padre determina su propio ancho.  
2. El padre pasa por encima de los hijos y:  
	1. Coloca el renderer child (establece sus x e y).  
	2. Llama al layout child si es necesario -están sucios o estamos en un layout global, o por alguna otra razón- que calcula la altura del child.  
3. El padre utiliza las alturas acumuladas de los hijos y las alturas de los márgenes y el relleno para establecer su propia altura - esto será utilizado por el padre del renderizador padre.  
4. Establece su bit dirty a false.  

Firefox utiliza un objeto "state" (nsHTMLReflowState) como parámetro para el diseño (llamado "reflow"). Entre otros, el estado incluye el ancho de los padres.  
  
La salida del layout de Firefox es un objeto "metrics" (nsHTMLReflowMetrics). Contendrá la altura calculada por el renderizador.

### Width calculation

La anchura del renderizador se calcula utilizando la anchura del bloque contenedor, la propiedad "width" del estilo del renderizador, los márgenes y los bordes.  
  
Por ejemplo, la anchura del siguiente div:

```html
<div style="width: 30%"/>
```

Sería calculado por WebKit de la siguiente manera(class RenderBox method calcWidth):  
  
El ancho del contenedor es el máximo de los contenedores availableWidth y 0. El availableWidth en este caso es el contentWidth que se calcula como:

```
clientWidth() - paddingLeft() - paddingRight()
```

`clientWidth` y `clientHeight` representan el interior de un objeto excluyendo el borde y la barra de desplazamiento.  
  
La anchura de los elementos es el atributo de estilo "`width`". Se calculará como un valor absoluto calculando el porcentaje de la anchura del contenedor.  
  
Ahora se añaden los bordes horizontales y los paddings.  

Hasta ahora se calculaba el "ancho preferido". Ahora se calcularán los anchos mínimo y máximo.  
  
Si la anchura preferida es mayor que la anchura máxima, se utilizará la anchura máxima. Si es menor que la anchura mínima (la unidad irrompible más pequeña), se utilizará la anchura mínima.  
  
Los valores se almacenan en caché en caso de que se necesite un diseño, pero la anchura no cambia.

### Line Breaking

Cuando un renderizador en medio de una presentación decide que necesita romperse, el renderizador se detiene y propaga al padre de la presentación que necesita romperse. El padre crea los renderizadores adicionales y llama a layout sobre ellos.

## Painting

En la fase de pintura, se recorre el árbol de renderizado y se llama al método "paint()" del renderizador para mostrar el contenido en la pantalla. La pintura utiliza el componente de infraestructura de interfaz de usuario.

### Global and Incremental

Al igual que el diseño, el pintado puede ser global (se pinta todo el árbol) o incremental. En el pintado incremental, algunos de los renderizadores cambian de forma que no afectan a todo el árbol. El renderizador modificado invalida su rectángulo en la pantalla. Esto hace que el SO lo vea como una "región sucia" y genere un evento "pintar". El SO lo hace inteligentemente y fusiona varias regiones en una. En Chrome es más complicado porque el renderizador está en un proceso diferente al proceso principal. Chrome simula el comportamiento del SO hasta cierto punto. La presentación escucha estos eventos y delega el mensaje a la raíz de renderizado. El árbol se recorre hasta que se alcanza el renderizador relevante. Este se repintará a sí mismo (y normalmente a sus hijos).

### The painting order

CSS2 define el orden del proceso de pintado. En realidad, se trata del orden en que se apilan los elementos en los contextos de apilamiento. Este orden afecta al pintado, ya que las pilas se pintan de atrás hacia delante. El orden de apilamiento de un renderizador de bloques es:

1. background color
2. background image
3. border
4. children
5. outline

### Firefox display list

Firefox repasa el árbol de renderizado y construye una lista de visualización para el rectángulo pintado. Contiene los renderizadores relevantes para el rectángulo, en el orden de pintado correcto (fondos de los renderizadores, luego bordes, etc.).

De este modo, el árbol sólo debe recorrerse una vez para un repintado, en lugar de varias veces, pintando todos los fondos, luego todas las imágenes, luego todos los bordes, etc.

Firefox optimiza el proceso al no añadir elementos que quedarán ocultos, como elementos completamente debajo de otros elementos opacos.

#### WebKit rectangle storage

Antes de volver a pintar, WebKit guarda el rectángulo antiguo como mapa de bits. A continuación, pinta sólo el delta entre los rectángulos nuevo y viejo.

### Dynamic changes

Los navegadores intentan realizar las mínimas acciones posibles en respuesta a un cambio. Así, los cambios en el color de un elemento sólo provocarán el repintado del elemento. Los cambios en la posición de un elemento provocarán el diseño y el repintado del elemento, sus hijos y posiblemente sus hermanos. La adición de un nodo DOM provocará el diseño y el repintado del nodo. Los cambios importantes, como aumentar el tamaño de la fuente del elemento "`html`", provocarán la invalidación de las cachés, el `relayout` y el `repaint` de todo el árbol.

### The rendering engine's threads

El motor de renderizado es monohilo. Casi todo, excepto las operaciones de red, ocurre en un único hilo. En Firefox y Safari es el hilo principal del navegador. En Chrome es el hilo principal del proceso de pestañas.  
  
Las operaciones de red pueden ser realizadas por varios hilos paralelos. El número de conexiones paralelas es limitado (normalmente de 2 a 6 conexiones).

### Event loop

El hilo principal del navegador es un bucle de eventos. Es un bucle infinito que mantiene vivo el proceso. Espera eventos (como eventos de diseño y pintura) y los procesa. Este es el código de Firefox para el bucle de eventos principal:

```js
while (!mExiting)
    NS_ProcessNextEvent(thread);
```
