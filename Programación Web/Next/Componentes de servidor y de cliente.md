Los componentes de servidor y cliente permiten a los desarrolladores crear aplicaciones que abarcan el servidor y el cliente, combinando la rica interactividad de las aplicaciones del lado del cliente con el rendimiento mejorado de la renderización tradicional del servidor.

Esta página repasará las diferencias entre los componentes de servidor y de cliente y cómo utilizarlos en tu aplicación Next.js.

## Componentes de servidor

Todos los componentes dentro del directorio app son React Server Components _por defecto_, incluyendo los archivos especiales y los componentes colocados. Esto le permite adoptar automáticamente los componentes de servidor sin ningún trabajo adicional y lograr un gran rendimiento desde el principio.

### ¿Por qué componentes de servidor?

Los **componentes de servidor** (RFC) permiten a los desarrolladores aprovechar mejor la infraestructura del servidor. Por ejemplo, las grandes dependencias que antes repercutían en el tamaño del paquete de JavaScript en el cliente pueden permanecer enteramente en el servidor, lo que permite mejorar el rendimiento. Sin embargo, el directorio ``app`` sigue necesitando **JavaScript**.

Cuando se cargue una ruta, se cargará el **Runtime** de Next.js y React, que es almacenable en caché y de tamaño predecible. Este tiempo de ejecución **no aumenta** de tamaño a medida que la aplicación crece. Además, el tiempo de ejecución se carga de forma **asíncrona**, lo que permite que el HTML del servidor se mejore progresivamente en el cliente.

Sólo se añade JavaScript adicional cuando se necesita la interactividad del lado del cliente en su aplicación mediante el uso de componentes de cliente.

## Componentes de cliente

Los Client Components se renderizan en el cliente. Con Next.js, los Client Components también pueden ser **pre-renderizados en el servidor** e **hidratados en el cliente**.

### Convención

Para utilizar un componente de cliente, cree un archivo dentro de app y añada la directiva **"use client"** en la parte superior del archivo (antes de cualquier importación).

`app/Counter.js`

```jsx
'use client';

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

Sólo es necesario marcar los componentes como **'use client'** cuando utilizan hooks de cliente como **useState** o **useEffect**. Es mejor dejar los componentes que no dependen de los hooks de cliente sin la directiva para que puedan ser renderizados automáticamente como un componente de servidor cuando no son importados por otro componente de cliente. Esto ayuda a garantizar la menor cantidad de JavaScript del lado del cliente.

## Cuando usar Server vs Client Components?

Para simplificar la decisión entre los componentes de servidor y los de cliente, recomendamos utilizar los **componentes de servidor** (por defecto en el directorio ``app``) hasta que tenga la necesidad de utilizar un componente de cliente.

Esta tabla resume los diferentes casos de uso de los Componentes Servidor y Cliente:

| Para que lo necesitamos?                                                           | Server Component | Client Component |
| ---------------------------------------------------------------------------------- | ---------------- | ---------------- |
| Fetch Data                                                                         | ✅               | ⚠️               |
| Access backend resources (directly)                                                | ✅               | ❌               |
| Keep sensitive information on the server (access tokens, API keys, etc)            | ✅               | ❌               |
| Keep large dependencies on the server / Reduce client-side JavaScript              | ✅               | ❌               |
| Add interactivity and event listeners (`onClick()`, `onChange()`, etc)             | ❌               | ✅               |
| Use State and Lifecycle Effects (`useState()`, `useReducer()`, `useEffect()`, etc) | ❌               | ✅               |
| Use browser-only APIs                                                              | ❌               | ✅               |
| Use custom hooks that depend on state, effects, or browser-only APIs               | ❌               | ✅               |
| Use React Class components                                                         | ❌               |  ✅                |

## Paquetes de terceros

La directiva **"use client"** es una nueva característica de React que se introdujo como parte de Server Components. Dado que los Server Components son tan nuevos, los paquetes de terceros en el ecosistema apenas están comenzando a agregarla a los componentes que usan características sólo de cliente como **useState**, **useEffect** y **createContext**.

En la actualidad, muchos componentes de paquetes npm que utilizan funciones sólo para clientes aún no tienen la directiva. Estos componentes de terceros funcionarán como se espera dentro de sus propios componentes de cliente, ya que ellos mismos tienen la directiva "use client", pero no funcionarán dentro de los componentes de servidor.

Por ejemplo, digamos que ha instalado el hipotético paquete acme-carousel que tiene un componente <AcmeCarousel />. Este componente utiliza useState, pero aún no tiene la directiva "use client".

Si utiliza <AcmeCarousel /> dentro de un componente cliente, funcionará como se espera:

`app/gallery.js`

```jsx
'use client';

