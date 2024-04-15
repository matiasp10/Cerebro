Next.js 13 introdujo una nueva forma de obtener y gestionar datos en tu aplicación. La API se ha simplificado para alinearse con React y la Plataforma Web. Esto significa que las anteriores APIs de Next.js, como ``getServerSideProps``, ``getStaticProps`` y ``getInitialProps``, no son compatibles con el nuevo directorio app. En su lugar, existe una forma más flexible de obtener, almacenar en caché y revalidar datos a nivel de componente.

## Obteniendo datos con los Server Components

Dentro del directorio ``app``, recomendamos obtener los datos dentro del componente de servidor que necesita directamente los datos. Los Server Components siempre obtienen los datos en el servidor.

La obtención de datos directamente en los Server Components tiene muchas ventajas, ya que este patrón de obtención le permite:

- Tener **acceso directo a los recursos de datos del backend** (por ejemplo, bases de datos, APIs) ya que nunca se ejecutan en el cliente.
- Mantener fácilmente la **seguridad** de su aplicación manteniendo la información sensible, como los tokens de acceso y las claves de la API, en el servidor.
- **Obtenga datos y renderice el componente en el mismo entorno**. Esto reduce tanto la comunicación de ida y vuelta entre el cliente y el servidor, como el trabajo en el hilo principal del lado del cliente.
- Realice **varias búsquedas de datos en un solo viaje de ida y vuelta**, en lugar de realizar varias solicitudes individuales en el cliente. Dependiendo de su región, la obtención de datos también puede realizarse más cerca de su fuente de datos, reduciendo la latencia y mejorando el rendimiento.
- Reducir las cascadas cliente-servidor (``Waterfalls``).
- Envíe **menos JavaScript al cliente**, ya que los componentes de servidor no envían un paquete de JavaScript.

> **Es bueno saberlo**: 
> 
> Todavía es posible obtener datos en Client Components.
> Recomendamos utilizar una biblioteca de terceros como SWR o React Query. En el futuro, también será posible obtener datos en Client Components utilizando el hook `use()` de React.

## Obtención de datos a nivel de componente

En este nuevo modelo, se pueden obtener datos dentro de los layouts, las páginas y los componentes. La obtención de datos también es compatible con **Streaming** y **Suspense**.

En el caso de los layouts, _no es posible pasar datos entre un layout padre y sus hijos_, por lo que recomendamos obtener los datos directamente dentro del layout que los necesita, incluso si se solicitan los mismos datos varias veces en una ruta. Entre bastidores, React y Next.js almacenarán en caché y desduplicarán las solicitudes para evitar que se obtengan los mismos datos más de una vez.

### Obtención de datos paralela y secuencial

Cuando se obtienen datos en los componentes, hay que tener en cuenta dos patrones de obtención de datos: **Paralelo** y **Secuencial**.

Con la obtención de datos **en paralelo**, las peticiones en una ruta se inician con urgencia y cargarán los datos al mismo tiempo. Esto reduce las cascadas cliente-servidor y el tiempo total que se tarda en cargar los datos.

Con la obtención **secuencial** de datos, **las peticiones** en una ruta **dependen unas de otras y cargarán los datos en un patrón de cascada**. Puede haber casos en los que se desee este patrón porque una obtención depende del resultado de la otra, o porque se desee que se cumpla una condición antes de la siguiente obtención para ahorrar recursos. Sin embargo, la obtención secuencial de datos puede ser involuntaria y conducir a tiempos de carga más largos.

## API Fetch()

El nuevo sistema de obtención de datos está construido sobre la API web nativa fetch() y hace uso de **async/await** dentro de los componentes del servidor.

[[Fetch API]]
[[Async]]

fetch() es una API web que se utiliza para obtener recursos remotos y devuelve una promesa. React extiende fetch para proporcionar un deduplicación automática de las solicitudes, y Next.js extiende el objeto ``fetch`` _options_ para permitir que cada solicitud establezca sus propias reglas de caché y revalidación.

### Deduplicación automática de peticiones fetch()

