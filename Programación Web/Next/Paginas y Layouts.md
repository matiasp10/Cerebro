Next.js 13 introdujo nuevas convenciones de archivos para permitirte crear fácilmente páginas, diseños compartidos y plantillas. 

## Pages

Una pagina es una UI que es unica para una ruta. Las paginas pueden definirse exportando un componente desde un archivo `page.js`. Puedes utilizar carpetas anidadas para definir rutas y archivos ``page.js`` para que una ruta sea accesible públicamente.

Crea tu primera página añadiendo un archivo ``page.js`` dentro del directorio de la aplicación:

![[Pasted image 20221117130939.png]]

`app/page.js`

```jsx
// `app/page.js` is the UI for the root `/` URL
export default function Page() {
  return <h1>Hello, Next.js!</h1>;
}
```

> Es bueno saberlo:
> 
> - Una página es siempre la hoja del subárbol de rutas.
> - Las extensiones de archivo js, jsx o tsx pueden utilizarse para las páginas.
> - Se requiere un archivo page.js para que un segmento de ruta sea accesible públicamente.
> - Las páginas son componentes de servidor por defecto, pero pueden ser configuradas como componentes de cliente.
> - Las páginas pueden obtener datos. Consulte la sección de obtención de datos para obtener más información.

## Layouts

Un ``layout`` es una interfaz de usuario que se comparte entre varias páginas. En la navegación, los layouts conservan el estado, siguen siendo interactivos y no se vuelven a renderizar. Los layouts también pueden ser anidados.

Un layout puede ser definido por defecto exportando un componente React desde un archivo layout.js. El componente debe aceptar una proposición children que será rellenada con una página, otro layout anidado, UI de carga, o UI de error durante la renderización.

![[Pasted image 20221117131634.png]]

`app/dashboard/layout.tsx`

```tsx
export default function DashboardLayout({
  children, // will be a page or nested layout
}: {
  children: React.ReactNode,
}) {
  return (
    <section>
      {/* Include shared UI here e.g. a header or sidebar */}
      <nav></nav>

      {children}
    </section>
  );
}
```

> Es bueno saberlo:
> 
> - El layout superior se llama "Root layout". Es un layout obligatorio que se comparte en todas las páginas de una aplicación. Debe contener las etiquetas html y body.
> - Cualquier segmento de la ruta puede definir opcionalmente su propio layout. Estos layouts serán compartidos por todas las páginas del segmento.
> - Los layouts en una ruta están anidados por defecto. Cada layout ancestral envuelve el layout que está por debajo de él usando hijos.
> - Puede utilizar los Grupos de Ruta para optar por segmentos de ruta específicos dentro y fuera de los layouts compartidos.
> - Los layouts son componentes de servidor por defecto, pero pueden ser configurados como componentes de cliente.
> - Los layouts pueden obtener datos.
> - No es posible pasar datos entre un diseño padre y sus hijos. Sin embargo, puedes obtener los mismos datos en una ruta más de una vez, y React deducirá automáticamente las peticiones sin afectar al rendimiento.
> - Las extensiones de archivo js, jsx, o tsx pueden ser usadas para los Layouts.
> - Se puede definir un archivo layout.js y page.js en la misma carpeta. El layout envolverá la página.

## Root Layout (Obligatorio)

El Root layout se define en el nivel superior del directorio de la aplicación y se aplica a todas las rutas. Este diseño permite modificar el HTML inicial devuelto por el servidor.

`app/layout.tsx`

