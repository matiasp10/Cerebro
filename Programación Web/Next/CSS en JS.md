> **Advertencia**: Las bibliotecas CSS-in-JS que requieren JavaScript en tiempo de ejecución **no están actualmente soportadas en Server Components**. El uso de CSS-in-JS con las nuevas características de React, como Server Components y Streaming, requiere que los autores de las librerías soporten la última versión de React, incluyendo la renderización concurrente.

Las siguientes librerías son compatibles con los Componentes del Cliente en el directorio app:

- styled-jsx
- styled-components

> **Nota**: Estamos probando diferentes librerías CSS-in-JS y añadiremos más ejemplos de librerías que soporten las características de React 18 y/o el directorio app.

Si quieres dar estilo a los Server Components, te recomendamos que utilices CSS Modules u otras soluciones que emitan archivos CSS, como PostCSS o Tailwind CSS.

## Configurando CSS-in-JS en `app`

La configuración de CSS-in-JS es un proceso de **tres pasos** que implica:

1. Un registro de estilos para recoger todas las reglas CSS en un render.
2. El nuevo hook ``useServerInsertedHTML`` para inyectar las reglas antes de cualquier contenido que pueda utilizarlas.
3. Un componente de cliente que envuelve su aplicación con el registro de estilos durante la renderización inicial del lado del servidor.

