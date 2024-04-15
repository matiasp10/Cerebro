En Next.js, una ruta puede ser estática o dinámica.

- En una ruta **estática**, los componentes se renderizan en el servidor en el momento de la construcción. El resultado del trabajo se almacena en caché y se reutiliza en las siguientes peticiones.
- En una ruta **dinámica**, los componentes se renderizan en el servidor en el momento de la solicitud.

## Renderizado estático (por defecto)

El **renderizado estático** (por defecto) _mejora el rendimiento_ porque todo el trabajo de renderizado se realiza con antelación y puede servirse desde una red de distribución de contenidos (**CDN**) geográficamente más cercana al usuario.

Puedes optar por la renderización dinámica utilizando una función dinámica o la obtención de datos dinámicos en un layout o página. Esto hará que Next.js renderice toda la ruta dinámicamente, en el momento de la solicitud.

Esta tabla resume cómo las funciones dinámicas y la obtención de datos estáticos (caché) afectan al comportamiento de la representación de una ruta.

| Data Fetching | Dynamic Functions | Rendering |
| ------------- | ----------------- | --------- |
| Cacheado       | No                | Estático  |
| Cacheado        | Si                | Dinámico  |
| No cacheado    | No                | Dinámico  |
| No cacheado    | Si                | Dinámico          |

Obsérvese cómo, para que una ruta se renderice estáticamente, las peticiones de datos se almacenan en caché y no hay funciones dinámicas.

## Obtención de datos estática (por defecto)

Por defecto, Next.js almacenará en caché el resultado de las peticiones ``fetch()`` que no opten específicamente por un comportamiento de caché. Esto significa que las peticiones fetch que no establezcan una opción de caché utilizarán la opción de **forzar caché**.

Si alguna de las peticiones fetch de la ruta utiliza la opción ``revalidate``, la ruta se volverá a renderizar estáticamente durante la revalidación.

## Renderizado dinámico

Durante el renderizado estático, si se descubre una función dinámica o una solicitud dinámica de ``fetch()`` (_sin caché_), Next.js pasará a renderizar dinámicamente toda la ruta en el momento de la solicitud. Cualquier solicitud de datos en caché puede seguir siendo reutilizada durante el renderizado dinámico.

### Usando funciones dinamicas

Las funciones dinámicas se basan en **información que sólo puede conocerse en el momento de la solicitud**, como las cookies del usuario o las cabeceras de las solicitudes actuales. En Next.js, éstas son: ``cookies()`` y ``headers()``.

Dado que el valor devuelto por estas funciones no puede conocerse con antelación, su uso en un layout o página forzará la representación dinámica en el momento de la solicitud.

### Usando obtención de datos dinámica

Las recuperaciones de datos dinámicos son peticiones ``fetch()`` que optan específicamente por el comportamiento de la caché estableciendo la opción de caché como '_no-store_' o _revalidate como 0_.

Las opciones de almacenamiento en caché para todas las solicitudes de obtención en un layout o página también pueden establecerse mediante el objeto `config-segment`.