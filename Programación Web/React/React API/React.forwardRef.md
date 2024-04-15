`React.forwardRef` crea un componente React que envía el atributo [ref](https://es.reactjs.org/docs/refs-and-the-dom.html) que recibe a otro componente más abajo en el árbol. Esta técnica no es muy común, pero es particularmente útil en dos escenarios:

-   [Enviar refs a componentes DOM](https://es.reactjs.org/docs/forwarding-refs.html#forwarding-refs-to-dom-components)
-   [Enviar refs en componentes de orden superior](https://es.reactjs.org/docs/forwarding-refs.html#forwarding-refs-in-higher-order-components)

`React.forwardRef` acepta una función de renderizado como un argumento. React llamará esta función con `props` y `ref` como dos argumentos. Esta función debe retornar un nodo React.

```
const FancyButton = React.forwardRef((props, ref) => (  <button ref={ref} className="FancyButton">    {props.children}
  </button>
));

// Ahora puedes obtener un ref directamente al botón del DOM
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

En el ejemplo anterior, React pasa un `ref` dado a un elemento `<FancyButton ref={ref}>` como un segundo argumento a la función de renderizado dentro de la llamada `React.forwardRef`. Esta función de renderizado pasa el `ref` al elemento `<button ref={ref}>`.

Como resultado, después que React adjunte el ref, `ref.current` apuntará directamente a la instancia del elemento DOM `<button>`.

Para más información, ver [reenvío de refs](https://es.reactjs.org/docs/forwarding-refs.html).