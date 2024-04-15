No todos los elementos siguen el patrón de una etiqueta de apertura, un contenido y una etiqueta de cierre. Algunos elementos constan de una sola etiqueta, que se utiliza normalmente para insertar/incorporar algo en el documento. Estos elementos se denominan _elementos vacíos_. Por ejemplo, el elemento `<img>` inserta un archivo de imagen en una página:

```html
<img src="https://raw.githubusercontent.com/mdn/beginner-html-site/gh-pages/images/firefox-icon.png" alt="Firefox icon" />
```

![[Pasted image 20230717163503.png|center|300]]

> [!note] Nota
> En HTML, no es necesario añadir un */* al final de la etiqueta de un elemento vacío, por ejemplo `<img src="images/cat.jpg" alt="cat" />`. Sin embargo, también es una sintaxis válida, y puedes hacerlo cuando quieras que tu HTML sea XML válido.

## Características 

Un elemento vacío es un elemento HTML que **no puede tener ningún nodo hijo** (es decir, elementos anidados o nodos de texto). Los elementos vacíos sólo tienen una etiqueta de inicio; las etiquetas de fin no deben especificarse para los elementos vacíos.  
  
En HTML, un elemento *void* no debe tener etiqueta de fin. Por ejemplo, `<input type="text"></input>` **no es HTML válido**. En cambio, los elementos *SVG* o *MathML* que no pueden tener ningún nodo hijo pueden utilizar una etiqueta de fin en lugar de la sintaxis de *autocierre XML* en su etiqueta de inicio.  
  
Las especificaciones *HTML*, *SVG* y *MathML* definen de forma muy precisa lo que puede contener cada elemento. Por tanto, algunas combinaciones de etiquetas carecen de significado semántico.  
  
Aunque no hay forma de marcar un elemento vacío como si tuviera hijos, se pueden añadir nodos hijos mediante programación al elemento en el DOM utilizando JavaScript. Pero no es una buena práctica, ya que el resultado no será fiable.

## Elementos vacíos

- [[area]]
- [[base]]
- [[br]]
- [[col]]
- [[embed]]
- [[hr]]
- [[img]]
- [[input]]
- [[HTML/Elementos/link|link]]
- [[meta]]
- [[param]] 🗑️
- [[source]]
- [[track]]
- [[wbr]]