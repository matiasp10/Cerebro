El enrutador Next.js utiliza **enrutamiento centrado en el servidor** con **navegación del lado del cliente**. Admite estados de carga instantánea y renderización concurrente. Esto significa que _la navegación mantiene el estado del lado del cliente_, _evita costosas repeticiones de renderizado_, es _interrumpible_ y _no provoca condiciones de carrera_ (cuando un dispositivo o sistema intenta realizar dos o más operaciones al mismo tiempo).

Hay dos formas de navegar entre rutas:

- `<Link>` Component
- `useRouter` Hook
___

## `<Link>` Component

`<Link>` es un componente de React que amplía el elemento HTML `<a>` para _proporcionar precarga_ y _navegación del lado del cliente entre rutas_. Es la forma principal de navegar entre rutas en Next.js.

Para utilizar `<Link>`, impórtalo desde _next/link_ y pasa una _prop href_ al componente:

```jsx file:app/page.js
import Link from 'next/link';
 
export default function Page() {
  return <Link href="/dashboard">Dashboard</Link>;
}
```

Hay accesorios opcionales que puede pasar a `<Link>`.

[[Programación Web/Next/API/Link]]

## `useRouter()` Hook

El hook `useRouter` permite cambiar programáticamente las rutas dentro de los **Componentes Cliente**.

Para utilizar `useRouter`, impórtelo desde `next/navigation`, y llame al hook dentro de su _Componente Cliente_:

```jsx file:app/page.jsx
'use client';
 
import { useRouter } from 'next/navigation';
 
export default function Page() {
  const router = useRouter();
 
  return (
    <button type="button" onClick={() => router.push('/dashboard')}>
      Dashboard
    </button>
  );
}
```

El `useRouter` proporciona métodos como **push()**, **refresh()**, y más.

> [!tip] Recomendación
> Utilice el componente `<Link>` para navegar entre rutas a menos que tenga un requisito específico para utilizar useRouter.

## Como funciona la navegación

- Una transición de ruta se inicia utilizando `<Link>` o llamando a `router.push()`. 
- El enrutador actualiza la URL en la barra de direcciones del navegador. 
- El enrutador evita el trabajo innecesario reutilizando segmentos que no han cambiado (por ejemplo, nested layouts) de la caché del lado del cliente. Esto también se conoce como renderización parcial.  
- Si se cumplen las condiciones de la navegación suave, el enrutador obtiene el nuevo segmento de la caché en lugar de hacerlo del servidor. Si no, el enrutador realiza una navegación dura y obtiene la carga útil del componente de servidor del servidor.  
- Si se crea, la interfaz de usuario de carga se muestra desde el servidor mientras se obtiene la carga útil.  
- El enrutador utiliza la carga útil almacenada en caché o nueva para renderizar los nuevos segmentos en el cliente.

### Almacenamiento en caché del lado del cliente de los componentes renderizados del servidor

> [!warning] Bueno saber
> Esta caché del lado del cliente es diferente de la caché HTTP de Next.js del lado del servidor.

El nuevo enrutador _dispone de una caché cliente en memoria_ que almacena el _resultado renderizado de los componentes del servidor_ (carga útil). La caché está dividida por segmentos de ruta, lo que permite su invalidación a cualquier nivel y garantiza la coherencia entre renderizaciones simultáneas.

A medida que los usuarios navegan por la aplicación, _el enrutador almacenará en la caché la carga útil de los segmentos obtenidos previamente y de los segmentos prefijados_.

Esto significa que, en determinados casos, _el enrutador puede reutilizar la caché en lugar de realizar una nueva petición al servidor_. Esto mejora el rendimiento al evitar volver a obtener datos y volver a renderizar componentes innecesariamente.

### Invalidar la caché

Las acciones del servidor pueden utilizarse para revalidar datos a petición por ruta (`revalidatePath`) o por etiqueta de caché (`revalidateTag`).

### Prefetching

El prefetching es una forma de _precargar una ruta en segundo plano antes de que sea visitada_. El resultado renderizado de las rutas precargadas _se añade a la caché del cliente del enrutador_. Esto hace que la navegación a una ruta precargada sea casi instantánea.

Por defecto, las rutas se preconfiguran a medida que se hacen visibles en la ventana gráfica cuando se utiliza el componente `<Link>`. Esto puede ocurrir cuando la página se carga por primera vez o a través del desplazamiento. Las rutas también se pueden preconfigurar mediante programación utilizando el método prefetch del hook `useRouter()`.

#### Rutas estáticas y dinámicas

- Si la ruta es **estática**, _todas_ las cargas útiles del Componente Servidor para los segmentos de ruta se _precargarán_.
- Si la ruta es **dinámica**, _se precarga la carga útil desde el primer diseño compartido hasta el primer archivo loading.js_. Esto reduce el coste de precargar toda la ruta dinámicamente y permite estados de carga instantáneos para rutas dinámicas.

> [!warning] Bueno saber
> - La precarga sólo está activada en producción.
> - Se puede desactivar pasando `prefetch={false}` a `<Link>`.

### Navegación suave

En la navegación, se reutiliza la caché de los segmentos modificados (si existe) y no se realizan nuevas peticiones de datos al servidor.

#### Condiciones para la navegación suave

En la navegación, Next.js utilizará la navegación suave _si la ruta a la que se navega se ha preconfigurado_ y _no incluye segmentos dinámicos_ o tiene los mismos parámetros dinámicos que la ruta actual.

Por ejemplo, considere la siguiente ruta que incluye un segmento dinámico `[team]`: `/dashboard/[team]/*`. Los segmentos almacenados en caché debajo de `/dashboard/[team]/*` sólo se invalidarán cuando cambie el parámetro `[team]`.

- Navegar de `/dashboard/team-red/*` a `/dashboard/team-red/*` será una navegación suave.  
- Navegar de `/dashboard/team-red/*` a `/dashboard/team-blue/*` será una navegación dura.

### Navegación dura

Al navegar, la caché se invalida y el servidor vuelve a obtener los datos y a reproducir los segmentos modificados.

### Navegación Back/Forward

La navegación hacia atrás y hacia delante (evento _popstate_) tiene un comportamiento de navegación suave. Esto significa que la caché del cliente se reutiliza y la navegación es casi instantánea.

### Focus y gestión del Scroll

Por defecto, Next.js fijará el foco y desplazará a la vista el segmento que haya cambiado en la navegación.
