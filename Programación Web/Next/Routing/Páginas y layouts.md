El **App Router** dentro de Next.js 13 introdujo nuevas convenciones de archivos para crear fácilmente _páginas_, _layouts compartidos_ y _templates_.
___

## Páginas

Una página es una interfaz de usuario exclusiva de una ruta. Puede definir páginas exportando un componente desde un archivo ``page.js``. Utilice carpetas anidadas para definir una ruta y un archivo ``page.js`` para que la ruta sea accesible públicamente.

Crea tu primera página añadiendo un archivo page.js dentro del directorio de la app:

![[Pasted image 20230601094819.png]]

```jsx file:app/page.js
// `app/page.js` is the UI for the `/` URL
export default function Page() {
  return <h1>Hello, Home page!</h1>;
}
```

```jsx file:app/dashboard/page.js
// `app/dashboard/page.js` is the UI for the `/dashboard` URL
export default function Page() {
  return <h1>Hello, Dashboard Page!</h1>;
}
```

> [!warning] Bueno saber
> - Una página es siempre la hoja del subárbol de rutas. 
> - Se pueden utilizar las extensiones de archivo .js, .jsx o .tsx para las páginas.  
> - Se necesita un archivo page.js para que un segmento de ruta sea accesible públicamente.  
> - Por defecto, las páginas son componentes de servidor, pero pueden convertirse en componentes de cliente.  
> - Las páginas pueden obtener datos. Consulte la sección Obtención de datos para obtener más información.

## Layouts

Un diseño es una _interfaz de usuario compartida entre varias páginas_. En la navegación, los diseños conservan el estado, siguen siendo interactivos y no se vuelven a renderizar. _Los diseños también pueden anidarse_.

Puedes definir un **layout por defecto** exportando un componente React desde un archivo ``layout.js``. El componente debe aceptar un **prop children** que se rellenará con _un layout child (si existe)_ o _una página child_ durante la renderización.

![[Pasted image 20230601101312.png]]

```jsx file:app/dashboard/layout.js
export default function DashboardLayout({
  children, // will be a page or nested layout
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

> [!warning] Bueno saber
> - El _layout superior_ se denomina "**root layout**". Este layout obligatorio se comparte en todas las páginas de una aplicación. Los diseños raíz deben contener etiquetas html y body.
> - _Cualquier segmento de ruta puede definir opcionalmente su propio layout_. Estos layouts serán compartidos por todas las páginas de ese segmento.
> - Los _layouts en una ruta están anidados por defecto_. Cada layout padre envuelve a los layouts hijos que están debajo de él usando la _prop React children_.
> - Puedes usar _Grupos de Rutas_ para optar por segmentos de ruta específicos dentro y fuera de los diseños compartidos.
> - Por defecto, los _layouts son componentes de servidor_, pero **pueden convertirse** en componentes de cliente.
> - Los diseños **pueden obtener datos**.
> - _No es posible pasar datos entre un diseño padre y sus hijos_. Sin embargo, puedes obtener los mismos datos en una ruta más de una vez, y React deducirá automáticamente las peticiones sin afectar al rendimiento.
> - Los layouts _no tienen acceso a los segmentos de ruta actuales_. Para acceder a los segmentos de ruta, puedes utilizar **useSelectedLayoutSegment** o **useSelectedLayoutSegments** en un componente cliente.
> - Las extensiones de archivo **.js**, **.jsx** o **.tsx** se pueden utilizar para Layouts.
> - Se puede definir un archivo ``layout.js`` y ``page.js`` en la misma carpeta. El layout envolverá la página.

### Root layout (Requerido)

El **root layout** se define en el nivel superior del directorio de la aplicación y _se aplica a todas las rutas_. Este diseño permite modificar el HTML inicial devuelto por el servidor.

```jsx file:app/layout.js
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

