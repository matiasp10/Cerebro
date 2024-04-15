Interceptar rutas le permite cargar una ruta dentro del layout actual manteniendo el contexto de la página actual. Este paradigma de enrutamiento puede ser útil cuando se desea "interceptar" una determinada ruta para mostrar una ruta diferente.

Por ejemplo, al hacer clic en una foto dentro de un feed, debería aparecer un modal superpuesto al feed con la foto. En este caso, Next.js intercepta la ruta `/feed` y "enmascara" esta URL para mostrar `/photo/123` en su lugar.

![[Pasted image 20230605112112.png]]

Sin embargo, cuando se navega a la foto directamente, por ejemplo, al hacer clic en una URL que se puede compartir o al actualizar la página, se debe mostrar la página completa de la foto en lugar del modal. No debería producirse ninguna interceptación de ruta.

![[Pasted image 20230605112127.png]]

___

## Convención

Las rutas interceptoras pueden definirse con la convención (..), que es similar a la convención de ruta relativa ../ pero para segmentos.

Puedes usar:

- (.) para emparejar segmentos del mismo nivel  
- (..) para segmentos de un nivel superior  
- (..)(..) para segmentos de dos niveles superiores  
- (...) para coincidir con segmentos del directorio raíz de la aplicación

Por ejemplo, puede interceptar el segmento de fotos desde dentro del segmento de alimentación creando un directorio (..)photo.

![[Pasted image 20230605112221.png]]

>[!note] Nota
>Tenga en cuenta que la convención (..) se basa en segmentos de ruta, no en el sistema de archivos.

___

## Ejemplos

### Modales

Las rutas interceptoras pueden utilizarse junto con las rutas paralelas para crear modales.

El uso de este patrón para crear modales supera algunos de los retos más comunes cuando se trabaja con modales, ya que le permite:

- Hacer que el contenido del modal se pueda compartir a través de una URL  
- Conservar el contexto al actualizar la página, en lugar de cerrar el modal  
- Cerrar el modal en la navegación hacia atrás en lugar de ir a la ruta anterior  
- Vuelva a abrir el modal en la navegación hacia delante

![[Pasted image 20230605112322.png]]

>[!note] Nota
>En el ejemplo anterior, la ruta al segmento de fotos puede utilizar el comparador (..) ya que @modal es una ranura y no un segmento. Esto significa que la ruta de la foto es sólo un nivel de segmento superior, a pesar de ser dos niveles de sistema de archivos superior.

Otros ejemplos podrían incluir la apertura de un modal de inicio de sesión en una barra de navegación superior, mientras que también tiene una página dedicada /login, o la apertura de un carrito de la compra en un modal lateral.