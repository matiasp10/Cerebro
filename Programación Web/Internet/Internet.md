Internet es una red mundial de ordenadores conectados entre sí que se comunican mediante un conjunto normalizado de protocolos.
## Introducción

Antes de saber qué es Internet, tenemos que entender qué es una red. Una **red** es _un grupo de ordenadores u otros dispositivos conectados entre sí_. Por ejemplo, en tu casa puedes tener una red de ordenadores y dispositivos. Su amigo que vive al lado puede tener una red similar de dispositivos. Su vecino puede tener una red similar de dispositivos. Todas estas redes, cuando se conectan entre sí, forman Internet.

> [!info] Concepto
> **Internet es una red de redes**.

Internet fue desarrollada a finales de los años 60 por el Departamento de Defensa de Estados Unidos para crear una red de comunicación descentralizada que pudiera resistir un ataque nuclear. Con los años, ha evolucionado hasta convertirse en una red compleja y sofisticada que se extiende por todo el planeta.

Hoy en día, Internet es una parte esencial de la vida moderna, utilizada por miles de millones de personas en todo el mundo para acceder a la información, comunicarse con amigos y familiares, hacer negocios y mucho más. Como desarrollador, es esencial conocer a fondo cómo funciona internet y las distintas tecnologías y protocolos que la sustentan.
## Cómo funciona Internet: Una visión general

A grandes rasgos, Internet funciona **conectando dispositivos y sistemas informáticos mediante un conjunto de protocolos normalizados**. Estos protocolos definen _cómo se intercambia la información_ entre dispositivos y garantizan que los datos se transmitan de forma **fiable** y **segura**.

El núcleo de Internet es una **red global de routers interconectados**, que se encargan de dirigir el tráfico entre distintos dispositivos y sistemas. Cuando se envían datos por Internet, _se dividen en pequeños paquetes que se envían desde el dispositivo a un router_. El enrutador _examina el paquete y lo reenvía al siguiente en la ruta hacia su destino_. Este proceso continúa hasta que el paquete llega a su destino final.

Para **garantizar que los paquetes se envían y reciben correctamente**, Internet utiliza una serie de protocolos, entre ellos el _Protocolo de Internet_ (**IP**) y el _Protocolo de Control de Transmisión_ (**TCP**). <mark style="background: #FFB8EBA6;">IP</mark> se encarga de _encaminar los paquetes a su destino correcto_, mientras que <mark style="background: #BBFABBA6;">TCP</mark> garantiza que los paquetes _se transmitan de forma fiable y en el orden correcto_.

Además de estos protocolos básicos, _existe una amplia gama de otras tecnologías y protocolos que se utilizan para permitir la comunicación y el intercambio de datos a través de Internet_, incluyendo el _Sistema de Nombres de Dominio_ (**DNS**), el _Protocolo de Transferencia de Hipertexto_ (**HTTP**) y el protocolo _Secure Sockets Layer/Transport Layer Security_ (**SSL/TLS**). Como desarrollador, es importante tener una sólida comprensión de cómo estas diferentes tecnologías y protocolos trabajan juntos para permitir la comunicación y el intercambio de datos a través de Internet.

## Conceptos básicos y terminología

Para entender Internet, es importante familiarizarse con algunos conceptos y terminología básicos. He aquí algunos términos y conceptos clave que conviene conocer:

- **Packet**: _Pequeña unidad de datos_ que se transmite por Internet.  
- **Router**: _Dispositivo que dirige paquetes_ de datos entre diferentes redes.  
- **IP Address**: _Identificador único_ asignado a cada dispositivo de una red, utilizado para encaminar los datos al destino correcto.  
- **Domain name**: Nombre legible por humanos que se utiliza para identificar un sitio web, como google.com.  
- **DNS**: El Sistema de Nombres de Dominio se encarga de traducir los nombres de dominio en direcciones IP.  
- **HTTP**: el protocolo de transferencia de hipertexto se utiliza para transferir datos entre un cliente (como un navegador web) y un servidor (como un sitio web).  
- **HTTPS**: versión cifrada de HTTP que se utiliza para proporcionar una comunicación segura entre un cliente y un servidor.  
- **SSL/TLS**: Los protocolos Secure Sockets Layer y Transport Layer Security se utilizan para proporcionar una comunicación segura a través de Internet.

Comprender estos conceptos y términos básicos es esencial para trabajar con internet y desarrollar aplicaciones y servicios basados en internet.

## El papel de los protocolos en Internet

Los protocolos desempeñan un papel fundamental a la hora de posibilitar la comunicación y el intercambio de datos en Internet. Un protocolo **es un conjunto de reglas y normas que definen cómo se intercambia información entre dispositivos y sistemas**.

Hay muchos protocolos diferentes utilizados en la comunicación por Internet, como el Protocolo de Internet (IP), el Protocolo de Control de Transmisión (TCP), el Protocolo de Datagramas de Usuario (UDP), el Sistema de Nombres de Dominio (DNS) y muchos otros.