import { useState } from 'react';
import { AcmeCarousel } from 'acme-carousel';

export default function Gallery() {
  let [isOpen, setIsOpen] = useState(false);

  return (
    <div>
      <button onClick={() => setIsOpen(true)}>View pictures</button>

      {/* 🟢 Works, since AcmeCarousel is used within a Client Component */}
      {isOpen && <AcmeCarousel />}
    </div>
  );
}
```

Sin embargo, si intenta utilizarlo directamente dentro de un componente de servidor, verá un error:

`app/page.js`

```jsx
import { AcmeCarousel } from 'acme-carousel';

export default function Page() {
  return (
    <div>
      <p>View pictures</p>

      {/* 🔴 Error: `useState` can not be used within Server Components */}
      <AcmeCarousel />
    </div>
  );
}
```

Esto se debe a que Next.js no sabe que <AcmeCarousel /> está utilizando funciones sólo para clientes.

Para solucionar esto, puedes envolver los componentes de terceros que dependen de las funciones solo para clientes en tus propios componentes de cliente:

`app/carousel.js`

```jsx
'use client';

import { AcmeCarousel } from 'acme-carousel';

export default AcmeCarousel;
```

Ahora, puede utilizar <Carousel /> directamente dentro de un componente de servidor:

`app/page.js`

```jsx
import Carousel from './carousel';

export default function Page() {
  return (
    <div>
      <p>View pictures</p>

      {/* 🟢 Works, since Carousel is a Client Component */}
      <Carousel />
    </div>
  );
}
```

No esperamos que necesites envolver la mayoría de los componentes de terceros, ya que es probable que los utilices dentro de los componentes de cliente. Sin embargo, una excepción son los componentes proveedores, ya que dependen del estado y el contexto de React, y suelen ser necesarios en la raíz de una aplicación.

## Obtención de datos

Aunque es posible obtener datos en los componentes de cliente, recomendamos obtener datos en los componentes de servidor a menos que tenga una razón específica para obtener datos en el cliente. Trasladar la obtención de datos al servidor mejora el rendimiento y la experiencia del usuario.

## Pasar props del servidor a los componentes del cliente (serialización)

Los objetos pasados desde los componentes del servidor a los componentes del cliente deben ser serializables. Esto significa que los valores como las funciones, las fechas, etc., no pueden ser pasados directamente a los componentes del cliente.

> **¿Dónde está el límite de la red?**
> 
> En el directorio `app`, el límite de la red está entre los componentes del servidor y los componentes del cliente. Esto es diferente del directorio `pages` donde el límite está entre `getStaticProps/getServerSideProps` y los componentes de página. Los datos obtenidos dentro de los Componentes del Servidor no necesitan ser serializados ya que no cruzan el límite de la red a menos que sean pasados a un Componente del Cliente.

## Mantener el código del servidor fuera de los componentes del cliente (envenenamiento)

Dado que los módulos de JavaScript pueden ser compartidos entre los componentes del servidor y del cliente, es posible que el código que sólo estaba destinado a ejecutarse en el servidor se cuele en el cliente.

Por ejemplo, tomemos la siguiente función de obtención de datos:

`lib/data.js`

```js
export async function getData() {
  let res = await fetch("https://external-service.com/data", {
    headers: {
      authorization: process.env.API_KEY,
    },
  });

  return res.json();
}
```

A primera vista, parece que ``getData`` funciona tanto en el servidor como en el cliente. Pero como la **variable de entorno** API_KEY no lleva el prefijo _NEXT_PUBLIC_, es una variable privada a la que sólo se puede acceder en el servidor. Next.js sustituye las variables de entorno privadas por la cadena vacía en el código del cliente para evitar la filtración de información segura.

Como resultado, aunque ``getData()`` puede ser importada y ejecutada en el cliente, no funcionará como se espera. Y aunque hacer la variable pública haría que la función funcionara en el cliente, filtraría información sensible.

Por lo tanto, esta función fue escrita con la intención de que sólo se ejecutara en el servidor.

Para prevenir este tipo de uso involuntario del código del servidor por parte del cliente, podemos utilizar el paquete de sólo-servidor para dar a otros desarrolladores un error de compilación si alguna vez importan accidentalmente uno de estos módulos en un componente de cliente.

Para utilizar el paquete de sólo-servidor, primero instale el paquete:

```bash
npm install server-only
```

A continuación, importe el paquete en cualquier módulo que contenga código sólo para el servidor:

`lib/data.js`

```js
import "server-only";

