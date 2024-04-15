El elemento HTML `<main>` representa el contenido dominante del `<body>` de un documento. El área de contenido principal consiste en contenido que está directamente relacionado con el tema central de un documento, o con la funcionalidad central de una aplicación, o que lo amplía.

> [!danger] Cuidado!
> Un documento no debe tener más de un elemento `<main>` que no tenga especificado el atributo hidden.

### Categorías de contenidos

Flow content, palpable content.

### Contenidos permitidos

Flow content.

### Omisión de etiquetas

Ninguna; tanto la etiqueta inicial como la final son obligatorias.

### Padres autorizados

Donde se espera contenido de flujo, pero sólo si es un elemento principal jerárquicamente correcto.

### Función ARIA implícita

main

### Roles ARIA permitidos

Ninguna función permitida

### DOM interface

[[HTMLElement]]

## Atributos

Este elemento sólo incluye los [[Atributos globales]].

## Notas de uso

El contenido de un elemento `<main>` debe ser único para el documento. El contenido que se repite en un conjunto de documentos o secciones de documentos, como barras laterales, enlaces de navegación, información de copyright, logotipos del sitio y formularios de búsqueda, no debe incluirse a menos que el formulario de búsqueda sea la función principal de la página.

`<main>` no contribuye al esquema del documento; es decir, a diferencia de elementos como `<body>`, encabezados como h2, y similares, `<main>` no afecta al concepto que tiene el DOM de la estructura de la página. Es estrictamente informativo.

## Accesibilidad

### Punto de referencia

El elemento `<main>` se comporta como un punto de referencia principal. Los puntos de referencia pueden ser utilizados por la tecnología de asistencia para identificar rápidamente y navegar a grandes secciones del documento. Es preferible utilizar el elemento `<main>` en lugar de declarar **role="main"**, a menos que existan problemas de compatibilidad con navegadores anteriores.

### Saltar navegación

La navegación salteada, también conocida como "skipnav", es una técnica que permite a un usuario de tecnología de apoyo saltarse rápidamente grandes secciones de contenido repetido (navegación principal, banners informativos, etc.). Esto permite al usuario acceder más rápidamente al contenido principal de la página.

Si se añade un atributo id al elemento `<main>`, éste puede ser el destino de un enlace de navegación de salto.

```html
<body>
  <a href="#main-content">Skip to main content</a>

  <!-- navigation and header content -->

  <main id="main-content">
    <!-- main page content -->
  </main>
</body>
```

### Modo Lector

La funcionalidad del modo lector del navegador busca la presencia del elemento `<main>`, así como de elementos de encabezamiento y seccionamiento del contenido al convertir el contenido a una vista de lector especializada.