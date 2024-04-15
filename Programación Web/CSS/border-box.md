La propiedad CSS **box-sizing** establece cómo se calcula la anchura y altura total de un elemento.

Por defecto, en el modelo de caja CSS, el `width` y el `height` que asignas a un elemento se aplican sólo a la caja de contenido del elemento. Si el elemento tiene algún borde o relleno, esto se añade a la anchura y altura para llegar al tamaño de la caja que se muestra en la pantalla. Esto significa que, al establecer la anchura y la altura, tienes que ajustar el valor que das para tener en cuenta cualquier borde o relleno que se pueda añadir. Por ejemplo, si tienes cuatro cajas con anchura: 25%, si alguna tiene relleno izquierdo o derecho o un borde izquierdo o derecho, por defecto no cabrán en una línea dentro de las restricciones del contenedor padre.

La propiedad box-sizing puede utilizarse para ajustar este comportamiento:

### context-box

Ofrece el comportamiento predeterminado de CSS para el tamaño de las cajas. Si estableces la anchura de un elemento en 100 píxeles, la caja de contenido del elemento tendrá una anchura de 100 píxeles, y la anchura de cualquier borde o relleno se añadirá a la anchura final renderizada, haciendo que el elemento sea más ancho que 100px.

### border-box

Indica al navegador que tenga en cuenta los bordes y el relleno en los valores que especifiques para la anchura y la altura de un elemento. Si estableces la anchura de un elemento en 100 píxeles, esos 100 píxeles incluirán cualquier borde o relleno que hayas añadido, y la caja de contenido se encogerá para absorber esa anchura extra. Esto suele facilitar mucho el tamaño de los elementos. box-sizing: border-box es el estilo por defecto que los navegadores utilizan para los elementos `<table>`, `<select>` y `<button>`, y para los elementos `<input>` cuyo tipo es `radio`, `checkbox`, `reset`, `button`, `submit`, `color` o `search`.

> [!note] Nota
> A menudo es útil establecer el tamaño de la caja en border-box para disponer los elementos. Esto hace que el manejo de los tamaños de los elementos sea mucho más fácil y, en general, elimina una serie de trampas con las que se puede tropezar al maquetar el contenido. Por otra parte, cuando se utiliza position: relative o position: absolute, el uso de box-sizing: content-box permite que los valores de posicionamiento sean relativos al contenido, e independientes de los cambios en los tamaños de borde y relleno, lo que a veces es deseable.

## Sintaxis

```css
box-sizing: border-box;
box-sizing: content-box;

/* Global values */
box-sizing: inherit;
box-sizing: initial;
box-sizing: revert;
box-sizing: revert-layer;
box-sizing: unset;
```