export async function getData() {
  let resp = await fetch("https://external-service.com/data", {
    headers: {
      authorization: process.env.API_KEY,
    },
  });

  return resp.json();
}
```

Ahora, cualquier componente de cliente que importe ``getData()`` recibirá un error de ``build`` explicando que este módulo sólo puede ser utilizado en el servidor.

El paquete correspondiente client-only se puede utilizar para marcar los módulos que contienen código sólo para el cliente - por ejemplo, el código que accede al objeto ``window``.

## Contexto

La mayoría de las aplicaciones de React se basan en el **contexto** para compartir datos entre componentes, ya sea directamente a través de ``createContext``, o indirectamente a través de componentes proveedores importados de bibliotecas de terceros.

En Next.js 13, el contexto está totalmente soportado dentro de los Componentes Cliente, pero no puede ser creado o consumido directamente dentro de los Componentes Servidor. Esto se debe a que los Componentes Servidor no tienen estado React (ya que no son interactivos), y el contexto se utiliza principalmente para renderizar componentes interactivos en lo profundo del árbol después de que se haya actualizado algún estado React.

Discutiremos las alternativas para compartir datos entre los Server Components, pero primero, echemos un vistazo a cómo usar el contexto dentro de los Client Components.

### Usar context en los componentes de cliente

Todas las APIs de contexto son totalmente compatibles con los componentes del cliente:

`app/sidebar.js`

```jsx
'use client';

import { createContext, useState } from 'react';

const SidebarContext = createContext();

export function Sidebar() {
  const [isOpen, setIsOpen] = useState();

  return (
    <SidebarContext.Provider value={{ isOpen }}>
      <SidebarNav />
    </SidebarContext.Provider>
  );
}

function SidebarNav() {
  let { isOpen } = useContext(SidebarContext);

  return (
    <div>
      <p>Home</p>

      {isOpen && <Subnav />}
    </div>
  );
}
```

Sin embargo, los proveedores de contexto son típicamente renderizados cerca del root de la app para compartir preocupaciones globales, como el tema actual. Debido a que el contexto no está soportado en los Componentes de Servidor, tratar de crear un contexto en la raíz de su aplicación causará un error:

`app/layout.js`

```jsx
import { createContext } from 'react';

// 🔴 createContext is not supported in Server Components
const ThemeContext = createContext();

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <ThemeContext.Provider value="dark">
          {children}
        </ThemeContext.Provider>
      </body>
    </html>
  );
}
```

Para solucionar esto, cree su contexto y renderice su proveedor dentro de un Componente Cliente:

`app/theme-provider.js`

```jsx
'use client';

