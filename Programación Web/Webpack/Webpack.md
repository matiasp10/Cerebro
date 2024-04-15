[Webpack Official page](https://webpack.js.org/concepts/)

En esencia, webpack es un paquete de módulos estáticos para aplicaciones JavaScript modernas. Cuando webpack procesa su aplicación, crea internamente un gráfico de dependencia a partir de uno o más puntos de entrada y luego **combina todos los módulos** que su proyecto necesita en uno o más paquetes, que son activos **estáticos** desde los que servir su contenido.

Desde la **versión 4.0.0**, webpack no requiere un archivo de configuración para agrupar su proyecto. Sin embargo, es **increíblemente configurable** para adaptarse mejor a sus necesidades.

### Trabaja con

- HTML
- JSON
- JavaScript
- CSS
- Archivos estaticos
- Imagenes
- Fuentes

### Nos permite

- Trabajar con modulos.
	- Modulos en formato AMD, CommonJS y ES15.
- Gestionar dependencias.
- Ejecutar tareas.
- Convertir archivos.

## Entry (Entrada)

Un punto de entrada indica qué módulo debe usar **Webpack** para comenzar a construir su gráfico de dependencia interno. **Webpack** descubrirá de qué otros módulos y bibliotecas depende ese punto de entrada (directa e indirectamente).

**webpack.config.js**

```js
module.exports = {
  entry: './path/to/my/entry/file.js',
};
```

## Output (Salida)

La propiedad de salida le dice a Webpack dónde emitir los paquetes que crea y cómo nombrar estos archivos. El valor predeterminado es **./dist/main.js** para el archivo de salida principal y la carpeta **./dist** para cualquier otro archivo generado.
Puede configurar esta parte del proceso especificando un campo de salida en su configuración:

**webpack.config.js**

```javascript
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js',
  },
};
```

En el ejemplo anterior, usamos las propiedades **output.filename** y **output.path** para decirle al paquete web el nombre de nuestro paquete y dónde queremos que se emita. En caso de que se pregunte si el módulo de ruta se importa en la parte superior, es un módulo central de Node.js que se usa para manipular rutas de archivos.

## Loaders (Cargadores)

Fuera de la caja (out of the box), Webpack solo comprende archivos **JavaScript** y **JSON**. Los loaders permiten que Webpack procese otros tipos de archivos y los convierta en módulos válidos que su aplicación puede consumir y agregar al gráfico de dependencia.

En un nivel alto, los loaders tienen dos propiedades en la configuración de su paquete web: 
- La propiedad `test` identifica qué archivo o archivos deben transformarse. 
- La propiedad `use` indica qué loader debe usarse para realizar la transformación.

**webpack.config.js**

```javascript
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js',
  },
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
};
```

La configuración anterior ha definido una propiedad de reglas para un solo módulo con dos propiedades requeridas: `test` y `use`. Esto le dice al compilador de webpack lo siguiente:

> "Hola, compilador Webpack, cuando encuentre una ruta que se resuelva en un archivo '.txt' dentro de una instrucción `require()/import`, use el `raw-loader` para transformarlo antes de agregarlo al paquete".

- [[Babel]]

## Plugins (Complementos)

Si bien los loaders se utilizan para transformar ciertos tipos de módulos, los complementos se pueden aprovechar para realizar una gama más amplia de tareas, como la **optimización de paquetes**, la **gestión de activos** y la **inyección de variables de entorno**.

Para usar un complemento, necesita `require()` y agregarlo al array de `plugins`. La mayoría de los complementos se pueden personalizar a través de opciones. Dado que puede usar un complemento varias veces en una configuración para diferentes propósitos, debe crear una instancia de él llamándolo con el operador `new`.

**webpack.config.js**

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
const webpack = require('webpack'); //to access built-in plugins

module.exports = {
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
  plugins: [new HtmlWebpackPlugin({ template: './src/index.html' })],
};
```

En el ejemplo anterior, el `html-webpack-plugin` genera un archivo **HTML** para su aplicación e inyecta automáticamente todos los paquetes generados en este archivo.

- [[HtmlWebpackPlugin]]
- [[Copy Webpack]]

## Mode (Modo)

Al establecer el parámetro de modo en desarrollo, producción o ninguno, puede habilitar las optimizaciones integradas de webpack que corresponden a cada entorno. El valor predeterminado es la producción.

```javascript
module.exports = {
  mode: 'production',
};
```

### Ejecutar webpack en modo desarrollo

```
npx webpack --mode production
npx webpack --mode development
```

## Compatibilidad del navegador

Webpack es compatible con todos los navegadores compatibles con **ES5** (IE8 y anteriores no son compatibles). Webpack necesita ``Promise`` para ``import()`` y ``require.ensure()``. Si desea admitir navegadores más antiguos, deberá cargar un **polyfill** antes de usar estas expresiones.

## Entorno

Webpack 5 runs on **Node.js version 10.13.0+**.

## Instalacion

```sh
npm i webpack webpack-cli -D

yarn add webpack webpack-cli -D
```

### Ejecutar

```sh
npx webpack
```