El elemento HTML `<p>` representa un párrafo. Los párrafos suelen representarse en los medios visuales como bloques de texto separados de los bloques adyacentes por líneas en blanco y/o sangría de primera línea, pero los párrafos HTML pueden ser cualquier agrupación estructural de contenido relacionado, como imágenes o campos de formulario.

Los párrafos son [[Elementos en bloque]] y, en particular, se cerrarán automáticamente si se analiza otro elemento de nivel de bloque antes de la etiqueta `</p>` de cierre.

### Contenidos permitidos

Contenido de frase.

### Omisión de etiquetas

La etiqueta de inicio es obligatoria. La etiqueta final puede omitirse si el elemento `<p>` va inmediatamente seguido de un elemento [[address]], [[article]], [[aside]], [[blockquote]], [[div]], [[dl]], [[fieldset]], [[footer]], [[form]], [[h1-h6]], [[header]], [[hr]], [[menu]], [[nav]], [[ol]], [[pre]], [[section]], [[table]], [[ul]] o otro elemento [[p]], o si no hay más contenido en el elemento padre y el elemento padre no es un elemento `<a>`.

### Padres autorizados

Cualquier elemento que acepte contenido de flujo.

### Función ARIA implícita

párrafo

### Roles ARIA permitidos

Cualquiera

### DOM interface

[[HTMLParagraphElement]]

## Accesibilidad 

Dividir el contenido en párrafos ayuda a que una página sea más accesible. Los lectores de pantalla y otras tecnologías de apoyo ofrecen atajos que permiten a los usuarios saltar al párrafo siguiente o al anterior, de modo que pueden hojear el contenido como el espacio en blanco permite a los usuarios visuales.

Utilizar elementos `<p>` vacíos para añadir espacio entre párrafos es problemático para las personas que navegan con tecnología de lectura de pantalla. Los lectores de pantalla pueden anunciar la presencia del párrafo, pero no su contenido, porque no lo hay. Esto puede confundir y frustrar a la persona que utiliza el lector de pantalla.

Si desea más espacio, utilice propiedades CSS como el margen para crear el efecto:

```css
p {
  margin-bottom: 2em; /* increase white space after a paragraph */
}
```