import { createContext } from 'react';

const ThemeContext = createContext();

export default function ThemeProvider({ children }) {
  return (
    <ThemeContext.Provider value="dark">
      {children}
    </ThemeContext.Provider>
  );
}
```

Su componente de servidor podrá ahora renderizar directamente su proveedor ya que ha sido marcado como un componente de cliente:

`app/layout.js`

```jsx
import ThemeProvider from './theme-provider';

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <ThemeProvider>{children}</ThemeProvider>
      </body>
    </html>
  );
}
```

Con el proveedor renderizado en la raíz, todos los demás componentes del cliente en toda la aplicación podrán consumir este contexto.

> **Nota**: Deberías renderizar los proveedores tan profundamente como sea posible en el árbol - observa cómo `ThemeProvider` sólo envuelve `{children}` en lugar de todo el documento `<html>`. Esto hace que sea más fácil para Next.js optimizar las partes estáticas de sus componentes de servidor.

### Renderización de proveedores de contexto de terceros en los componentes del servidor

Los paquetes npm de terceros a menudo incluyen Proveedores que necesitan ser renderizados cerca de la raíz de su aplicación. Si estos proveedores incluyen la directiva "use client", pueden ser renderizados directamente dentro de tus Server Components. Sin embargo, dado que los Server Components son tan nuevos, muchos proveedores de terceros no habrán añadido la directiva todavía.

Si intentas renderizar un proveedor de terceros que no tiene "use client", se producirá un error:

`app/layout.js`

```jsx
import { ThemeProvider } from 'acme-theme';

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        {/* 🔴 Error: `createContext` can't be used in Server Components */}
        <ThemeProvider>{children}</ThemeProvider>
      </body>
    </html>
  );
}
```

Para solucionar esto, envuelva los proveedores de terceros en su propio componente de cliente:

`app/providers.js`

```jsx
'use client';

import { ThemeProvider } from 'acme-theme';
import { AuthProvider } from 'acme-auth';

export function Providers({ children }) {
  return (
    <ThemeProvider>
      <AuthProvider>
        {children}
      </AuthProvider>
    </ThemeProvider>
  );
}
```

Ahora, puede importar y renderizar ``<Providers />`` directamente dentro del root:

```jsx
import { Providers } from './providers';

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

Con los proveedores renderizados en la raíz, todos los componentes y ganchos de estas bibliotecas funcionarán como se espera dentro de sus propios Componentes Cliente.

Una vez que una biblioteca de terceros haya añadido **"use client"** a su código de cliente, podrá eliminar el componente de cliente envolvente.

### Compartiendo la data entre server components

Dado que los Server Components no son interactivos y, por lo tanto, no leen el estado de React, no necesitas toda la potencia del contexto para compartir datos. Puedes utilizar patrones nativos de JavaScript como singletons globales dentro del ámbito del módulo si tienes datos comunes a los que varios Server Components necesitan acceder.

Por ejemplo, se puede utilizar un módulo para compartir una conexión de base de datos a través de múltiples componentes:

`utils/database.js`

```js
export const db = new DatabaseConnection(...);
```

`app/users/layout.js`

```jsx
import { db } from "@utils/database";

export async function UsersLayout() {
  let users = await db.query(...);
  // ...
}
```

`app/users/[id]/page.js`

```jsx
import { db } from "@utils/database";

export async function DashboardPage() {
  let user = await db.query(...);
  // ...
}
```

En el ejemplo anterior, tanto el layout como la page necesitan hacer consultas a la base de datos. Cada uno de estos componentes comparte el acceso a la base de datos mediante la importación del módulo ``@utils/database``.

### Compartir solicitudes fetch entre server component

