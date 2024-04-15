Aparte de las convenciones de las carpetas y archivos, Next.js no se preocupa de cómo organizar y colocar los archivos del proyecto.

Esta página comparte el comportamiento predeterminado y las funciones que puede utilizar para organizar su proyecto.

- Colocación segura por defecto.
- Características de la organización de proyectos.
- Estrategias de organización de proyectos
___

## Colocación segura por defecto

En el directorio `app`, la jerarquía de carpetas anidadas define la estructura de rutas.

Cada carpeta representa un segmento de ruta que se asigna a un segmento correspondiente en una ruta URL.

Sin embargo, aunque la estructura de la ruta se define a través de carpetas, una ruta **no es accesible públicamente** hasta que se añade un archivo `page.js` o `route.js` a un segmento de ruta.

![[Pasted image 20230620104533.png]]

Incluso cuando una ruta se hace accesible públicamente, **sólo el contenido devuelto por `page.js` o `route.js` se envía al cliente**.

![[Pasted image 20230620104658.png]]

Esto significa que los archivos de proyecto pueden colocarse de forma segura dentro de segmentos de ruta en el directorio de la aplicación sin ser accidentalmente enrutables.

![[Pasted image 20230620104718.png]]

>[!warning] Bueno saber
>- Esto es diferente del directorio pages, donde cualquier archivo en pages es considerado una ruta.
>- Aunque puedes colocar los archivos de tu proyecto en app, no tienes por qué hacerlo. Si lo prefieres, puedes mantenerlos fuera del directorio app.

___

## Características de la organización de proyectos

Next.js ofrece varias funciones que te ayudarán a organizar tu proyecto.

### Private Folders

Las carpetas privadas pueden crearse anteponiendo un guion bajo a la carpeta: `_nombredecarpeta`

Esto indica que la carpeta es un detalle de implementación privado y no debe ser considerado por el sistema de enrutamiento, optando así por la carpeta y todas sus subcarpetas fuera de enrutamiento.

![[Pasted image 20230620111713.png]]

Dado que los archivos del directorio de aplicaciones pueden colocarse de forma segura por defecto, las carpetas privadas no son necesarias para la colocación. Sin embargo, pueden ser útiles para:

- Separar la lógica de interfaz de usuario de la lógica de enrutamiento.
- Organización coherente de los archivos internos de un proyecto y del ecosistema Next.js.
- Ordenar y agrupar archivos en editores de código.
- Evitar posibles conflictos de nombres con las futuras convenciones de archivos de Next.js.

>[!warning] Bueno saber
>- Aunque no es una convención del framework, también puedes considerar marcar los archivos fuera de las carpetas privadas como "privados" utilizando el mismo patrón de guión bajo.
>- Puede crear segmentos de URL que comiencen con un guión bajo anteponiendo al nombre de la carpeta %5F (la forma codificada en URL de un guión bajo): %5FnombreDeCarpeta.
>- Si no utilizas carpetas privadas, sería útil conocer las convenciones especiales de Next.js para evitar conflictos inesperados de nombres.

### Grupos de rutas

Los grupos de rutas pueden crearse encerrando una carpeta entre paréntesis: `(folderName)`

Esto indica que la carpeta tiene fines organizativos y no debe incluirse en la ruta URL de la ruta.

![[Pasted image 20230621121648.png]]

Los grupos de rutas son útiles para:

- Organización de rutas en grupos, por ejemplo, por sección del sitio, intención o equipo.  
- Habilitar diseños anidados en el mismo nivel de segmento de ruta:  
	- Creación de varios diseños anidados en el mismo segmento, incluidos varios diseños raíz. 
	- Añadir un diseño a un subconjunto de rutas en un segmento común.

___

### Directorio `src`

Next.js permite almacenar el código de la aplicación (incluida la aplicación) dentro de un directorio src opcional. Esto separa el código de la aplicación de los archivos de configuración del proyecto, que suelen estar en la raíz del proyecto.

![[Pasted image 20230621121827.png]]

____

### Module Path Aliases

Next.js admite alias de rutas de módulos que facilitan la lectura y el mantenimiento de las importaciones en archivos de proyecto profundamente anidados.

```jsx file:app/dashboard/settings/analytics/page.js
// before
import { Button } from '../../../components/button'
 
// after
import { Button } from '@/components/button'
```

____

## Estrategias de organización del proyecto

No hay una manera "correcta" o "incorrecta" cuando se trata de organizar tus propios archivos y carpetas en un proyecto Next.js.

En la sección siguiente se ofrece una visión general de muy alto nivel de las estrategias más comunes. Lo más sencillo es elegir una estrategia que funcione para ti y tu equipo y ser coherente en todo el proyecto.

> [!warning] Bueno saber
> En nuestros ejemplos de abajo, estamos usando las carpetas components y lib como marcadores de posición generalizados, su nomenclatura no tiene ningún significado especial para el framework y tus proyectos pueden usar otras carpetas como ui, utils, hooks, styles, etc.

### Almacenar los archivos del proyecto fuera de `app`

Esta estrategia almacena todo el código de la aplicación en carpetas compartidas en la raíz del proyecto y mantiene el directorio de `app` únicamente para fines de enrutamiento.

![[Pasted image 20230621122103.png]]

### Almacenar los archivos del proyecto en carpetas de nivel superior dentro de `app`

Esta estrategia almacena todo el código de la aplicación en carpetas compartidas en la raíz del directorio de `app`.

![[Pasted image 20230621122200.png]]

### Dividir archivos de proyecto por característica o ruta

Esta estrategia almacena el código de aplicación compartido globalmente en el directorio raíz de `app` y divide el código de aplicación más específico en los segmentos de ruta que los utilizan.

![[Pasted image 20230621122246.png]]
