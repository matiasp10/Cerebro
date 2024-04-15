- [[Eventos - Introduccion]]

Muchos eventos conducen **automáticamente** a determinadas acciones realizadas por el navegador.

Por ejemplo:

- Un clic en un enlace: inicia la navegación a su URL.
- Un clic en el botón de envío de un formulario inicia su envío al servidor.
- Al presionar un botón del ratón sobre un texto y moverlo, se selecciona el texto.

### Evitar acciones del navegador

Hay dos formas de decirle al navegador que no queremos que actúe:

-   La forma principal es utilizar el objeto `event`. Hay un método **`event.preventDefault()`**.
-   Si el controlador se asigna usando `on<event>` (no por `addEventListener`), entonces devolver `false` también funciona igual.

```html
<a href="/" onclick="return false">Haz clic aquí</a>

<a href="/" onclick="event.preventDefault()">aquí</a>
```

### Controlador pasivo

La opción opcional **passive**: **true** de addEventListener indica al navegador que el controlador ==no== llamará a preventDefault().

Hay algunos eventos como ==touchmove== en dispositivos móviles (cuando el usuario mueve el dedo por la pantalla), que provocan el desplazamiento por defecto, pero ese desplazamiento se puede evitar usando **preventDefault()** en el controlador.

> Técnicamente, al evitar acciones predeterminadas y agregar JavaScript, podemos personalizar el comportamiento de cualquier elemento. Por ejemplo, podemos hacer que un enlace `<a>` funcione como un botón, y un botón `<button>` se comporte como un enlace (redirigir a otra URL o algo así). 
> Pero en general deberíamos mantener el significado semántico de los elementos HTML. Por ejemplo, la navegación debe realizarla `<a>`, no un botón.

