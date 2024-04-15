La función del servidor ``generateStaticParams`` puede utilizarse en combinación con los segmentos de ruta dinámicos para definir la lista de parámetros de los segmentos de ruta que se generarán estáticamente en el momento de la ``build`` en lugar de hacerlo bajo demanda.

Sustituye a ``getStaticPaths`` con una API simplificada. ``generateStaticParams`` no requiere ningún parámetro de contexto. Se ejecuta en el `build time` antes de que se generen los correspondientes layouts o Páginas. No será llamado de nuevo durante la **revalidación** (ISR).

``app/blog/[slug]/page.js``

```tsx
export async function generateStaticParams() {
  const posts = await getPosts();

  return posts.map((post) => ({
    slug: post.slug,
  }));
}
```

El principal beneficio de la función ``generateStaticParams`` es su recuperación inteligente de datos. Si el contenido se obtiene dentro de la función ``generateStaticParams`` utilizando una solicitud de obtención, las solicitudes se deduplican automáticamente. Esto significa que una solicitud de obtención con los mismos argumentos a través de múltiples ``generateStaticParams``, ``Layouts`` y ``Pages`` _sólo se hará una vez_, lo que disminuye el `build time`.
