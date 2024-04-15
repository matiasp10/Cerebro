**HTTP** (Hyper Text Transfer Protocol) es el protocolo que todo desarrollador web debe conocer, ya que impulsa toda la web. Conocer HTTP sin duda puede ayudarte a desarrollar mejores aplicaciones.
## ¿Qué es HTTP?

Lo primero es lo primero: ¿qué es HTTP? HTTP es un protocolo de comunicación de capa de aplicación basado en TCP/IP que estandariza la forma en que clientes y servidores se comunican entre sí. Define cómo se solicita y transmite el contenido a través de Internet. Por protocolo de capa de aplicación, quiero decir que es simplemente una capa de abstracción que estandariza cómo se comunican los hosts (clientes y servidores). El propio HTTP depende de TCP/IP para transmitir peticiones y respuestas entre el cliente y el servidor. Por defecto, se utiliza el puerto TCP 80, pero también se pueden utilizar otros puertos. HTTPS, sin embargo, utiliza el puerto 443.

## HTTP/0.9 - The One Liner (1991)

La primera versión documentada de HTTP fue HTTP/0.9, presentada en 1991. Era el protocolo más simple que existía, con un único método llamado GET. Si un cliente tenía que acceder a alguna página web en el servidor, habría hecho una simple petición como la siguiente

```json
GET /index.html
```

Y la respuesta del servidor habría sido la siguiente

```json
(response body)
(connection closed)
```

Es decir, el servidor recibía la petición, respondía con el HTML y, una vez transferido el contenido, se cerraba la conexión. Había

- Sin cabeceras  
- GET era el único método permitido  
- La respuesta debía ser HTML

Como se puede ver, el protocolo en realidad no tenía nada más que ser un trampolín para lo que estaba por venir.

## HTTP/1.0 - 1996

En 1996 se desarrolló la siguiente versión de HTTP, HTTP/1.0, que mejoró considerablemente la versión original.  
  
A diferencia de HTTP/0.9, que sólo estaba diseñado para respuestas HTML, HTTP/1.0 ahora podía tratar otros formatos de respuesta, como imágenes, archivos de vídeo, texto sin formato o cualquier otro tipo de contenido. Se añadieron más métodos (POST y HEAD), se modificaron los formatos de solicitud y respuesta, se añadieron cabeceras HTTP tanto a la solicitud como a la respuesta, se añadieron códigos de estado para identificar la respuesta, se introdujo la compatibilidad con juegos de caracteres, tipos multiparte, autorización, almacenamiento en caché, codificación de contenidos y mucho más.  
  
A continuación se muestra un ejemplo de solicitud y respuesta HTTP/1.0:

```json
GET / HTTP/1.0
Host: cs.fyi
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5)
Accept: */*
```

Como puede ver, junto con la solicitud, el cliente también ha enviado su información personal, el tipo de respuesta requerido, etc. Mientras que en HTTP/0.9 el cliente nunca podía enviar esa información porque no había cabeceras.  
  
Un ejemplo de respuesta a la petición anterior podría tener el siguiente aspecto

```json
HTTP/1.0 200 OK 
Content-Type: text/plain
Content-Length: 137582
Expires: Thu, 05 Dec 1997 16:00:00 GMT
Last-Modified: Wed, 5 August 1996 15:55:28 GMT
Server: Apache 0.84

(response body)
(connection closed)
```

Al principio de la respuesta aparece HTTP/1.0 (HTTP seguido del número de versión), luego aparece el código de estado 200 seguido de la frase de motivo (o descripción del código de estado, si lo prefiere).  
  
En esta nueva versión, las cabeceras de la petición y la respuesta seguían estando codificadas en ASCII, pero *el cuerpo de la respuesta podía ser de cualquier tipo*: imagen, vídeo, HTML, texto sin formato o cualquier otro tipo de contenido. Así que, ahora que el servidor podía enviar cualquier tipo de contenido al cliente, no mucho después de su introducción, el término "Hipertexto" en HTTP se convirtió en un término inapropiado. HMTP o Hypermedia Transfer Protocol (protocolo de transferencia hipermedia) podría haber tenido más sentido, pero supongo que nos quedamos con ese nombre de por vida.

