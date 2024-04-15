```jsx
render()
```

El método `render()` es el único método requerido en un componente de clase.

Cuando se llama, debe examinar a `this.props` y `this.state` y devolver uno de los siguientes tipos:

-   **Elementos de React.** normalmente creados a través de [JSX](https://es.reactjs.org/docs/introducing-jsx.html). Por ejemplo, `<div />` y `<MyComponent />` son elementos de React que enseñan a React a renderizar un nodo DOM, u otro componente definido por el usuario, respectivamente.
-   **Arrays y fragmentos.** Permiten que puedas devolver múltiples elementos desde el render. Consulta la documentación sobre [fragmentos](https://es.reactjs.org/docs/fragments) para más detalles.
-   **Portales**. Te permiten renderizar hijos en otro subárbol del DOM. Consulta la documentación sobre [portales](https://es.reactjs.org/docs/portals) para más detalles.
-   **String y números.** Estos son renderizados como nodos de texto en el DOM.
-   **Booleanos o `nulos`**. No renderizan nada. (Principalmente existe para admitir el patrón `return test && <Child />`, donde `test` es booleano.)

La función `render ()` debe ser pura, lo que significa que no modifica el estado del componente, devuelve el mismo resultado cada vez que se invoca y no interactúa directamente con el navegador.

Si necesitas interactuar con el navegador, realiza tu trabajo en `componentDidMount()` o en los demás métodos de ciclo de vida. Mantener `render()` pure hace que los componentes sean más fáciles de considerar.

> Nota
> 
> `render()` no será invocado si [`shouldComponentUpdate()`](https://es.reactjs.org/docs/react-component.html#shouldcomponentupdate) devuelve falso.