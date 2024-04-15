- [[Eventos - Introduccion]]
## Propagación

El principio de la propagacion nos dice que cuando un evento ocurre en un elemento, este ejecuta sus manejadores, luego los manejadores del padre y asi sucesivamente.

##### Ejemplo

Dado 3 elementos anidados FORM > DIV > P con un manejador cada uno de ellos.

```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form onclick="alert('form')">FORM
  <div onclick="alert('div')">DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
```

La ejecucion al hacer click en P sera:
1.  En ese `<p>`.
2.  Luego en el `<div>` de arriba.
3.  Luego en el `<form>` de más arriba.
4.  Y así sucesivamente hasta el objeto `document`.

![[Pasted image 20220802150030.png]]

Este proceso se conoce como “propagación” porque los eventos “se propagan” desde el elemento más al interior, a través de los padres, como una burbuja en el agua.

>No todos los eventos se propagan, por ejemplo el evento ==focus== no lo hace.

### event.target

El elemento anidado más profundo que causó el evento es llamado elemento objetivo, accesible como ==event.target==.

Nota la diferencia de this ( = event.currentTarget):

- **event.target** – es el elemento “objetivo” que inició el evento, no cambia a través de todo el proceso de propagación.
- **this** – es el elemento “actual”, el que tiene un manejador ejecutándose en el momento.

#### Ejemplo

si tenemos un solo manejador ==form.onclick==, este puede atrapar todos los clicks dentro del formulario. No importa dónde el clic se hizo, se propaga hasta el ``<form>`` y ejecuta el manejador.

En el manejador **form.onclick**:

- **this** (=event.currentTarget) es el elemento ``<form>``, porque el manejador se ejecutó en él.
- **event.target** es el elemento actual dentro de el formulario al que se le hizo clic.

### Detener la propagacion

Una propagación de evento empieza desde el elemento objetivo hacia arriba. Normalmente este continúa hasta ``<html>`` y luego hacia el objeto document, algunos eventos incluso alcanzan window, llamando a todos los manejadores en el camino.

Se le puede decir a un evento que ya se ah procesado y se detenga su propagacion.

Para esto se utiliza el metodo **event.stopPropagation()**.

```html
<body onclick="alert(`No se propagó hasta aquí`)">
  <button onclick="event.stopPropagation()">Haz clic</button>
</body>
```
>Si quisieramos que a diferencia del metodo stopPropagation que ejecuta el primer controlador, no se ejecute ninguno y la propagacion corte inmediatamente, **event.stopImmediatePropagation()**.

## Captura

Hay otra fase en el procesamiento de eventos llamada “captura”. Es raro usarla en código real, pero a veces puede ser útil.

En realidad existen 3 fases en el estandar de eventos del DOM:

1.  **Fase de captura** – el evento desciende al elemento.
2.  **Fase de objetivo** – el evento alcanza al elemento.
3.  **Fase de propagación** – el evento se propaga hacia arriba del elemento.

![[Pasted image 20220802154705.png]]

Se explica así: por un clic en `<td>` el evento va primero a través de la cadena de ancestros hacia el elemento (fase de captura), luego alcanza el objetivo y se desencadena ahí (fase de objetivo), y por último va hacia arriba (fase de propagación), ejecutando los manejadores en su camino.

> **Antes solo hablamos de la propagación porque la fase de captura es raramente usada. Normalmente es invisible a nosotros.**

Para atrapar un evento en la fase de captura, necesitamos preparar la opción `capture` como `true` en el manejador:

```js
elem.addEventListener(..., {capture: true})
// o, solo "true" es una forma más corta de {capture: true}
elem.addEventListener(..., true)
```

Hay dos posibles valores para la opción `capture`:

-   Si es `false` (por defecto), entonces el manejador es preparado para la fase de propagación.
-   Si es `true`, entonces el manejador es preparado para la fase de captura.

#### Ejemplo

```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form>FORM
  <div>DIV
    <p>P</p>
  </div>
</form>

<script>
  for(let elem of document.querySelectorAll('*')) {
    elem.addEventListener("click", e => alert(`Captura: ${elem.tagName}`), true);
    elem.addEventListener("click", e => alert(`Propagación: ${elem.tagName}`));
  }
</script>
```

El código prepara manejadores de clic en _cada_ elemento en el documento para ver cuáles están funcionando.

Si haces clic en `<p>`, verás que la secuencia es:

1.  `HTML` → `BODY` → `FORM` → `DIV` (fase de captura, el primer detector):
2.  `P` (fase de objetivo, se dispara dos veces, tan pronto como preparemos los dos detectores: de captura y propagación)
3.  `DIV` → `FORM` → `BODY` → `HTML` (fase de propagación, el segundo detector).

Hay un propiedad `event.eventPhase` que nos dice el número de fase en la qué el evento fue capturado. Pero es raramente usada, ya que usualmente lo sabemos en el manejador.


## Resumen

Cuando ocurre un evento, el elemento más anidado dónde ocurrió se reconoce como el “elemento objetivo” (`event.target`).

Cada manejador puede acceder a las propiedades del objeto `event`:

-   **`event.target`** – el elemento más profundo que originó el evento.
-   **`event.currentTarget` (=`this`)** – el elemento actual que maneja el evento (el que tiene al manejador en él)
-   **`event.eventPhase`** – la fase actual (captura=1, objetivo=2, propagación=3).

Cualquier manejador de evento puede detener el evento al llamar **`event.stopPropagation()`**, pero no es recomendado porque no podemos realmente asegurar que no lo necesitaremos más adelante, quizá para completar diferentes cosas.

La fase de captura raramente es usada, usualmente manejamos los eventos en propagación.