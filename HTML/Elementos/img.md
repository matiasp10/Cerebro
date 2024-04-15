El elemento HTML `<img>` incrusta una imagen en el documento.

## Formatos de imagen compatibles

El estándar HTML no enumera los formatos de imagen compatibles, por lo que los agentes de usuario pueden admitir formatos diferentes.

Los formatos de archivo de imagen más utilizados en la web son:  
  
- **APNG** (Animated Portable Network Graphics) - Buena elección para secuencias de animación sin pérdidas (GIF tiene menos rendimiento).  
- **AVIF** (AV1 Image File Format) - Buena elección tanto para imágenes como para imágenes animadas debido a su alto rendimiento.  
- **GIF** (Graphics Interchange Format) - Buena opción para imágenes y animaciones sencillas.  
- **JPEG** (Joint Photographic Expert Group image) - Buena opción para la compresión con pérdida de imágenes fijas (actualmente el más popular).  
- **PNG** (Portable Network Graphics) - Buena opción para la compresión sin pérdidas de imágenes fijas (calidad ligeramente superior a JPEG).  
- **SVG** (Scalable Vector Graphics) - Formato de imagen vectorial. Se utiliza para imágenes que deben dibujarse con precisión a diferentes tamaños.  
- **WebP** (Web Picture format) - Excelente opción tanto para imágenes como para imágenes animadas.  

Se recomiendan formatos como **WebP** y **AVIF** ya que funcionan mucho mejor que PNG, JPEG, GIF tanto para imágenes fijas como animadas. **WebP** está ampliamente soportado mientras que **AVIF** carece de soporte en Edge.  

**SVG** sigue siendo el formato recomendado para imágenes que deben dibujarse con precisión a diferentes tamaños.

## Errores de carga de imágenes

Si se produce un error al cargar o renderizar una imagen, y se ha establecido un manejador de eventos onerror para el evento de error, se llamará a ese manejador de eventos. Esto puede ocurrir en varias situaciones, incluyendo:  
  
- El atributo **src** está vacío ("") o es nulo.  
- La URL **src** es la misma que la URL de la página en la que se encuentra el usuario.  
- La imagen está dañada de alguna forma que impide que se cargue.  
- Los metadatos de la imagen están dañados de tal forma que es imposible recuperar sus dimensiones y no se han especificado dimensiones en los atributos del elemento `<img>`.  
- La imagen está en un formato no compatible con el agente de usuario.

## Atributos

Este elemento incluye los [[Atributos globales]].

### alt

Define una descripción de texto alternativa de la imagen.

> [!note] Nota
> Nota: Los navegadores no siempre muestran imágenes. Hay varias situaciones en las que un navegador puede no mostrar imágenes, como por ejemplo:
> - Navegadores no visuales (como los utilizados por personas con deficiencias visuales).
> - El usuario decide no mostrar imágenes (ahorro de ancho de banda, razones de privacidad).
> - La imagen no es válida o es de un tipo no compatible.
> 
> En estos casos, el navegador puede sustituir la imagen por el texto del atributo alt del elemento. Por estas y otras razones, proporcione un valor útil para alt siempre que sea posible.

Establecer este atributo a una cadena vacía (alt="") indica que esta imagen no es una parte clave del contenido (es decoración o un píxel de seguimiento), y que los navegadores no visuales pueden omitirla de la representación. Los navegadores visuales también ocultarán el icono de imagen rota si el atributo alt está vacío y la imagen no se muestra.  
  
Este atributo también se utiliza al copiar y pegar la imagen en un texto, o al guardar una imagen enlazada en un marcador.

### crossorigin

Indica si la obtención de la imagen debe realizarse mediante una solicitud CORS. Los datos de imagen de una imagen habilitada para CORS devuelta desde una solicitud CORS pueden reutilizarse en el elemento `<canvas>` sin que se marquen como "contaminados".  
  
Si no se especifica el atributo crossorigin, se envía una solicitud no CORS (sin la cabecera de solicitud Origin), y el navegador marca la imagen como contaminada y restringe el acceso a sus datos de imagen, impidiendo su uso en elementos `<canvas>`.  
  