Uno de los principales inconvenientes de HTTP/1.0 era que *no se podían realizar varias peticiones por conexión*. Es decir, cada vez que un cliente necesitara algo del servidor, tendría que abrir una nueva conexión TCP y, una vez satisfecha esa única petición, la conexión se cerraría. Y para cualquier siguiente requerimiento, tendrá que ser en una nueva conexión. ¿Por qué es malo? Bueno, supongamos que usted visita una página web que tiene 10 imágenes, 5 hojas de estilo y 5 archivos JavaScript, por un total de 20 elementos que necesita obtener cuando se solicita a esa página web. Dado que el servidor cierra la conexión en cuanto se completa la petición, habrá una serie de 20 conexiones separadas en las que cada uno de los elementos se servirá uno a uno en sus conexiones separadas. Este gran número de conexiones se traduce en un grave problema de rendimiento, ya que la necesidad de una nueva conexión TCP impone una importante penalización de rendimiento debido al [[TCP 3-Way Handshake Process|Handshake de tres vías]] seguido de un inicio lento.

## HTTP/1.1 - 1997

Tras sólo 3 años de HTTP/1.0, en 1999 se publicó la siguiente versión, HTTP/1.1, que introdujo numerosas mejoras con respecto a su predecesora. Las principales mejoras con respecto a HTTP/1.0 fueron las siguientes

- Se han añadido **nuevos métodos HTTP**, que introducen *PUT, PATCH, OPTIONS, DELETE*.  
- **Identificación del nombre de host** En HTTP/1.0 la cabecera Host no era obligatoria, pero HTTP/1.1 la hizo obligatoria.  
- **Conexiones persistentes** Como se ha comentado anteriormente, en HTTP/1.0 sólo había una petición por conexión y la conexión se cerraba tan pronto como se cumplía la petición, lo que provocaba un gran impacto en el rendimiento y problemas de latencia. HTTP/1.1 introdujo las conexiones persistentes, es decir, las conexiones no se cerraban por defecto y se mantenían abiertas, lo que permitía múltiples peticiones secuenciales. Para cerrar las conexiones, la cabecera Connection: close tenía que estar disponible en la petición. Los clientes suelen enviar esta cabecera en la última petición para cerrar la conexión de forma segura.  
- **Pipelining** También introdujo el soporte para pipelining, donde *el cliente podía enviar múltiples peticiones al servidor sin esperar la respuesta del servidor en la misma conexión* y el servidor tenía que enviar la respuesta en la misma secuencia en la que se recibían las peticiones. Pero, ¿cómo sabe el cliente que éste es el punto en el que finaliza la descarga de la primera respuesta y comienza el contenido de la siguiente? Bien, para resolver esto, debe haber una cabecera *Content-Length* presente que los clientes puedan usar para identificar dónde termina la respuesta y puede empezar a esperar la siguiente respuesta.

> [!note] nota
> Debe tenerse en cuenta que para beneficiarse de conexiones persistentes o pipelining, la cabecera **Content-Length** *debe estar disponible en la respuesta*, ya que esto permitiría al cliente saber cuándo se completa la transmisión y puede enviar la siguiente solicitud (en la forma secuencial normal de envío de solicitudes) o comenzar a esperar la siguiente respuesta (cuando el pipelining está habilitado).
> 
> Pero este enfoque seguía planteando un problema. Y es, ¿qué pasa si los datos son dinámicos y el servidor no puede encontrar la longitud del contenido de antemano? Bueno, en ese caso, realmente no puedes beneficiarte de las conexiones persistentes, ¿verdad? Para solucionarlo, HTTP/1.1 introdujo la *codificación por trozos*. En tales casos, el servidor puede omitir content-Length en favor de la codificación en trozos. Sin embargo, si ninguno de ellos está disponible, entonces la conexión debe cerrarse al final de la petición.

- **Transferencias por trozos**: En el caso de contenidos dinámicos, _cuando el servidor no puede averiguar realmente la longitud del contenido al iniciar la transmisión_, puede empezar a enviar el contenido por trozos (trozo a trozo) y añadir la longitud del contenido de cada trozo al enviarlo. Y cuando se envían todos los trozos, es decir, cuando se ha completado toda la transmisión, envía un trozo vacío, es decir, con la longitud del contenido a cero, para indicar al cliente que la transmisión se ha completado. Para notificar al cliente la transferencia en trozos, el servidor incluye la cabecera **Transfer-Encoding: chunked**.
- A diferencia de HTTP/1.0, que sólo disponía de autenticación básica, HTTP/1.1 incluye **autenticación de resumen y proxy**.  
- **Almacenamiento en caché**.
- **Rangos de bytes**
- **Juegos de caracteres**
- **Negociación de idiomas**  
- **Cookies de cliente**  
- **Compresión mejorada**  
- **Nuevos códigos de estado**  
- .. y mucho más

