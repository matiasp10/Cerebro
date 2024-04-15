- [[Eventos - Introduccion]]

No solo podemos asignar controladores, sino también generar eventos desde JavaScript.

## Constructor de eventos

Las clases de eventos integradas forman una jerarquía, similar a las clases de elementos DOM. La raíz es la clase incorporada [Event](http://www.w3.org/TR/dom/#event).

```js
let event = new Event(type[, options]);
```

- **type** – tipo de event, un string como "click" o nuestro propio evento como "mi-evento".

- **options** – el objeto con 2 propiedades opcionales:
	- **bubbles**: true/false – si es true, entonces el evento se propaga.
	- **cancelable**: true/false – si es true, entonces la “acción predeterminada” puede ser prevenida. Más adelante veremos qué significa para los eventos personalizados.

Por defecto, **los dos son false**: {bubbles: false, cancelable: false}.

### dispatchEvent

Después de que se crea un objeto de evento, debemos **“ejecutarlo”** en un elemento usando la llamada **elem.dispatchEvent(event)**.

Luego, los controladores reaccionan como si fuera un evento normal del navegador. Si el evento fue creado con la bandera bubbles, entonces se propaga.

### Crear eventos especificos

Hay eventos especificos de la UI que tienen su propio constructor, este nos permite especificar propiedades estandar para el tipo de evento.

```js
let event = new MouseEvent("click", {
  bubbles: true,
  cancelable: true,
  clientX: 100,
  clientY: 100
});

alert(event.clientX); // 100
```

### Eventos personalizados

Para nuestros tipos de eventos completamente nuevos, como "hello", deberíamos usar **new** **CustomEvent**. Técnicamente, CustomEvent es lo mismo que Event, con una excepción.

En el segundo argumento (objeto) podemos agregar una propiedad adicional **detail** para cualquier información personalizada que queramos pasar con el evento.

### Los eventos dentro de eventos son sincronicos

Usualmente los eventos se procesan en una cola. Por ejemplo: si el navegador está procesando `onclick` y ocurre un nuevo evento porque el mouse se movió, entonces el manejo de este último se pone en cola, y el controlador correspondiente `mousemove` será llamado cuando el procesamiento de `onclick` haya terminado.