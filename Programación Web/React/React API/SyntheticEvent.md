Esta guía de referencia documenta el contenedor ``SyntheticEvent`` que forma parte del sistema de eventos de React. 

## Resumen

A tus manejadores de eventos se les pasarán instancias de `SyntheticEvent`, un contenedor agnóstico al navegador alrededor del evento nativo del navegador. Tiene la misma interfaz que el evento nativo del navegador, incluyendo `stopPropagation()` y `preventDefault()`, excepto que **los eventos funcionan de manera idéntica en todos los navegadores**.

Si encuentras que **necesitas el evento del navegador subyacente por alguna razón**, simplemente use el atributo `nativeEvent` para obtenerlo. Los eventos sintéticos son diferentes y no tienen una correspondencia directa con los eventos nativos del navegador. Por ejemplo en `onMouseLeave` `event.nativeEvent` apuntará al evento `mouseout`. La correspondencia específica no es parte de la API pública y puede cambiar en cualquier momento. Cada objeto `SyntheticEvent` tiene los siguientes atributos:

```jsx
boolean bubbles
boolean cancelable
DOMEventTarget currentTarget
boolean defaultPrevented
number eventPhase
boolean isTrusted
DOMEvent nativeEvent
void preventDefault()
boolean isDefaultPrevented()
void stopPropagation()
boolean isPropagationStopped()
void persist()
DOMEventTarget target
number timeStamp
string type
```

