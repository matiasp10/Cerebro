[[Webpack]]

- Unos de las razones por que utilizamos webpack es porque nos permite optimizar y comprimir nuestro proyecto
- Debes utilizar los siguientes paquetes
	- **css-minimizer-webpack-plugin** ⇒ Nos ayuda a comprimir nuestros archivos finales CSS
	- **terser-webpack-plugin** ⇒ Permite minificar de una mejor forma

### Instalacion

NPM

```jsx
npm i css-minimizer-webpack-plugin terser-webpack-plugin -D
```

YARN

```jsx
yarn add css-minimizer-webpack-plugin terser-webpack-plugin -D
```

**webpack.config.js**


```js
...
const CssMinimizerPlugin = require('css-minimizer-webpack-plugin');
const TerserPlugin = require('terser-webpack-plugin');

module.exports = {
	...
	optimization: {
    minimize: true,
    minimizer: [
      new CssMinimizerPlugin(),
      new TerserPlugin()
    ]
  }
}
```

Cuando nombremos en la configuración de webpack es importante usar `[contenthash]` para evitar problemas con la cache