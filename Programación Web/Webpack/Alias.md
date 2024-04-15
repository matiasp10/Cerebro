[[Webpack]]

- **Alias** ⇒ nos permiten otorgar nombres paths específicos evitando los paths largos.
- Para crear un alias debes agregar la siguiente configuración a webpack.

```jsx
module.exports = {
	...
	resolve: {
		...
    alias: {
      '@nombreDeAlias': path.resolve(__dirname, 'src/<directorio>'),
    },
	}
}
```

- Puedes usarlo en los imports de la siguiente manera

```jsx
import modulo from "@ejemplo/archivo.js";
```