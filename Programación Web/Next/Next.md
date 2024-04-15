## Resumen de características

Este es un resumen de las nuevas funciones del directorio de aplicaciones:

| Caracteristicas | ¿Que hay de nuevo?                                                                                                                                                                                                                                 |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Routing         | Nuevo enrutador basado en el sistema de archivos construido sobre Server Components que soporta diseños, enrutamiento anidado, estados de carga, manejo de errores y más.                                                                          |
| Rendering       | Renderizado del lado del cliente y del lado del servidor con componentes del cliente y del servidor. Optimización adicional con Renderización Estática y Dinámica en el servidor con Next.js. Streaming en tiempos de ejecución de Edge y Node.js. |
| Data fetching   | Simplificación de la obtención de datos con soporte async/await en React Components y la API fetch() que se alinea con React y la Plataforma Web.                                                                                                  |
| Caching         | Nueva caché HTTP de Next.js y caché del lado del cliente optimizada para los componentes del servidor y la navegación del lado del cliente.                                                                                                        |
| Optimizations   | Componente de imagen mejorado con carga lenta nativa del navegador. Nuevo módulo de fuentes con optimización automática de fuentes.                                                                                                                |
| Transpilation   | Transpilación y agrupación automática de dependencias de paquetes locales (como monorepos) o de dependencias externas (node_modules).                                                                                                              |
| API             | Actualizaciones del diseño de la API en todo Next.js. Consulte la sección de referencia de la API para conocer las nuevas API.                                                                                                                     |
| Tooling         | Presentamos Turbopack, un sustituto de Webpack basado en Rust hasta 700 veces más rápido.                                                                                                                                                          |

## Pensar en los componentes del servidor

Al igual que React cambió la forma de pensar en la construcción de interfaces de usuario, los componentes de servidor de React introducen un nuevo modelo mental para la construcción de aplicaciones híbridas que aprovechan el servidor y el cliente.

En lugar de que React renderice toda tu aplicación del lado del cliente, React ahora te da la flexibilidad de elegir dónde renderizar tus componentes en función de su propósito.

Por ejemplo, considera una página en tu aplicación Next.js:

![[Pasted image 20221116201619.png]]
Si dividimos la página en componentes más pequeños, notaremos que la mayoría de los componentes no son interactivos y pueden ser renderizados en el servidor como Componentes de Servidor. Para las piezas más pequeñas de la interfaz de usuario interactiva, podemos añadir componentes de cliente. Esto se alinea con el enfoque "server-first" de Next.js.

Para facilitar esta transición, los Server Components están por defecto en el directorio de la aplicación, por lo que no hay que dar pasos adicionales para adoptarlos. Después, puedes optar por los componentes de cliente cuando sea necesario.

## Características

- [[Routing]]
	- [[Definiendo rutas]]
	- [[Paginas y Layouts]]
	- [[Enlaces y navegación]]
	- [[Carga de UI]]
	- [[Manejo de errores]]
- [[Renderizado (Next)]]
	- [[Componentes de servidor y de cliente]]
	- [[Renderizado estático y dinámico]]
	- [[Edge y Node Runtimes]]
- [[Obtención de datos]]
	- [[Fetching]]
	- [[Cacheo de datos]]
	- [[Revalidación de datos]]
	- [[Mutación de datos]]
	- [[Streaming y Suspense]]
	- [[Generando parámetros estáticos]]
	- [[API routes]]
- [[Next/Estilos]]
	- [[Módulos CSS]]
	- [[Tailwind CSS]]
	- [[Global CSS]]
	- [[CSS en JS]]
	- [[Hojas de estilo externas]]
	- [[Sass]]



## API

### Componentes

- [[Next/Link]]
- [[Next/Image]]
- [[Next/Font]]
- [[Next/Script]]

### Convención de archivos

- [[Layout]]
- [[Next/Page]]
- [[Next/Loading]]
- [[Next/Error]]
- [[Next/Template]]
- [[Next/Head]]
- [[Next/Not Found]]

### Funciones Server Components

- [[Next/Cookies]]
- [[Next/fetch]]
- [[Next/headers]]
- [[Next/generateStaticParams]]
- [[Next/notFound]]
- [[Next/redirect]]
- [[Next/previewData]]

### Hooks Client Components

- [[Next/useRouter]]
- [[Next/useSearchParams]]
- [[Next/useSelectedLayoutSegment]]
- [[Next/useSelectedLayoutSegments]]
- [[Next/usePathname]]

# Next Overview
 
```ccard
type: folder_brief_live
```
 
