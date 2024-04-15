**Importando**

```
import TestRenderer from 'react-test-renderer'; // ES6
const TestRenderer = require('react-test-renderer'); // ES5 con npm
```

## Resumen

Este paquete proporciona un procesador de React que se puede usar para procesar componentes de React a objetos JavaScript puros, sin depender del DOM o de un entorno móvil nativo.

Básicamente, este paquete facilita tomar una instantánea de la jerarquía de la vista de la plataforma (similar a un árbol DOM) representada por un componente React DOM o React Native sin usar un navegador o [jsdom](https://github.com/tmpvar/jsdom).

Ejemplo:

```
import TestRenderer from 'react-test-renderer';

function Link(props) {
  return <a href={props.page}>{props.children}</a>;
}

const testRenderer = TestRenderer.create(
  <Link page="https://www.facebook.com/">Facebook</Link>
);

console.log(testRenderer.toJSON());
// { type: 'a',
//   props: { href: 'https://www.facebook.com/' },
//   children: [ 'Facebook' ] }
```

Puede usar la función de pruebas de instantánea (`snapshot`) de Jest para guardar automáticamente una copia del árbol JSON en un archivo y comprobar en tus pruebas que no ha cambiado: [Aprende más sobre ello](https://jestjs.io/docs/en/snapshot-testing).

También puede recorrer la salida para encontrar nodos específicos y hacer afirmaciones sobre ellos.

```
import TestRenderer from 'react-test-renderer';

function MyComponent() {
  return (
    <div>
      <SubComponent foo="bar" />
      <p className="my">Hello</p>
    </div>
  )
}

function SubComponent() {
  return (
    <p className="sub">Sub</p>
  );
}

const testRenderer = TestRenderer.create(<MyComponent />);
const testInstance = testRenderer.root;

expect(testInstance.findByType(SubComponent).props.foo).toBe('bar');
expect(testInstance.findByProps({className: "sub"}).children).toEqual(['Sub']);
```

### TestRenderer

-   [`TestRenderer.create()`](https://es.reactjs.org/docs/test-renderer.html#testrenderercreate)
-   [`TestRenderer.act()`](https://es.reactjs.org/docs/test-renderer.html#testrendereract)

### Instancias de TestRenderer

-   [`testRenderer.toJSON()`](https://es.reactjs.org/docs/test-renderer.html#testrenderertojson)
-   [`testRenderer.toTree()`](https://es.reactjs.org/docs/test-renderer.html#testrenderertotree)
-   [`testRenderer.update()`](https://es.reactjs.org/docs/test-renderer.html#testrendererupdate)
-   [`testRenderer.unmount()`](https://es.reactjs.org/docs/test-renderer.html#testrendererunmount)
-   [`testRenderer.getInstance()`](https://es.reactjs.org/docs/test-renderer.html#testrenderergetinstance)
-   [`testRenderer.root`](https://es.reactjs.org/docs/test-renderer.html#testrendererroot)

### TestInstance

-   [`testInstance.find()`](https://es.reactjs.org/docs/test-renderer.html#testinstancefind)
-   [`testInstance.findByType()`](https://es.reactjs.org/docs/test-renderer.html#testinstancefindbytype)
-   [`testInstance.findByProps()`](https://es.reactjs.org/docs/test-renderer.html#testinstancefindbyprops)
-   [`testInstance.findAll()`](https://es.reactjs.org/docs/test-renderer.html#testinstancefindall)
-   [`testInstance.findAllByType()`](https://es.reactjs.org/docs/test-renderer.html#testinstancefindallbytype)
-   [`testInstance.findAllByProps()`](https://es.reactjs.org/docs/test-renderer.html#testinstancefindallbyprops)
-   [`testInstance.instance`](https://es.reactjs.org/docs/test-renderer.html#testinstanceinstance)
-   [`testInstance.type`](https://es.reactjs.org/docs/test-renderer.html#testinstancetype)
-   [`testInstance.props`](https://es.reactjs.org/docs/test-renderer.html#testinstanceprops)
-   [`testInstance.parent`](https://es.reactjs.org/docs/test-renderer.html#testinstanceparent)
-   [`testInstance.children`](https://es.reactjs.org/docs/test-renderer.html#testinstancechildren)