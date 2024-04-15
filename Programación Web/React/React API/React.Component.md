React te permite definir componentes como clases o funciones. Los componentes definidos como clases actualmente proporcionan una serie de características extra que explicamos en esta página. Para definir una clase de componente React, necesitas extender `React.Component`:

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

El único método que _debes_ definir en una subclase de `React.Component` es [`render()`](https://es.reactjs.org/docs/react-component.html#render). Todos los demás métodos descritos en esta página son opcionales.

**Recomendamos encarecidamente no crear tus propias clases de componentes base.** En los componentes de React, [la reutilización de código se consigue principalmente a través de la composición en lugar de la herencia](https://es.reactjs.org/docs/composition-vs-inheritance.html).

> Nota:
> 
> React no te obliga a usar la sintaxis de clases ES6. Si prefieres evitarlo, puede utilizar el módulo `create-react-class` o una abstracción personalizada similar en su lugar. Échale un vistazo a [Usando React sin ES6](https://es.reactjs.org/docs/react-without-es6.html) para aprender mas.

### El ciclo de vida del componente

Cada componente tiene varios “métodos de ciclo de vida” que puedes sobrescribir para ejecutar código en momentos particulares del proceso. **Puedes usar [este diagrama de ciclo de vida](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/) como una hoja de referencia.** En la lista de abajo, los métodos de ciclo de vida comúnmente usados están marcados en **negrita**. El resto de ellos existen para casos de uso relativamente raros.

![[Pasted image 20221114093752.png]]

#### Montaje

Estos métodos se llaman cuando se crea una instancia de un componente y se inserta en el DOM:

-   [[constructor()]]
-   [[static getDerivedStateFromProps()]]
-   [[render()]]
-   [[componentDidMount()]]

> Nota:
> 
> Este método se considera obsoleto y deberías [evitarlo](https://es.reactjs.org/blog/2018/03/27/update-on-async-rendering.html) en código nuevo:
> 
> -   [[UNSAFE_componentWillMount()]]

#### Actualización

Una actualización puede ser causada por cambios en las props o el estado. Estos métodos se llaman en el siguiente orden cuando un componente se vuelve a renderizar:

-   [[static getDerivedStateFromProps()]]
-   [[shouldComponentUpdate()]]
-   [[render()]]
-   [[getSnapshotBeforeUpdate()]]
-   [[componentDidUpdate()]]

> Nota:
> 
> Estos métodos están considerados _legacy_ (deprecados) y debes [evitarlos](https://es.reactjs.org/blog/2018/03/27/update-on-async-rendering.html) en código nuevo:
> 
> -   [`UNSAFE_componentWillUpdate()`](https://es.reactjs.org/docs/react-component.html#unsafe_componentwillupdate)
> -   [`UNSAFE_componentWillReceiveProps()`](https://es.reactjs.org/docs/react-component.html#unsafe_componentwillreceiveprops)

#### Desmontaje

Este método es llamado cuando un componente se elimina del DOM:

-   [[componentWillUnmount()]]

#### Manejo de errores

Estos métodos se invocan cuando hay un error durante la renderización, en un método en el ciclo de vida o en el constructor de cualquier componente hijo.

-   [[static getDerivedStateFromError()]]
-   [[componentDidCatch()]]

### Otras APIs

A diferencia de los métodos de ciclo de vida anteriores (que React llama por ti), los métodos siguientes son los métodos que **tu puedes llamar desde tus componentes**.

Hay sólo dos de ellos: setState() y forceUpdate().

-   [[setState()]]
-   [[forceUpdate()]]

### Propiedades de clase

-   [[defaultProps]]
-   [[displayName]]

### Propiedades de instancia

-   [[props]]
-   [[estado]]