```jsx
export default function RootLayout({ children }: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

> Es bueno saberlo:
> 
> - El directorio "app" debe incluir un Root layout.
> - El Root layout debe definir las etiquetas `<html>`, y `<body>` ya que Next.js no las crea automáticamente.
> - Puedes utilizar el archivo especial `head.js` para gestionar los elementos HTML `<head>` que cambian entre los segmentos de la ruta. Por ejemplo, el elemento `<title>`.
> - Puede utilizar grupos de rutas para crear múltiples diseños raíz.

Migración desde el directorio pages: El diseño raíz reemplaza los archivos ``_app.js`` y ``_document.js``.

## Layouts anidadas

Los layouts definidos dentro de una carpeta se aplican a segmentos específicos de la ruta y se muestran cuando esos segmentos están activos. Por defecto, los diseños en la jerarquía de archivos están anidados, lo que significa que envuelven a los layouts hijos a través de su ``children props``.

![[Pasted image 20221117132836.png]]

``app/dashboard/layout.tsx``

```jsx
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return <section>{children}</section>;
}
```

Si se combinaran los dos layouts anteriores, el Root layout (``app/layout.js``) envolvería el layout del dashboard (``app/dashboard/layout.js``), que envolvería los segmentos de ruta dentro de ``app/dashboard/*``.

Los dos layouts se anidarían así:

![[Pasted image 20221117133029.png]]

## Templates

Las **templates** son similares a los ``layouts`` en el sentido de que envuelven cada layout o página hijo. A diferencia de los layouts que persisten a través de las rutas y mantienen el estado, las templates **crean una nueva instancia para cada uno de sus hijos en la navegación**. Esto significa que cuando un usuario navega entre rutas que comparten una template, se monta una nueva instancia del componente, se recrean los elementos del DOM, no se conserva el estado y se resincronizan los efectos.

Puede haber casos en los que necesites esos comportamientos específicos, y las templates serían una opción más adecuada que las rutas. Por ejemplo:

- **Animaciones** de entrada/salida usando CSS o librerías de animación.
- Funciones que dependen de **useEffect** (por ejemplo, registro de vistas de página) y **useState** (por ejemplo, un formulario de comentarios por página).
- Para **cambiar el comportamiento por defecto del framework**. Por ejemplo, los límites de suspensión dentro de las maquetas sólo muestran el fallback la primera vez que se carga la maqueta y no cuando se cambia de página. Para las plantillas, el fallback se muestra en cada navegación.

> **Recomendación**: Recomendamos el uso de Layouts a menos que tenga una razón específica para usar Template.

Una plantilla puede ser definida exportando un componente React por defecto desde un archivo ``template.js``. El componente debe aceptar una ``children prop`` que serán segmentos anidados.

![[Pasted image 20221117133510.png]]

`app/template.tsx`

```jsx
export default function Template({ children }: {
  children: React.ReactNode
}) {
  return <div>{children}</div>;
}
```

La salida renderizada de un segmento de ruta con un layout y una template será como tal:

`Output`

```jsx
<Layout>
  {/* Note that the template is given a unique key. */}
  <Template key={routeParam}>{children}</Template>
</Layout>
```

## Modificando ``<head>``

En el directorio app, puedes modificar los elementos HTML ``<head>`` como el **título** y la **meta** utilizando un nuevo archivo especial ``head.js``. Esto sustituye a **next/head** en el directorio pages.

![[Pasted image 20221117134718.png]]

`app/post/[slug]/head.tsx`

```jsx
async function getPost(slug) {
  const res = await fetch('...');
  return res.json();
}

export default async function Head({ params }) {
  const post = await getPost(params.slug);

  return (
    <>
      <title>{post.title}</title>
    </>
  )
}
```

> Es bueno saberlo:
> 
> - Por ahora, sólo se permite devolver ciertas etiquetas desde la exportación de Head:
> 	- `<title>`
> 	- `<meta>`
> 	- `<link>` (sólo si tiene el atributo precedence)
> 	- `<script>` (sólo si tiene el atributo async)
> - Si necesitas obtener datos para Head y también utilizar los mismos datos en un diseño o página, puedes obtener los datos dos veces y Next.js deducirá automáticamente las solicitudes.

**Advertencia**: Actualmente, la exportación de ``<Head>`` no se vuelve a renderizar en la transición del lado del cliente usando next/link, sólo en la renderización inicial y en las recargas. Para solucionar esto en el caso de ``<title>``, puedes utilizar un componente cliente con useEffect que actualice ``document.title``. Planeamos arreglar esto en una futura versión.