HTTP/1.1 se introdujo en 1999 y ha sido un estándar durante muchos años. Aunque mejoró mucho respecto a su predecesor, con la web cambiando cada día, empezó a mostrar su vejez. Hoy en día, cargar una página web consume más recursos que antes. Una simple página web hoy en día tiene que abrir más de 30 conexiones. Bueno, HTTP/1.1 tiene conexiones persistentes, entonces ¿por qué tantas conexiones? dirás. La razón es que *en HTTP/1.1 sólo puede haber una conexión pendiente en cualquier momento*. HTTP/1.1 intentó arreglar esto introduciendo el pipelining, pero no solucionó completamente el problema debido al bloqueo de cabecera de línea, donde una petición lenta o pesada puede bloquear las peticiones que vienen detrás y una vez que una petición se queda atascada en un pipeline, tendrá que esperar a que se cumplan las siguientes peticiones. Para superar estas deficiencias de HTTP/1.1, los desarrolladores empezaron a aplicar soluciones alternativas, como el uso de hojas de sprites, imágenes codificadas en CSS, archivos CSS/Javascript únicos y enormes, fragmentación de dominios, etc.

## SPDY - 2009

Google siguió adelante y empezó a experimentar con protocolos alternativos para hacer la web más rápida y mejorar la seguridad web, reduciendo al mismo tiempo la latencia de las páginas web. En 2009, anunciaron SPDY.

> SPDY es una marca comercial de Google y no es un acrónimo.

Se ha visto que si seguimos aumentando el ancho de banda, el rendimiento de la red aumenta al principio, pero llega un momento en que no hay mucha ganancia de rendimiento. Pero si hacemos lo mismo con la latencia, es decir, si seguimos reduciendo la latencia, hay una ganancia de rendimiento constante. Esta era la idea central de la ganancia de rendimiento detrás de SPDY, _disminuir la latencia para aumentar el rendimiento de la red_.

> [!info] ¿Sabias que?
> Para quienes no conozcan la diferencia, **la latencia es el retardo**, es decir, lo que tardan los datos en viajar entre el origen y el destino (se mide en milisegundos) y el **ancho de banda** es la cantidad de datos transferidos por segundo (bits por segundo).

Las características de SPDY incluyen multiplexación, compresión, priorización, seguridad, etc. No voy a entrar en los detalles de SPDY, ya que te harás una idea cuando entremos en el meollo de HTTP/2 en la siguiente sección, como he dicho HTTP/2 se inspira principalmente en SPDY.  
  
SPDY no intentaba realmente sustituir a HTTP; era una capa de traducción sobre HTTP que existía en la capa de aplicación y modificaba la solicitud antes de enviarla a la red. Empezó a convertirse en un estándar de facto y la mayoría de los navegadores empezaron a implementarlo.  
  
En 2015, en Google no querían tener dos estándares en competencia y decidieron fusionarlo con HTTP, dando lugar a HTTP/2 y eliminando SPDY.

## HTTP/2 - 2015

A estas alturas, ya debes estar convencido de por qué necesitábamos otra revisión del protocolo HTTP. HTTP/2 *se diseñó para el transporte de contenidos de baja latencia*. Las principales características o diferencias con respecto a la antigua versión HTTP/1.1 incluyen

- **Binario** en lugar de textual 
- **Multiplexación** - Múltiples peticiones HTTP asíncronas a través de una única conexión  
- **Compresión de cabeceras** mediante HPACK  
- **Empuje del servidor** - Múltiples respuestas para una única petición  
- **Priorización de peticiones**  
- **Seguridad**

![[Pasted image 20230807101838.png|center]]

### 1. Binary Protocol

HTTP/2 trata de resolver el problema del aumento de la latencia que existía en HTTP/1.x convirtiéndolo en un protocolo binario. Al ser un protocolo binario, es _más fácil de analizar_, pero a diferencia de HTTP/1.x ya no es legible por el ojo humano. Los principales componentes de HTTP/2 son **Frames** y **Streams**.

#### Frames and Streams

Los mensajes HTTP se componen ahora de una o más frames. Hay un marco **HEADERS** para los metadatos y un marco **DATA** para la carga útil, y existen otros tipos de marcos (*HEADERS, DATA, RST_STREAM, SETTINGS, PRIORITY, etc.*) que puedes consultar en las especificaciones de HTTP/2.  
  
Cada solicitud y respuesta HTTP/2 recibe un ID de stream único y se divide en marcos. Los marcos no son más que *piezas binarias de datos*. Una *colección de marcos se denomina* **stream**. Cada marco tiene un stream *id* que identifica el stream al que pertenece y cada marco tiene una *cabecera común*. Además, aparte de que el ID de stream es único, cabe mencionar que cualquier solicitud iniciada por el cliente utiliza números impares y la respuesta del servidor tiene números pares de ID de stream.  
  
