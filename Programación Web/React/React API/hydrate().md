```
hydrate(elemento, contenedor[, callback])
```

> Nota:
> 
> `hydrate` ha sido reemplazado con `hydrateRoot` en React 18. Consulta [hydrateRoot](https://es.reactjs.org/docs/react-dom-client.html#hydrateroot) para más información.

Es igual a [`render()`](https://es.reactjs.org/docs/react-dom.html#render), pero es utilizado para hidratar un contenedor cuyo contenido HTML fue renderizado por [`ReactDOMServer`](https://es.reactjs.org/docs/react-dom-server.html). React tratará de agregar detectores de eventos al marcado existente.

React espera que el contenido renderizado sea idéntico entre el servidor y el cliente. Puede arreglar las diferencias del contenido de texto, pero deberías tratar los desajustes como errores y arreglarlos. En modo de desarrollo, React alerta sobre desajustes durante la hidratación. No hay garantías de que las diferencias de atributos sean arregladas en caso de desajustes. Esto es importante por razones de rendimiento, porque en la mayoría de las aplicaciones los desajustes son raros y validar todo el marcado sería demasiado costoso.

Si el atributo de un elemento o contenido de texto es inevitablemente diferente entre el servidor y el cliente (por ejemplo, una marca de tiempo), puedes silenciar la alerta agregando `suppressHydrationWarning={true}` al elemento. Esto solo funciona a 1 nivel de profundidad, y está pensado como una vía de escape. No abuses de él. A menos que sea contenido de texto, React aun no intentará arreglarlo, así que es posible que continúe inconsistente hasta próximas actualizaciones.

Si necesitas renderizar algo diferente de manera intencional en el servidor y en el cliente, puedes realizar un renderizado en 2 pasos. Los componentes que renderizan contenido diferente al cliente, pueden leer una variable de estado como `this.state.isClient`, la cual puedes cambiar a `true` en `componentDidMount()`. De esta manera, el paso de renderizado inicial renderizará el mismo contenido que el servidor, evitando desajustes, pero un paso adicional ocurrirá síncronamente justo después de la hidratación. Recuerda que este enfoque hará que tus componentes sean más lentos debido a que se deben renderizar dos veces, así que utilízalo con precaución.

Recuerda estar consciente de la experiencia de usuario en conexiones lentas. El código Javascript puede ser cargado significativamente después de que el HTML inicial sea renderizado, entonces, si renderizas algo diferente en el paso exclusivo por el cliente, la transición puede ser discorde. Sin embargo, si se ejecuta bien, puede ser beneficioso para renderizar una «capa» de la aplicación en el servidor, y solo mostrar unos _widgets_ extra en el cliente. Para aprender cómo hacer esto sin tener desajustes en el marcado, consulta la explicación en el párrafo anterior.
