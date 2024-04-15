Next.js tiene soporte incorporado para **Sass** usando las extensiones ``.scss`` y ``.sass``. Puedes utilizar Sass a nivel de componente a través de los Módulos CSS y la extensión ``.module.scss`` o ``.module.sass``.

En primer lugar, instale sass:

```bash
npm install --save-dev sass
```

> **Es bueno saberlo**: Sass soporta dos sintaxis diferentes, cada una con su propia extensión. La extensión .scss requiere que uses la sintaxis SCSS, mientras que la extensión .sass requiere que uses la sintaxis indentada ("Sass").

Si no está seguro de cuál elegir, comience con la extensión .scss que es un superconjunto de CSS, y no requiere que aprenda la Sintaxis Indentada ("Sass").

## Personalizando las configuraciones de Sass

Si quieres configurar el compilador Sass, utiliza ``sassOptions`` en ``next.config.js``.

```js
const path = require('path');

module.exports = {
  sassOptions: {
    includePaths: [path.join(__dirname, 'styles')],
  },
};
```

## Variables Sass

Next.js es compatible con las variables Sass exportadas desde los archivos de módulos CSS.

Por ejemplo, utilizando la variable Sass exportada **primaryColor**:

``app/variables.module.scss``

```scss
$primary-color: #64ff00;

:export {
  primaryColor: $primary-color;
}
```

``app/page.js``

```jsx
// maps to root `/` URL

import variables from './variables.module.scss';

export default function Page() {
  return <h1 style={{ color: variables.primaryColor }}>Hello, Next.js!</h1>;
}
```