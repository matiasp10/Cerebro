El objeto **`console`** provee acceso a la consola de depuración de los navegadores. Los detalles de como funciona varían de navegador en navegador, pero hay un conjunto de características que _de facto_ son proporcionadas generalmente.

El objeto `console` puede ser accedido desde cualquier objeto global. `Window` en el ámbito de navegación y `WorkerGlobalScope` como variantes específicas de `workers` a través de la propiedad `console`. Está expuesto como `Window.console`, y puede ser referenciado como `console`. Por ejemplo:

```js
console.log("Falló al abrir el enlace especificado");
```
## Métodos 
### console.assert()

Registra un mensaje y envía una traza de error a la consola si el primer argumento es false.
### console.clear()

Limpia la consola.
### console.count()

Registra el número de veces que esta línea ha sido llamada con la etiqueta dada.
### console.countReset()

Reinicia el valor del contador para la etiqueta dada.
### console.debug()

Registra un mensaje con el nivel de debug.
### console.dir()

Muestra un listado interactivo de las propiedades de un objeto JavaScript específico. Este listado permite usar triángulos de lista desplegables para examinar el contenido de objetos hijo.
### console.dirxml()

Muestra una representación en forma de árbol de un elemento XML/HTML si es posible o la vista del objeto JavaScript si no es posible.
### console.error()

Muestra un mensaje de error. Se pueden utilizar sustituciones de cadenas y argumentos adicionales con este método.
### console.exception()

Un alias para error().
### console.group()

Crea un nuevo grupo, indentando todos los mensajes subsecuentes en un nuevo nivel. Para retroceder un nivel, se utiliza groupEnd().
### console.groupCollapsed()

Crea un nuevo grupo, indentando todos los mensajes subsecuentes en un nuevo nivel. A diferencia de group(), inicia con la línea de grupo colapsada, requiriendo el uso de un botón de apertura para expandir el grupo. Para retroceder un nivel, se utiliza groupEnd().
### console.groupEnd()

Finaliza el grupo actual.
### console.info()

Muestra un mensaje de información en la consola. Puedes usar sustituciones de cadenas y argumentos adicionales con este método.
### console.log()

Para salida general de la información registrada. Puedes usar sustituciones de cadenas y argumentos adicionales con este método.
### console.profile()

Inicia el profiler incluído del navegador (por ejemplo, la Firefox performance tool). Puedes especificar un nombre opcional para el perfil.
### console.profileEnd()

Detiene el profiler. Puedes ver el resultado en la herramienta de rendimiento del navegador (por ejemplo, la Firefox performance tool).
### console.table()

Muestra datos tabulares en forma de tabla.
### console.time()

Inicia un temporizador con un nombre especificado como parámetro. Hasta 10 000 temporizadores simultáneos pueden ejecutarse en una página determinada.
### console.timeEnd()

Detiene el temporizador especificado y registra el tiempo transcurrido en milisegundos desde que fue iniciado.
### console.timeLog()

Muestra el valor del temporizador especificado en la consola.
### console.timeStamp()

Agrega un marcador a las herramientas del navegador Chrome o Firefox.
### console.trace()

Muestra una traza de pila.
### console.warn()

Muestra un mensaje de advertencia. Puedes usar sustituciones de cadenas y argumentos adicionales con este método.