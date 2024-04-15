El archivo especial `loading.js` te ayuda a crear una IU de carga significativa con [[React.Suspense]] . Con esta convención, puede _mostrar un estado de carga instantánea desde el servidor mientras se carga el contenido de un segmento de ruta_, el nuevo contenido se intercambia automáticamente una vez que se completa la renderización.

![[Pasted image 20230601202350.png]]

___

## Estados de carga instantánea

Un **estado de carga instantánea** es una interfaz de usuario que se muestra inmediatamente después de la navegación. Puedes pre-renderizar indicadores de carga como _esqueletos_ y _spinners_, o _una parte pequeña pero significativa de futuras pantallas_ como una foto de portada, un título, etc. Esto ayuda a los usuarios a entender que la aplicación está respondiendo y proporciona una mejor experiencia de usuario.

Crea un estado de carga añadiendo un archivo `loading.js` dentro de una carpeta.

![[Pasted image 20230601202510.png]]

```jsx file:app/dashboard/loading.js
export default function Loading() {
  // You can add any UI inside Loading, including a Skeleton.
  return <LoadingSkeleton />;
}
```

En la misma carpeta, loading.js se anidará dentro de layout.js. Envolverá automáticamente el archivo page.js y cualquier hijo debajo en un límite `<Suspense>`.

![[Pasted image 20230601202600.png]]

> [!warning] Bueno saberlo
> - La **navegación es inmediata**, incluso con rutas centradas en el servidor.  
> - La **navegación es interrumpible**, lo que significa que para cambiar de ruta _no es necesario esperar a que el contenido de la ruta se cargue completamente_ antes de navegar a otra ruta.  
> - Los **layouts compartidos siguen siendo interactivos** mientras se cargan nuevos segmentos de ruta.

> [!tip] Recomendación
> Utilice la convención `loading.js` para los segmentos de ruta (layouts y páginas), ya que Next.js optimiza esta funcionalidad.

___

## Streaming con suspense

Además de `loading.js`, también puede crear manualmente **Suspense Boundaries** para sus propios componentes de interfaz de usuario. **App Router** admite el streaming con Suspense para los tiempos de ejecución _Node.js_ y _Edge_.

### ¿Que es streaming?

Para aprender cómo funciona Streaming en React y Next.js, es útil entender **Server-Side Rendering** (SSR) y sus limitaciones.

Con **SSR**, hay una serie de pasos que deben completarse antes de que un usuario pueda ver e interactuar con una página:

1. En primer lugar, **el servidor obtiene todos los datos** de una página determinada.  
2. A continuación, el servidor **genera el HTML** de la página.  
3. El **HTML, CSS y JavaScript de la página se envían al cliente**.  
4. Se **muestra una interfaz de usuario no interactiva** utilizando el HTML y CSS generados.  
5. Finalmente, **React hidrata la interfaz de usuario para hacerla interactiva**.

![[Pasted image 20230601204242.png]]

Estos pasos son _secuenciales_ y de _bloqueo_, lo que significa que _el servidor sólo puede renderizar el HTML de una página una vez que se han obtenido todos los datos_. Y, en el cliente, _React solo puede hidratar la interfaz de usuario una vez que se ha descargado el código de todos los componentes_ de la página.

**SSR** con React y Next.js ayuda a _mejorar el rendimiento_ de carga percibido mostrando una página no interactiva al usuario lo antes posible.

![[Pasted image 20230601204303.png]]

Sin embargo, _puede seguir siendo lento_, ya que es necesario completar la obtención de datos en el servidor antes de mostrar la página al usuario.

El **streaming** _permite dividir el HTML de la página en trozos más pequeños_ y enviarlos progresivamente del servidor al cliente.

![[Pasted image 20230601204322.png]]

Esto permite que _partes de la página se muestren antes_, sin esperar a que se carguen todos los datos antes de que se pueda mostrar la interfaz de usuario.

El streaming funciona bien con el modelo de componentes de React porque cada componente puede considerarse un **chunk**. Los componentes que tienen mayor prioridad (por ejemplo, la información del producto) o que no dependen de los datos pueden enviarse primero (por ejemplo, el diseño), y React puede iniciar la hidratación antes. Los componentes que tienen menor prioridad (por ejemplo, reseñas, productos relacionados) pueden enviarse en la misma petición al servidor después de que se hayan obtenido sus datos.

![[Pasted image 20230601204401.png]]

El streaming _es especialmente beneficioso cuando se quiere evitar que las solicitudes de datos largas bloqueen la renderización de la página_, ya que puede reducir el Tiempo hasta el primer byte (TTFB) y la Primera pintura de contenido (FCP). También ayuda a mejorar el Tiempo hasta la Interactividad (TTI), especialmente en dispositivos más lentos.

___

## Ejemplo

`<Suspense>` funciona _envolviendo un componente que realiza una acción asíncrona_ (por ejemplo, obtener datos), mostrando la interfaz de usuario de reserva (por ejemplo, esqueleto, spinner) mientras está sucediendo, y luego intercambiando en su componente una vez que la acción se completa.

```JSX file:app/dashboard/page.js
import { Suspense } from 'react';
import { PostFeed, Weather } from './Components';
 
export default function Posts() {
  return (
    <section>
      <Suspense fallback={<p>Loading feed...</p>}>
        <PostFeed />
      </Suspense>
      <Suspense fallback={<p>Loading weather...</p>}>
        <Weather />
      </Suspense>
    </section>
  );
}
```

Al usar Suspense, usted obtiene los beneficios de:

1. **Streaming Server Rendering** - Renderización progresiva de HTML desde el servidor al cliente.  
2. **Hidratación selectiva** - React prioriza qué componentes hacer interactivos primero basándose en la interacción del usuario.
___

## SEO

- Next.js esperará a que se complete la obtención de datos dentro de **generateMetadata** antes de transmitir la interfaz de usuario al cliente. Esto garantiza que la primera parte de una respuesta transmitida incluya etiquetas `<head>`.  
- Dado que el streaming se renderiza en el servidor, **no afecta al SEO**. Puede utilizar la herramienta Mobile Friendly Test de Google para ver cómo se muestra su página a los rastreadores web de Google y ver el HTML serializado (fuente).