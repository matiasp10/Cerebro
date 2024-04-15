La convención del archivo `error.js` le permite manejar con elegancia los errores en tiempo de ejecución en rutas anidadas.

- Envolver automáticamente un segmento de ruta y sus hijos anidados en un **React Error Boundary**.   
- Cree una _interfaz de usuario de errores adaptada a segmentos específicos_ utilizando la jerarquía del sistema de archivos para ajustar la granularidad.  
- _Aislar los errores en los segmentos afectados_ manteniendo el resto de la aplicación funcional.  
- _Añadir funcionalidad para intentar recuperarse de un error_ sin una recarga completa de la página.

Cree una interfaz de usuario de error añadiendo un archivo `error.js` dentro de un segmento de ruta y exportando un componente React:

![[Pasted image 20230602094110.png]]

```jsx file:app/dashboard/error.js
'use client'; // Error components deben ser Client Components
 
import { useEffect } from 'react';
 
export default function Error({ error, reset }) {
  useEffect(() => {
    // Log the error to an error reporting service
    console.error(error);
  }, [error]);
 
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button
        onClick={
          // Attempt to recover by trying to re-render the segment
          () => reset()
        }
      >
        Try again
      </button>
    </div>
  );
}
```

___

## ¿Como funciona `error.js`?

![[Pasted image 20230602094238.png]]

- `error.js` crea automáticamente un **React Error Boundary** que envuelve un segmento hijo anidado o un componente `page.js`.  
- El componente React exportado desde el archivo `error.js` se utiliza como componente de reserva.  
- Si se lanza un error dentro del limite de error, _se contiene el error y se renderiza el componente fallback_.  
- Cuando el componente de error fallback está activo, _los layouts por encima del limite de error mantienen su estado y siguen siendo interactivos_, y el componente de error puede mostrar la funcionalidad para recuperarse del error.

## Recuperación de errores

A veces, la causa de un error puede ser temporal. En estos casos, basta con volver a intentarlo para resolver el problema.  

Un componente de error puede utilizar la función `reset()` para _pedir al usuario que intente recuperarse del error_. Cuando se ejecuta, la función intentará volver a mostrar el contenido del contorno de error. Si tiene éxito, el componente de error fallback es reemplazado por el resultado de la re-presentación.

```jsx file:app/dashboard/error.js
'use client';
 
export default function Error({ error, reset }) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

## Rutas anidadas

Los componentes React creados a través de archivos especiales se renderizan en una jerarquía anidada específica.  
  
Por ejemplo, una ruta anidada con dos segmentos que incluyen archivos `layout.js` y `error.js` se representa en la siguiente jerarquía de componentes simplificada:

![[Pasted image 20230605094352.png]]

La jerarquía de componentes anidados tiene implicaciones para el comportamiento de los archivos `error.js` a través de una ruta anidada:  
  
- Los errores burbujean hasta el límite de _error padre más cercano_. Esto significa que un archivo `error.js` gestionará los errores de todos sus segmentos hijos anidados. Se puede conseguir una interfaz de usuario de errores más o menos granular colocando archivos `error.js` en diferentes niveles de las carpetas anidadas de una ruta.  
- Un límite de `error.js` no manejará errores lanzados en un componente `layout.js` en el mismo segmento porque el límite de error está anidado dentro de ese componente layout.

## Gestión de errores en los layouts

Los límites de `error.js` _no detectan los errores lanzados en los componentes_ `layout.js` o `template.js` del mismo segmento. Esta jerarquía intencionada mantiene la IU importante que se comparte entre rutas hermanas (como la navegación) visible y funcional cuando se produce un error.  
  
Para gestionar errores dentro de un layout o template específicos, coloca un archivo `error.js` en el segmento padre del diseño.  
  
Para gestionar errores dentro del layout o template raíz, utiliza una variación de `error.js` llamada `global-error.js`.

## Gestión de errores en los root layouts

El límite raíz `app/error.js` **no captura los errores** lanzados en el componente raíz `app/layout.js` o `app/template.js`.  
  
Para gestionar específicamente los errores en estos componentes raíz, utiliza una variación de `error.js` llamada `app/global-error.js` ubicada en el directorio raíz de la app. 
  
A diferencia del `error.js` raíz, el límite de error `global-error.js` **envuelve toda la aplicación**, y su componente fallback reemplaza el diseño raíz cuando está activo. Debido a esto, es importante tener en cuenta que `global-error.js` debe definir sus propias etiquetas `<html>` y `<body>`.  
  
`global-error.js` es la interfaz de usuario de error menos granular y se puede considerar un "cajón de sastre" para la **gestión de errores de toda la aplicación**. Es poco probable que se active con frecuencia, ya que los componentes raíz suelen ser menos dinámicos, y otros límites `error.js` atraparán la mayoría de los errores.  
  
Aunque se defina un `error.js` global, se recomienda definir un `error.js` raíz cuyo componente de reserva se mostrará en el layout raíz, que incluye la interfaz de usuario y la marca compartidas globalmente.

```jsx file:app/global-error.js
'use client';
 
export default function GlobalError({ error, reset }) {
  return (
    <html>
      <body>
        <h2>Something went wrong!</h2>
        <button onClick={() => reset()}>Try again</button>
      </body>
    </html>
  );
}
```

## Errores del servidor

Si se produce un error durante la obtención de datos o dentro de un componente de servidor, _Next.js enviará el objeto Error resultante al archivo `error.js` más cercano como prop de error_.  
  
Al ejecutar next dev, el error será serializado y reenviado desde el Componente Servidor al cliente `error.js`. Para garantizar la seguridad al ejecutar next start en producción, se reenvía un mensaje de error genérico a error junto con un .digest que contiene un hash del mensaje de error. Este hash se puede utilizar para corresponder a los registros del servidor.
