En su forma más simple, todas las conexiones TCP comienzan con un protocolo de tres vías en el que el cliente y el servidor comparten una serie de paquetes antes de empezar a compartir los datos de la aplicación.

- **SYN** - El cliente elige un número aleatorio, digamos *x*, y lo envía al servidor.  
- **SYN ACK** - El servidor reconoce la petición enviando un paquete ACK de vuelta al cliente que está formado por un número aleatorio, digamos *y*, recogido por el servidor y el número *x+1*, donde *x* es el número enviado por el cliente.  
- **ACK** - El cliente incrementa el número *y* recibido del servidor y envía un paquete ACK de vuelta con el número *y+1*

Una vez completado el handshake de tres vías, puede comenzar el intercambio de datos entre el cliente y el servidor. Hay que tener en cuenta que el cliente puede empezar a enviar los datos de la aplicación en cuanto envíe el último paquete ACK, pero el servidor aún tendrá que esperar a recibir el paquete ACK para satisfacer la solicitud.

![[Pasted image 20230807100546.png|center]]

Sin embargo, algunas implementaciones de HTTP/1.0 intentaron superar este problema introduciendo una nueva cabecera llamada **Connection**: *keep-alive* que pretendía decirle al servidor "Eh servidor, no cierres esta conexión, la necesito de nuevo". Pero aún así, no estaba tan ampliamente soportado y el problema persistía.  
  
Además de no tener conexión, HTTP también es un protocolo sin estado, es decir, el servidor no mantiene la información sobre el cliente, por lo que cada una de las peticiones tiene que tener la información necesaria para que el servidor pueda satisfacer la petición por sí mismo, sin ninguna asociación con peticiones anteriores. Además del gran número de conexiones que el cliente tiene que abrir, también tiene que enviar datos redundantes, lo que aumenta el uso del ancho de banda.