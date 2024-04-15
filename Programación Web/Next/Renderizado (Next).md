El renderizado convierte el código que escribes en interfaces de usuario.

React 18 y Next.js 13 introdujeron nuevas formas de renderizar tu aplicación. Esta página te ayudará a entender las diferencias entre los entornos de renderizado, las estrategias, los tiempos de ejecución y cómo optar por ellos.

## Entornos de renderizado

Hay dos entornos en los que se puede renderizar el código de tu aplicación: el cliente y el servidor.

![[Pasted image 20221117212106.png]]

- El **cliente** se refiere al navegador en el dispositivo de un usuario que envía una solicitud a un servidor para su código de aplicación. A continuación, convierte la respuesta del servidor en una interfaz con la que el usuario puede interactuar.
- El **servidor** es el ordenador de un centro de datos que almacena el código de la aplicación, recibe las peticiones del cliente, realiza algunos cálculos y envía una respuesta adecuada.

> **Nota**: Servidor es un nombre general que puede referirse a los ordenadores de las regiones de origen donde se despliega su aplicación, a la red de borde (Edge network) donde se distribuye el código de su aplicación o a las redes de entrega de contenidos (CDN) donde se puede almacenar en caché el resultado del trabajo de renderización.

## Renderización del cliente y del servidor a nivel de componente

Antes de React 18, la forma principal de renderizar tu aplicación usando React era completamente en el cliente.

Next.js proporcionaba una forma más sencilla de dividir tu aplicación en páginas y prerrepresentarlas en el servidor generando HTML y enviándolo al cliente para que fuera hidratado por React ([[hydrate()]]). Sin embargo, esto llevó a que se necesitara JavaScript adicional en el cliente para que el HTML inicial fuera interactivo.

Ahora, con Server and Client Components, React puede renderizar en el cliente y en el servidor, lo que significa que puedes elegir el entorno de renderización a nivel de componente. Por defecto, el directorio ``app`` utiliza Server Components, lo que permite renderizar fácilmente los componentes en el servidor y reducir la cantidad de JavaScript enviada al cliente. Sin embargo, tienes la opción de usar Componentes Cliente dentro de la app y renderizar en el cliente.

Puedes intercalar Componentes de Servidor y de Cliente en tu aplicación, y entre bastidores, React fusionará sin problemas el trabajo de ambos entornos.

![[Pasted image 20221117213702.png]]

## Renderización estática y dinámica en el servidor

Además de la renderización del lado del cliente y del lado del servidor con componentes React, Next.js te da la opción de optimizar la renderización en el servidor con la Renderización Estática y Dinámica.

### Renderizado estático

Con el **renderizado estático**, tanto los componentes del servidor como los del cliente pueden ser pre-renderizados en el servidor en el `build time`. El resultado del trabajo se almacena en **caché** y se reutiliza en las siguientes peticiones. El resultado de la caché también se puede **revalidar**.

> **Nota**: Esto equivale a la Generación Estática de Sitios (SSG) y a la Regeneración Estática Incremental (ISR).

Los componentes del servidor y del cliente se renderizan de forma diferente durante la renderización estática:

Los componentes del cliente tienen su HTML y JSON prerrenderizados y cacheados en el servidor. El resultado almacenado en caché se envía entonces al cliente para su hidratación.
Los componentes de servidor son renderizados en el servidor por React, y su carga útil se utiliza para generar HTML. La misma carga útil renderizada se utiliza también para hidratar los componentes en el cliente, con lo que no se necesita JavaScript en el cliente.

### Renderizado dinámico

Con el **renderizado dinámico**, tanto los componentes del servidor como los del cliente se renderizan en el servidor en el momento de la solicitud. El resultado del trabajo no se almacena en caché.

> **Nota**: Esto es equivalente al renderizado del lado del servidor `(getServerSideProps())`.

## Edge y Node.js Runtimes

En el servidor, hay **dos tiempos de ejecución** en los que se pueden renderizar tus páginas:

- El **Node.js Runtime** (_por defecto_) que tiene acceso a todas las APIs de Node.js y paquetes compatibles del ecosistema.
- El **Edge Runtime**, que se basa en las API de la web y sólo es compatible con los paquetes compatibles con el tiempo de ejecución de Edge.

Ambos tiempos de ejecución soportan la transmisión de datos desde el servidor, dependiendo de su infraestructura de despliegue.

> **Nota**: Al desplegar Next.js en Vercel, los segmentos de ruta que utilizan el tiempo de ejecución Edge pueden desplegarse globalmente como funciones Edge para mejorar el rendimiento. Tanto los tiempos de ejecución Node.js como Edge pueden desplegarse en Regiones de Origen para situarse geográficamente cerca de sus datos. Ambos tiempos de ejecución admiten respuestas en streaming, incluidos los estados de carga instantánea.