Si se especifica el atributo cross-origin, entonces se envía una petición CORS (con la cabecera de petición Origin); pero si el servidor no opta por permitir el acceso cross-origin a los datos de la imagen por parte del sitio de origen (no enviando ninguna cabecera de respuesta Access-Control-Allow-Origin, o no incluyendo el origen del sitio en ninguna cabecera de respuesta Access-Control-Allow-Origin que envíe), entonces el navegador bloquea la carga de la imagen, y registra un error CORS en la consola devtools.  
  
Valores permitidos:

#### anonymous

Una solicitud CORS se envía con las credenciales omitidas (es decir, sin cookies, certificados X.509 o cabecera de solicitud de autorización).

#### use-credentials

La solicitud CORS se envía con todas las credenciales incluidas (es decir, cookies, certificados X.509 y la cabecera de solicitud Autorización). Si el servidor no opta por compartir las credenciales con el sitio de origen (devolviendo la cabecera de respuesta Access-Control-Allow-Credentials: true), el navegador marca la imagen como contaminada y restringe el acceso a sus datos de imagen.

Si el atributo tiene un valor no válido, los navegadores lo manejan como si se utilizara el valor anónimo. Consulte Atributos de configuración CORS para obtener información adicional.

### decoding

Proporciona una sugerencia de decodificación de imagen al navegador. Valores permitidos:

#### sync

Decodifica la imagen de forma sincrónica, para presentarla de forma atómica con otros contenidos.

#### async  

Decodifica la imagen de forma asíncrona, para reducir el retraso en la presentación de otros contenidos.  
  
#### auto  

Por defecto: no hay preferencia para el modo de decodificación. El navegador decide qué es lo mejor para el usuario.

### elementtiming  

Marca la imagen para su observación por parte de la API PerformanceElementTiming. El valor dado se convierte en un identificador para el elemento de imagen observado. Véase también la página del atributo elementtiming.  
  
### fetchpriority 🧪

Indica la prioridad relativa que se utilizará para obtener la imagen. Valores permitidos:  
#### high  

Indica una prioridad alta con respecto a otras imágenes.  
  
#### low  

Señala una búsqueda de baja prioridad en relación con otras imágenes.  
  
#### auto  

Predeterminado: Señala la determinación automática de la prioridad de obtención en relación con otras imágenes.  
  
### height

La altura intrínseca de la imagen, en píxeles. Debe ser un número entero sin unidad.

>[!note] Nota
>Incluir la altura y la anchura permite que el navegador calcule la relación de aspecto de la imagen antes de cargarla. Esta relación de aspecto se utiliza para reservar el espacio necesario para mostrar la imagen, reduciendo o incluso evitando un desplazamiento del diseño cuando la imagen se descarga y se pinta en la pantalla. Reducir el desplazamiento del diseño es uno de los principales componentes de una buena experiencia de usuario y del rendimiento de la web.

### ismap  

Este atributo booleano indica que la imagen forma parte de un mapa del lado del servidor. Si es así, las coordenadas en las que el usuario ha hecho clic en la imagen se envían al servidor.

> [!note] Nota
> Este atributo sólo está permitido si el elemento `<img>` es descendiente de un elemento `<a>` con un atributo href válido. De este modo, los usuarios sin dispositivos señaladores disponen de un destino alternativo.

### loading  

Indica cómo debe cargar la imagen el navegador:  
  
#### eager  

Carga la imagen inmediatamente, independientemente de si la imagen está o no dentro de la ventana visible (este es el valor por defecto).  
  
#### lazy  

Retrasa la carga de la imagen hasta que alcance una distancia calculada de la ventana gráfica, definida por el navegador. La intención es evitar el ancho de banda de red y almacenamiento necesario para manejar la imagen hasta que sea razonablemente seguro que se necesitará. Por lo general, esto mejora el rendimiento del contenido en la mayoría de los casos de uso típicos.

> [!note] Nota
> La carga sólo se aplaza cuando JavaScript está activado. Se trata de una medida contra el rastreo, ya que si un agente de usuario admite la carga diferida cuando el scripting está deshabilitado, sería posible que un sitio rastreara la posición aproximada de desplazamiento de un usuario a lo largo de una sesión, colocando estratégicamente imágenes en el marcado de una página de modo que un servidor pueda rastrear cuántas imágenes se solicitan y cuándo.

### referrerpolicy  

Una cadena que indica qué referrer utilizar cuando se obtiene el recurso:  

#### no-referrer
No se enviará la cabecera Referer.

#### no-referrer-when-downgrade
La cabecera Referer no se enviará a orígenes sin TLS (HTTPS).  

