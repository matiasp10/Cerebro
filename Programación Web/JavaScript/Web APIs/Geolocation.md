> [!info] Contexto seguro
> Esta función sólo está disponible en contextos seguros (HTTPS), en algunos o todos los navegadores compatibles.

La interfaz de geolocalización representa un objeto capaz de obtener la posición del dispositivo mediante programación. Proporciona a los contenidos web acceso a la ubicación del dispositivo. Esto permite que un sitio web o una app ofrezcan resultados personalizados en función de la ubicación del usuario.

Un objeto con esta interfaz se obtiene utilizando la propiedad `navigator.geolocation` implementada por el objeto `Navigator`.

> [!note] Nota
> Por razones de seguridad, cuando una página web intenta acceder a la información de localización, se notifica al usuario y se le pide que conceda permiso. Ten en cuenta que cada navegador tiene sus propias políticas y métodos para solicitar este permiso.

# Propiedades de instancia

La interfaz `Geolocation` no implementa ni hereda ninguna propiedad.

# Métodos de instancia 

La interfaz Geolocalización no hereda ningún método.

## Geolocation.getCurrentPosition()

Determina la ubicación actual del dispositivo y devuelve un objeto `GeolocationPosition` con los datos.



## Geolocation.watchPosition()

Devuelve un valor `long` que representa la función callback recién establecida que se invocará cada vez que cambie la ubicación del dispositivo.

## Geolocation.clearWatch()

Elimina el manejador particular previamente instalado usando watchPosition().