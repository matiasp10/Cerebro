Next.js 13 introdujo una nueva convención de archivos, ``error.js``, para ayudarte a manejar los errores en tu aplicación. Esta convención, basada en los límites de error de React ([[Límites de errores]]), permite mostrar una solución alternativa si se produce un error en el subárbol de la ruta.

## Límites de error

``error.js`` define el límite de error para un segmento de ruta y los hijos por debajo de él. Se puede utilizar para mostrar información específica sobre el error, y la funcionalidad para intentar recuperarse del error.

Crea un límite de error por defecto añadiendo un ``error.js`` como archivo dentro de una carpeta:

![[Pasted image 20221117201731.png]]

`app/feed/error.tsx`

```tsx
'use client';

import { useEffect } from 'react';

export default function Error({
  error,
  reset,
}: {
  error: Error;
  reset: () => void;
}) {
  useEffect(() => {
    // Log the error to an error reporting service
    console.error(error);
  }, [error]);

  return (
    <div>
      <p>Something went wrong!</p>
      <button onClick={() => reset()}>Reset error boundary</button>
    </div>
  );
}
```

Los límites de error deben ser **Componentes del Cliente**.

En la misma carpeta, ``error.js`` se anidará dentro de ``layout.js`` y ``template.js`` (si existen). Envolverá el archivo ``page.js`` y cualquier hijo debajo en un límite de error, pero no el layout o la template en el mismo nivel.

![[Pasted image 20221117201904.png]]

Durante un error, layouts y templates que se encuentren por encima del límite seguirán siendo interactivas y se conservará su estado. Para capturar cualquier error en el diseño o la plantilla, mueva el límite de error hasta el segmento padre.

## Tratando los errores del servidor

Si se lanza un error durante la obtención de datos o dentro de un componente de servidor, Next.js enviará el objeto **Error** resultante al archivo ``error.js`` más cercano como prop de **error**.

Cuando se ejecuta ``next dev``, el **error** será serializado y reenviado desde el componente servidor al cliente ``error.js``. Para garantizar la seguridad cuando se ejecuta ``next start`` en producción, se reenvía un mensaje de error genérico a **error** junto con un ``.digest`` que contiene un hash del mensaje de error. Este hash puede ser utilizado para corresponder a los registros del servidor.
