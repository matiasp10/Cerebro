## Creando rutas

Next.js utiliza un enrutador basado en un sistema de archivos en el que se utilizan carpetas para definir las rutas.

Cada carpeta representa un segmento de ruta que se asigna a un segmento de URL. Para crear una ruta anidada, puede anidar carpetas unas dentro de otras.

![[Pasted image 20221116210154.png]]

Se utiliza un archivo ``page.js`` especial para que los segmentos de la ruta sean accesibles al público.

![[Pasted image 20221116210218.png]]

En este ejemplo, la ruta URL ``/dashboard/analytics`` **no es accesible al público** porque no tiene un archivo ``page.js`` correspondiente. Esta carpeta podría utilizarse para almacenar componentes, hojas de estilo, imágenes u otros archivos colocados.

> [!warning] Bueno de saber
> Las extensiones de archivo .js, .jsx o .tsx pueden utilizarse para archivos especiales.

## Creación de IU

Se utilizan convenciones de archivo especiales para crear una interfaz de usuario para cada segmento de ruta. Las más comunes son las páginas, que muestran la interfaz de usuario exclusiva de una ruta, y los diseños, que muestran la interfaz de usuario compartida por varias rutas.

Por ejemplo, para crear tu primera página, añade un archivo page.js dentro del directorio de la app y exporta un componente React:

```jsx file:page.js
export default function Page() {
  return <h1>Hello, Next.js!</h1>;
}
```