> Nota: A partir de la versión 17, `e.persist()` no hace nada porque `SyntheticEvent` ya no se [reutiliza](https://es.reactjs.org/docs/legacy-event-pooling.html).

> Nota: A partir de la versión 0.14, devolver `false` desde un controlador de eventos ya no detendrá la propagación de eventos. En su lugar, `e.stopPropagation()` o `e.preventDefault()` deben activarse manualmente, según corresponda.

## Eventos Soportados

React normaliza los eventos para que tengan propiedades consistentes en diferentes navegadores.

Los controladores de eventos a continuación se activan por un evento en la fase de propagación. Para registrar un controlador de eventos llamado en la fase de captura, agrega `Capture` al nombre del evento; por ejemplo, en lugar de usar `onClick`, usarías`onClickCapture` para manejar el evento de click en la fase de captura.

### Eventos del Portapapeles

Nombres de Eventos:

```jsx
onCopy onCut onPaste
```

Propiedades:

```
DOMDataTransfer clipboardData
```

---

### Eventos de Composición

Nombres de Eventos:

```
onCompositionEnd onCompositionStart onCompositionUpdate
```

Propiedades:

```
string data
```

---

### Eventos del Teclado

Nombres de Eventos:

```
onKeyDown onKeyPress onKeyUp
```

Propiedades:

```
boolean altKey
number charCode
boolean ctrlKey
boolean getModifierState(key)
string key
number keyCode
string locale
number location
boolean metaKey
boolean repeat
boolean shiftKey
number which
```

La propiedad `key` puede tomar cualquiera de los valores documentados en [la especificación de DOM Level 3 Events](https://www.w3.org/TR/uievents-key/#named-key-attribute-values).

---

### Eventos de Enfoque

Nombres de Eventos:

```
onFocus onBlur
```

Estos eventos de enfoque funcionan en todos los elementos en React DOM, no sólo en los elementos de formulario.

Propiedades:

```
DOMEventTarget relatedTarget
```

#### onFocus

El manejador de evento `onFocus` se llama cuando el elemento (o algún elemento dentro de él) recibe el foco. Por ejemplo, se llama cuando el usuario hace clic en una entrada de texto.

```jsx
function Example() {
  return (
    <input
      onFocus={(e) => {
        console.log('Focused on input');
      }}
      placeholder="onFocus is triggered when you click this input."
    />
  )
}
```

#### onBlur

El manejador de evento `onBlur` se llama cuando el foco ha dejado el elemento (o ha dejado algún elemento dentro de él). Por ejemplo, se llama cuando el usuario hace clic fuera de una entrada de texto que tiene el foco.

```jsx
function Example() {
  return (
    <input
      onBlur={(e) => {
        console.log('Triggered because this input lost focus');
      }}
      placeholder="onBlur is triggered when you click this input and then you click outside of it."
    />
  )
}
```

#### Detectar la entrada y salida del foco

Puedes usar `currentTarget` y `relatedTarget` para diferenciar si los eventos de foco y pérdida de foco se originan desde _fuera_ del elemento padre. Aquí hay una demo que puedes copiar y pegar que muestra como detectar el foco en un hijo, el foco sobre el propio elemento y cuando el foco entra o sale de todo el subárbol.

```jsx
function Example() {
  return (
    <div
      tabIndex={1}
      onFocus={(e) => {
        if (e.currentTarget === e.target) {
          console.log('focused self');
        } else {
          console.log('focused child', e.target);
        }
        if (!e.currentTarget.contains(e.relatedTarget)) {
          // Not triggered when swapping focus between children
          console.log('focus entered self');
        }
      }}
      onBlur={(e) => {
        if (e.currentTarget === e.target) {
          console.log('unfocused self');
        } else {
          console.log('unfocused child', e.target);
        }
        if (!e.currentTarget.contains(e.relatedTarget)) {
          // Not triggered when swapping focus between children
          console.log('focus left self');
        }
      }}
    >
      <input id="1" />
      <input id="2" />
    </div>
  );
}
```

---

### Eventos de Formulario

Nombres de Eventos:

```
onChange onInput onInvalid onReset onSubmit 
```

Para obtener más información sobre el evento onChange, consulte [Formularios](https://es.reactjs.org/docs/forms.html).

---

### Eventos genéricos

Nombres de eventos:

```
onError onLoad
```

---

### Eventos del Ratón

Nombres de Eventos:

```
onClick onContextMenu onDoubleClick onDrag onDragEnd onDragEnter onDragExit
onDragLeave onDragOver onDragStart onDrop onMouseDown onMouseEnter onMouseLeave
onMouseMove onMouseOut onMouseOver onMouseUp
```

Los eventos `onMouseEnter` y `onMouseLeave` se propagan desde el elemento que se deja hasta el que se ingresa en lugar del bubbling normal y no tienen una fase de captura.

Propiedades:

```
boolean altKey
number button
number buttons
number clientX
number clientY
boolean ctrlKey
boolean getModifierState(key)
boolean metaKey
number pageX
number pageY
DOMEventTarget relatedTarget
number screenX
number screenY
boolean shiftKey
```

---

### Eventos Puntero

Nombres de Eventos:

```
onPointerDown onPointerMove onPointerUp onPointerCancel onGotPointerCapture
onLostPointerCapture onPointerEnter onPointerLeave onPointerOver onPointerOut
```

Los eventos `onPointerEnter` y `onPointerLeave` se propagan desde el elemento que se deja hasta el que se ingresa en lugar del bubbling normal y no tienen una fase de captura.

Propiedades:

Como se define en [la especificación W3](https://www.w3.org/TR/pointerevents/), los eventos de puntero extienden los [Eventos de Ratón](https://es.reactjs.org/docs/events.html#mouse-events) con las siguientes propiedades:

```
number pointerId
number width
number height
number pressure
number tangentialPressure
number tiltX
number tiltY
number twist
string pointerType
boolean isPrimary
```

Una nota sobre la compatibilidad con varios navegadores:

Los eventos de puntero aún no son compatibles con todos los navegadores (en el momento de escritura de este artículo, los navegadores compatibles incluyen: Chrome, Firefox, Edge e Internet Explorer). React no admite _polyfills_ deliberadamente para otros navegadores, ya que un _polyfill_ de conformidad estándar aumentaría significativamente el tamaño del paquete de `react-dom`.

Si su aplicación requiere eventos de puntero, le recomendamos que agregue un polyfill de evento de puntero de terceros.

---

### Eventos de Selección

Nombres de Eventos

```
onSelect
```

---

### Eventos Táctiles

Nombres de Eventos:

```
onTouchCancel onTouchEnd onTouchMove onTouchStart
```

Propiedades:

```
boolean altKey
DOMTouchList changedTouches
boolean ctrlKey
boolean getModifierState(key)
boolean metaKey
boolean shiftKey
DOMTouchList targetTouches
DOMTouchList touches
```

---

### Eventos de la Interfaz de Usuario

Nombres de Eventos:

```
onScroll
```

> Nota
> 
> A partir de React 17, el event `onScroll` **no hace _bubbling_** en React. Esto se alinea con el comportamiento del navegador y previene confusiones cuando un elemento anidado con _scroll_ dispara eventos en un padre distante.

Properties:

```
number detail
DOMAbstractView view
```

---

### Eventos de la Rueda del Ratón

Nombres de Eventos:

```
onWheel
```

Propiedades:

```
number deltaMode
number deltaX
number deltaY
number deltaZ
```

---

### Eventos de Medios

Nombres de Eventos:

```
onAbort onCanPlay onCanPlayThrough onDurationChange onEmptied onEncrypted
onEnded onError onLoadedData onLoadedMetadata onLoadStart onPause onPlay
onPlaying onProgress onRateChange onSeeked onSeeking onStalled onSuspend
onTimeUpdate onVolumeChange onWaiting
```

---

### Eventos de Imagen

Nombres de Eventos:

```
onLoad onError
```

---

### Eventos de Animación

Nombres de Eventos:

```
onAnimationStart onAnimationEnd onAnimationIteration
```

Propiedades:

```
string animationName
string pseudoElement
float elapsedTime
```

---

### Eventos de Transición

Nombres de Eventos:

```
onTransitionEnd
```

Propiedades:

```
string propertyName
string pseudoElement
float elapsedTime
```

---

### Otros Eventos

Nombres de Eventos:

```
onToggle
```