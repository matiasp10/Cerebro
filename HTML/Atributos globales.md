## itemid

El identificador único y global de un artículo.

## itemprop

Se usa para agregar propiedades a un elemento. Se puede especificar a cada elemento HTML un atributo `itemprop`, donde un `itemprop` consiste en un par de nombre y valor.

## itemref

Las propiedades que no son descendientes de un elemento con el atributo `itemscope` se pueden asociar con el elemento usando un `itemref`. Proporciona una lista de IDs de elementos (no `itemid`s) con propiedades adicionales en otras partes del documento.

## itemscope

`itemscope` (normalmente) funciona junto con [`itemtype`](https://developer.mozilla.org/es/docs/Web/HTML/Global_attributes#itemtype) para especificar que el HTML contenido en un bloque es sobre un elemento en particular. `itemscope` crea el «_Item_» y define el alcance del `itemtype` asociado con él. `itemtype` es una URL válida de un vocabulario (tal como [schema.org](https://schema.org/)) que describe el elemento y las propiedades de su contexto.

## itemtype

Especifica la URL del vocabulario que se utilizará para definir `itemprop`s (propiedades del elemento) en la estructura de datos. [`itemscope`](https://developer.mozilla.org/es/docs/Web/HTML/Global_attributes#itemscope) se utiliza para establecer el alcance de la estructura de datos en la que estará activo el vocabulario establecido por `itemtype`.

## lang

Ayuda a definir el idioma de un elemento: el idioma en el que se encuentran los elementos no editables o el idioma en el que el usuario debe escribir los elementos editables. El atributo contiene una “etiqueta de idioma” (compuesta de “subetiquetas de idioma” separadas por guiones) en el formato definido en [_Etiquetas para identificar idiomas (BCP47)_](https://www.ietf.org/rfc/bcp/bcp47.txt). [xml:lang](https://developer.mozilla.org/es/docs/Web/HTML/Global_attributes#attr-xml:lang) tiene prioridad sobre él.

## part

Una lista separada por espacios de los nombres de las partes del elemento. Los nombres de las partes permiten que CSS seleccione y aplique estilo a elementos específicos en la sombra de un árbol mediante el pseudoelemento [`::part` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/::part "Currently only available in English (US)").

## slot

Asigna un espacio en la sombra de un árbol [DOM de sombra (en-US)](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM "Currently only available in English (US)") a un elemento: Un elemento con un atributo `slot` es asignado al espacio creado por el elemento [`<slot>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/slot) cuyo valor del atributo [`name`](https://developer.mozilla.org/es/docs/Web/HTML/Element/slot#attr-name) coincide con el valor del atributo `slot`.

## spellcheck

Un atributo enumerado define si se puede verificar el elemento para detectar errores ortográficos. Puede tener los siguientes valores:

-   `true`, el cual indica que, si es posible, el elemento se debe revisar para detectar errores ortográficos;
-   `false`, indica que el elemento **no** se debe revisar para detectar errores ortográficos.

## style

Contiene declaraciones de estilo [CSS](https://developer.mozilla.org/es/docs/Web/CSS) que se aplicarán al elemento. Ten en cuenta que se recomienda que los estilos se definan en un archivo o archivos separados. Este atributo y el elemento [`<style>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/style) principalmente tienen el propósito de permitir un estilo rápido, por ejemplo, con fines de prueba.

## tabindex

Un atributo entero que indica si el elemento puede tomar el foco de entrada (es _enfocable_), si debe participar en la navegación secuencial del teclado y, de ser así, en qué posición. Puede tomar varios valores:

-   un _valor negativo_ significa que el elemento se debe poder enfocar, pero no debe ser accesible mediante la navegación secuencial del teclado;
-   `0` significa que el elemento se debe poder enfocar y ser accesible a través de la navegación secuencial del teclado, pero su orden relativo está definido por la convención de la plataforma;
-   un _valor positivo_ significa que el elemento se debe poder enfocar y ser accesible mediante la navegación secuencial del teclado; el orden en el que se enfocan los elementos es el valor creciente del [tabindex](https://developer.mozilla.org/es/docs/Web/HTML/Global_attributes#attr-tabindex). Si varios elementos comparten el mismo `tabindex`, su orden relativo sigue sus posiciones relativas en el documento.

## title

Contiene un texto que representa información de advertencia relacionada con el elemento al que pertenece. Normalmente, pero no necesariamente, dicha información se puede presentar al usuario como información sobre herramientas.

## translate

Un atributo enumerado que se utiliza para especificar si los valores de atributo de un elemento y los valores de sus hijos de nodo [`Text` (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/Text "Currently only available in English (US)") se deben traducir cuando la página está localizada, o si se deben dejar sin cambios. Puede tener los siguientes valores:

-   la cadena vacía y `yes`, indican que el elemento se traducirá.
-   `no`, lo cual indica que el elemento **no** se traducirá.