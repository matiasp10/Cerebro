El middleware permite ejecutar código antes de que se complete una solicitud. A continuación, basándose en la solicitud entrante, puede modificar la respuesta reescribiendo, redirigiendo, modificando las cabeceras de solicitud o respuesta, o respondiendo directamente.

El middleware se ejecuta antes de que coincidan el contenido almacenado en caché y las rutas.
___

## Convención 

Utilice el archivo `middleware.ts` (o `.js`) en la raíz de su proyecto para definir Middleware. Por ejemplo, al mismo nivel que `pages` o `app`, o dentro de `src` si procede.

___

## Ejemplo

```jsx file:middleware.ts
import { NextResponse } from 'next/server'
import type { NextRequest } from 'next/server'
 
// This function can be marked `async` if using `await` inside
export function middleware(request: NextRequest) {
  return NextResponse.redirect(new URL('/home', request.url))
}
 
// See "Matching Paths" below to learn more
export const config = {
  matcher: '/about/:path*',
}
```

## Paths coincidentes

El middleware se invocará para cada ruta de su proyecto. El orden de ejecución es el siguiente:

1. `headers` de `next.config.js`
2. `redirects` de `next.config.js`
3. Middleware (`rewrites`, `redirects`, etc.)
4. `beforeFiles` (`rewrites`) de `next.config.js`
5. Filesystem routes (`public/`, `_next/static/`, `pages/`, `app/`, etc.)
6. `afterFiles` (`rewrites`) de `next.config.js`
7. Dynamic Routes (`/blog/[slug]`)
8. `fallback` (`rewrites`) de `next.config.js`

Hay dos formas de definir en qué rutas se ejecutará Middleware:

### Matcher

**matcher** permite filtrar `Middleware` para que se ejecute en rutas específicas.

```jsx file:middleware.js
export const config = {
  matcher: '/about/:path*',
}
```

Puede hacer coincidir una única ruta o varias rutas con una sintaxis de matriz:

```jsx file:middleware.js
export const config = {
  matcher: ['/about/:path*', '/dashboard/:path*'],
}
```

La configuración del `matcher` permite regex completo, por lo que se admiten emparejamientos como _lookaheads_ negativos o emparejamientos de caracteres. Un ejemplo de un _lookahead_ negativo para que coincida con todos excepto rutas específicas se puede ver aquí:

```jsx file:middleware.js
export const config = {
  matcher: [
    /*
     * Match all request paths except for the ones starting with:
     * - api (API routes)
     * - _next/static (static files)
     * - _next/image (image optimization files)
     * - favicon.ico (favicon file)
     */
    '/((?!api|_next/static|_next/image|favicon.ico).*)',
  ],
}
```

>[!warning] Bueno saber
>Los valores del `matcher` deben ser **constantes** para que puedan ser analizados estáticamente en tiempo de compilación. Los valores dinámicos, como las variables, se ignorarán.

Matchers configurados:

1. DEBE empezar por `/`.
2. Puede incluir parámetros con nombre: `/about/:path` coincide con `/about/a` y `/about/b` pero no con `/about/a/c`.
3. Puede tener modificadores en parámetros con nombre (empezando por `:`): `/about/:path*` coincide con `/about/a/b/c` porque `*` es _cero o más_. `?` es _cero o uno_ y `+` `uno o más`.
4. Puede utilizar una expresión regular encerrada entre paréntesis: `/about/(.*)` es lo mismo que `/about/:ruta*`.

> [!warning] Bueno saber
> Por compatibilidad con versiones anteriores, Next.js siempre considera `/public` como `/public/index`. Por lo tanto, un matcher de `/public/:path` coincidirá.

### Declaraciones condicionales

```jsx file:middleware.ts
import { NextResponse } from 'next/server'
import type { NextRequest } from 'next/server'
 
export function middleware(request: NextRequest) {
  if (request.nextUrl.pathname.startsWith('/about')) {
    return NextResponse.rewrite(new URL('/about-2', request.url))
  }
 
  if (request.nextUrl.pathname.startsWith('/dashboard')) {
    return NextResponse.rewrite(new URL('/dashboard/user', request.url))
  }
}
```

___

## NextResponse

La API de NextResponse le permite:

- redirigir la solicitud entrante a una URL diferente.
- reescribir la respuesta mostrando una URL determinada.
- Establecer cabeceras de solicitud para rutas API, getServerSideProps y destinos de reescritura.
- Establecer cookies de respuesta.
- Establecer cabeceras de respuesta

Para producir una respuesta desde Middleware, puede:

1. **Reescribir** a una ruta (`Page` o `Edge API Route)` que produce una respuesta.
2. **Devolver** un _NextResponse_ directamente.
___

## Cookies

Las cookies son cabeceras normales. En una solicitud, se almacenan en la cabecera Cookie. En una respuesta están en la cabecera Set-Cookie. Next.js proporciona una manera conveniente de acceder y manipular estas cookies a través de la extensión de cookies en NextRequest y NextResponse.

1. Para las peticiones entrantes, las cookies vienen con los siguientes métodos: get, getAll, set y delete cookies. Puede comprobar la existencia de una cookie con has o eliminar todas las cookies con clear.
2. Para las respuestas salientes, las cookies tienen los siguientes métodos get, getAll, set y delete.

```jsx file:middleware.ts
import { NextResponse } from 'next/server'
import type { NextRequest } from 'next/server'
 
export function middleware(request: NextRequest) {
  // Assume a "Cookie:nextjs=fast" header to be present on the incoming request
  // Getting cookies from the request using the `RequestCookies` API
  let cookie = request.cookies.get('nextjs')
  console.log(cookie) // => { name: 'nextjs', value: 'fast', Path: '/' }
  const allCookies = request.cookies.getAll()
  console.log(allCookies) // => [{ name: 'nextjs', value: 'fast' }]
 
  request.cookies.has('nextjs') // => true
  request.cookies.delete('nextjs')
  request.cookies.has('nextjs') // => false
 
  // Setting cookies on the response using the `ResponseCookies` API
  const response = NextResponse.next()
  response.cookies.set('vercel', 'fast')
  response.cookies.set({
    name: 'vercel',
    value: 'fast',
    path: '/',
  })
  cookie = response.cookies.get('vercel')
  console.log(cookie) // => { name: 'vercel', value: 'fast', Path: '/' }
  // The outgoing response will have a `Set-Cookie:vercel=fast;path=/test` header.
 
  return response
}
```

___

## Configurando headers

Puedes configurar las cabeceras de solicitud y respuesta utilizando la API **NextResponse** (la configuración de cabeceras de solicitud está disponible desde Next.js v13.0.0).

```jsx file:middleware.js
import { NextResponse } from 'next/server'
 
export function middleware(request) {
  // Clone the request headers and set a new header `x-hello-from-middleware1`
  const requestHeaders = new Headers(request.headers)
  requestHeaders.set('x-hello-from-middleware1', 'hello')
 
  // You can also set request headers in NextResponse.rewrite
  const response = NextResponse.next({
    request: {
      // New request headers
      headers: requestHeaders,
    },
  })
 
  // Set a new response header `x-hello-from-middleware2`
  response.headers.set('x-hello-from-middleware2', 'hello')
  return response
}
```

>[!warning] Bueno saber
>Evite configurar cabeceras grandes ya que podría causar el error **431 Request Header Fields Too Large** dependiendo de la configuración de su servidor web backend.

## Producir una respuesta

Puedes **responder desde Middleware directamente** devolviendo una instancia _Response_ o _NextResponse_. (Esto está disponible desde Next.js v13.1.0)

```jsx file:middleware.js 
import { NextResponse } from 'next/server'
import { isAuthenticated } from '@lib/auth'
 
// Limit the middleware to paths starting with `/api/`
export const config = {
  matcher: '/api/:function*',
}
 
export function middleware(request) {
  // Call our authentication function to check the request
  if (!isAuthenticated(request)) {
    // Respond with JSON indicating an error message
    return new NextResponse(
      JSON.stringify({ success: false, message: 'authentication failed' }),
      { status: 401, headers: { 'content-type': 'application/json' } }
    )
  }
}
```

____

## Indicadores avanzados de middleware

En la versión 13.1 de Next.js se introdujeron dos _flags_ adicionales para middleware, **skipMiddlewareUrlNormalize** y **skipTrailingSlashRedirect** para manejar casos de uso avanzados.

**skipTrailingSlashRedirect** permite deshabilitar las redirecciones predeterminadas de Next.js para añadir o eliminar barras finales, lo que permite un manejo personalizado dentro del middleware que puede permitir mantener la barra final para algunas rutas, pero no para otras, lo que facilita las migraciones incrementales.

```js file:next.config.js
module.exports = {
  skipTrailingSlashRedirect: true,
}
```

```jsx file:middleware.js
const legacyPrefixes = ['/docs', '/blog']
 
export default async function middleware(req) {
  const { pathname } = req.nextUrl
 
  if (legacyPrefixes.some((prefix) => pathname.startsWith(prefix))) {
    return NextResponse.next()
  }
 
  // apply trailing slash handling
  if (
    !pathname.endsWith('/') &&
    !pathname.match(/((?!\.well-known(?:\/.*)?)(?:[^/]+\/)*[^/]+\.\w+)/)
  ) {
    req.nextUrl.pathname += '/'
    return NextResponse.redirect(req.nextUrl)
  }
}
```

**skipMiddlewareUrlNormalize** permite deshabilitar la normalización de URL que Next.js hace para que el manejo de las visitas directas y las transiciones de cliente sean las mismas. Hay algunos casos avanzados en los que se necesita un control total utilizando la URL original que esto desbloquea.

```js file:next.config.js
module.exports = {
  skipMiddlewareUrlNormalize: true,
}
```

```jsx file:middleware.js
export default async function middleware(req) {
  const { pathname } = req.nextUrl
 
  // GET /_next/data/build-id/hello.json
 
  console.log(pathname)
  // with the flag this now /_next/data/build-id/hello.json
  // without the flag this would be normalized to /hello
}
```