> [!warning] Bueno saber
> - El directorio ``app`` **debe incluir un root layout**.
> - El diseño raíz debe _definir las etiquetas_ `<html>` y `<body>`, ya que Next.js no las crea automáticamente. 
> - Puedes usar el _soporte SEO integrado_ para gestionar elementos HTML `<head>`, por ejemplo, el elemento `<title>`.
> - Puede utilizar grupos de rutas para crear _múltiples root layouts_.
> - El diseño raíz es un _componente de servidor por defecto_ y **no** se puede establecer como un componente de cliente.

### Layouts anidadas

Los layouts definidos dentro de una carpeta (por ejemplo, `app/dashboard/layout.js`) se aplican a _segmentos de ruta específicos_ (por ejemplo, `acme.com/dashboard`) y se muestran cuando esos segmentos están activos. Por defecto, los layouts en la jerarquía de archivos están anidados, lo que significa que _envuelven a los diseños hijos a través de sus props hijas_.

![[Pasted image 20230601102803.png]]

```jsx file:app/dashboard/layout.js
export default function DashboardLayout({ children }) {
  return <section>{children}</section>;
}
```

Si combinaras los dos diseños anteriores, el root layout (`app/layout.js`) envolvería el diseño del dashboard (`app/dashboard/layout.js`), que envolvería segmentos de ruta dentro de `app/dashboard/*`.

Los dos layouts se anidarían así:

![[Pasted image 20230601102927.png]]

Puede utilizar los **Grupos de rutas** para optar por segmentos de ruta específicos dentro y fuera de los diseños compartidos.

## Templates

Los Templates son similares a los layouts en que envuelven cada diseño o página hijo. A diferencia de los layouts que persisten a través de las rutas y mantienen el estado, las templates **crean una nueva instancia para cada uno de sus hijos en la navegación**. Esto significa que cuando un usuario navega entre rutas que comparten una plantilla, se monta una _nueva instancia del componente_, se _recrean los elementos DOM_, _no se conserva el estado_ y se _re-sincronizan los efectos_.

Puede haber casos en los que necesite esos comportamientos específicos, y las templates serían una opción más adecuada que los diseños. Por ejemplo:

- **Animaciones de entrada/salida** usando CSS o librerías de animación.  
- Funciones que dependen de **useEffect** (por ejemplo, registro de loggins) y **useState** (por ejemplo, un formulario de comentarios).  
- Para **cambiar el comportamiento por defecto** del framework. Por ejemplo, los límites de suspensión dentro de las maquetaciones sólo muestran el fallback la primera vez que se carga la maquetación y no al cambiar de página. Para las plantillas, el fallback se muestra en cada navegación.

> [!tip] Recomendación 
> **Recomendamos utilizar Layouts** a menos que tenga una razón específica para utilizar Template.

Se puede definir una template exportando un componente React predeterminado desde un archivo template.js. El componente debe aceptar un prop children que serán segmentos anidados.

![[Pasted image 20230601103449.png]]

```jsx file:app/template.js
export default function Template({ children }) {
  return <div>{children}</div>;
}
```

La salida renderizada de un segmento de ruta con un diseño y una plantilla será como tal:

```output
<Layout>
  {/* Tenga en cuenta que la plantilla recibe una key única. */}
  <Template key={routeParam}>{children}</Template>
</Layout>
```

## Modificando `<head>`

En el directorio `app`, puedes modificar los elementos HTML `<head>` como **title** y **meta** utilizando el soporte SEO incorporado.

Los _metadatos pueden definirse exportando un objeto de metadatos_ o una _función generateMetadata_ en un archivo layout.js o page.js.

```jsx file:app/page.js
export const metadata = {
  title: 'Next.js',
};
 
export default function Page() {
  return '...';
}
```

> [!warning] Bueno saber
> **No debe añadir manualmente** etiquetas `<head>` como `<title>` y `<meta>` a los root layouts. En su lugar, debe utilizar la API de metadatos, que gestiona automáticamente requisitos avanzados como la transmisión y la eliminación de duplicados de elementos `<head>`.


