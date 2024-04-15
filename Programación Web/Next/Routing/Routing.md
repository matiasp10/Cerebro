Next.js 13 introdujo un nuevo enrutador basado en el sistema de archivos construido sobre React Server Components con soporte para diseños, enrutamiento anidado, estados de carga, manejo de errores y más.

## Terminología

Verá que estos términos se utilizan en toda la documentación. He aquí una referencia rápida:

![[Pasted image 20221116202722.png]]

- **Tree**: Una convención para visualizar una estructura jerárquica. Por ejemplo, un árbol de componentes con componentes padres e hijos, una estructura de carpetas, etc.
- **Subtree**: Parte de un árbol, que comienza en una nueva raíz (la primera) y termina en las hojas (la última).
- **Root**: El primer nodo de un árbol o subárbol, como por ejemplo un diseño de raíz.
- **Leaf**: Nodos de un subárbol que no tienen hijos, como el último segmento de una ruta URL.

![[Pasted image 20221116202757.png]]

- **Ruta de la URL**: Parte de la URL que viene después del dominio.
- **Segmento de URL**: Parte de la ruta de la URL delimitada por barras inclinadas.

## El directorio app

El nuevo ``router`` funciona en un nuevo directorio llamado app. El directorio app funciona junto con el directorio ``pages`` para permitir una adopción incremental. Esto te permite optar por algunas rutas de tu aplicación en el nuevo comportamiento mientras mantienes otras rutas en el directorio pages para el comportamiento anterior.

> [!tip] Es bueno saberlo
> Las rutas a través de los directorios no deben resolverse a la misma ruta URL y causarán un error de construcción para evitar un conflicto.

![[Pasted image 20221116202938.png]]
_Por defecto_, los componentes dentro de la aplicación son **componentes de servidor React**. Esto es una optimización del rendimiento y le permite adoptarlos fácilmente. Sin embargo, también puedes utilizar Client Components.

> [!attention] Recomendación
> Consulte la página de componentes de servidor y cliente si no conoce los componentes de servidor.

## Funciones de carpetas y archivos

Next.js utiliza un enrutador basado en el sistema de archivos donde:

- _Las carpetas se utilizan para definir rutas_. Una ruta es una ruta única de carpetas anidadas, siguiendo la jerarquía del sistema de archivos desde la carpeta raíz hasta una carpeta final que incluye un archivo ``page.js``.
- Los archivos se utilizan para crear la interfaz de usuario que se muestra para un segmento de ruta.

## Segmentos de ruta

Cada carpeta de una ruta representa un segmento de ruta. Cada segmento de ruta se asigna a un segmento correspondiente en una ruta URL.

![[Pasted image 20221116203621.png]]

## Rutas anidadas

Para crear una ruta anidada, puedes anidar carpetas dentro de otras. 
Por ejemplo, puede añadir una nueva ruta ``/dashboard/settings`` anidando dos nuevas carpetas en el directorio de la aplicación.

La ruta ``/dashboard/settings`` está compuesta por tres segmentos:

- ``/`` (segmento raíz)
- ``dashboard`` (segmento)
- ``settings`` (Segmento de la hoja)

## Convenciones de archivos

Next.js proporciona un _conjunto de archivos especiales_ para crear UI con un comportamiento específico en rutas anidadas:

| **Archivo**          | **Comportamiento**                                                     |
| ---------------- | ------------------------------------------------------------------ |
| ``layout``           | Interfaz de usuario compartida para un segmento y sus hijos        |
| ``page``             | Interfaz de usuario única de una ruta y acceso público a las rutas |
| ``loading``      | Carga de la interfaz de usuario de un segmento y sus hijos         |
| ``not-found``    | Interfaz de usuario no encontrada para un segmento y sus hijos     |
| ``error``        | Error UI para un segmento y sus hijos                              |
| ``global-error`` | Interfaz global de error                                           |
| ``route``            | Endpoint de la API del servidor                                    |
| ``template``         | Interfaz de usuario de diseño re renderizado especializado         |
| ``default``                 | IU de fallback para rutas paralelas                                                                   |