#### origen
El Referer enviado se limitará al origen de la página de referencia: su esquema, host y puerto. 

#### origin-when-cross-origin
El referrer enviado a otros orígenes se limitará al esquema, el host y el puerto. Las navegaciones en el mismo origen seguirán incluyendo la ruta.  

#### mismo-origen
Se enviará un referrer para el mismo origen, pero las peticiones cross-origin no contendrán información del referrer.  

#### origen estricto
Sólo envía el origen del documento como referrer cuando el nivel de seguridad del protocolo permanece igual (HTTPS→HTTPS), pero no lo envía a un destino menos seguro (HTTPS→HTTP).  

#### strict-origin-when-cross-origin (por defecto)
Envía una URL completa cuando se realiza una solicitud con el mismo origen, sólo envía el origen cuando el nivel de seguridad del protocolo se mantiene igual (HTTPS→HTTPS), y no envía ninguna cabecera a un destino menos seguro (HTTPS→HTTP).  

#### unsafe-url
El referrer incluirá el origen y la ruta (pero no el fragmento, la contraseña o el nombre de usuario). Este valor es inseguro, porque filtra orígenes y rutas de recursos protegidos por TLS a orígenes inseguros.

### sizes

Una o varias cadenas separadas por comas, que indican un conjunto de tamaños de origen. Cada tamaño de fuente consta de:  
  
1. Una condición de medio. Debe omitirse para el último elemento de la lista.  
2. Un valor de tamaño de origen.  

Las condiciones de medios describen propiedades de la ventana gráfica, no de la imagen. Por ejemplo, (max-height: 500px) 1000px propone utilizar una fuente de 1000px de ancho, si la ventana gráfica no es superior a 500px.  
  
Los valores de tamaño de fuente especifican el tamaño de visualización previsto de la imagen. Los agentes de usuario utilizan el tamaño de fuente actual para seleccionar una de las fuentes proporcionadas por el atributo srcset, cuando esas fuentes se describen utilizando descriptores de anchura (w). El tamaño de fuente seleccionado afecta al tamaño intrínseco de la imagen (el tamaño de visualización de la imagen si no se aplica ningún estilo CSS). Si el atributo srcset está ausente, o no contiene valores con un descriptor de anchura, entonces el atributo sizes no tiene efecto.  
  
### src  

URL de la imagen. Obligatorio para el elemento <img>. En los navegadores que admiten srcset, src se trata como una imagen candidata con un descriptor de densidad de píxeles 1x, a menos que una imagen con este descriptor de densidad de píxeles ya esté definida en srcset, o a menos que srcset contenga descriptores w.

### srcset  
Una o varias cadenas separadas por comas que indican las posibles fuentes de imágenes que puede utilizar el agente de usuario. Cada cadena se compone de:  
  
1. Una URL a una imagen  
2. Opcionalmente, un espacio en blanco seguido de uno de los siguientes elementos: 
	1. Un descriptor de anchura (un número entero positivo seguido directamente de w). El descriptor de anchura se divide por el tamaño de la fuente indicado en el atributo sizes para calcular la densidad de píxeles efectiva.  
	2. Un descriptor de densidad de píxeles (un número positivo de coma flotante seguido directamente de x).  

Si no se especifica ningún descriptor, se asigna a la fuente el descriptor por defecto 1x.  
  
Es incorrecto mezclar descriptores de anchura y descriptores de densidad de píxeles en el mismo atributo srcset. Los descriptores duplicados (por ejemplo, dos fuentes en el mismo srcset que se describen ambas con 2x) tampoco son válidos.  
  
Si el atributo srcset utiliza descriptores de anchura, el atributo sizes también debe estar presente, o se ignorará el propio srcset.  
  
El agente de usuario selecciona cualquiera de las fuentes disponibles a su discreción. Esto les proporciona un margen de maniobra significativo para adaptar su selección basándose en cosas como las preferencias del usuario o las condiciones del ancho de banda. Consulte nuestro tutorial sobre imágenes responsivas para ver un ejemplo.  
  
### width  
La anchura intrínseca de la imagen en píxeles. Debe ser un número entero sin unidad.  
  
### usemap  
La URL parcial (empezando por #) de un mapa de imagen asociado al elemento.

> [!note] Nota
> No se puede utilizar este atributo si el elemento `<img>` está dentro de un elemento `<a>` o `<button>`.

