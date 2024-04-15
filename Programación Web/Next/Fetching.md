> Es bueno saberlo:
> 
> Este nuevo modelo de datos está siendo desarrollado por el equipo de React. Recomendamos leer el soporte de las promesas React RFC que introduce async/await en los componentes de servidor y un nuevo hook use() para los componentes de cliente.

React y Next.js 13 han introducido una nueva forma de obtener y gestionar datos en tu aplicación. El nuevo sistema de obtención de datos funciona en el directorio ``app`` y se basa en la API web **fetch()**.

fetch() es una API web utilizada para obtener recursos remotos que devuelve una promesa. React extiende fetch para proporcionar un deduplicación automática de las solicitudes, y Next.js extiende el objeto de opciones de fetch para permitir que cada solicitud establezca su propio almacenamiento en caché y revalidación.

## Async/Await en Server Components

Con la propuesta RFC, puedes utilizar async y await para obtener datos en Server Components.

`app/page.tsx`

```tsx
async function getData() {
  const res = await fetch('https://api.example.com/...');
  // The return value is *not* serialized
  // You can return Date, Map, Set, etc.

  // Recommendation: handle errors
  if (!res.ok) {
    // This will activate the closest `error.js` Error Boundary
    throw new Error('Failed to fetch data');
  }

  return res.json();
}

export default async function Page() {
  const data = await getData();

  return <main></main>;
}
```

> **Advertencia**: Puedes usar `async/await` en diseños y páginas, que son Componentes del Servidor. Usar `async/await` dentro de otros componentes, con TypeScript, puede causar errores por el tipo de respuesta de JSX. Estamos trabajando con el equipo de TypeScript para resolver este problema. Como solución temporal, puede utilizar `{/* @ts-expect-error Server Component */}` para desactivar la comprobación de tipo para el componente.

### Funciones Server Components

Next.js proporciona funciones de servidor útiles que puede necesitar cuando obtiene datos en los componentes del servidor:

- cookies()
- headers()

## use() en Client Components

``use`` es una nueva función de React que acepta una promesa conceptualmente similar a await. ``use`` maneja la promesa devuelta por una función de forma compatible con componentes, hooks y Suspense.

_fetch_ **no está actualmente soportado en los Componentes Cliente** y puede desencadenar múltiples re-renders. Por ahora, si necesitas obtener datos en un componente de cliente, recomendamos usar una biblioteca de terceros como SWR o React Query.

## Obtención de datos estáticos

Por defecto, fetch recuperará y almacenará automáticamente los datos en la caché.

```ts
fetch('https://...'); // cache: 'force-cache' is the default
```

### Revalidando los datos

Para revalidar los datos almacenados en caché en un intervalo de tiempo, puede utilizar la opción next.revalidate en fetch(). La unidad por defecto es de segundos.

```ts
fetch('https://...', { next: { revalidate: 10 } });
```

## Obtención de datos dinámicos

Para obtener datos frescos en cada solicitud **fetch()**, utilice la opción de caché: _'no-store'_.

```ts
fetch('https://...', { cache: 'no-store' });
```

## Patrones de obtención de datos

### Obtención de datos en paralelo

Para minimizar las cascadas cliente-servidor, recomendamos este patrón para obtener datos en paralelo:

`app/artist/[username]/page.jsx`

```tsx
import Albums from './albums';

async function getArtist(username) {
  const res = await fetch(`https://api.example.com/artist/${username}`);
  return res.json();
}

async function getArtistAlbums(username) {
  const res = await fetch(`https://api.example.com/artist/${username}/albums`);
  return res.json();
}


export default async function Page({ params: { username } }) {
  // Initiate both requests in parallel
  const artistData = getArtist(username);
  const albumData = getArtistAlbums(username);

  // Wait for the promises to resolve
  const [artist, album] = await Promise.all([artistData, albumData]);

  return (
    <>
      <h1>{artist.name}</h1>
      <Albums list={albumData}></Albums>
    </>
  );
}
```

Al iniciar la obtención antes de llamar a await en el componente del servidor, cada solicitud puede comenzar a obtener solicitudes al mismo tiempo. Esto configura los componentes para evitar cascadas.

Podemos ahorrar tiempo iniciando ambas peticiones en paralelo, sin embargo, el usuario no verá el resultado renderizado hasta que ambas promesas se resuelvan.

Para mejorar la experiencia del usuario, puedes añadir un límite de suspensión para romper el trabajo de renderizado y mostrar parte del resultado lo antes posible:

`artist/[username]/page.jsx`

```tsx
// ...

