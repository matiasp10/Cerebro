[[Programación Web/Interfaz de programación de aplicaciones/Introduccion]]

REST no es un protocolo ni un estándar, sino más bien un **conjunto de límites de arquitectura**. Los desarrolladores de las API pueden implementarlo de distintas maneras.

![[REST API.png]]

Cuando el cliente **envía una solicitud** a través de una API de RESTful, esta transfiere una representación del estado del recurso requerido a quien lo haya solicitado o al extremo. La información se entrega por medio de **HTTP** en uno de estos formatos: **JSON (JavaScript Object Notation), HTML, XLT, Python, PHP o texto sin formato**. JSON es el lenguaje de programación más popular, ya que tanto las máquinas como las personas lo pueden comprender y **no depende de ningún lenguaje**, a pesar de que su nombre indique lo contrario. 

Los **encabezados** y los **parámetros** también son importantes en los métodos HTTP de una solicitud HTTP de la API de RESTful, ya que contienen información de identificación importante con respecto a los **metadatos**, la **autorización**, el identificador uniforme de recursos (**URI**), el almacenamiento en **caché**, las **cookies** y **otros elementos** de la solicitud. Hay **encabezados de solicitud y de respuesta**, pero cada uno tiene sus propios códigos de estado e información de conexión HTTP.

## Condiciones para que sea una API RESTful

- Arquitectura **cliente-servidor** compuesta de clientes, servidores y recursos, con la **gestión de solicitudes a través de HTTP**.
- Comunicación entre el cliente y el servidor sin estado, lo cual implica que **no se almacena la información del cliente entre las solicitudes de GET** y que cada una de ellas es **independiente** y está **desconectada** del resto.
- **Datos que pueden almacenarse en caché** y optimizan las interacciones entre el cliente y el servidor.
- Una **interfaz uniforme entre los elementos**, para que la información se transfiera de forma estandarizada. Para ello deben cumplirse las siguientes condiciones:
	- Los recursos solicitados deben ser **identificables** e **independientes** de las representaciones enviadas al cliente.
	- El cliente debe poder **manipular los recursos a través de la representación que recibe**, ya que esta contiene suficiente información para permitirlo.
	- Los **mensajes autodescriptivos** que se envíen al cliente deben contener la información necesaria para describir cómo debe procesarla.
	- Debe contener **hipertexto** o **hipermedios**, lo cual significa que cuando el cliente acceda a algún recurso, debe poder utilizar hipervínculos para buscar las demás acciones que se encuentren disponibles en ese momento.
- Un **sistema en capas** que organiza en jerarquías invisibles para el cliente cada uno de los servidores (los encargados de la seguridad, del equilibrio de carga, etc.) que participan en la recuperación de la información solicitada.
- **Código disponible según se solicite** (opcional), es decir, la capacidad para enviar códigos ejecutables del servidor al cliente cuando se requiera, lo cual amplía las funciones del cliente. 

REST es un **conjunto de pautas que pueden implementarse según sea necesario**. Por esta razón, las API de REST son más **rápidas** y **ligeras**, cuentan con mayor capacidad de ajuste