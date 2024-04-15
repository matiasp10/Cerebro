Hay dos formas de almacenamiento en caché en Next.js: a nivel de **segmento** y por **petición**.

## Cache a nivel de segmento

El almacenamiento en caché a nivel de segmento **permite almacenar en caché y revalidar los datos utilizados en los segmentos de la ruta**.

Este mecanismo permite que los diferentes segmentos de una ruta controlen la duración de la caché de una ruta. Cada ``page.tsx`` y ``layout.tsx`` en la jerarquía de la ruta puede exportar un valor de revalidación que establece el tiempo de revalidación para la ruta.

``app/page.tsx``

```tsx
export const revalidate = 60; // revalidate this page every 60 seconds
```

Además del valor de revalidación exportado, las solicitudes realizadas mediante **fetch** pueden especificar una opción de revalidación para controlar la frecuencia de revalidación de la ruta.

``app/page.tsx``

```tsx
// revalidate this page every 10 seconds, since the getData's fetch
// request has `revalidate: 10`.
async function getData() {
  const res = await fetch('https://...', { next: { revalidate: 10 } });
  return res.json();
}

export default async function Page() {
  const data = await getData();
  // ...
}
```

Si una ``page``, un ``layout``  y una ``fetch request`` especifican una frecuencia de revalidación, se utilizará el valor más bajo de los tres.

``app/dashboard/layout.tsx``

```tsx
export const revalidate = 60;

export default function Layout() {
  // ...
}
```

``app/dashboard/page.tsx``

```tsx
export const revalidate = 30;

async function getData() {
  const res = await fetch('https://...', { next: { revalidate: 10 } });
  return res.json();
}

export default async function Page() {
  const data = await getData();
  // ...
}
```

En este ejemplo, el ``layout``, la ``page`` y la ``fetch request`` piden que la ruta se revalide en diferentes momentos.

Dado que la solicitud de obtención tiene el menor tiempo de revalidación, esta página utilizará su valor y se revalidará cada 10 segundos.

> Es bueno saberlo:
> 
> Puede configurar `fetchCache` como '_only-cache_' o '_force-cache_' para asegurarse de que todas las peticiones de fetch optan por el almacenamiento en caché, pero la frecuencia de revalidación podría seguir siendo reducida por las peticiones de fetch individuales.

## Cache por peticiones

El almacenamiento en caché por solicitud **permite almacenar en caché y desduplicar las solicitudes por solicitud**.

React expone una nueva función, ``cache()``, que memoriza el resultado de una función envuelta. La misma función llamada con los mismos argumentos reutilizará un valor en caché en lugar de volver a ejecutar la función. Esta función ``cache()`` se introdujo en el soporte de primera clase para promesas RFC.

Se puede utilizar ``cache()`` para desduplicar la obtención de datos por solicitud. Si una instancia de la función con los mismos argumentos ha sido llamada antes, en cualquier parte de la petición del servidor, entonces podemos devolver un valor en caché.

``utils/getUser.tsx``

```tsx
import { cache } from 'react';

export const getUser = cache(async (id) => {
  const user = await db.user.findUnique({ id });
  return user;
});
```

``app/user/[id]/layout.tsx``

```tsx
import { getUser } from '@utils/getUser';

export default async function UserLayout({ params: { id } }) {
  const user = await getUser(id);
  // ...
}
```

``app/user/[id]/page.tsx``

```tsx
import { getUser } from '@utils/getUser';

export default async function Page({ params: { id } }) {
  const user = await getUser(id);
  // ...
}
```

Aunque la función ``getUser()`` se llama dos veces en el ejemplo anterior, sólo se hará una consulta a la base de datos. Esto se debe a que ``getUser()`` está envuelta en ``cache()``, por lo que la segunda petición puede reutilizar el resultado de la primera.

> Es bueno saberlo: 
> - **fetch()** ya ha sido parcheada para incluir soporte para **cache()** automáticamente, por lo que no es necesario envolver las funciones que usan **fetch()** con **cache()**.
> - En este nuevo modelo, se recomienda **obtener los datos directamente en el componente que los necesita**, incluso si se solicitan los mismos datos en varios componentes en lugar de perforarlos.
> - Puedes **envolver las funciones que no controlas**, como las bibliotecas de terceros, con **caché** para obtener el mismo comportamiento de caché por solicitud.
> - El uso de la caché permite la **obtención de datos compartidos** sin tener que saber si un diseño principal fue renderizado durante esta solicitud.
> - Se recomienda **utilizar el paquete de sólo servidor** para asegurarse de que las funciones de obtención de datos del servidor no se utilicen accidentalmente en el cliente.

### Patrón de precarga con cache()

Como patrón, sugerimos exponer opcionalmente una exportación de ``preload()`` en las utilidades o componentes que hacen la obtención de datos.

``components/User.tsx``

```tsx
import { getUser } from "@utils/getUser";

export const preload = (id) => {
  void getUser(id);
}
export default async function User({ id }) {
  const result = await getUser(id);
  // ...
}
```

Llamando a la precarga, puedes empezar a obtener los datos que probablemente vas a necesitar.

``app/user/[id]/page.tsx``

```tsx
import User, { preload } from "@components/User";

export default async function Page({ params: { id } }) {
  preload(id); // starting loading the user data now
  const condition = await fetchCondition();
  return condition ? <User id={id} /> : null;
}
```

> Es bueno saberlo:
> - La función `preload()` puede tener cualquier nombre. Es un patrón, no una API.
> - Este patrón es completamente opcional y algo que puedes utilizar para optimizar en cada caso. Este patrón es una optimización adicional sobre la **obtención de datos en paralelo**. Ahora no tienes que pasar promesas como props y puedes confiar en el patrón de precarga.

## Combinando cache, precarga y only-server

Puedes combinar la función de caché, el patrón de precarga y el paquete de sólo servidor para crear una utilidad de obtención de datos que pueda utilizarse en toda tu aplicación.

``utils/getUser.tsx``

```tsx
import { cache } from 'react';
import 'server-only';

export const preload = (id) => {
  void getUser(id);
}

export const getUser = cache(async (id) => {
  // ...
});
```

Con este enfoque se pueden obtener los datos con urgencia, almacenar en caché las respuestas y garantizar que esta obtención de datos sólo se produce en el servidor.

Las exportaciones ``getUser.tsx`` pueden ser utilizadas por los diseños, las páginas o los componentes para darles el control sobre cuándo se obtienen los datos de un usuario.