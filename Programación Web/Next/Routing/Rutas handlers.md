Los Manejadores de Ruta le permiten crear manejadores de solicitud personalizados para una ruta dada usando las APIs de Solicitud y Respuesta Web.

![[Pasted image 20230605200306.png]]

> [!warning] Bueno saber
> Los controladores de rutas sólo están disponibles en el directorio de aplicaciones. Son el equivalente de las rutas API dentro del directorio de páginas, lo que significa que no es necesario utilizar las rutas API y los controladores de ruta juntos.

___

## Convención

Los **Route Handlers** se definen en un archivo `route.js|ts` dentro del directorio de la app:

```jsx file:app/api/route.js
export async function GET(request: Request) {}
```

Los manejadores de ruta pueden anidarse dentro del directorio de la aplicación, de forma similar a `page.js` y `layout.js`. Pero no puede haber un archivo route.js en el mismo nivel de segmento de ruta que `page.js`.

### Métodos HTTP admitidos

Se admiten los siguientes métodos _HTTP: GET, POST, PUT, PATCH, DELETE, HEAD y OPTIONS_. Si se llama a un método no soportado, Next.js devolverá una respuesta **405 Method Not Allowed**.

### API `NextRequest` y `NextResponse` ampliadas

Además de soportar `Request` y `Response` nativos. Next.js los amplía con `NextRequest` y `NextResponse` para proporcionar prácticos ayudantes para casos de uso avanzados.

___

## Comportamiento

### Gestores de rutas estáticas

Los Manejadores de Ruta se evalúan estáticamente por defecto cuando se utiliza el método GET con el objeto Response.

```jsx file:app/items/route.js
import { NextResponse } from 'next/server';
 
export async function GET() {
  const res = await fetch('https://data.mongodb-api.com/...', {
    headers: {
      'Content-Type': 'application/json',
      'API-Key': process.env.DATA_API_KEY,
    },
  });
  const data = await res.json();
 
  return NextResponse.json({ data });
}
```

### Manejadores de rutas dinámicas

Los handlers de rutas se evalúan dinámicamente cuando:  
  
- Utilizando el objeto Request con el método GET.  
- Usando cualquiera de los otros métodos HTTP.  
- Usando funciones dinámicas como cookies y cabeceras.  
- Las Opciones de Configuración de Segmento especifican manualmente el modo dinámico.

Por ejemplo:

```jsx file:app/products/api/route.js
import { NextResponse } from 'next/server';
 
export async function GET(request) {
  const { searchParams } = new URL(request.url);
  const id = searchParams.get('id');
  const res = await fetch(`https://data.mongodb-api.com/product/${id}`, {
    headers: {
      'Content-Type': 'application/json',
      'API-Key': process.env.DATA_API_KEY,
    },
  });
  const product = await res.json();
 
  return NextResponse.json({ product });
}
```

Del mismo modo, el método POST hará que el Manejador de Ruta sea evaluado dinámicamente.

```jsx file:app/items/route.js
import { NextResponse } from 'next/server';
 
export async function POST() {
  const res = await fetch('https://data.mongodb-api.com/...', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'API-Key': process.env.DATA_API_KEY,
    },
    body: JSON.stringify({ time: new Date().toISOString() }),
  });
 
  const data = await res.json();
 
  return NextResponse.json(data);
}
```

>[!note] Nota
>Anteriormente, las Rutas API podían utilizarse para casos de uso como la gestión de envíos de formularios. Los Manejadores de Ruta no son probablemente la solución para estos casos de uso. Recomendaremos el uso de mutaciones para esto cuando esté listo.

### Solución de rutas

Se puede considerar que una ruta es la primitiva de enrutamiento de nivel más bajo.

- No participan en diseños o navegaciones del lado del cliente como page.  
- No puede haber un archivo route.js en la misma ruta que `page.js`.

| Page                 | Route              | Result   |
| -------------------- | ------------------ | -------- |
| `app/page.js`        | `app/route.js`     | Conflict |
| `app/page.js`        | `app/api/route.js` | Valid    |
| `app/[user]/page.js` | `app/api/route.js` | Valid    |

Cada archivo route.js o page.js asume todos los verbos HTTP para esa ruta.

```jsx file:app/page.js
export default function Page() {
  return <h1>Hello, Next.js!</h1>;
}
 
// ❌ Conflict
// `app/route.js`
export async function POST(request) {}
```

___

## Ejemplos

Los siguientes ejemplos muestran cómo combinar Route Handlers con otras APIs y características de Next.js.

### Revalidando datos estáticos

Puede revalidar la obtención de datos estáticos utilizando la opción next.revalidate:

```jsx file:app/items/route.js
import { NextResponse } from 'next/server';
 
export async function GET() {
  const res = await fetch('https://data.mongodb-api.com/...', {
    next: { revalidate: 60 }, // Revalidate every 60 seconds
  });
  const data = await res.json();
 
  return NextResponse.json(data);
}
```

Como alternativa, puede utilizar la opción de configuración revalidar segmento:

```jsx
export const revalidate = 60;
```

### Funciones dinámicas

Los Route Handlers se pueden utilizar con funciones dinámicas de Next.js, como cookies y cabeceras.

#### Cookies

Puede leer cookies con cookies de next/headers. Esta función de servidor puede ser llamada directamente en un Route Handler, o anidada dentro de otra función.

Esta instancia de cookies es de sólo lectura. Para establecer las cookies, debe devolver una nueva respuesta utilizando la función Set-Cookie

```jsx file:app/api/route.js
import { cookies } from 'next/headers';
 
