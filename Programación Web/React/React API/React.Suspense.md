`React.Suspense` permite especificar el indicador de carga en caso de que algunos componentes en el árbol más abajo de él todavía no estén listos para renderizarse. En el futuro planeamos permitir a `Suspense` manejar más escenarios como la carga de datos. Puedes leer más sobre este tema en [nuestra hoja de ruta](https://es.reactjs.org/blog/2018/11/27/react-16-roadmap.html).

Hoy en día, los componentes de carga diferida son el **único** caso compatible con `<React.Suspense>`:

```
// Este componente está cargado dinámicamente
const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    // Muestra <Spinner> hasta que OtherComponent cargue
    <React.Suspense fallback={<Spinner />}>
      <div>
        <OtherComponent />
      </div>
    </React.Suspense>
  );
}
```

Esto está documentado en nuestra [guía de división de código](https://es.reactjs.org/docs/code-splitting.html#reactlazy). Ten en cuenta que los componentes `lazy` pueden estar muy profundo en el árbol `Suspense` — no tiene que envolverlos a todos. La mejor práctica es colocar `<Suspense>` donde se desee ver un indicador de carga y usar `lazy()` para hacer división de código.

> Note
> 
> For content that is already shown to the user, switching back to a loading indicator can be disorienting. It is sometimes better to show the “old” UI while the new UI is being prepared. To do this, you can use the new transition APIs [`startTransition`](https://es.reactjs.org/docs/react-api.html#starttransition) and [`useTransition`](https://es.reactjs.org/docs/hooks-reference.html#usetransition) to mark updates as transitions and avoid unexpected fallbacks.

#### `React.Suspense` in Server Side Rendering

During server side rendering Suspense Boundaries allow you to flush your application in smaller chunks by suspending. When a component suspends we schedule a low priority task to render the closest Suspense boundary’s fallback. If the component unsuspends before we flush the fallback then we send down the actual content and throw away the fallback.

#### `React.Suspense` during hydration

Suspense boundaries depend on their parent boundaries being hydrated before they can hydrate, but they can hydrate independently from sibling boundaries. Events on a boundary before its hydrated will cause the boundary to hydrate at a higher priority than neighboring boundaries. [Read more](https://github.com/reactwg/react-18/discussions/130)

### [](https://es.reactjs.org/docs/react-api.html#starttransition)`   `