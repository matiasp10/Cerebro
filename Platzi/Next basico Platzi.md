1.

Next.js es una herramienta que nos permite:

Renderizado híbrido-estático o desde el servidor (SSR), compatibilidad con TypeScript, agrupación inteligente, búsqueda previa de rutas y más.

2.

¿Qué es ESLint?

Una herramienta para analizar código e identificar posibles errores en el código JavaScript.

<mark style="background: #FF5582A6;">3.

¿Cuál es el recurso asignado en jsconfig.js para manejar las rutas de nuestros archivos?

alias

REPASAR CLASE</mark>

La respuesta correcta es la opción "c": paths es el recurso asignado en jsconfig.js para manejar las rutas de nuestros archivos.

En un archivo jsconfig.js, el objeto "paths" es un recurso utilizado para asignar alias a rutas de archivos o carpetas específicas en un proyecto de JavaScript. Esto permite que los archivos y carpetas se refieran a través de un alias en lugar de una ruta absoluta, lo que puede hacer que el código sea más fácil de leer y mantener.

Por ejemplo, si tenemos una carpeta "src" con un archivo "main.js" dentro, podríamos utilizar el objeto "paths" para asignar un alias a la ruta de ese archivo de la siguiente manera:

```js
{
  "compilerOptions": {
    "paths": {
      "src/*": ["src/*"]
    }
  }
}
```

De esta manera, en lugar de tener que escribir la ruta completa al archivo "main.js" cada vez que lo queramos importar en otro archivo, podríamos simplemente utilizar el alias "src/main.js". Esto hace que el código sea más legible y fácil de mantener.

4.

¿De dónde importamos el componente recomendado de Next.js para implementar imágenes?

next/image

5.

¿Cuál es la forma recomendada de implementar enlaces en Next.js?

Con el componente: `<Link href="/">Link</Link> de next/link`

6.

¿Qué es React.Fragment?

Un React Fragment es un componente dentro de la API de React que agrupa componentes sin agregar nodos extra.

<mark style="background: #FF5582A6;">7.

¿Qué función cumplen las keys en React?

Las keys nos permiten optimizar componentes en el DOM virtual.</mark>

La respuesta correcta es la opción "a": Las keys nos permiten diferenciar los elementos únicos en el DOM virtual.

En React, las "keys" son un atributo opcional que se puede asignar a elementos dentro de un componente. Las keys se utilizan para diferenciar elementos únicos dentro del DOM virtual de React, que es una representación en memoria del DOM real.

Cuando React renderiza un componente, crea una representación virtual del DOM en memoria y luego la compara con la representación anterior para determinar qué cambios hacer en el DOM real. Si no se utilizan keys para identificar elementos únicos, React puede tener dificultades para determinar qué elementos han cambiado y puede tener que volver a renderizar todo el componente en lugar de solo los elementos que han cambiado. Esto puede afectar el rendimiento de la aplicación y hacer que sea más lenta.

Por lo tanto, es importante utilizar keys para identificar elementos únicos en el DOM virtual de React para ayudar a React a determinar qué elementos han cambiado y cómo actualizar el DOM real de manera más eficiente. Las keys deben ser valores únicos y no deben cambiarse a medida que el componente se actualiza.

8.

¿Qué es el server side rendering?

Nos permite que el servidor sea quien genere el contenido html/css/js en tiempo de ejecución.

<mark style="background: #FF5582A6;">9.

¿Qué es Static Site Generation?

Static Site Generation es el proceso de compilar y renderizar (crear el contenido html/css/JavaScript) en tiempo de deploy.

REPASAR CLASE</mark>

La respuesta correcta es la opción "b": Static Site Generation es el proceso de compilar y renderizar (crear el contenido html/css/JavaScript) en tiempo de compilación.

Static Site Generation es una técnica utilizada para generar sitios web estáticos a partir de contenido y plantillas. Esto se hace mediante el uso de herramientas de Static Site Generation, que toman el contenido y las plantillas como entrada y generan el sitio web como salida. El proceso de compilación y renderización se realiza en tiempo de compilación, lo que significa que se realiza una vez y el resultado es un sitio web completo que se puede servir a los usuarios sin necesidad de procesamiento adicional en el lado del servidor.

Los sitios web estáticos tienen muchas ventajas, como un rendimiento más rápido y una mayor seguridad, ya que no hay código dinámico que ejecutar en el lado del servidor. Por lo tanto, Static Site Generation se ha vuelto cada vez más popular en los últimos años como una manera de crear sitios web de alto rendimiento y fáciles de mantener.

10.

¿Qué es una aplicación web progresiva (PWA)?

Son aplicaciones web que permiten incorporar comportamientos de una app nativa.

11.

¿Qué es Next.js?

Framework

12.

Vercel es la empresa que construyó y le da mantenimiento a Next.js, por lo que ofrecen un muy buen soporte para desplegar proyectos creados con esta tecnología.

Verdadero

13.

¿Para qué sirve Next/Head?

Exponer un componente donde podemos integrar elementos al encabezado de nuestra aplicación.

14.

¿Qué es useContext?

Un React Hook que nos permite acceder a algún estado global.