export default async function Page({ params: { username } }) {
  // Initiate both requests in parallel
  const artistData = getArtist(username);
  const albumData = getArtistAlbums(username);

  // Wait for the artist's promise to resolve first
  const artist = await artistData;

  return (
    <>
      <h1>{artist.name}</h1>
      {/* Send the artist information first,
      and wrap albums in a suspense boundary */}
      <Suspense fallback={<div>Loading...</div>}>
        <Albums promise={albumData} />
      </Suspense>
    </>
  );
}

// Albums Component
async function Albums({ promise }) {
  // Wait for the albums promise to resolve
  const albums = await promise;

  return (
    <ul>
      {albums.map((album) => (
        <li key={album.id}>{album.name}</li>
      ))}
    </ul>
  );
}
```

### Obtención de datos secuenciales 

Para obtener datos de forma secuencial, puedes obtenerlos directamente dentro del componente que los necesita, o puedes esperar el resultado de la obtención dentro del componente que los necesita:

`app/artist/page.tsx`

```tsx
// ...

async function Playlists({ artistID }) {
  // Wait for the playlists
  const playlists = await getArtistPlaylists(artistID);

  return (
    <ul>
      {playlists.map((playlist) => (
        <li key={playlist.id}>{playlist.name}</li>
      ))}
    </ul>
  );
}

export default async function Page({ params: { username } }) {
  // Wait for the artist
  const artist = await getArtist(username);
  // If you add multiple requests here with `await`
  // fetches would be parallelized

  return (
    <>
      <h1>{artist.name}</h1>
      <Suspense fallback={<div>Loading...</div>}>
        <Playlists artistID={artist.id} />
      </Suspense>
    </>
  );
}
```

Al obtener datos dentro del componente, cada solicitud de obtención y segmento anidado en la ruta no puede comenzar a obtener datos y a renderizar hasta que la solicitud o el segmento anterior haya finalizado.

### Bloqueo de la renderización en una ruta

Al obtener los datos en un diseño, la renderización de todos los segmentos de la ruta por debajo sólo puede comenzar una vez que los datos hayan terminado de cargarse.

En el directorio de páginas, las páginas que utilizan la renderización del servidor mostrarían el spinner de carga del navegador hasta que ``getServerSideProps`` haya terminado, y luego renderizarían el componente React para esa página. Esto puede ser descrito como un "todo o nada" de obtención de datos. O tienes todos los datos para tu página, o ninguno.

En el directorio ``app``, tienes opciones adicionales para explorar:

1. En primer lugar, puedes utilizar ``loading.js`` para mostrar un estado de carga instantáneo desde el servidor mientras se transmite el resultado de tu función de obtención de datos.
2. En segundo lugar, puedes mover la obtención de datos a un nivel más bajo en el árbol de componentes para bloquear sólo la representación de las partes de la página que lo necesitan. Por ejemplo, moviendo la obtención de datos a un componente específico en lugar de obtenerlos en el diseño raíz.
Siempre que sea posible, es mejor obtener los datos en el segmento que los utiliza. Esto también permite mostrar un estado de carga sólo para la parte de la página que se está cargando, y no para toda la página.

## Obtención de datos sin fetch()

Es posible que no siempre tengas la posibilidad de utilizar y configurar directamente las solicitudes de fetch si utilizas una biblioteca de terceros, como un ORM o un cliente de base de datos.

En los casos en los que no puedas utilizar fetch pero quieras controlar el comportamiento de caché o revalidación de un layout o página, puedes confiar en el comportamiento de caché por defecto del segmento o utilizar la configuración de caché del segmento.

### Comportamiento por defecto del caché

Cualquier biblioteca de obtención de datos que no utilice fetch directamente no afectará al almacenamiento en caché de una ruta, y será estática o dinámica dependiendo del segmento de la ruta.

Si el segmento es estático, la salida de la solicitud se almacenará en la caché y se revalidará (si está configurado) junto con el resto del segmento. Si el segmento es dinámico, la salida de la solicitud no se almacenará en la caché y se volverá a cargar en cada solicitud cuando se renderice el segmento.

> **Es bueno saberlo**: Las funciones dinámicas como cookies() y headers() harán que el segmento de la ruta sea dinámico.

### Configuración de la cache del segmento

Como solución temporal, hasta que se pueda configurar el comportamiento de la caché de las consultas de terceros, se puede utilizar la configuración del segmento para personalizar el comportamiento de la caché de todo el segmento.

``app/page.tsx``

```ts
import type { Post } from '@prisma/client';
import prisma from './lib/prisma';

export const revalidate = 3600; // revalidate every hour

async function getPosts() {
  const posts: Post[] = await prisma.post.findMany();
  return posts;
}

export default async function Page() {
  const posts = await getPosts();
  // ...
}
```