## Jerarquía de componentes

Los componentes React definidos en archivos especiales de un segmento de ruta se renderizan en una jerarquía específica:

- `layout.js`
- `template.js`
- `error.js` (_React error boundary_)
- `loading.js` (_React suspense boundary_)
- `not-found.js` (_React error boundary_)
- `page.js` o `layout.js` anidados

![[Pasted image 20230531123203.png]]

En una ruta anidada, los componentes de un segmento estarán anidados dentro de los componentes de su segmento padre.

![[Pasted image 20230531123250.png]]

## Colocación

Además de los archivos especiales, tiene la opción de colocar sus propios archivos dentro de las carpetas. Por ejemplo, hojas de estilo, pruebas, componentes, etc.

Esto se debe a que mientras las carpetas definen rutas, **sólo los contenidos devueltos por page.js o route.js son públicamente direccionables**.

![[Pasted image 20230531123409.png]]

## Enrutamiento centrado en el servidor con navegación del lado del cliente

A diferencia del directorio de páginas que utiliza el enrutamiento del lado del cliente, el nuevo enrutador de ``app`` utiliza el **enrutamiento centrado en el servidor** para alinearse con los Componentes del Servidor y la obtención de datos en el servidor. Con el enrutamiento centrado en el servidor, el cliente no tiene que descargar un mapa de rutas y la misma solicitud de Server Components puede utilizarse para buscar rutas. Esta optimización es útil para todas las aplicaciones, pero tiene un mayor impacto en aplicaciones con muchas rutas.

Aunque el enrutamiento está centrado en el servidor, el enrutador utiliza la navegación del lado del cliente con el ``Componente Link`` - asemejándose al comportamiento de una _SPA_. Esto significa que cuando un usuario navega a una nueva ruta, _el navegador no recargará la página_. En su lugar, la URL se actualizará y Next.js sólo renderizará los segmentos que cambien.

Además, a medida que los usuarios navegan por la aplicación, _el enrutador almacenará el resultado de la carga útil del componente de servidor React en una caché del lado del cliente en memoria_. La caché está dividida por segmentos de la ruta, lo que permite la invalidación en cualquier nivel y garantiza la coherencia entre los renders concurrentes. Esto significa que, en ciertos casos, se puede reutilizar la caché de un segmento previamente obtenido, mejorando aún más el rendimiento.

## Renderización parcial

Al navegar entre rutas hermanas (por ejemplo, ``/dashboard/settings`` y ``/dashboard/analytics`` a continuación), _Next.js sólo obtendrá y renderizará los diseños y páginas de las rutas que cambien_. No recuperará ni renderizará nada por encima de los segmentos del subárbol. Esto significa que en las rutas que comparten un diseño, éste se conservará cuando un usuario navegue entre páginas hermanas.

![[Pasted image 20230531231103.png]]

Sin la renderización parcial, cada navegación haría que toda la página volviera a renderizarse en el servidor. Renderizar solo el segmento que se está actualizando reduce la cantidad de datos transferidos y el tiempo de ejecución, lo que mejora el rendimiento.

## Patrones de enrutamiento avanzados

El **App Router** también proporciona un conjunto de convenciones para ayudarle a implementar patrones de enrutamiento más avanzados. Estos incluyen:

- **Rutas paralelas**: Permiten mostrar simultáneamente dos o más páginas en la misma vista por las que se puede navegar de forma independiente. Puede utilizarlas para vistas divididas que tengan su propia subnavegación. Por ejemplo, cuadros de mando.
- **Rutas de interceptación**: Permiten interceptar una ruta y mostrarla en el contexto de otra ruta. Puede utilizarlas cuando sea importante mantener el contexto de la página actual. Por ejemplo, ver todas las tareas mientras se edita una o ampliar una foto en un feed.

Estos patrones permiten crear interfaces de usuario más ricas y complejas, democratizando funciones que históricamente eran complejas de implementar para equipos pequeños y desarrolladores individuales.

[[Definiendo rutas]]