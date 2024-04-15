[[Webpack]]

- El modo watch hace que nuestro proyecto se compile de forma automática.
	- Es decir que está atento a cambios
- Para habilitarlo debemos agregar lo siguiente en la configuración de webpack:
```jsx
module.exports = {
	...
	watch: true
}
```

- Cada vez que haya un cambio hara un build automático
- Otra manera es mandar la opción mediante parámetros de consola en `package.json`:
```json
{
	"scripts": {
		"dev:watch": "webpack --config webpack.config.dev.js --watch"
	}
}
```

- Vale la pena recordar que si aplicamos en modo producción se tomara más tiempo porque se optimizaran los recursos
    - Por ello en modo desarrollo se salta ese paso y es más rápido la compilación
