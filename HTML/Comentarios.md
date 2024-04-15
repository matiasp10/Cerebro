Los comentarios HTML no se muestran en el navegador, pero pueden ayudar a documentar el código fuente HTML.


```html
<!-- Escribe tu comentario aqui -->
```

> [!warning] Observe
> Hay un signo de exclamación (!) en la etiqueta inicial, pero no en la final.

## Usos

### Añadir comentarios

Con los comentarios puedes colocar notificaciones y recordatorios en tu código HTML:

```html
<!-- This is a comment -->

<p>This is a paragraph.</p>

<!-- Remember to add more information here -->
```

### Ocultar contenido

Los comentarios pueden utilizarse para ocultar contenidos.  
  
Esto puede ser útil si oculta contenido temporalmente:

```html
<p>This is a paragraph.</p>

<!-- <p>This is another paragraph </p> -->

<p>This is a paragraph too.</p>
```

También puede ocultar más de una línea. Todo lo que se encuentre entre el `<!--` y el `-->` se ocultará de la pantalla.

```html
<p>This is a paragraph.</p>
<!-- 
<p>Look at this cool image:</p>
<img border="0" src="pic_trulli.jpg" alt="Trulli">
-->
<p>This is a paragraph too.</p>
```

Los comentarios también son estupendos para depurar HTML, porque puedes comentar líneas de código HTML, de una en una, para buscar errores.

### Ocultar contenido en línea

Los comentarios pueden utilizarse para ocultar partes en medio del código HTML.

```html
<p>This <!-- great text --> is a paragraph.</p>
```
