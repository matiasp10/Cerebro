El paquete `react-dom` proporciona métodos específicos del DOM que pueden ser utilizados en el nivel más alto de tu aplicación como una vía de escape del modelo de React si así lo necesitas.

```jsx
import * as ReactDOM from 'react-dom';
```

Si utilizas ES5 con npm, puedes escribir:

```jsx
var ReactDOM = require('react-dom');
```

El paquete `react-dom` también proporciona módulos específicos para aplicaciones en el cliente y el servidor:

-   [[client]]
-   [[server]]

## Resumen

El paquete `react-dom` exporta estos métodos:

-   [[createPortal()]]
-   [[flushSync()]]

Estos métodos de `react-dom` también se exportan, pero se consideran legados:

-   [[render()]]
-   [[hydrate()]]
-   [[findDOMNode()]]
-   [[unmountComponentAtNode()]]

> Nota:
> 
> Tanto `render` como `hydrate` se han reemplazado por [métodos del cliente](https://es.reactjs.org/docs/react-dom-client.html) en React 18. Estos métodos te advertirán que tu aplicación se comportará como si estuviera ejecutándose en React 17 (más información [aquí](https://es.reactjs.org/link/switch-to-createroot)).

### Soporte de navegadores

React es compatible con todos los navegadores modernos, aunque [se requieren algunos polyfills](https://es.reactjs.org/docs/javascript-environment-requirements.html) para entornos más antiguos.

> Nota
> 
> No aseguramos la compatibilidad con los navegadores más antiguos que no incluyen métodos ES5 o microtareas como Internet Explorer. Quizá encuentres que tus aplicaciones funcionan en estos navegadores si _polyfills_ como [es5-shim y es5-sham](https://github.com/es-shims/es5-shim) están incluidos en la página, pero estás por tu cuenta si decides tomar este camino.