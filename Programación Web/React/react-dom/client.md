The `react-dom/client` package provides client-specific methods used for initializing an app on the client. Most of your components should not need to use this module.

```
import * as ReactDOM from 'react-dom/client';
```

If you use ES5 with npm, you can write:

```
var ReactDOM = require('react-dom/client');
```

## Resumen

The following methods can be used in client environments:

-   [[createRoot()]]
-   [[hydrateRoot()]]

### Soporte de navegadores

React supports all modern browsers, although [some polyfills are required](https://es.reactjs.org/docs/javascript-environment-requirements.html) for older versions.

> Note
> 
> We do not support older browsers that don’t support ES5 methods or microtasks such as Internet Explorer. You may find that your apps do work in older browsers if polyfills such as [es5-shim and es5-sham](https://github.com/es-shims/es5-shim) are included in the page, but you’re on your own if you choose to take this path.