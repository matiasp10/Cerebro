React te permite añadir _controladores de eventos_ a tu JSX. Los controladores de eventos son tus propias funciones que se ejecutarán en respuesta a interacciones como hacer clic, _hover_, enfocar _inputs_ en formularios, entre otras.
___
## Añadiendo controladores de eventos

Para agregar un controlador de evento, primero definirás una función y luego [la pasarás como una prop](https://es.react.dev/learn/passing-props-to-a-component) a la etiqueta JSX apropiada. Por ejemplo, este es un botón que no hace nada todavía:

```jsx file:App.js
export default function Button() {
  return (
    <button>
      No hago nada
    </button>
  );
}
```

Puedes hacer que muestre un mensaje cuando un usuario haga clic siguiendo estos tres pasos:

1. Declara una función llamada `handleClick` _dentro_ de tu componente `Button`.
2. Implementa la lógica dentro de esa función (utiliza `alert` para mostrar el mensaje).
3. Agrega `onClick={handleClick}` al JSX del `<button>`.

```jsx file:App.js
export default function Button() {
  function handleClick() {
    alert('¡Me hiciste clic!');
  }

  return (
    <button onClick={handleClick}>
      Hazme clic
    </button>
  );
}
```

Definiste la función `handleClick` y luego [la pasaste como una prop](https://es.react.dev/learn/passing-props-to-a-component) al `<button>`. `handleClick` es un **controlador de evento.** Las funciones controladoras de evento:

- Usualmente están definidas _dentro_ de tus componentes.
- Tienen nombres que empiezan con `handle`, seguido del nombre del evento.

Por convención, es común llamar a los controladores de eventos como `handle` seguido del nombre del evento. A menudo verás `onClick={handleClick}`, `onMouseEnter={handleMouseEnter}`, etcétera.

Por otro lado, puedes definir un controlador de evento en línea en el JSX:

```jsx
<button onClick={function handleClick() {
  alert('¡Me hiciste clic!');
}}>
```

O, de manera más corta, usando una función flecha:

```jsx
<button onClick={() => {
  alert('¡Me hiciste clic!');
}}>
```

Todos estos estilos son equivalentes. Los controladores de eventos en línea son convenientes para funciones cortas.

> [!warning] Atención
> Las funciones que se pasan a los controladores de eventos deben ser pasadas, no llamadas. Por ejemplo:
> 
> | pasar una función (correcto)     | llamar una función (incorrecto) |
| -------------------------------- | ------------------------------- |
| `<button onClick={handleClick}>` | `<button onClick={handleClick()}>` |
> 
> La diferencia es sutil. En el primer ejemplo, la función `handleClick` es pasada como un controlador de evento `onClick`. Esto le dice a React que lo recuerde y solo llama la función cuando el usuario hace clic en el botón.
> 
> En el segundo ejemplo, los `()` al final del `handleClick()` ejecutan la función _inmediatamente_ mientras se [renderiza](https://es.react.dev/learn/render-and-commit), sin ningún clic. Esto es porque el JavaScript dentro de [`{` y `}` en JSX](https://es.react.dev/learn/javascript-in-jsx-with-curly-braces) se ejecuta de inmediato.
> 
> Cuando escribes código en línea, la misma trampa se presenta de otra manera:
> 
| pasar una función (correcto)            | llamar una función (incorrecto)   |
| --------------------------------------- | --------------------------------- |
| `<button onClick={() => alert('...')}>` | `<button onClick={alert('...')}>` |
> Pasar código en línea así no lo ejecutará al hacer clic; lo ejecutará cada vez que el componente se renderice:
> 

```jsx
// Esta alerta se ejecuta cuando el componente se renderiza, no cuando ¡hiciste clic!
<button onClick={alert('¡Me hiciste clic!')}>
```

> [!warning] Atención 
> Si quieres definir un controlador de evento en línea, envuélvelo en una función anónima de esta forma:

```jsx
<button onClick={() => alert('¡Me hiciste clic!')}>
```

> [!warning] Atención
> En lugar de ejecutar el código que está dentro cada vez que se renderiza, esto crea una función para que se llame más tarde.
> 
> En ambos casos, lo que quieres pasar es una función:
> 
> - `<button onClick={handleClick}>` pasa la función `handleClick`.
> - `<button onClick={() => alert('...')}>` pasa la función `() => alert('...')`.
### Leyendo las props en controladores de eventos

Como los controladores de eventos son declarados dentro de un componente, tienen acceso a las props del componente. Este es un botón que, cuando se hace clic, muestra una alerta con su prop `message`:

```jsx file:App.js
function AlertButton({ message, children }) {
  return (
    <button onClick={() => alert(message)}>
      {children}
    </button>
  );
}

export default function Toolbar() {
  return (
    <div>
      <AlertButton message="¡Reproduciendo!">
        Reproducir película
      </AlertButton>
      <AlertButton message="¡Subiendo!">
        Subir imagen
      </AlertButton>
    </div>
  );
}
```

Esto le permite a estos dos botones mostrar diferentes mensajes. Intenta cambiar los mensajes que se les pasan.
### Pasar controladores de eventos como props 

A menudo querrás que el componente padre especifique un controlador de evento de un componente hijo. Considera unos botones: dependiendo de dónde estás usando un componente `Button`, es posible que quieras ejecutar una función diferente, tal vez una reproduzca una película y otra cargue una imagen.

Para hacer esto, pasa una prop que el componente recibe de su padre como el controlador de evento así:

```jsx file:App.js
function Button({ onClick, children }) {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  );
}

function PlayButton({ movieName }) {
  function handlePlayClick() {
    alert(`¡Reproduciendo ${movieName}!`);
  }

  return (
    <Button onClick={handlePlayClick}>
      Reproducir "{movieName}"
    </Button>
  );
}

function UploadButton() {
  return (
    <Button onClick={() => alert('¡Subiendo!')}>
      Subir imagen
    </Button>
  );
}

export default function Toolbar() {
  return (
    <div>
      <PlayButton movieName="Kiki: Entregas a domicilio" />
      <UploadButton />
    </div>
  );
}
```

Aquí, el componente `Toolbar` renderiza un `PlayButton` y un `UploadButton`:

- `PlayButton` pasa `handlePlayClick` como la prop `onClick` al `Button` que está dentro.
- `UploadButton` pasa `() => alert('Uploading!')` como la prop `onClick` al `Button` que está dentro.

Finalmente, tu componente `Button` acepta una prop llamada `onClick`. Pasa esa prop directamente al `<button>` integrado en el navegador con `onClick={onClick}`. Esto le dice a React que llame la función pasada cuando reciba un clic.

Si usas un [sistema de diseño](https://uxdesign.cc/everything-you-need-to-know-about-design-systems-54b109851969), es común para componentes como los botones que contengan estilos pero no especifiquen un comportamiento. En cambio, componentes como `PlayButton` y `UploadButton` pasarán los controladores de eventos.

### Nombrar props de controladores de eventos

Componentes integrados como `<button>` y `<div>` solo admiten [nombres de eventos del navegador](https://es.react.dev/reference/react-dom/components/common#common-props) como `onClick`. Sin embargo, cuando estás creando tus propios componentes, puedes nombrar sus props de controlador de evento como quieras.

Por convención, las props de controladores de eventos deberían empezar con `on`, seguido de una letra mayúscula.

Por ejemplo, la propiedad `onClick` del componente `Button` pudo haberse llamado `onSmash`:

```jsx file:App.js
function Button({ onSmash, children }) {
  return (
    <button onClick={onSmash}>
      {children}
    </button>
  );
}

export default function App() {
  return (
    <div>
      <Button onSmash={() => alert('¡Reproduciendo!')}>
        Reproducir película
      </Button>
      <Button onSmash={() => alert('¡Subiendo!')}>
        Subir imagen
      </Button>
    </div>
  );
}
```

En este ejemplo, `<button onClick={onSmash}>` muestra que el `<button>` (minúsculas) del navegador todavía necesita una prop llamada `onClick`, ¡pero el nombre de la prop recibida por tu componente `Button` personalizado depende de ti!

Cuando tu componente admite múltiples interacciones, podrías nombrar las props de controladores de eventos para conceptos específicos de la aplicación. Por ejemplo, este componente `Toolbar` recibe los controladores de eventos de `onPlayMovie` y `onUploadImage`:

```jsx file:App.js
export default function App() {
  return (
    <Toolbar
      onPlayMovie={() => alert('¡Reproduciendo!')}
      onUploadImage={() => alert('¡Subiendo!')}
    />
  );
}

function Toolbar({ onPlayMovie, onUploadImage }) {
  return (
    <div>
      <Button onClick={onPlayMovie}>
        Reproducir película
      </Button>
      <Button onClick={onUploadImage}>
        Subir imagen
      </Button>
    </div>
  );
}

function Button({ onClick, children }) {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  );
}
```

Fíjate como el componente `App` no necesita saber _qué_ hará `Toolbar` con `onPlayMovie` o `onUploadImage`. Eso es un detalle de implementación del `Toolbar`. Aquí, `Toolbar` los pasa como controladores `onClick` en sus `Button`s, pero podría luego iniciarlos con un atajo de teclado. Nombrar props a partir de interacciones específicas de la aplicación como `onPlayMovie` te da la flexibilidad de cambiar cómo se usan más tarde.

> [!note] Nota
> Asegúrate de usar las etiquetas HTML apropiadas para tus controladores de eventos. Por ejemplo, para controlar clics, utiliza [`<button onClick={handleClick}>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/button) en lugar de `<div onClick={handleClick}>`. Al utilizar un botón (`<button>`) real del navegador se habilitan comportamientos integrados del navegador como la navegación por teclado. Si no te gustan los estilos predeterminados del navegador de un botón y quieres que se parezca más a un enlace u otro elemento diferente de UI, puedes lograrlo con CSS.
## Propagación de eventos

Los controladores de eventos también atraparán eventos de cualquier componente hijo que tu componente pueda tener. Decimos que un evento «se expande» o «se propaga» hacia arriba en el árbol de componentes cuando: empieza donde el evento sucedió, y luego sube en el árbol.

Este `<div>` contiene dos botones. Tanto el `<div>` _como_ cada botón tienen sus propios controladores `onClick`. ¿Qué controlador crees que se activará cuando hagas clic en un botón?

```jsx file:App.js
export default function Toolbar() {
  return (
    <div className="Toolbar" onClick={() => {
      alert('¡Hiciste clic en la barra de herramientas!');
    }}>
      <button onClick={() => alert('¡Reproduciendo!')}>
        Reproducir película
      </button>
      <button onClick={() => alert('¡Subiendo!')}>
        Subir imagen
      </button>
    </div>
  );
}
```

Si haces clic en cualquiera de los botones, su `onClick` se ejecutará primero, seguido por el `onClick` del `<div>`. Así que dos mensajes aparecerán. Si haces clic en el propio toolbar, solo el `onClick` del `<div>` padre se ejecutará.

> [!warning] Atención
> Todos los eventos se propagan en React excepto `onScroll`, el cual solo funciona en la etiqueta JSX a la que lo agregues. 
### Detener la propagación

Los controladores de eventos reciben un **objeto del evento** como su único parámetro. Por convención, normalmente es llamado `e`, que quiere decir «evento». Puedes usar este objeto para leer información del evento.

Ese objeto del evento también te permite detener la propagación. Si quieres evitar que un evento llegue a los componentes padre, necesitas llamar `e.stopPropagation()` como este componente `Button` lo hace:

```jsx file:App.js
function Button({ onClick, children }) {
  return (
    <button onClick={e => {
      e.stopPropagation();
      onClick();
    }}>
      {children}
    </button>
  );
}

export default function Toolbar() {
  return (
    <div className="Toolbar" onClick={() => {
      alert('¡Hiciste clic en la barra de herramientas!');
    }}>
      <Button onClick={() => alert('¡Reproduciendo!')}>
        Reproducir película
      </Button>
      <Button onClick={() => alert('¡Subiendo!')}>
        Subir imagen
      </Button>
    </div>
  );
}
```

Cuando haces clic en un botón:

1. React llama al controlador `onClick` pasado al `<button>`.
2. Ese controlador, definido en `Button`, hace lo siguiente:
    - Llama `e.stopPropagation()`, que evita que el evento se expanda aún más.
    - Llama a la función `onClick`, la cual es una prop pasada desde el componente `Toolbar`.
3. Esa función, definida en el componente `Toolbar`, muestra la alerta propia del botón.
4. Como la propagación fue detenida, el controlador `onClick` del `<div>` padre no se ejecuta.

Como resultado del `e.stopPropagation()`, al hacer clic en los botones ahora solo muestra una alerta (la del `<button>`) en lugar de las dos (la del `<button>` y la del `<div>` del toolbar padre). Hacer clic en un botón no es lo mismo que hacer clic en el toolbar que lo rodea, así que detener la propagación tiene sentido para esta interfaz.

> [!summary] Eventos de la fase de captura
> En raros casos, puede que necesites capturar todos los eventos en elementos hijos, _incluso si pararon la propagación_. Por ejemplo, tal vez quieras hacer log de cada clic para un análisis, independientemente de la lógica de propagación. Puedes hacer esto agregando `Capture` al final del nombre del evento:

```jsx
<div onClickCapture={() => { /* esto se ejecuta primero */ }}>
  <button onClick={e => e.stopPropagation()} />
  <button onClick={e => e.stopPropagation()} />
</div>
```

> [!summary] Eventos de la fase de captura
> Cada evento se propaga en tres fases:
> 
> 1. Viaja hacia abajo, llamando a todos los controladores `onClickCapture`.
> 2. Ejecuta el controlador `onClick` del elemento en que se hace clic.
> 3. Viaja hacia arriba, llamando a todos los controladores `onClick`.
>    
> Los eventos de captura son útiles para código como enrutadores o para analítica, pero probablemente no lo usarás en código de aplicaciones.
### Pasar controladores como alternativa a la propagación

Fíjate como este controlador de clic ejecuta una línea de código _y luego_ llama a la prop `onClick` pasada por el padre:

```jsx hl:4-5
function Button({ onClick, children }) {
  return (
    <button onClick={e => {
      e.stopPropagation();
      onClick();
    }}>
      {children}
    </button>
  );
}
```

También puede que añadas más código a este controlador antes de llamar al controlador de evento `onClick` del padre. Este patrón proporciona una _alternativa_ a la propagación. Le permite al componente hijo controlar el evento, mientras también le permite al componente padre especificar algún comportamiento adicional. A diferencia de la propagación, no es automático. Pero el beneficio de este patrón es que puedes seguir claramente la cadena de código completa que se ejecuta como resultado de algún evento.

Si dependes de la propagación y es difícil rastrear cuales controladores se ejecutaron y por qué, intenta este enfoque.

### Evitar el comportamiento por defecto

Algunos eventos del navegador tienen comportamientos por defecto asociados a ellos. Por ejemplo, un evento submit de un `<form>`, que ocurre cuando se hace clic en un botón que está dentro de él, por defecto recargará la página completa:

```jsx file:App.js
export default function Signup() {
  return (
    <form onSubmit={() => alert('¡Enviando!')}>
      <input />
      <button>Enviar</button>
    </form>
  );
}
```

Puedes llamar `e.preventDefault()` en el objeto del evento para evitar que esto suceda:

```jsx file:App.js
export default function Signup() {
  return (
    <form onSubmit={e => {
      e.preventDefault();
      alert('¡Enviando!');
    }}>
      <input />
      <button>Enviar</button>
    </form>
  );
}
```

No confundas `e.stopPropagation()` y `e.preventDefault()`. Ambos son útiles, pero no están relacionados:

- [`e.stopPropagation()`](https://developer.mozilla.org/es/docs/Web/API/Event/stopPropagation) evita que los controladores de eventos adjuntos a etiquetas de nivel superior se activen.
- [`e.preventDefault()`](https://developer.mozilla.org/es/docs/Web/API/Event/preventDefault) evita el comportamiento por defecto del navegador para algunos eventos que lo tienen.
## ¿Pueden los controladores de eventos tener efectos secundarios?

¡Absolutamente! Los controladores de eventos son el mejor lugar para los efectos secundarios.

A diferencia de las funciones de renderizado, los controladores de eventos no necesitan ser [puros](https://es.react.dev/learn/keeping-components-pure), asi que es un buen lugar para _cambiar_ algo; por ejemplo, cambiar el valor de un input en respuesta a la escritura, o cambiar una lista en respuesta a un botón presionado. Sin embargo, para cambiar una información, primero necesitas alguna manera de almacenarla. En React, esto se hace usando el [estado, la memoria de un componente.](https://es.react.dev/learn/state-a-components-memory) Aprenderás todo sobre ello en la siguiente página.
## Recapitulación

- Puedes controlar eventos pasando una función como prop a un elemento como `<button>`.
- Los controladores de eventos deben ser pasados, **¡no llamados!** `onClick={handleClick}`, no `onClick={handleClick()}`.
- Puedes definir una función controladora de evento de manera separada o en línea.
- Los controladores de eventos son definidos dentro de un componente, así pueden acceder a las props.
- Puedes declarar un controlador de evento en un padre y pasarlo como una prop al hijo.
- Puedes definir tus propias props controladoras de evento con nombres específicos de aplicación.
- Los eventos se propagan hacia arriba. Llama `e.stopPropagation()` en el primer parámetro para evitarlo.
- Los eventos pueden tener comportamientos por defecto del navegador no deseados. Llama `e.preventDefault()` para prevenirlo.
- Llamar explícitamente a una prop controladora de evento desde un controlador hijo es una buena alternativa a la propagación.