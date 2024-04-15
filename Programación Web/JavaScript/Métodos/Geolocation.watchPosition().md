> [!note] Contexto seguro
> Esta función sólo está disponible en contextos seguros (HTTPS), en algunos o todos los navegadores compatibles.

El método `watchPosition()` del objeto `Geolocation` se utiliza para registrar una función manejadora que será llamada automáticamente cada vez que cambie la posición del dispositivo. También puede, opcionalmente, especificar una función de devolución de llamada de gestión de errores.

# Sintaxis

```js
watchPosition(success)
watchPosition(success, error)
watchPosition(success, error, options)
```

## Parámetros

### success

Función callback que toma un objeto `GeolocationPosition` como parámetro de entrada.

### error (opcional)

Función callback opcional que toma un objeto `GeolocationPositionError` como un parámetro de entrada.

### options (opcional)

Un objeto opcional que proporciona opciones de configuración para el reloj de localización. Véase [[Geolocation.getCurrentPosition()]] para más detalles sobre las posibles opciones.

## Valor de retorno

Un ID entero que identifica al controlador registrado. El ID se puede pasar a [[Geolocation.clearWatch()]] para anular el registro del controlador.

# Ejemplos

```js
let id;
let target;
let options;

function success(pos) {
  const crd = pos.coords;

  if (target.latitude === crd.latitude && target.longitude === crd.longitude) {
    console.log("Congratulations, you reached the target");
    navigator.geolocation.clearWatch(id);
  }
}

function error(err) {
  console.error(`ERROR(${err.code}): ${err.message}`);
}

target = {
  latitude: 0,
  longitude: 0,
};

options = {
  enableHighAccuracy: false,
  timeout: 5000,
  maximumAge: 0,
};

id = navigator.geolocation.watchPosition(success, error, options);
```