export async function GET(request) {
  const cookieStore = cookies();
  const token = cookieStore.get('token');
 
  return new Response('Hello, Next.js!', {
    status: 200,
    headers: { 'Set-Cookie': `token=${token}` },
  });
}
```

Alternativamente, puede utilizar abstracciones sobre las API Web subyacentes para leer cookies (NextRequest):

```jsx file:app/api/route.js
export async function GET(request) {
  const token = request.cookies.get('token');
}
```

#### Headers

Puede leer cabeceras con cabeceras de next/headers. Esta función del servidor puede ser llamada directamente en un Route Handler, o anidada dentro de otra función.

Esta instancia de cabeceras es de sólo lectura. Para establecer las cabeceras, es necesario devolver una nueva respuesta con nuevas cabeceras.

```jsx file:app/api/route.js
import { headers } from 'next/headers';
 
export async function GET(request) {
  const headersList = headers();
  const referer = headersList.get('referer');
 
  return new Response('Hello, Next.js!', {
    status: 200,
    headers: { referer: referer },
  });
}
```

Como alternativa, puede utilizar abstracciones sobre las API Web subyacentes para leer las cabeceras (NextRequest):

```jsx file:app/api/route.js
export async function GET(request) {
  const requestHeaders = new Headers(request.headers);
}
```

### Redirecciones 

```jsx file:app/api/route.js
import { redirect } from 'next/navigation';
 
export async function GET(request) {
  redirect('https://nextjs.org/');
}
```

### Segmentos de rutas dinamicos

Los Manejadores de Ruta pueden utilizar Segmentos Dinámicos para crear manejadores de solicitud a partir de datos dinámicos.

```jsx file:app/items/[slug]/route.js
export async function GET(
  request: Request,
  {
    params,
  }: {
    params: { slug: string };
  },
) {
  const slug = params.slug; // 'a', 'b', or 'c'
}
```

|Route|Example URL|`params`|
|---|---|---|
|`app/items/[slug]/route.js`|`/items/a`|`{ slug: 'a' }`|
|`app/items/[slug]/route.js`|`/items/b`|`{ slug: 'b' }`|
|`app/items/[slug]/route.js`|`/items/c`|`{ slug: 'c' }`|

### Streaming

```jsx
// https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream#convert_async_iterator_to_stream
function iteratorToStream(iterator) {
  return new ReadableStream({
    async pull(controller) {
      const { value, done } = await iterator.next();
 
      if (done) {
        controller.close();
      } else {
        controller.enqueue(value);
      }
    },
  });
}
 
function sleep(time) {
  return new Promise((resolve) => {
    setTimeout(resolve, time);
  });
}
 
const encoder = new TextEncoder();
 
async function* makeIterator() {
  yield encoder.encode('<p>One</p>');
  await sleep(200);
  yield encoder.encode('<p>Two</p>');
  await sleep(200);
  yield encoder.encode('<p>Three</p>');
}
 
export async function GET() {
  const iterator = makeIterator();
  const stream = iteratorToStream(iterator);
 
  return new Response(stream);
}
```

### Request body

Puede leer el cuerpo de la solicitud utilizando los métodos estándar de la Web API:

```jsx file:app/items/route.js
import { NextResponse } from 'next/server';
 
export async function POST(request) {
  const res = await request.json();
  return NextResponse.json({ res });
}
```

### CORS

Puede establecer cabeceras CORS en una respuesta utilizando los métodos estándar de la Web API:

```jsx file:app/api/route.js
export async function GET(request) {
  return new Response('Hello, Next.js!', {
    status: 200,
    headers: {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE, OPTIONS',
      'Access-Control-Allow-Headers': 'Content-Type, Authorization',
    },
  });
}
```

### Edge y Node.js Runtimes

Los controladores de rutas disponen de una API web isomórfica para admitir sin problemas los tiempos de ejecución Edge y Node.js, incluida la compatibilidad con el streaming. Dado que los controladores de ruta utilizan la misma configuración de segmento de ruta que las páginas y los diseños, admiten funciones muy esperadas, como los controladores de ruta de regeneración estática de uso general.

Puede utilizar la opción de configuración del segmento de tiempo de ejecución para especificar el tiempo de ejecución:

```jsx
export const runtime = 'edge'; // 'nodejs' is the default
```

### Respuestas no-UI

Puede utilizar Route Handlers para devolver contenido que no sea UI. Ten en cuenta que sitemap.xml, robots.txt, iconos de aplicaciones e imágenes open graph tienen soporte integrado.

```jsx file:app/rss.xml/route.js
export async function GET() {
  return new Response(`<?xml version="1.0" encoding="UTF-8" ?>
<rss version="2.0">
 
<channel>
  <title>Next.js Documentation</title>
  <link>https://nextjs.org/docs</link>
  <description>The React Framework for the Web</description>
</channel>
 
</rss>`);
}
```

### Opciones de configuración de segmentos

Los manejadores de ruta utilizan la misma configuración de segmento de ruta que las páginas y los diseños.

```jsx file:app/items/route.js
export const dynamic = 'auto';
export const dynamicParams = true;
export const revalidate = false;
export const fetchCache = 'auto';
export const runtime = 'nodejs';
export const preferredRegion = 'auto';
```


