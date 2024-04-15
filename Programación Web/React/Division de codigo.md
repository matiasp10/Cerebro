## _Bundling_

La mayoría de las aplicaciones React tendrán sus archivos “empaquetados” o en un _bundle_ con herramientas como [[Webpack]]. El _bundling_ es el proceso de seguir los archivos importados y fusionarlos en un archivo único: un _bundle_ o “paquete”. Este _bundle_ se puede incluir en una página web para cargar una aplicación completa de una sola vez.


#### Ejemplo

**App:**

```jsx
// app.js
import { add } from './math.js';

console.log(add(16, 26)); // 42
```

```jsx
// math.js
export function add(a, b) {
  return a + b;
}
```

**Bundle:**

```jsx
function add(a, b) {
  return a + b;
}

console.log(add(16, 26)); // 42
```

> **Nota**: Tus _bundles_ van a lucir muy diferente a esto.

Si usas [Create React App](https://create-react-app.dev/), [Next.js](https://nextjs.org/), [Gatsby](https://www.gatsbyjs.org/), o una herramienta similar, vas a tener una configuración de Webpack incluida para generar el _bundle_ de tu aplicación.

Si no, tú mismo vas a tener que configurar el _bundling_.

## División de código

El _Bundling_ es genial, pero a medida que tu aplicación crezca, tu _bundle_ también crecerá. Especialmente si incluyes grandes bibliotecas de terceros. Necesitas vigilar el código que incluyes en tu _bundle_, de manera que no lo hagas accidentalmente puedes hacer que tu aplicación sea tan grande que se tome mucho tiempo en cargar.

Para evitar terminar con un _bundle_ grande, es bueno adelantarse al problema y comenzar a dividir tu _bundle_. División de código es una funcionalidad disponible en _bundlers_ como [Webpack](https://webpack.js.org/guides/code-splitting/), [Rollup](https://rollupjs.org/guide/en/#code-splitting) y Browserify (vía [factor-bundle](https://github.com/browserify/factor-bundle)) que puede crear múltiples _bundles_ a ser cargados dinámicamente durante la ejecución de tu aplicación.

Dividir el código de tu aplicación puede ayudarte a cargar solo lo necesario en cada momento para el usuario, lo cual puede mejorar dramáticamente el rendimiento de tu aplicación. Si bien no habrás reducido la cantidad total de código en tu aplicación, habrás evitado cargar código que el usuario podría no necesitar nunca, y reducido la cantidad necesaria de código durante la carga inicial.

## import()

La mejor manera de introducir división de código en tu aplicación es a través de la sintaxis de `import()` dinámico.

**Antes:**

```jsx
import { add } from './math';

console.log(add(16, 26));
```

**Después:**

```jsx
import("./math").then(math => {
  console.log(math.add(16, 26));
});
```

Cuando Webpack se encuentra esta sintaxis, comienza a dividir el código de tu aplicación automáticamente. Si estás usando Create React App, esto ya viene configurado para ti y puedes comenzar a [usarlo](https://create-react-app.dev/docs/code-splitting/). También es compatible por defecto en [Next.js](https://nextjs.org/docs/advanced-features/dynamic-import).

Si configuras Webpack por ti mismo, probablemente vas a querer leer la [guía sobre división de código](https://webpack.js.org/guides/code-splitting/) de Webpack. Tu configuración de Webpack debería verse vagamente [como esta](https://gist.github.com/gaearon/ca6e803f5c604d37468b0091d9959269).

Cuando uses [Babel](https://babeljs.io/), tienes que asegurarte de que Babel reconozca la sintaxis de `import()` dinámico pero no la transforme. Para ello vas a necesitar [@babel/plugin-syntax-dynamic-import](https://classic.yarnpkg.com/en/package/@babel/plugin-syntax-dynamic-import).

## React.lazy

La función `React.lazy` te deja renderizar un _import_ dinámico como un componente regular.

**Antes:**

```jsx
import OtherComponent from './OtherComponent';
```

**Después:**

```jsx
const OtherComponent = React.lazy(() => import('./OtherComponent'));
```

`React.lazy` recibe una función que debe ejecutar un `import()` dinámico. Este debe retornar una `Promise` que se resuelve en un módulo con un _export_ `default` que contenga un componente de React.

El componente lazy debería entonces ser renderizado adentro de un componente `Suspense`, lo que nos permite mostrar algún contenido predeterminado (como un indicador de carga) mientras estamos esperando a que el componente lazy cargue.

```jsx
import React, { Suspense } from 'react';

const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </Suspense>
    </div>
  );
}
```

La prop `fallback` acepta cualquier elemento de React que quieras renderizar mientras esperas que `OtherComponent` cargue. Puedes poner el componente `Suspense` en cualquier parte sobre el componente lazy. Incluso puedes envolver múltiples componentes lazy con un solo componente `Suspense`.

```jsx
import React, { Suspense } from 'react';

const OtherComponent = React.lazy(() => import('./OtherComponent'));
const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <section>
          <OtherComponent />
          <AnotherComponent />
        </section>
      </Suspense>
    </div>
  );
}
```

### Evitar el fallback

Cualquier componente puede suspenderse como resultado del renderizado, incluso componentes que ya se mostraron al usuario. Para que el contenido de la pantalla siempre sea consistente, si un componente que ya se ha mostrado se suspende, React trata de esconder su árbol hacia arriba hasta la barrera `<Suspense>` más cercana. Sin embargo, desde la perspectiva del usuario esto puede desorientar.

Considera este componente para cambiar de pestaña:

```jsx
import React, { Suspense } from 'react';
import Tabs from './Tabs';
import Glimmer from './Glimmer';

const Comments = React.lazy(() => import('./Comments'));
const Photos = React.lazy(() => import('./Photos'));

function MyComponent() {
  const [tab, setTab] = React.useState('photos');
  
  function handleTabSelect(tab) {
    setTab(tab);
  };

  return (
    <div>
      <Tabs onTabSelect={handleTabSelect} />
      <Suspense fallback={<Glimmer />}>
        {tab === 'photos' ? <Photos /> : <Comments />}
      </Suspense>
    </div>
  );
}
```

En este ejemplo, si la pestaña se cambia de `'photos'` a `'comments'`, pero `Comments` se suspende, el usuario solo verá un destello. Esto tiene sentido porque el usuario no quiere ya ver `Photos`, el componente `Comments` aún no está listo para renderizar nada, y React necesita mantener la experiencia de usuario de forma consistente, así que no tiene otra opción que mostrar el componente `Glimmer` de arriba.

Sin embargo, a veces esta experiencia de usuario no es deseable. En particular, a veces es mejor mostrar la IU “vieja” mientras se prepara la nueva IU. Puedes usar la nueva API [`startTransition`](https://es.reactjs.org/docs/react-api.html#starttransition) para que React haga esto:

```jsx
function handleTabSelect(tab) {
  startTransition(() => {
    setTab(tab);
  });
}
```

Aquí, le dices a React que poner la pestaña en `'comments'` no es una actualización urgente, sino que es una [transición](https://es.reactjs.org/docs/react-api.html#transitions) que puede tomar algún tiempo. React mantendrá entonces la IU anterior en su lugar y aún interactiva, y cambiará a mostrar `<Comments />` cuando esté lista. Mira [Transiciones](https://es.reactjs.org/docs/react-api.html#transitions) para más información.

### Límites de error

Si el otro módulo no se carga (por ejemplo, debido a un fallo de la red), se generará un error. Puedes manejar estos errores para mostrar una buena experiencia de usuario y manejar la recuperación con [Límites de error](https://es.reactjs.org/docs/error-boundaries.html). Una vez hayas creado tu límite de error (Error Boundary) puedes usarlo en cualquier parte sobre tus componentes lazy para mostrar un estado de error cuando haya un error de red.

```jsx
import React, { Suspense } from 'react';
import MyErrorBoundary from './MyErrorBoundary';

const OtherComponent = React.lazy(() => import('./OtherComponent'));
const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

const MyComponent = () => (
  <div>
    <MyErrorBoundary>
      <Suspense fallback={<div>Loading...</div>}>
        <section>
          <OtherComponent />
          <AnotherComponent />
        </section>
      </Suspense>
    </MyErrorBoundary>
  </div>
);
```

## División de código basada en rutas

Decidir en qué parte de tu aplicación introducir la división de código puede ser un poco complicado. Quieres asegurarte de elegir lugares que dividan los _bundles_ de manera uniforme, sin interrumpir la experiencia del usuario.

Un buen lugar para comenzar es con las rutas. La mayoría de la gente en la web está acostumbrada a que las transiciones entre páginas se tomen cierto tiempo en cargar. También tiendes a volver a renderizar todo de una vez, así que es improbable que tus usuarios interactúen con otros elementos en la página al mismo tiempo.

Este es un ejemplo de cómo configurar la división de código basada en rutas en tu aplicación usando bibliotecas como [React Router](https://reactrouter.com/) con `React.lazy`.

```jsx
import React, { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  </Router>
);
```

## Exports con nombres

`React.lazy` actualmente solo admite _exports_ tipo `default`. Si el módulo que desea importar utiliza _exports_ con nombre, puede crear un módulo intermedio que lo vuelva a exportar como `default`. Esto garantiza que el _tree shaking_ siga funcionando y que no importes componentes no utilizados.

```jsx
// ManyComponents.js
export const MyComponent = /* ... */;
export const MyUnusedComponent = /* ... */;
```

```jsx
// MyComponent.js
export { MyComponent as default } from "./ManyComponents.js";
```

```jsx
// MyApp.js
import React, { lazy } from 'react';
const MyComponent = lazy(() => import("./MyComponent.js"));
```