Aparte de las HEADERS y DATA, otro tipo de marco que creo que vale la pena mencionar aquí es *RST_STREAM* que es un tipo de marco especial que se utiliza para abortar algún stream, es decir, el cliente puede enviar este marco para hacer saber al servidor que ya no necesito este stream. En HTTP/1.1 la única forma de hacer que el servidor dejara de enviar la respuesta al cliente era cerrando la conexión, lo que provocaba un aumento de la latencia porque había que abrir una nueva conexión para cualquier petición consecutiva. Mientras que en HTTP/2, el cliente puede usar RST_STREAM y dejar de recibir un stream específico mientras que la conexión seguirá abierta y los otros streams seguirán en juego.

### 2. Multiplexing

Dado que HTTP/2 es ahora un protocolo binario y como he dicho anteriormente que utiliza marcos y streams para las peticiones y respuestas, una vez que se abre una conexión TCP, *todos los streams se envían de forma asíncrona* a través de la misma conexión sin abrir ninguna conexión adicional. Y a su vez, *el servidor responde de la misma forma asíncrona*, es decir, la respuesta no tiene orden y el cliente utiliza el identificador de stream asignado para identificar el stream al que pertenece un paquete concreto. Esto también resuelve el problema de bloqueo de cabecera que existía en HTTP/1.x, es decir, el cliente no tendrá que esperar a la solicitud que está tardando y otras solicitudes seguirán siendo procesadas.

### 3. Header Compression

Formaba parte de una RFC independiente cuyo objetivo específico era optimizar las cabeceras enviadas. La esencia de esto es que cuando estamos constantemente accediendo al servidor desde un mismo cliente hay muchos datos redundantes que estamos enviando en las cabeceras una y otra vez, y a veces puede haber cookies aumentando el tamaño de las cabeceras lo que resulta en un uso de ancho de banda y un aumento de la latencia. Para solucionar este problema, HTTP/2 introdujo la compresión de cabeceras.  
  
A diferencia de la solicitud y la respuesta, las cabeceras no se comprimen en formatos gzip o compress, etc., sino que existe un mecanismo diferente para la compresión de cabeceras: los valores literales se codifican utilizando código Huffman y el cliente y el servidor mantienen una tabla de cabeceras, y *tanto el cliente como el servidor omiten cualquier cabecera repetitiva* (por ejemplo, agente de usuario, etc.) en las solicitudes posteriores y las referencian utilizando la tabla de cabeceras mantenida por ambos.  
  
Ya que hablamos de cabeceras, permítanme añadir que las cabeceras siguen siendo las mismas que en HTTP/1.1, salvo por la adición de algunas pseudocabeceras, como :method, :scheme, :host y :path.

### 4. Server Push

Server push es otra de las grandes características de HTTP/2: *el servidor, sabiendo que el cliente va a pedir un determinado recurso, puede enviárselo al cliente sin que éste se lo pida*. Por ejemplo, supongamos que un navegador carga una página web, analiza toda la página para averiguar el contenido remoto que tiene que cargar desde el servidor y, a continuación, envía las consiguientes peticiones al servidor para obtener ese contenido.  
  
Server push permite al servidor reducir los viajes de ida y vuelta enviando los datos que sabe que el cliente va a solicitar. El servidor envía una trama especial llamada *PUSH_PROMISE* para notificar al cliente: "¡Oye, estoy a punto de enviarte este recurso! No me lo pidas". La trama PUSH_PROMISE está asociada al stream que ha provocado el push y contiene el ID del flujo prometido, es decir, el flujo en el que el servidor enviará el recurso que se va a empujar.

### 5. Request Prioritization

Un cliente puede asignar una prioridad a un stream incluyendo la información de priorización en el marco HEADERS con la que se abre un stream. En cualquier otro momento, el cliente puede enviar un marco *PRIORITY* para cambiar la prioridad de un stream.  
  
Sin ninguna información de prioridad, el servidor procesa las peticiones de forma asíncrona, es decir, sin ningún orden. Si hay una prioridad asignada a un stream, entonces basado en esta información de prioridad, el servidor decide cuántos de los recursos necesitan ser dados para procesar qué petición.

### 6. Security

Hubo un amplio debate sobre si la seguridad (a través de TLS) debería ser obligatoria para HTTP/2 o no. Al final, se decidió no hacerla obligatoria. Sin embargo, la mayoría de los proveedores declararon que sólo admitirán HTTP/2 cuando se utilice sobre TLS. Así que, *aunque HTTP/2 no requiere cifrado por especificaciones, se ha convertido en obligatorio por defecto*. Una vez aclarado esto, HTTP/2, cuando se implementa sobre TLS, impone algunos requisitos, por ejemplo, debe utilizarse TLS versión 1.2 o superior, debe haber un cierto nivel de claves mínimas, se requieren claves efímeras, etc.