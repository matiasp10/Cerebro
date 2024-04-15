Next.js le permite actualizar rutas estáticas específicas sin necesidad de reconstruir todo su sitio. La revalidación (también conocida como regeneración estática incremental) le permite conservar las ventajas de la estática mientras se escala a millones de páginas.

Hay dos tipos de revalidación en Next.js:

- **Background**: Revalida los datos en un intervalo de tiempo específico.
- **On-demand**: Revalida los datos basándose en un evento como una actualización de datos.

## Revalidación en Background

Para revalidar los datos almacenados en caché en un intervalo específico, puede utilizar la opción ``next.revalidate`` en ``fetch()``. La unidad por defecto son los segundos.

```jsx
fetch('https://...', { next: { revalidate: 60 } });
```

### ¿Cómo funciona?

1. Cuando se hace una petición a la ruta que se ha renderizado estáticamente en el momento de la construcción, se mostrarán inicialmente los datos en caché.
2. Cualquier solicitud a la ruta después de la solicitud inicial y antes de 60 segundos también se almacena en caché y es instantánea.
3. Una vez transcurridos los 60 segundos, la siguiente solicitud seguirá mostrando los datos almacenados en la caché.
4. Next.js activará una regeneración de los datos en segundo plano.
5. Una vez que la ruta se genere con éxito, Next.js invalidará la caché y mostrará la ruta actualizada. Si la regeneración en segundo plano falla, los datos antiguos seguirán inalterados.

Cuando se realiza una petición a un segmento de ruta que no se ha generado, Next.js renderizará dinámicamente la ruta en la primera petición. Las futuras peticiones servirán los segmentos de ruta estáticos de la caché.

> **Nota**: Comprueba si tu proveedor de datos ascendente tiene la caché activada por defecto. Es posible que tenga que deshabilitarlo (por ejemplo, `useCdn: false`), de lo contrario una revalidación no podrá extraer datos frescos para actualizar la caché de ISR. El almacenamiento en caché puede ocurrir en una CDN (para un punto final que se solicita) cuando devuelve la cabecera `Cache-Control`. ISR en Vercel persigue la caché globalmente y maneja las revalidaciones.

## Revalidación On-demand

Si establece un tiempo de revalidación de 60, todos los visitantes verán la misma versión generada de su sitio durante un minuto. La única forma de invalidar la caché es si alguien visita la página después de que haya pasado el minuto.

A partir de la versión 12.2.0, Next.js admite la regeneración estática incremental bajo demanda para purgar manualmente la caché de Next.js para una página específica. Esto facilita la actualización de su sitio cuando:

- Se crea o actualiza el contenido de su CMS sin cabeza.
- Cambios en los metadatos del e-commerce (precio, descripción, categoría, opiniones, etc.).

### Uso

En primer lugar, crea un token secreto que sólo conozca tu aplicación Next.js. Este secreto se utilizará para evitar el acceso no autorizado a la ruta de la API de revalidación. Puedes acceder a la ruta (ya sea manualmente o con un webhook) con la siguiente estructura de URL

```bash
https://<your-site.com>/api/revalidate?secret=<token>
```

A continuación, añada el secreto como una variable de entorno a su aplicación.

.env

```bash
MY_SECRET_TOKEN=<token>
```

Por último, cree la ruta API de revalidación:

``pages/api/revalidate.js``

```jsx
export default async function handler(req, res) {
  // Check for secret to confirm this is a valid request
  if (req.query.secret !== process.env.MY_SECRET_TOKEN) {
    return res.status(401).json({ message: 'Invalid token' });
  }

  try {
    // This should be the actual path not a rewritten path
    // e.g. for "/blog/[slug]" this should be "/blog/post-1"
    await res.revalidate('/path-to-revalidate');
    return res.json({ revalidated: true });
  } catch (err) {
    // If there was an error, Next.js will continue
    // to show the last successfully generated page
    return res.status(500).send('Error revalidating');
  }
}
```

Nota: Por ahora, necesita crear la ruta API dentro del directorio de páginas.

### Testing

Para verificar que la configuración de su ISR bajo demanda es correcta cuando se ejecuta localmente con ``next dev``, tendrá que crear una `production build` e iniciar ``production server``:

```bash
$ next build
$ next start
```

A continuación, puede confirmar que la ruta estática ha sido revalidada con éxito.

## Manejo de errores y revalidación

Si se produce un error al intentar revalidar, se seguirá utilizando la última ruta generada con éxito. En la siguiente solicitud, Next.js volverá a intentar la revalidación.
