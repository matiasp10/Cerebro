> [!note] Contexto seguro
> Esta función sólo está disponible en contextos seguros (HTTPS), en algunos o todos los navegadores compatibles.

El método `Geolocation.clearWatch()` se utiliza para anular el registro de los controladores de localización/error previamente instalados mediante `Geolocation.watchPosition()`.

# Sintaxis

```js
clearWatch(id)
```

## Parámetros

### id

El número de ID devuelto por el método Geolocation.watchPosition() al instalar el manejador que desea eliminar.

## Valor de retorno

[[Undefined]]

# Ejemplos

```js
let id;
let target;
let options;

function success(pos) {
  const crd = pos.coords;

  if (target.latitude === crd.latitude && target.longitude === crd.longitude) {
    console.log("Congratulations, you've reached the target!");
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