`React` es el punto de entrada a la biblioteca de React. Si se carga React desde una etiqueta `<script>`, estas API de alto nivel estarán disponibles en el `React` global. Si se usa ES6 con npm se puede escribir `import React from 'react'`. Si se usa ES5 con npm, se puede escribir `var React = require('react')`.

### Componentes

Los componentes de React permiten dividir la UI en piezas independientes, reusables y pensar acerca de cada pieza aisladamente. Los componentes de React pueden ser definidos creando subclases `React.Component` o `React.PureComponent`.

-   [[React.Component]]
-   [[React.PureComponent]]

Si no se usan las clases ES6, se puede usar el módulo `create-react-class`. Para más información, ver [Usar React sin ES6](https://es.reactjs.org/docs/react-without-es6.html).

Los componentes de React también pueden ser definidos como funciones que se pueden envolver:

-   [[React.memo]]

### Crear elementos de React

Se recomienda [usar JSX](https://es.reactjs.org/docs/introducing-jsx.html) para describir cómo debe verse la UI. Cada elemento de JSX es solo un azúcar sintáctico para llamar [`React.createElement()`](https://es.reactjs.org/docs/react-api.html#createelement). Normalmente no se recurrirá a los siguientes métodos directamente si se está usando JSX.

-   [[createElement()]]
-   [[createFactory()]]

Para más información, ver [Usar React sin JSX](https://es.reactjs.org/docs/react-without-jsx.html).

### Transformar elementos

`React` proporciona varias API para manipular elementos:

-   [[cloneElement()]]
-   [[isValidElement()]]
-   [[React.Children]]

### Fragmentos

`React` también proporciona un componente para renderizar múltiples elementos sin un contenedor.

-   [[React.Fragment]]

### Refs

-   [[React.createRef]]
-   [[React.forwardRef]]

### Suspense

Suspense permite que los componentes “esperen” algo antes de renderizar. Hoy Suspense solo mantiene un caso de uso: [cargar componentes activamente con `React.lazy`](https://es.reactjs.org/docs/code-splitting.html#reactlazy). En el futuro mantendrá otros casos de uso como captura de datos.

-   [[React.lazy]]
-   [[React.Suspense]]

### Transitions

_Transitions_ are a new concurrent feature introduced in React 18. They allow you to mark updates as transitions, which tells React that they can be interrupted and avoid going back to Suspense fallbacks for already visible content.

-   [[React.startTransition]]
-   [[React.useTransition]]

### Hooks

Los _Hooks_ son una nueva adición en React 16.8. Permiten usar el estado y otras características de React sin escribir una clase. Los Hooks tienen una [sección de documentos dedicados](https://es.reactjs.org/docs/hooks-intro.html) y una referencia API separada:

-   Hooks Básicos
    -   [[useState]]
    -   [[useEffect]]
    -   [[useContext]]
-   Hooks Adicionales
    -   [[useReducer]]
    -   [[useCallback]]
    -   [[useMemo]]
    -   [[useRef]]
    -   [[useImperativeHandle]]
    -   [[useLayoutEffect]]
    -   [[useDebugValue]]
    -   [[useDeferredValue]]
    -   [[useTransition]]
    -   [[useId]]
-   Library Hooks
> Los siguientes Hooks se proporcionan para que los autores de las bibliotecas las integren profundamente en el modelo de React, y no se suelen utilizar en el código de la aplicación.
    -   [[useSyncExternalStore]]
    -   [[useInsertionEffect]]