Cuando se obtienen datos, es posible que se quiera compartir el resultado de una obtención entre una página o layout y algunos de sus componentes hijos. Esto es un acoplamiento innecesario entre los componentes y puede llevar a pasar props de un lado a otro entre los componentes.

En su lugar, recomendamos situar la obtención de datos junto al componente que los consume. Las solicitudes de obtención se deduplican automáticamente en los componentes del servidor, de modo que cada segmento de la ruta puede solicitar exactamente los datos que necesita sin preocuparse por las solicitudes duplicadas. Next.js leerá el mismo valor de la caché de obtención.

## Mover los componentes del cliente a las hojas

Para mejorar el rendimiento de su aplicación, le recomendamos que mueva los componentes del cliente a las hojas de su árbol de componentes siempre que sea posible.

Por ejemplo, puede tener un ``Layout`` que tiene elementos estáticos (por ejemplo, logo, enlaces, etc) y una barra de búsqueda interactiva que utiliza estado.

En lugar de convertir todo el diseño en un componente de cliente, mueva la lógica interactiva a un componente de cliente (por ejemplo, ``<SearchBar />``) y mantenga su layout como un componente de servidor. Esto significa que no tienes que enviar todo el Javascript del componente del layout al cliente.

`app/layout.js`

```ts
// SearchBar is a Client Component
import SearchBar from './SearchBar';
// Logo is a Server Component
import Logo from './Logo';

// Layout is a Server Component by default
export default function Layout({ children }) {
  return (
    <>
      <nav>
        <Logo />
        <SearchBar />
      </nav>
      <main>{children}</main>
    </>
  );
}
```

## Importando Server Components en Client Components

Los componentes del servidor y del cliente pueden intercalarse en el mismo árbol de componentes. Entre bastidores, **React fusionará el trabajo de ambos entornos**.

Sin embargo, en React, hay una restricción en torno a la importación de Componentes de Servidor dentro de Componentes de Cliente porque los Componentes de Servidor pueden tener código sólo de servidor (por ejemplo, utilidades de base de datos o sistema de archivos).

Por ejemplo, importar un Componente Servidor en un Componente Cliente no funcionará:

`app/ClientComponent.js`

```ts
'use client';

// ❌ This pattern will not work. You cannot import a Server
// Component into a Client Component
import ServerComponent from './ServerComponent';

export default function ClientComponent() {
  return (
    <>
      <ServerComponent />
    </>
  );
}
```

Puede pasar un Componente Servidor como hijo o prop de un Componente Cliente. Puede hacerlo envolviendo ambos componentes en otro Componente Servidor. Por ejemplo:

`app/page.js`

```tsx
// ✅ This pattern works. You can pass a Server Component
// as a child or prop of a Client Component.
import ClientComponent from "./ClientComponent";
import ServerComponent from "./ServerComponent";

// Pages are Server Components by default
export default function Page() {
  return (
    <ClientComponent>
      <ServerComponent />
    </ClientComponent>
  );
}
```

Con este patrón, React sabrá que necesita renderizar ``<ServerComponent/>`` en el servidor antes de enviar el resultado (que no contiene ningún código exclusivo del servidor) al cliente. Desde la perspectiva del componente cliente, su hijo ya estará renderizado.

Este patrón ya se aplica en los layouts y páginas con el prop de los hijos, por lo que no es necesario crear un componente envolvente adicional.

Por ejemplo, el componente ``<ClientLayout/>`` aceptará el componente ``<ServerPage/>`` como su hijo:

`app/dashboard/layout.js`

```tsx
'use client';

// The Dashboard Layout is a Client Component
export default function ClientLayout({ children }) {
  // Can use useState / useEffect here
  return (
    <>
      <h1>Layout</h1>
      {children}
    </>
  );
}
```

`app/dashboard/page.js`

```tsx
// The Dashboard Page is a Server Component that will be
// passed to Dashboard Layout
export default function ServerPage() {
  return (
    <>
      <p>Page</p>
    </>
  );
}
```