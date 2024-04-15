Los _Hooks_ son una adición nueva en React 16.8. Te permiten usar el estado y otras características de React sin la necesidad de escribir una clase.

Esta página responde algunas de las preguntas frecuentes acerca de los [Hooks](https://es.reactjs.org/docs/hooks-overview.html).

-   **[Estrategia de adopción](https://es.reactjs.org/docs/hooks-faq.html#adoption-strategy)**
    
    -   [¿Qué versiones de React incluyen Hooks?](https://es.reactjs.org/docs/hooks-faq.html#which-versions-of-react-include-hooks)
    -   [¿Necesito reescribir todos mis componentes que ya sean clases?](https://es.reactjs.org/docs/hooks-faq.html#do-i-need-to-rewrite-all-my-class-components)
    -   [¿Qué puedo hacer con Hooks que no pueda hacer con clases?](https://es.reactjs.org/docs/hooks-faq.html#what-can-i-do-with-hooks-that-i-couldnt-with-classes)
    -   [¿Qué tanto de mi conocimiento de React se mantiene relevante?](https://es.reactjs.org/docs/hooks-faq.html#how-much-of-my-react-knowledge-stays-relevant)
    -   [¿Debería usar Hooks, clases, o una mezcla de ambos?](https://es.reactjs.org/docs/hooks-faq.html#should-i-use-hooks-classes-or-a-mix-of-both)
    -   [¿Cubren los Hooks todos los casos de uso de las clases?](https://es.reactjs.org/docs/hooks-faq.html#do-hooks-cover-all-use-cases-for-classes)
    -   [¿Reemplazan los hooks a los render props y los Componentes de Orden Superior (HOC)?](https://es.reactjs.org/docs/hooks-faq.html#do-hooks-replace-render-props-and-higher-order-components)
    -   [¿Qué significan los Hooks para APIs populares como el connect de Redux, o React Router?](https://es.reactjs.org/docs/hooks-faq.html#what-do-hooks-mean-for-popular-apis-like-redux-connect-and-react-router)
    -   [¿Funcionan los Hooks con tipado estático?](https://es.reactjs.org/docs/hooks-faq.html#do-hooks-work-with-static-typing)
    -   [¿Cómo probar Componentes que usan Hooks?](https://es.reactjs.org/docs/hooks-faq.html#how-to-test-components-that-use-hooks)
    -   [¿Qué hacen cumplir las reglas de lint?](https://es.reactjs.org/docs/hooks-faq.html#what-exactly-do-the-lint-rules-enforce)
-   **[De las clases a los Hooks](https://es.reactjs.org/docs/hooks-faq.html#from-classes-to-hooks)**
    
    -   [¿Cómo corresponden los métodos del ciclo de vida a los Hooks?](https://es.reactjs.org/docs/hooks-faq.html#how-do-lifecycle-methods-correspond-to-hooks)
    -   [¿Cómo puedo obtener datos con los Hooks?](https://es.reactjs.org/docs/hooks-faq.html#how-can-i-do-data-fetching-with-hooks)
    -   [¿Existe algo similar a las variables de instancia?](https://es.reactjs.org/docs/hooks-faq.html#is-there-something-like-instance-variables)
    -   [¿Debería usar una o muchas variables de estado?](https://es.reactjs.org/docs/hooks-faq.html#should-i-use-one-or-many-state-variables)
    -   [¿Puedo correr un efecto solo cuando ocurran actualizaciones?](https://es.reactjs.org/docs/hooks-faq.html#can-i-run-an-effect-only-on-updates)
    -   [¿Cómo obtengo las props o el estado previo?](https://es.reactjs.org/docs/hooks-faq.html#how-to-get-the-previous-props-or-state)
    -   [¿Por qué estoy viendo props o estado obsoletos dentro de mi función?](https://es.reactjs.org/docs/hooks-faq.html#why-am-i-seeing-stale-props-or-state-inside-my-function)
    -   [¿Cómo implemento getDerivedStateFromProps?](https://es.reactjs.org/docs/hooks-faq.html#how-do-i-implement-getderivedstatefromprops)
    -   [¿Hay algo similar a forceUpdate?](https://es.reactjs.org/docs/hooks-faq.html#is-there-something-like-forceupdate)
    -   [¿Puedo crear una referencia (ref) a un Componente de función?](https://es.reactjs.org/docs/hooks-faq.html#can-i-make-a-ref-to-a-function-component)
    -   [¿Cómo puedo medir un nodo del DOM?](https://es.reactjs.org/docs/hooks-faq.html#how-can-i-measure-a-dom-node)
    -   [¿Qué significa [thing, setThing] = useState()?](https://es.reactjs.org/docs/hooks-faq.html#what-does-const-thing-setthing--usestate-mean)
-   **[Optimizaciones de desempeño](https://es.reactjs.org/docs/hooks-faq.html#performance-optimizations)**
    
    -   [¿Puedo saltarme un efecto durante las actualizaciones?](https://es.reactjs.org/docs/hooks-faq.html#can-i-skip-an-effect-on-updates)
    -   [¿Es seguro omitir funciones de la lista de dependencias?](https://es.reactjs.org/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies)
    -   [¿Qué puedo hacer si las dependencias de un efecto cambian con mucha frecuencia?](https://es.reactjs.org/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often)
    -   [¿Cómo implemento shouldComponentUpdate?](https://es.reactjs.org/docs/hooks-faq.html#how-do-i-implement-shouldcomponentupdate)
    -   [¿Cómo memorizar (memoize) los cálculos?](https://es.reactjs.org/docs/hooks-faq.html#how-to-memoize-calculations)
    -   [¿Cómo crear objetos costosos de manera diferida (lazy)?](https://es.reactjs.org/docs/hooks-faq.html#how-to-create-expensive-objects-lazily)
    -   [¿Son los hooks lentos debido a la creación de funciones en el render?](https://es.reactjs.org/docs/hooks-faq.html#are-hooks-slow-because-of-creating-functions-in-render)
    -   [¿Cómo evitar pasar callbacks hacia abajo?](https://es.reactjs.org/docs/hooks-faq.html#how-to-avoid-passing-callbacks-down)
    -   [¿Cómo leer un valor que cambia frecuentemente desde useCallback?](https://es.reactjs.org/docs/hooks-faq.html#how-to-read-an-often-changing-value-from-usecallback)
-   **[Bajo el capó](https://es.reactjs.org/docs/hooks-faq.html#under-the-hood)**
    
    -   [¿Cómo asocia React las llamadas a los Hooks con Componentes?](https://es.reactjs.org/docs/hooks-faq.html#how-does-react-associate-hook-calls-with-components)
    -   [¿Cuáles son los antecedentes de los Hooks?](https://es.reactjs.org/docs/hooks-faq.html#what-is-the-prior-art-for-hooks)