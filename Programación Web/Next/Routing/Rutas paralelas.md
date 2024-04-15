El enrutamiento paralelo le _permite renderizar simultánea o condicionalmente una o más páginas en el mismo layout_. En el caso de secciones muy dinámicas de una aplicación, como dashboards y feeds de redes sociales, Parallel Routing puede utilizarse para implementar patrones de enrutamiento complejos.

Por ejemplo, puede mostrar simultáneamente las páginas de equipo y de análisis.

![[Pasted image 20230605105251.png]]

El enrutamiento paralelo _permite definir estados de error y carga independientes para cada ruta_, ya que se están transmitiendo de forma independiente.

![[Pasted image 20230605105304.png]]

El Enrutamiento Paralelo también le permite renderizar condicionalmente una ranura basándose en ciertas condiciones, como el estado de autenticación. Esto permite un código totalmente separado en la misma URL.

___

## Convención

Las rutas paralelas se crean utilizando ranuras con nombre. Las ranuras se definen con la convención `@folder` y se pasan al layout del mismo nivel como accesorios.

>[!note] Nota
>Las ranuras _no son segmentos de ruta y no afectan a la estructura de URL_. La ruta de archivo `/@team/members` sería accesible en `/members`.

Por ejemplo, la siguiente estructura de archivos define dos ranuras explícitas: `@analytics` y `@team`.

![[Pasted image 20230605105359.png]]

La estructura de carpetas anterior significa que el componente en `app/layout.js` ahora acepta las _props_ de las ranuras `@analytics` y `@team`, y puede renderizarlas en paralelo junto con la prop _children_:

```jsx file:app/layout.js
export default function Layout(props) {
  return (
    <>
      {props.children}
      {props.team}
      {props.analytics}
    </>
  );
}
```

> [!warning] Bueno saber
> La propiedad children es una ranura implícita que no necesita ser asignada a una carpeta. Esto significa que `app/page.js` es equivalente a `app/@children/page.js`.

___

## Rutas inigualables

Por defecto, el contenido mostrado dentro de una ranura coincidirá con la URL actual.

En el caso de una ranura no coincidente, el contenido que Next.js renderiza difiere en función de la técnica de enrutamiento y la estructura de carpetas.

### default.js

Puede definir un archivo `default.js` para que se muestre como alternativa cuando Next.js no pueda recuperar el estado activo de una ranura basándose en la URL actual.

Considere la siguiente estructura de carpetas. La ranura `@team` tiene un directorio de configuración, pero `@analytics` no.

![[Pasted image 20230605105541.png]]

Si navegas desde la raíz `/` a `/settings`, el contenido que se muestra es diferente en función del tipo de navegación y la disponibilidad del archivo `default.js`.

|                  | Con @analytics/default.js                          | sin @analytics/default.js                       |
| ---------------- | -------------------------------------------------- | ----------------------------------------------- |
| Navegación suave | `@team/settings/page.js` y `@analytics/page.js`    | `@team/settings/page.js` y `@analytics/page.js` |
| Navegación dura  | `@team/settings/page.js` y `@analytics/default.js` | 404                                             |

- En una **navegación suave** - Next.js renderizará el estado previamente activo de la ranura, incluso si no coincide con la URL actual.
- En una **navegación dura** - una navegación que requiere una recarga completa de la página - Next.js intentará primero renderizar el archivo default.js de la ranura no emparejada. Si no está disponible, se mostrará un 404.

>[!note] Nota
>El 404 para rutas no coincidentes ayuda a asegurar que no se renderice accidentalmente una ruta que no debería ser renderizada en paralelo.

___

## useSelectedLayoutSegment(s)

Tanto `useSelectedLayoutSegment` como `useSelectedLayoutSegments` aceptan una `parallelRoutesKey`, que permite leer el segmento de ruta activo dentro de esa ranura.

```jsx file:app/layout.js
'use client';
import { useSelectedLayoutSegment } from 'next/navigation';
 
export default async function Layout(props) {
  const loginSegments = useSelectedLayoutSegment('authModal');
  // ...
}
```

Cuando un usuario navega a `@authModal/login`, o `/login` en la barra de URL, `loginSegments` será igual a la cadena "_login_".

___

## Ejemplos

### Modals

El Enrutamiento Paralelo puede ser usado para renderizar modales.

![[Pasted image 20230605110012.png]]

```jsx file:app/layout.js
export default async function Layout(props) {
  return (
    <>
      {/* ... */}
      {props.authModal}
    </>
  );
}
```

```jsx file:app/@authModal/login/page.js
import { Modal } from 'components/modal';
 
export default function Login() {
  return (
    <Modal>
      <h1>Login</h1>
      {/* ... */}
    </Modal>
  );
}
```

Para asegurarte de que el contenido del modal no se muestra cuando no está activo, puedes crear un archivo default.js que devuelva null.

```jsx file:app/@authModal/login/default.js
export default function Default() {
  return null;
}
```

#### Rechazar un modal

Si un modal se inició a través de la navegación del cliente, por ejemplo utilizando `<Link href="/login">`, puede descartar el modal llamando a `router.back()` o utilizando un componente Link.

```jsx file:app/@authModal/login/page.jsx
'use client';
import { useRouter } from 'next/navigation';
import { Modal } from 'components/modal';
 
export default async function Login() {
  const router = useRouter();
  return (
    <Modal>
      <span onClick={() => router.back()}>Close modal</span>
      <h1>Login</h1>
      ...
    </Modal>
  );
}
```

Si desea navegar a otro lugar y descartar un modal, también puede utilizar una ruta de captura.

![[Pasted image 20230605110149.png]]

```jsx file:app/@authModal/[...catchAll]/page.js
export default function CatchAll() {
  return null;
}
```

>[!note] Nota
>Las rutas Catch-all prevalecen sobre default.js.

### Rutas condicionales 

Las rutas paralelas se pueden utilizar para implementar rutas condicionales. Por ejemplo, puede renderizar una ruta @dashboard o @login dependiendo del estado de autenticación.

```jsx file:app/layout.js
import { getUser } from '@/lib/auth';
 
export default function Layout({ params, dashboard, login }) {
  const isLoggedIn = getUser();
  return isLoggedIn ? dashboard : login;
}
```

![[Pasted image 20230605110251.png]]