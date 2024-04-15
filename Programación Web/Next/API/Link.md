`<Link>` es un componente de React que amplía el elemento HTML `<a>` para proporcionar precarga y navegación del lado del cliente entre rutas. Es la forma principal de navegar entre rutas en Next.js.

```js file:app/page.js
import Link from 'next/link';
 
export default function Page() {
  return <Link href="/dashboard">Dashboard</Link>;
}
```

## Props

| Prop     | Ejemplo           | Tipo             | Requerido |
| -------- | ----------------- | ---------------- | --------- |
| href     | href="/dashboard" | String or Object | Yes       |
| replace  | replace={false}   | Boolean          | -         |
| prefetch | prefetch={false}  | Boolean          | -         |

> [!warning] Bueno saber
> Los atributos de la etiqueta `<a>` como className o target="_blank" se pueden añadir a `<Link>` como props y se pasarán al elemento `<a>` subyacente.

### href (requerido)

La ruta o URL a la que navegar.

```jsx
<Link href="/dashboard">Dashboard</Link>
```

`href` también puede aceptar un objeto, por ejemplo:

```jsx
// Navigate to /about?name=test
<Link
  href={{
    pathname: '/about',
    query: { name: 'test' },
  }}
>
  About
</Link>
```

### replace

Por defecto es false. Cuando es true, next/link reemplazará el estado actual del historial en lugar de añadir una nueva URL al historial del navegador.

```jsx file:app/page.js
import Link from 'next/link';
 
export default function Page() {
  return (
    <Link href="/dashboard" replace>
      Dashboard
    </Link>
  );
}
```

### prefetch

Por defecto es true. Cuando es true, next/link **precargará la página** (denotada por el href) en segundo plano. Esto es útil para mejorar el rendimiento de las navegaciones del lado del cliente. Cualquier <Link /> en la ventana gráfica (inicialmente o a través del scroll) será precargado.

La precarga puede desactivarse pasando prefetch={false}. La precarga solo se activa en producción.

```jsx file:app/page.js
import Link from 'next/link';
 
export default function Page() {
  return (
    <Link href="/dashboard" prefetch={false}>
      Dashboard
    </Link>
  );
}
```

## Ejemplos

### Enlace a rutas dinámicas

En el caso de las rutas dinámicas, puede ser útil utilizar literales de plantilla para crear la ruta del enlace.

Por ejemplo, puedes generar una lista de enlaces a la ruta dinámica `app/blog/[slug]/page.js`:

```jsx file:app/blog/page.js
import Link from 'next/link';
 
function Page({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>
          <Link href={`/blog/${post.slug}`}>{post.title}</Link>
        </li>
      ))}
    </ul>
  );
}
```

### Middleware

Es común usar Middleware para autenticación u otros propósitos que involucren reescribir al usuario a una página diferente. Para que el componente `<Link />` pueda precargar correctamente enlaces con reescrituras a través de Middleware, es necesario indicar a Next.js tanto _la URL que debe mostrar como la URL que debe precargar_. Esto es necesario para evitar fetches innecesarios a middleware para saber la ruta correcta a prefetch.

Por ejemplo, si quieres servir una ruta `/dashboard` que tiene vistas autenticadas y de visitante, puedes añadir algo similar a lo siguiente en tu Middleware para redirigir al usuario a la página correcta:

```jsx file:middleware.js
export function middleware(req) {
  const nextUrl = req.nextUrl;
  if (nextUrl.pathname === '/dashboard') {
    if (req.cookies.authToken) {
      return NextResponse.rewrite(new URL('/auth/dashboard', req.url));
    } else {
      return NextResponse.rewrite(new URL('/public/dashboard', req.url));
    }
  }
}
```

En este caso, debería utilizar el siguiente código en su componente `<Link />`:

```jsx 
import Link from 'next/link';
import useIsAuthed from './hooks/useIsAuthed';
 
export default function Page() {
  const isAuthed = useIsAuthed();
  const path = isAuthed ? '/auth/dashboard' : '/dashboard';
  return (
    <Link as="/dashboard" href={path}>
      Dashboard
    </Link>
  );
}
```