**React almacenará automáticamente en una caché temporal las solicitudes de obtención de datos con la misma entrada**. Se trata de una optimización para evitar que los mismos datos se obtengan más de una vez durante un pase de renderizado, y es especialmente útil cuando varios componentes necesitan obtener los mismos datos.

Por ejemplo, puede obtener el usuario actual en varios componentes de un árbol que se extiende a través de layouts anidados. Esta optimización garantiza que no sólo es seguro, sino que se fomenta la obtención de datos en el componente en el que se utilizan.

En el servidor, la caché dura el tiempo de vida de una petición al servidor hasta que se completa el proceso de renderización.
En el cliente, la caché dura lo que dura una sesión (que podría incluir múltiples re-renders del lado del cliente) antes de una recarga completa de la página.
En los casos en los que no se puede utilizar fetch, React proporciona una función de caché que permite almacenar manualmente los datos durante la duración de la solicitud.

## Obtención de datos estáticos y dinámicos

En Next.js, hay dos tipos de datos: **Estáticos** y **Dinámicos**.

- Los **datos estáticos** son datos que no cambian a menudo. Por ejemplo, una entrada de blog que se actualiza raramente.
- Los **datos dinámicos** son los que cambian a menudo o pueden ser específicos para los usuarios. Por ejemplo, una lista de productos en un carrito de la compra.

Por defecto, **Next.js realiza automáticamente búsquedas estáticas**. Esto significa que los datos se obtienen en el momento del `build`, se **almacenan** en la caché y se **reutilizan** en cada solicitud. Como desarrollador, puedes controlar cómo se almacenan en caché y se revalidan los datos estáticos.

El uso de datos estáticos tiene dos **ventajas**:

1. **Reduce la carga** de su base de datos al minimizar el número de peticiones realizadas.
2. Los datos **se almacenan automáticamente en la caché** para mejorar el rendimiento de la carga.

Sin embargo, hay algunos casos en los que se desea obtener los datos más recientes. Next.js soporta esto permitiéndole marcar las solicitudes como dinámicas. Esto significa que los datos se obtendrán en el momento de la solicitud y no se almacenarán en la caché.

### Obteniendo los datos

La **caché es el proceso de almacenar datos en una ubicación** (por ejemplo, una red de distribución de contenidos) para que no sea necesario volver a obtenerlos de la fuente original en cada solicitud y se sirvan más rápidamente.

La caché de Next.js es una caché HTTP persistente que puede distribuirse globalmente. Esto significa que la caché **puede escalar automáticamente** y ser compartida en múltiples regiones dependiendo de su plataforma (por ejemplo, Vercel).

Next.js amplía el objeto _options_ de la función ``fetch()`` para permitir que cada solicitud en el servidor establezca su propio comportamiento de caché persistente. Junto con la obtención de datos a nivel de componente, esto le permite configurar el almacenamiento en caché dentro del código de su aplicación directamente donde se están utilizando los datos.

Durante la renderización del servidor, cuando Next.js se encuentra con una obtención, comprobará la caché para ver si los datos ya están disponibles. Si lo está, devolverá los datos almacenados en la caché. Si no es así, buscará y almacenará los datos para futuras peticiones.

### Revalidación de los datos

La revalidación es el proceso de purgar la caché y volver a obtener los datos más recientes. Esto es útil cuando tus datos cambian y quieres asegurarte de que tu aplicación muestra la última versión.

Next.js proporciona dos tipos de **revalidación**:

- **Background**: Revalida los datos en un intervalo de tiempo específico.
- **On-demand**: Revalida los datos cada vez que hay una actualización.

### Streaming y Suspense

**Streaming** y **Suspense** son nuevas características de React que te permiten renderizar progresivamente y transmitir incrementalmente unidades renderizadas de la UI al cliente.

Con los componentes de servidor y los layouts anidados en Next.js, puedes renderizar instantáneamente partes de la página que no requieren datos específicamente, y mostrar un estado de carga para las partes de la página que están obteniendo datos. Esto significa que el usuario no tiene que esperar a que se cargue toda la página para poder empezar a interactuar con ella.

![[Pasted image 20221118164624.png]]
