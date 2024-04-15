Next.js dispone de dos **Runtimes** de servidor en los que puedes renderizar partes del código de tu aplicación: el _Node.js Runtime_ y el _Edge Runtime_. Dependiendo de tu infraestructura de despliegue, ambos tiempos de ejecución soportan el **streaming**.

**Por defecto**, el directorio de aplicaciones utiliza el tiempo de ejecución de **Node.js**, que también es el predeterminado para las funciones sin servidor. También puedes utilizar el tiempo de ejecución de Edge, que es el tiempo de ejecución ligero utilizado por el Middleware y las rutas API de Edge.

Hay dos maneras de cambiar entre los tiempos de ejecución: **Globalmente** y por **segmento de ruta**.

## Opción global runtime

Para configurar el runtime para toda tu aplicación, puedes establecer la opción ``experimental runtime`` en tu archivo ``next.config.js``:

`next.config.js`

```js
module.exports = {
  experimental: {
    runtime: 'experimental-edge', // 'node.js' (default) | 'experimental-edge'
  },
};
```

Esta opción determina qué runtime debe utilizarse por defecto para los segmentos de ruta.

## Opción segmento de ruta

En cada segmento de la ruta, puede exportar opcionalmente una variable para establecer el runtime '**nodejs**' o '**experimental-edge**':

`app/page.js`

```ts
export const runtime = 'experimental-edge'; // 'node.js' (default) | 'experimental-edge'
```

Cuando se establecen tanto el runtime por segmento como el runtime global, el runtime por segmento anula el runtime global. Si no se establece el runtime por segmento, se utilizará la opción de runtime global.

## Runtime diferencias

|                  | Node (Server) | Node (Serverless) | Edge        |
| ---------------- | ------------- | ----------------- | ----------- |
| Cold Boot        | /             | ~250ms            | Instantaneo |
| HTTP Streaming   | Si            | Si                | Si          |
| IO               | Todos         | Todos             | Fetch       |
| Escabilidad      | /             | Alta              | La mas alta |
| Seguridad        | Normal        | Alta              | Alta        |
| Latencia         | Normal        | Baja              | La mas baja |
| Tamaño de codigo | /             | 50MB              | 1MB         |
| npm Packages     | Todos         | Todos             | Pocos            |


