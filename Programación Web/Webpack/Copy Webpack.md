[[Webpack]]

Copia archivos individuales o directorios completos, que ya existen, en el directorio de compilación.

### Instalacion

```console
npm install copy-webpack-plugin --save-dev
```

o

```console
yarn add -D copy-webpack-plugin
```

o

```console
pnpm add -D copy-webpack-plugin
```

Luego agregue el complemento a la **configuración** de su webpack. Por ejemplo:

**webpack.config.js**

```js
const CopyPlugin = require("copy-webpack-plugin");

module.exports = {
  plugins: [
    new CopyPlugin({
      patterns: [
        { from: "source", to: "dest" },
        { from: "other", to: "public" },
      ],
    }),
  ],
};
```

[Copy Webpage Official page](https://webpack.js.org/plugins/copy-webpack-plugin/)

