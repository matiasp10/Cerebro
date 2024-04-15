- [[Eventos - Introduccion]]

Para reaccionar a los eventos necesitaremos de un **handler** o **controlador**, el cual es una **función** que se ejecuta en caso de un evento.
### Asignar un handler a un evento
##### HTML

Puede establecerse un handler directamente en el HTML con la propiedad `on<event>`

``` html
<input value="Click me" onclick="alert('Click!')" type="button">
```

Cuando se hace click en el input se ejecuta el codigo dentro del "onClick".

Escribir mucho codigo en la etiqueta HTML no es muy conveniente por lo cual es mejor crear una funcion y pasarla.

```html
<script> 
function countRabbits() { 
	for(let i=1; i<=3; i++) { 
		alert("Conejo número " + i); 
	} 
} 
</script> 
<input type="button" _onclick__="countRabbits()"_ value="¡Cuenta los conejos!">`
```
##### Propiedad del DOM

Podemos asignar un handler usando una propiedad del DOM ``on<event>``.

```html
<input id="elem" type="button" value="Haz click en mí"> 
<script> 
elem.onclick = function() { 
	alert('¡Gracias!'); 
};
</script>
```

Para eliminar un handler, asigna `elem.onclick = null`.
### Valor de This de un handler

El valor de this de un handler es el elemento el cual tiene el handler dentro.

```html
<button onclick="alert(this.innerHTML)">Haz click en mí</button>
```

Este alert mostrara el mensaje "Haz click en mi".
### Asignar múltiples handlers a un elemento

Para poder agregar multiples handlers se utilizan los metodos **addEventListener** y **removeEventListener**.

```js
element.addEventListener(event, handler, [options]);
```

- **event**: nombre del evento por ejemplo "click".
- **handler**: la funcion controladora.
- **options**: objeto opcional con propiedades.
	- **once**: si es true entonces el listener se remueve automáticamente después de activarlo.
	- **capture**: la fase en la que se controla el evento. Por razones históricas, options también puede ser false/true, lo que es igual a {capture: false/true}.
	- **passive**: si es true entonces el handler no llamará a preventDefault(), esto lo explicaremos más adelante en Acciones predeterminadas del navegador.

```js
element.removeEventListener(event, handler, [options]);
```
Un ejemplo de multiples handlers seria:

```html
<input id="elem" type="button" value="Haz click en mí"/>

<script>
  function handler1() {
    alert('¡Gracias!');
  };

  function handler2() {
    alert('¡Gracias de nuevo!');
  }

  elem.onclick = () => alert("Hola");
  elem.addEventListener("click", handler1); // Gracias!
  elem.addEventListener("click", handler2); // Gracias de nuevo!
</script>
```
### Objeto del evento

Cuando un evento ocurre, el navegador crea un objeto del evento que coloca los detalles dentro y los pasa como un argumento al handler.

```html
<input type="button" value="¡Haz click en mí!" id="elem">

<script>
  elem.onclick = function(event) {
    // muestra el tipo de evento, el elemento y las coordenadas del click
    alert(event.type + " en el " + event.currentTarget);
    alert("Coordenadas: " + event.clientX + ":" + event.clientY);
  };
</script>
```
En este ejemplo obtenemos las coordenadas del cursos a partir del objeto del evento.
###### Algunas propiedades del objeto event:

- **event.type**: Tipo de evento, en este caso fue "click".
- **event.currentTarget**: Elemento que maneja el evento. Lo que exactamente igual a this, a menos que el handler sea una función de flecha o su this esté vinculado a otra cosa, entonces podemos obtener el elemento desde event.currentTarget.
- **event.clientX** / **event.clientY**: Coordenadas del cursor relativas a la ventana, para eventos de cursor.

Hay más propiedades. La mayoría dependen del **tipo de evento**: los eventos del teclado tienen algunas propiedades establecidas, las de cursor otras.
### Objeto del handler

Podemos asignar no solo una función, sino un **objeto** como handler del evento usando addEventListener. Cuando el evento ocurre, el método handleEvent es llamado.

```html
<button id="elem">Haz click en mí</button>

<script>
  let obj = {
    handleEvent(event) {
      alert(event.type + " en " + event.currentTarget);
    }
  };

  elem.addEventListener('click', obj);
</script>
```

Como podemos ver, cuando addEventListener recibe como handler a un objeto, llama a obj.handleEvent(event) en caso de un evento.
Tambien podria usarse una clase para esto.
