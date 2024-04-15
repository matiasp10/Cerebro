El directorio app introduce la compatibilidad con el **streaming** y React **Suspense** durante el renderizado del servidor en los tiempos de ejecución Node.js y Edge.

## Conceptos

El _streaming_ permite **enviar de forma incremental la interfaz de usuario desde el servidor al cliente**, renderizando progresivamente los componentes y las páginas. Esto permite mostrar el contenido más rápidamente, sin esperar a que se complete la obtención de los datos antes de renderizar la interfaz de usuario.

El _streaming_ es particularmente beneficioso cuando hay una solicitud de red lenta para recuperar los datos. En lugar de bloquear la renderización de toda la página debido a la lentitud de la API o de la búsqueda en la base de datos...

![[Pasted image 20221120101158.png]]

La interfaz de usuario puede enviarse de forma incremental al cliente. Los usuarios no tienen que esperar a que se cargue toda la página para empezar a interactuar con ella.

![[Pasted image 20221120101222.png]]

Con Next.js, su interfaz de usuario puede ser resistente a las velocidades inconsistentes de la red. Las solicitudes rápidas pueden ser transmitidas al cliente tan pronto como estén listas. Las **solicitudes lentas**, o **inconsistentes**, pueden envolverse en un **límite de suspensión** para mostrar un componente de reserva hasta que se haya completado la renderización en el servidor.

Cuando se utiliza la renderización _no-streaming_ en el servidor, se bloquea la transferencia de datos del servidor al cliente hasta que se haya completado la renderización de toda la página. Una vez que los datos se transfieren al cliente, la página no es interactiva hasta que se descargue y ejecute el paquete de JavaScript del lado del cliente.

![[Pasted image 20221120101505.png]]

Con el directorio ``app``, los componentes pueden ser introducidos de forma incremental. Esto reduce tanto el tiempo hasta el primer byte (**TTFB**) como la primera pintura de contenido (**FCP**) para mostrar la UI desde el servidor.

![[Pasted image 20221120101554.png]]

## Uso

Puede transmitir la interfaz de usuario en Next.js utilizando **loading.js** (para todo un segmento de ruta) o con los **límites de suspensión** (para una interfaz de usuario de carga más granular).

### Loading UI instantáneo 

El archivo especial ``loading.js`` permite _mostrar un estado de carga instantáneo desde el servidor mientras se carga el contenido de un segmento de ruta_. Una vez que haya finalizado la obtención de datos en el segmento de ruta, la interfaz de usuario de carga se cambiará por la página.

``app/dashboard/loading.tsx``

```tsx
export default function Loading() {
  return <p>Loading...</p>
}
```

![[Pasted image 20221120101744.png]]

### Limites de suspensión

Los límites de React Suspense ([[React.Suspense]]) permiten la carga granular de la interfaz de usuario para la obtención de datos. Next.js renderizará el contenido en el servidor y enviará progresivamente las actualizaciones a través de flujos HTTP al cliente.

Un límite de suspensión envuelve un componente React. Mientras la renderización del componente está suspendida, _se mostrará el fallback del límite de suspensión_.

``app/dashboard/page.tsx``

```tsx
import { Suspense } from "react";
import { PostFeed, Weather } from "./Components";

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

![[Pasted image 20221120104222.png]]

