> [!note] Contexto seguro
> Esta función sólo está disponible en contextos seguros (HTTPS), en algunos o todos los navegadores compatibles.

El método `Geolocation.getCurrentPosition()` se utiliza para obtener la posición actual del dispositivo.

# Sintaxis

```js
getCurrentPosition(success)
getCurrentPosition(success, error)
getCurrentPosition(success, error, options)
```

## Parámetros

### success

Función callback que toma un objeto `GeolocationPosition` como único parámetro de entrada.

### error (opcional)

Función callback opcional que toma un objeto `GeolocationPositionError` como único parámetro de entrada.

### options (opcional)

Un objeto opcional que incluye los siguientes parámetros:

#### maximumAge

Valor `long` positivo que indica la antigüedad máxima en milisegundos de una posible posición almacenada en caché que es aceptable devolver. Si se establece en 0, significa que el dispositivo no puede utilizar una posición almacenada en caché y debe intentar recuperar la posición actual real. Si se establece en Infinito, el dispositivo debe devolver una posición en caché independientemente de su antigüedad. Valor por defecto: 0.

#### timeout

Valor `long` positivo que representa el tiempo máximo (en milisegundos) que el dispositivo puede tardar en devolver una posición. El valor por defecto es Infinito, lo que significa que `getCurrentPosition()` no devolverá hasta que la posición esté disponible.

#### enableHighAccuracy

Valor booleano que indica que la aplicación desea recibir los mejores resultados posibles. Si es verdadero y si el dispositivo es capaz de proporcionar una posición más precisa, lo hará. Tenga en cuenta que esto puede dar lugar a tiempos de respuesta más lentos o a un mayor consumo de energía (con un chip GPS en un dispositivo móvil, por ejemplo). Por otro lado, si es false, el dispositivo puede tomarse la libertad de ahorrar recursos respondiendo más rápidamente y/o consumiendo menos energía. Por defecto: false.

## Valor de retorno

[[Undefined]]

# Ejemplos

```js
const options = {
  enableHighAccuracy: true,
  timeout: 5000,
  maximumAge: 0,
};

function success(pos) {
  const crd = pos.coords;

  console.log("Your current position is:");
  console.log(`Latitude : ${crd.latitude}`);
  console.log(`Longitude: ${crd.longitude}`);
  console.log(`More or less ${crd.accuracy} meters.`);
}

function error(err) {
  console.warn(`ERROR(${err.code}): ${err.message}`);
}

navigator.geolocation.getCurrentPosition(success, error, options);
```