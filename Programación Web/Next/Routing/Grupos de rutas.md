En el directorio `app`, las carpetas anidadas se asignan normalmente a rutas URL. Sin embargo, puede marcar una carpeta como **Grupo de rutas** para evitar que la carpeta se incluya en la ruta URL de la ruta.

Esto le permite organizar sus segmentos de ruta y archivos de proyecto en grupos lógicos sin afectar a la estructura de rutas URL.

Los grupos de rutas son útiles para:

- **Organizar las rutas en grupos**, por ejemplo, por sección de obra, intención o equipo.
- Habilitación de **layouts anidados en el mismo nivel de segmento de ruta**:
	- Creación de varios layouts anidados en el mismo segmento, incluidos varios root layout.
	- Añadir un layout a un subconjunto de rutas en un segmento común.

___

## Convención 

Se puede crear un grupo de rutas encerrando el nombre de una carpeta entre paréntesis: `(folderName)`

___

## Ejemplos

### Organizar rutas sin afectar a la ruta URL

Para organizar las rutas sin afectar a la URL, cree un grupo para mantener juntas las rutas relacionadas. _Las carpetas entre paréntesis se omitirán en la URL_ (por ejemplo, `(marketing)` o `(shop)`).

![[Pasted image 20230601191153.png]]

Aunque las rutas dentro de `(marketing)` y `(shop)` comparten la misma jerarquía de URL, puede crear un diseño diferente para cada grupo añadiendo un archivo `layout.js` dentro de sus carpetas.

![[Pasted image 20230601191327.png]]

### Optar por segmentos específicos en un layout

Para optar por rutas específicas en un layout, cree un nuevo grupo de rutas (por ejemplo, `(shop)`) y mueva las rutas que comparten el mismo layout en el grupo (por ejemplo, `account` y `cart`). Las rutas fuera del grupo no compartirán el layout (por ejemplo, `checkout`).

![[Pasted image 20230601191451.png]]

### Creación de varios root layouts

Para crear varios **root layouts**, elimine el archivo `layout.js` de nivel superior y añada un archivo `layout.js` dentro de cada grupo de rutas. Esto es útil para dividir una aplicación en _secciones que tienen una interfaz de usuario o experiencia completamente diferente_. Las etiquetas `<html>` y `<body>` deben añadirse a cada root layout.

![[Pasted image 20230601191609.png]]

En el ejemplo anterior, tanto (`marketing`) como (`shop`) tienen su propio diseño raíz.

___

> [!warning] Bueno saberlo
> - La denominación de los grupos de rutas **no tiene ningún significado especial**, salvo el de organización. No afectan a la ruta URL.
> - Las rutas que incluyen un grupo de rutas no deben resolverse a la misma ruta URL que otras rutas. Por ejemplo, dado que los grupos de rutas no afectan a la estructura de URL, `(marketing)/about/page.js` y `(shop)/about/page.js` resolverían a `/about` y **provocarían un error**.
> - Si utiliza varios root layouts sin un archivo layout.js de nivel superior, su archivo home `page.js` _debe definirse en uno de los grupos de rutas_, Por ejemplo: `app/(marketing)/page.js`.
> - La navegación a través de varios root layouts provocará una carga completa de la página (a diferencia de la navegación del lado del cliente). Por ejemplo, navegar desde `/cart` que utiliza `app/(shop)/layout.js` a `/blog` que utiliza `app/(marketing)/layout.js` **provocará una carga completa de la página**. Esto sólo se aplica a los _múltiples root layouts_.
