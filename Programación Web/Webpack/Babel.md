[[Webpack]]

**Babel** (pronunciado "babble") es un proyecto impulsado por la comunidad utilizado por muchas empresas y proyectos, y es mantenido por un grupo de voluntarios.

Babel es una herramienta que te ayuda a escribir código en la **última versión de JavaScript**. Cuando sus entornos compatibles no admitan ciertas funciones de forma nativa, Babel lo ayudará a **compilar esas funciones en una versión compatible**.

**In**

```js
// ES2020 nullish coalescing
function greet(input) {
  return input ?? "Hello world";
}
```

**Out**

````js
function greet(input) {
  return input != null ? input : "Hello world";
}
````

### Instalacion babel loader

```bash
npm install babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime -D
```

```bash
yarn add babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime -D
```

- **babel-loader** nos permite usar babel con webpack
- **@babel/core** es babel en general
- **@babel/preset-env** trae y te permite usar las ultimas características de JavaScript
- **@babel/plugin-transform-runtime** te permite trabajar con todo el tema de asincronismo como ser `async` y `await`
- Debes crear el archivo de configuración de babel el cual tiene como nombre `.babelrc`

```js
{
  "presets": [
    "@babel/preset-env"
  ],
  "plugins": [
    "@babel/plugin-transform-runtime"
  ]
}
```

Para comenzar a utilizar webpack debemos agregar la siguiente configuración en **webpack.config.js**

```js
{
...,
module: {
    rules: [
      {
        // Test declara que extensión de archivos aplicara el loader
        test: /\.js$/,
        // Use es un arreglo u objeto donde dices que loader aplicaras
        use: {
          loader: "babel-loader"
        },
        // Exclude permite omitir archivos o carpetas especificas
        exclude: /node_modules/
      }
    ]
  }
}
```