IP se encarga de encaminar los paquetes de datos a su destino correcto, mientras que TCP y UDP garantizan que los paquetes se transmitan de forma fiable y eficiente. El DNS se utiliza para traducir los nombres de dominio en direcciones IP, y el HTTP para transferir datos entre clientes y servidores.

**Una de las principales ventajas de utilizar protocolos normalizados es que permiten que dispositivos y sistemas de distintos fabricantes y proveedores se comuniquen entre sí sin problemas**. Por ejemplo, un navegador web desarrollado por una empresa puede comunicarse con un servidor web desarrollado por otra, siempre que ambos se adhieran al protocolo HTTP.

Como desarrollador, es importante entender los distintos protocolos utilizados en la comunicación por Internet y cómo funcionan juntos para permitir la transferencia de datos e información a través de Internet.

## Direcciones IP y nombres de dominio

Tanto las direcciones IP como los nombres de dominio son conceptos importantes que hay que entender cuando se trabaja con Internet.  
  
Una dirección **IP** es un _identificador único asignado a cada dispositivo de una red_. Se utiliza para <mark style="background: #ABF7F7A6;">encaminar los datos al destino correcto</mark>, garantizando que la información se envía al destinatario previsto. Las direcciones IP _suelen representarse como una serie de cuatro números separados por puntos_, como "192.168.1.1".

Los **nombres de dominio**, por su parte, son _nombres legibles por humanos_ que se utilizan para _identificar sitios web y otros recursos_ de Internet. Suelen estar _compuestos por dos o más partes, separadas por puntos_. Por ejemplo, "google.com" es un nombre de dominio. Los _nombres de dominio se traducen en direcciones IP mediante el Sistema de Nombres de Dominio_ (**DNS**).  
  
El DNS es una parte fundamental de la infraestructura de Internet, _responsable de traducir los nombres de dominio en direcciones IP_. Cuando usted introduce un nombre de dominio en su navegador web, su ordenador envía una consulta DNS a un servidor DNS, que devuelve la dirección IP correspondiente. Su ordenador utiliza entonces esa dirección IP para conectarse al sitio web u otro recurso que haya solicitado.

![[Pasted image 20230810190008.png|center]]

## Introducción a HTTP y HTTPS

**HTTP** (_Hypertext Transfer Protocol_) y **HTTPS** (_HTTP Secure_) son dos de los protocolos más utilizados en aplicaciones y servicios basados en Internet.  

HTTP es el protocolo utilizado para _transferir datos entre un cliente_ (como un navegador web) _y un servidor_ (como un sitio web). Cuando visitas un sitio web, tu navegador envía una petición HTTP al servidor, solicitando la página web u otro recurso que hayas pedido. El servidor devuelve al cliente una respuesta HTTP con los datos solicitados.

_HTTPS es una versión más segura de HTTP_, que cifra los datos que se transmiten entre el cliente y el servidor _mediante el cifrado SSL/TLS_ (Secure Sockets Layer/Transport Layer Security). Esto proporciona una capa adicional de seguridad, ayudando a proteger información sensible como credenciales de acceso, información de pago y otros datos personales.  
  
Cuando visite un sitio web que utilice HTTPS, _su navegador mostrará el icono de un candado en la barra de direcciones_, indicando que la conexión es segura. También es posible que vea las letras "https" al principio de la dirección del sitio web, en lugar de "http".

## Creación de aplicaciones con TCP/IP

**TCP/IP** (_Transmission Control Protocol/Internet Protocol_) es el _protocolo de comunicación subyacente utilizado por la mayoría de aplicaciones y servicios basados en Internet_. Proporciona una entrega de datos fiable, ordenada y con comprobación de errores entre aplicaciones que se ejecutan en distintos dispositivos.  
  
A la hora de crear aplicaciones con TCP/IP, hay que entender algunos conceptos clave:

- **Ports**: Los puertos se utilizan para _identificar la aplicación o servicio que se ejecuta en un dispositivo_. A cada aplicación o servicio se le asigna un número de puerto único, lo que permite que los datos se envíen al destino correcto.  
- **Sockets**: Un socket es una _combinación de una dirección IP y un número de puerto_, que representa un punto final específico para la comunicación. Los sockets se utilizan para establecer conexiones entre dispositivos y transferir datos entre aplicaciones.
- **Connections**: Una conexión _se establece entre dos sockets cuando dos dispositivos quieren comunicarse entre sí_. Durante el proceso de establecimiento de la conexión, los dispositivos negocian diversos parámetros, como el tamaño máximo del segmento y el tamaño de la ventana, que determinan cómo se transmitirán los datos a través de la conexión.  
- **Data transfer**: Una vez establecida la conexión, se pueden transferir datos entre las aplicaciones que se ejecutan en cada dispositivo. Los datos _suelen transmitirse en segmentos, cada uno de los cuales contiene un número de secuencia y otros metadatos para garantizar una entrega fiable_.

Cuando construyas aplicaciones con TCP/IP, necesitarás asegurarte de que tu aplicación está diseñada para trabajar con los puertos, sockets y conexiones apropiados. También tendrás que estar familiarizado con los distintos protocolos y estándares que se utilizan habitualmente con TCP/IP, como HTTP, FTP (File Transfer Protocol) y SMTP (Simple Mail Transfer Protocol). Comprender estos conceptos y protocolos es esencial para crear aplicaciones y servicios basados en Internet eficaces, escalables y seguros.

