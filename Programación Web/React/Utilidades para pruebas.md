**Importando**

```jsx
import ReactTestUtils from 'react-dom/test-utils'; // ES6
var ReactTestUtils = require('react-dom/test-utils'); // ES5 con npm
```

## Introducción

`ReactTestUtils` facilita probar los componentes de React en cualquiera de los frameworks de pruebas que elijas. En Facebook usamos [Jest](https://facebook.github.io/jest/) para realizar las pruebas de JavaScript sin problemas. Aprende como iniciar con Jest en el [tutorial para React](https://jestjs.io/docs/tutorial-react) que se encuentra en el sitio web de Jest.

> Nota:
> 
> Recomendamos utilizar [React Testing Library](https://testing-library.com/react) que está diseñada para permitir e incentivar la escritura de las pruebas para que usen los componentes de la misma forma en que lo harían los usuarios finales.
> 
> Para versiones de React <= 16 la biblioteca [Enzyme](https://airbnb.io/enzyme/) facilita el proceso de realizar aserciones, manipular y navegar por los resultados de tus componentes de React.

-   [`act()`](https://es.reactjs.org/docs/test-utils.html#act)
-   [`mockComponent()`](https://es.reactjs.org/docs/test-utils.html#mockcomponent)
-   [`isElement()`](https://es.reactjs.org/docs/test-utils.html#iselement)
-   [`isElementOfType()`](https://es.reactjs.org/docs/test-utils.html#iselementoftype)
-   [`isDOMComponent()`](https://es.reactjs.org/docs/test-utils.html#isdomcomponent)
-   [`isCompositeComponent()`](https://es.reactjs.org/docs/test-utils.html#iscompositecomponent)
-   [`isCompositeComponentWithType()`](https://es.reactjs.org/docs/test-utils.html#iscompositecomponentwithtype)
-   [`findAllInRenderedTree()`](https://es.reactjs.org/docs/test-utils.html#findallinrenderedtree)
-   [`scryRenderedDOMComponentsWithClass()`](https://es.reactjs.org/docs/test-utils.html#scryrendereddomcomponentswithclass)
-   [`findRenderedDOMComponentWithClass()`](https://es.reactjs.org/docs/test-utils.html#findrendereddomcomponentwithclass)
-   [`scryRenderedDOMComponentsWithTag()`](https://es.reactjs.org/docs/test-utils.html#scryrendereddomcomponentswithtag)
-   [`findRenderedDOMComponentWithTag()`](https://es.reactjs.org/docs/test-utils.html#findrendereddomcomponentwithtag)
-   [`scryRenderedComponentsWithType()`](https://es.reactjs.org/docs/test-utils.html#scryrenderedcomponentswithtype)
-   [`findRenderedComponentWithType()`](https://es.reactjs.org/docs/test-utils.html#findrenderedcomponentwithtype)
-   [`renderIntoDocument()`](https://es.reactjs.org/docs/test-utils.html#renderintodocument)
-   [`Simulate`](https://es.reactjs.org/docs/test-utils.html#simulate)