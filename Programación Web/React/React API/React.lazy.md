`React.lazy()` permite definir un componente que es cargado dinámicamente. Esto ayuda a reducir el tamaño del bundle para demorar los componentes de carga que no son usados durante la renderización inicial.

Puedes aprender cómo usarlo desde nuestra [documentación de división de código](https://es.reactjs.org/docs/code-splitting.html#reactlazy). También puedes consultar [este artículo](https://medium.com/@pomber/lazy-loading-and-preloading-components-in-react-16-6-804de091c82d) que explica cómo usarlo con más detalle.

```
// Este componente está cargado dinámicamente
const SomeComponent = React.lazy(() => import('./SomeComponent'));
```

Ten en cuenta que renderizar componentes `lazy` requiere que haya un componente `<React.Suspense>` más alto en el árbol de renderización. Así es como se especifica un indicador de carga.