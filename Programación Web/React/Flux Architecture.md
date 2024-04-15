- [[Patrones de diseño]]

Desarrollado por Facebook para facilitar la gestion del estado.
En Flux, el estado se separa completamente de los componentes de React en sus propios _stores_(almacenes). El estado en el store no se cambia directamente, sino con diferentes _actions_(acciones).

Cuando una **acción cambia el estado** de un store, las vistas se vuelven a generar:

![[Pasted image 20221028105741.png]]

Si alguna acción en la aplicación, por ejemplo "presionar un botón", provoca la necesidad de cambiar el estado, el cambio se realiza con una acción. Esto hace que vuelva a renderizar la vista:

![[Pasted image 20221028105750.png]]

Flux ofrece una forma estándar de cómo y dónde se mantiene el estado de la aplicación y cómo se modifica.

## Actores

### Vista

La vista serían los componentes web, ya sean construidos nativamente, con Polymer, con Angular, React, etc...

### Store

La _Store_ sería **lo más parecido al modelo de la aplicación**. Guarda los datos/estado de la aplicación y en Flux puede haber varias (Luego veremos que en algunas implementaciones sólo hay un único store).

No hay métodos en la _Store_ que permitan modificar los datos en ella, eso se hace a través de _dispatchers_ y acciones.

### Action

Un acción es simplemente un **objeto JavaScript que indica una intención de realizar algo** y que lleva datos asociados si es necesario. Por ejemplo si tenemos una aplicación tipo _Carrito de la compra_, y añadimos un item al carrito, la acción que representaría esto sería:

```javascript
{
    type: 'ADD_ITEM',
    item: item
}
```

### Dispatcher

Las acciones como la anterior son enviadas a un _dispatcher_ que se encarga de _dispararla_ o propagarla hasta la Store.

La vista es la que se encarga de enviar las acciones al _dispatcher_.

Un _dispatcher_ no es más que un **mediador entre la _Store_ o _Stores_ y las acciones**. Sirve para desacoplar la Store de la vista, ya que así no es necesario conocer que Store maneja una acción concreta.

En Resumen, el patrón **FLUX** sigue el siguiente recorrido:

- La **vista**, mediante un evento envía una acción con la intención de realizar un cambio en el estado.
- La **acción** contiene el tipo y los datos (si los hubiere) y es enviada al dispatcher.
- El **dispatcher** propaga la acción al Store y se procesa en orden de llegada.
- El **Store** recibe la acción y dependiendo del tipo recibido, actualiza el estado y notifica a las vistas de ese cambio.
- La **vista** recibe la notificación y se actualiza con los cambios.

Todo en un único sentido.

## Librerias

- [Redux](https://redux.js.org/)