## Protección de las comunicaciones por Internet con SSL/TLS

Como hemos comentado anteriormente, **SSL/TLS** es un protocolo utilizado para _cifrar los datos que se transmiten a través de Internet_. Se utiliza habitualmente para proporcionar conexiones seguras a aplicaciones como navegadores web, clientes de correo electrónico y programas de transferencia de archivos.  

Cuando se utiliza SSL/TLS para asegurar la comunicación en Internet, hay algunos conceptos clave que hay que entender:

- **Certificates**: Los certificados SSL/TLS se utilizan para _establecer la confianza entre el cliente y el servidor_. Contienen información sobre la identidad del servidor y están _firmados por un tercero de confianza_ (una autoridad de certificación) para verificar su autenticidad.  
- **Handshake**: Durante el proceso de handshake SSL/TLS, _el cliente y el servidor intercambian información para negociar el algoritmo de cifrado y otros parámetros de la conexión segura_.  
- **Encryption**: Una vez establecida la conexión segura, _los datos se cifran utilizando el algoritmo acordado y pueden transmitirse de forma segura entre el cliente y el servidor_.

Al crear aplicaciones y servicios basados en Internet, es importante comprender cómo funciona SSL/TLS y asegurarse de que su aplicación está diseñada para utilizar SSL/TLS al transmitir datos confidenciales como credenciales de inicio de sesión, información de pago y otros datos personales. También tendrá que asegurarse de que obtiene y mantiene certificados SSL/TLS válidos para sus servidores, y de que sigue las mejores prácticas para configurar y proteger sus conexiones SSL/TLS. De este modo, ayudará a proteger los datos de sus usuarios y garantizará la integridad y confidencialidad de la comunicación de su aplicación a través de Internet.

## El futuro: Tendencias y tecnologías emergentes

Internet evoluciona constantemente y no dejan de surgir nuevas tecnologías y tendencias. Como desarrollador, es importante estar al día de los últimos avances para crear aplicaciones y servicios innovadores y eficaces.  
  
Estas son algunas de las tendencias y tecnologías emergentes que están configurando el futuro de Internet:

- **5G**: 5G es la última generación de tecnología de redes móviles, que ofrece velocidades más rápidas, menor latencia y mayor capacidad que las generaciones anteriores. Se espera que permita nuevos casos de uso y aplicaciones, como los vehículos autónomos y la cirugía a distancia.  
- **Internet de las Cosas (IoT)**: IoT se refiere a la red de dispositivos físicos, vehículos, electrodomésticos y otros objetos que están conectados a Internet y pueden intercambiar datos. A medida que IoT siga creciendo, se espera que revolucione sectores como la sanidad, el transporte y la fabricación.  
- **Inteligencia Artificial (IA)**: Las tecnologías de IA, como el aprendizaje automático y el procesamiento del lenguaje natural, ya se utilizan para impulsar una amplia gama de aplicaciones y servicios, desde asistentes de voz hasta la detección del fraude. A medida que la IA siga avanzando, se espera que permita nuevos casos de uso y transforme sectores como la sanidad, las finanzas y la educación.
- **Blockchain**: Blockchain es una tecnología de libro mayor distribuido que permite transacciones seguras y descentralizadas. Se está utilizando para impulsar una amplia gama de aplicaciones, desde la criptomoneda hasta la gestión de la cadena de suministro.  
- **Edge computing**: La computación de borde se refiere al procesamiento y almacenamiento de datos en el borde de la red, en lugar de en centros de datos centralizados. Se espera que permita nuevos casos de uso y aplicaciones, como análisis en tiempo real y aplicaciones de baja latencia.

Si se mantiene al día de estas y otras tendencias y tecnologías emergentes, podrá asegurarse de que sus aplicaciones y servicios se crean para aprovechar las últimas capacidades y ofrecer la mejor experiencia posible a sus usuarios.

## Conclusión  

![[popularNetworkProtocols.gif|center]]

Y con esto llegamos al final de este artículo. Hemos cubierto mucho terreno, así que tomémonos un momento para repasar lo que hemos aprendido:  
  
- Internet es una red global de ordenadores interconectados que utiliza un conjunto estándar de protocolos de comunicación para intercambiar datos.  
- Internet funciona conectando dispositivos y sistemas informáticos mediante protocolos estandarizados, como IP y TCP.  
- El núcleo de internet es una red global de routers interconectados que dirigen el tráfico entre distintos dispositivos y sistemas.  
- Los conceptos básicos y la terminología con los que debes familiarizarte incluyen paquetes, routers, direcciones IP, nombres de dominio, DNS, HTTP, HTTPS y SSL/TLS.  
- Los protocolos desempeñan un papel fundamental a la hora de posibilitar la comunicación y el intercambio de datos a través de Internet, permitiendo que dispositivos y sistemas de distintos fabricantes y proveedores se comuniquen sin problemas.