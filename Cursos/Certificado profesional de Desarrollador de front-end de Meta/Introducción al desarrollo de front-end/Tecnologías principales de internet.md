## Introducción a los protocolos de internet

- Direcciones IP
- Transmisión de datos

Protocolos de internet
- Los mas usados son IPV4 (4 octetos por ej. `192.0.2.235`) e IPV6 (6 hexadecimales por ej. `4527:0a00:1567:0200:ff00:0042:8329`)

Cuando los datos se envían a través de internet se envían como **paquetes IP**, estos contienen una IP Header y un IP Data.

Cuando enviamos estos paquetes pueden haber errores, para resolver estos problemas el **paquete IP** también contiene otros protocolos como:

- Protocolo de control de transmisión (TCP), este resuelve problemas pero a costa de un pequeño retraso al momento de enviar los datos, se usa para enviar datos que deben llegar correctamente y en orden, tales como imágenes y texto.
- Protocolo de datagramas del usuario (UDP), puede resolver problemas como cuando se daña un paquete, pero pueden llegar desordenados o no llegar en absoluto, se usa para enviar datos que permiten cierto grado de perdida de los mismos, como por ejemplo una llamada de voz o una transmisión de video.

## Introducción a HTTP

HTTPS es la versión segura de HTTP

HTTP: protocolo operativo básico de la web (permite al navegador web comunicarse con un servidor que aloja el sitio web). Significa `Hypertext Transfer Protocol`.

Esta basado en solicitud-respuesta.

### Composición de una solicitud HTTP 

- Método (GET, PUT, POST, DELETE)
- Path (ruta)
- Version
- Cabeceras

### Composicion de una respuesta HTTP

- Método (GET, PUT, POST, DELETE)
- Estado de solicitud
	- 100 - 199 : Informativos
	- 200 - 299 : Exitosos
	- 300 - 399 : Redirecciones
	- 400 - 499 : Error de cliente
	- 500 - 599 : Error de servidor
- Path (ruta)
- Version
- Cabeceras
- body (opcional)