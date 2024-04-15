```
constructor(props)
```

**Si no inicializas el estado y no enlazas los métodos, no necesitas implementar un constructor para tu componente React.**

El constructor para un componente React es llamado antes de ser montado. Al implementar el constructor para una subclase `React.Component`, deberías llamar a `super(props)` antes que cualquier otra instrucción. De otra forma, `this.props` no estará definido en el constructor, lo que puede ocasionar a errores.

Normalmente, los constructores de React sólo se utilizan para dos propósitos:

-   Para inicializar un estado local asignando un objeto al `this.state`.
-   Para enlazar [manejadores de eventos](https://es.reactjs.org/docs/handling-events.html) a una instancia.

**No debes llamar `setState()`** en el `constructor()`. En su lugar, si su componente necesita usar el estado local, **asigna directamente el estado inicial al `this.state`** directamente en el constructor:

```jsx
constructor(props) {
  super(props);
  // No llames this.setState() aquí!
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```

El constructor es el único lugar donde debes asignar `this.state` directamente. En todos los demás métodos, debes usar `this.setState()` en su lugar.

Evita introducir cualquier efecto secundario o suscripciones en el constructor. Para estos casos de uso, use `componentDidMount()` en su lugar.

> Nota
> 
> **¡Evita copiar las props en el estado! Es un error muy común:**

```jsx
constructor(props) {
 super(props);
 // No hagas esto!
 this.state = { color: props.color };
}
```

> El problema es que es innecesario (puedes usar `this.props.color` directamente en su lugar), esto crea errores (actualizaciones a la prop `color` no se reflejarán en el estado).
> 
> **Sólo utiliza este patrón si deseas ignorar intencionalmente las actualizaciones de prop.** En ese caso, tiene sentido renombrar la prop a `initialColor` o `defaultColor`. Puedes forzar al componente a “limpiar” su estado interno [cambiando su `key`](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html#recommendation-fully-uncontrolled-component-with-a-key) cuando sea necesario.
> 
> Lee nuestro [post en el blog sobre como evitar estados derivados](https://es.reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html) para aprender qué hacer si crees que necesitas algún estado que dependa de las props.