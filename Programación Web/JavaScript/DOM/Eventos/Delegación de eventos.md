- [[Eventos - Introduccion]]

La delegacion de eventos es un patron de manejo de eventos, donde si tenemos muchos eventos manejados de manera similar, podemos en vez de asignar un controlador para cada evento, ponemos un unico manejador a su ancestro comun.

**El algoritmo**:

1.  Pone un único manejador en el contenedor.
2.  Dentro del manejador revisa el elemento de origen `event.target`.
3.  Si el evento ocurrió dentro de un elemento que nos interesa, maneja el evento.

### Ejemplo

Este es nuestro html:

```html
<table>
  <tr>
    <th colspan="3"><em>Bagua</em> Chart: Direction, Element, Color, Meaning</th>
  </tr>
  <tr>
    <td class="nw"><strong>Northwest</strong><br>Metal<br>Silver<br>Elders</td>
    <td class="n">...</td>
    <td class="ne">...</td>
  </tr>
  <tr>...2 more lines of this kind...</tr>
  <tr>...2 more lines of this kind...</tr>
</table>
```

![[Pasted image 20220802163725.png]]

En lugar de asignar un manejador `onclick` a cada `<td>` (puede haber muchos), configuramos un manejador “atrapa-todo” en el elemento `<table>`.

```js
let selectedTd;

table.onclick = function(event) {
  let target = event.target; // ¿dónde fue el clic?

  if (target.tagName != 'TD') return; // ¿no es un TD? No nos interesa

  highlight(target); // destacarlo
};

function highlight(td) {
  if (selectedTd) { // quitar cualquier celda destacada que hubiera antes
    selectedTd.classList.remove('highlight');
  }
  selectedTd = td;
  selectedTd.classList.add('highlight'); // y destacar el nuevo td
}
```

Pero hay un inconveniente.

El clic puede ocurrir no sobre `<td>`, sino dentro de él.

Entonces hay que verificar si el elemento es un td o no.