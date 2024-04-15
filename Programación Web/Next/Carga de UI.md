Next.js 13 introdujo una nueva convención de archivos, ``loading.js``, para ayudarte a crear una IU de carga significativa con React Suspense ([[React.Suspense]]). Con esta convención, puedes mostrar un estado de carga instantáneo desde el servidor mientras se carga el contenido de un segmento de ruta, el nuevo contenido se intercambia automáticamente una vez que se completa la renderización.

![[Pasted image 20221117200843.png]]

## Estados de carga instantánea

Los estados de carga instantánea permiten pre-renderizar indicadores de carga como **esqueletos** y **spinners**, o una parte pequeña pero significativa de futuras pantallas como una foto de portada, un título, etc. Esto ayuda a los usuarios a entender que la aplicación está respondiendo y proporciona una mejor experiencia de usuario.

Crea un estado de carga añadiendo un archivo ``loading.js`` dentro de una carpeta.

![[Pasted image 20221117201039.png]]

`app/dashboard/loading.tsx`

```tsx
export default function Loading() {
  // You can add any UI inside Loading, including a Skeleton.
  return <LoadingSkeleton />
}
```

En la misma carpeta, ``loading.js`` estará anidado dentro de ``layout.js``. Envolverá el archivo ``page.js`` y cualquier hijo debajo en un límite ``<Suspense>``.

![[Pasted image 20221117201150.png]]

> **Es bueno saberlo**:
> 
> - La navegación es inmediata, incluso con el enrutamiento centrado en el servidor.
> - La navegación es interrumpible, lo que significa que no hay que esperar a que el contenido de la ruta se cargue completamente antes de navegar a otra ruta.
> - Los diseños compartidos siguen siendo interactivos mientras se cargan los nuevos segmentos de la ruta.

## Definir manualmente los límites del suspenso

Además de ``loading.js``, también se pueden crear manualmente límites de suspensión.

A diferencia de ``loading.js``, donde la navegación se produce inmediatamente y la interfaz de usuario de carga se muestra antes de que se complete la solicitud al servidor. 
Cuando se definen manualmente los Límites de Suspensión, la navegación ocurrirá después de que se cargue el nuevo segmento.

> **Recomendación**: Utilice la convención loading.js para los segmentos de ruta (diseños y páginas) ya que Next.js optimiza esta funcionalidad. Se recomienda utilizar los Límites Suspensivos en sus propios componentes.