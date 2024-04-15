Si no conoce con antelación los nombres exactos de los segmentos y desea crear rutas a partir de **datos dinámicos**, puede utilizar segmentos dinámicos que _se rellenan en el momento de la solicitud_ o _se prerenderizan en el momento de la compilación_.
___

## Convención

Se puede crear un **segmento dinámico** encerrando el nombre de una carpeta entre _corchetes_: `[folderName]`. Por ejemplo, `[id]` o `[slug]`.

Los segmentos dinámicos se pasan como `params prop` a las funciones `layout`, `page`, `route` y `generateMetadata`.

___

## Ejemplo

Por ejemplo, un blog podría incluir la siguiente ruta `app/blog/[slug]/page.js` donde `[slug]` es el _Segmento Dinámico_ para las entradas del blog.

```jsx file:app/blog/[slug]/page.js
export default function Page({ params }) {
  return <div>My Post</div>;
}
```

| **Ruta**                      | **Ejemplo URL** | **params**        |
| ------------------------- | ----------- | ------------- |
| `app/blog/[slug]/page.js` | `/blog/a`     | `{ slug: 'a' }` |
| `app/blog/[slug]/page.js` | `/blog/b`     | `{ slug: 'b' }` |
| `app/blog/[slug]/page.js` | `/blog/c`     | 	`{ slug: 'c' }`              |

___

## Generando parámetros estáticos 

La función `generateStaticParams` puede utilizarse en combinación con segmentos de ruta dinámicos para _generar rutas de forma estática_ en el momento de la construcción en lugar de hacerlo bajo demanda en el momento de la solicitud.

```jsx file:app/blog/[slug]/page.js
export async function generateStaticParams() {
  const posts = await fetch('https://.../posts').then((res) => res.json());
 
  return posts.map((post) => ({
    slug: post.slug,
  }));
}
```

La principal ventaja de la función `generateStaticParams` es su recuperación inteligente de datos. Si el contenido se obtiene dentro de la función `generateStaticParams` utilizando una solicitud `fetch`, _las solicitudes se deduplican automáticamente_. Esto significa que una solicitud de obtención con los mismos argumentos a través de múltiples `generateStaticParams`, layouts y páginas **sólo se hará una vez**, lo que disminuye los tiempos de construcción.

___

## Segmentos Catch-All

Los segmentos dinámicos pueden ampliarse para _abarcar todos los segmentos posteriores_ añadiendo una elipsis dentro de los corchetes `[...nombrecarpeta]`.

Por ejemplo, `app/shop/[...slug]/page.js` coincidirá con `/shop/clothes`, pero también con `/shop/clothes/tops`, `/shop/clothes/tops/t-shirts`, etc.

| **Ruta**                     | **Ejemplo URL** | **`params`**                |
| ---------------------------- | --------------- | --------------------------- |
| `app/shop/[...slug]/page.js` | `/shop/a`       | `{ slug: ['a'] }`           |
| `app/shop/[...slug]/page.js` | `/shop/a/b`     | `{ slug: ['a', 'b'] }`      |
| `app/shop/[...slug]/page.js` | `/shop/a/b/c`   | `{ slug: ['a', 'b', 'c'] }` |

___

## Segmentos Catch-All opcionales

Los segmentos Catch-all pueden hacerse opcionales incluyendo el parámetro entre corchetes dobles: `[[...nombrecarpeta]]`.

Por ejemplo, `app/shop/[[...slug]]/page.js` también coincidirá con `/shop`, además de con `/shop/clothes`, `/shop/clothes/tops`, `/shop/clothes/tops/t-shirts`.

La diferencia entre los segmentos **catch-all** y **catch-all opcional** es que con optional, la ruta sin el parámetro también es coincidente (`/shop` en el ejemplo anterior).

| **Ruta**                       | **Ejemplo URL** | **`params`**                |
| ------------------------------ | --------------- | --------------------------- |
| `app/shop/[[...slug]]/page.js` | `/shop`         | `{}`                        |
| `app/shop/[[...slug]]/page.js` | `/shop/a`       | `{ slug: ['a'] }`           |
| `app/shop/[[...slug]]/page.js` | `/shop/a/b`     | `{ slug: ['a', 'b'] }`      |
| `app/shop/[[...slug]]/page.js` | `/shop/a/b/c`   | `{ slug: ['a', 'b', 'c'] }` |

