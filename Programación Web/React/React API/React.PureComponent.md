`React.PureComponent` es similar a [`React.Component`](https://es.reactjs.org/docs/react-api.html#reactcomponent). La diferencia entre ellos es que [`React.Component`](https://es.reactjs.org/docs/react-api.html#reactcomponent) no implementa [`shouldComponentUpdate()`](https://es.reactjs.org/docs/react-component.html#shouldcomponentupdate), pero `React.PureComponent` lo implementa con un prop superficial y una comparación del estado.

Si la función `render()` del componente de React renderiza el mismo resultado dados los mismos props y estado, se puede usar `React.PureComponent` para una mejora en el desempeño en algunos casos.

> Nota
> 
> `shouldComponentUpdate()` del `React.PureComponent` solo compara superficialmente los objetos. Si estos contienen estructuras de datos complejos pueden producir falsos negativos para diferencias más profundas. Solo se extiende `PureComponent` cuando se espera tener los props y el estado simples o usar [`forceUpdate()`](https://es.reactjs.org/docs/react-component.html#forceupdate) cuando se sabe que las estructuras de datos profundos han cambiado. O considera usar [objetos inmutables](https://immutable-js.com/) para facilitar comparaciones rápidas de los datos anidados.
> 
> Además, `shouldComponentUpdate()` del `React.PureComponent` omite las actualizaciones de los props para todo el componente del subárbol. Asegúrate que todos los componentes hijos también sean “puros”.