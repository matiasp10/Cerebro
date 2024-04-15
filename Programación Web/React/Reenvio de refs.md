El reenvío de refs es una técnica para **pasar automáticamente una [ref](https://es.reactjs.org/docs/refs-and-the-dom.html) a través de un componente a uno de sus hijos**. Esto normalmente no es necesario para la mayoría de los componentes en una aplicación. Sin embargo, puede ser útil para ciertos tipos de componentes, especialmente en bibliotecas de componentes reutilizables. Los escenarios más comunes son descritos a continuación.

## Reenviando refs a componentes DOM

Considere un componente `FancyButton` que renderiza el elemento DOM nativo `button`:

```jsx
function FancyButton(props) {
  return (
    <button className="FancyButton">
      {props.children}
    </button>
  );
}
```

Los componentes React ocultan sus detalles de implementación, incluyendo su salida renderizada. Otros componentes que usen `FancyButton` **usualmente no necesitarán** [obtener una ref](https://es.reactjs.org/docs/refs-and-the-dom.html) del elemento DOM interno `button`. Esto es bueno, ya que previene que los componentes dependan demasiado de la estructura DOM de otros.

Aunque dicho encapsulamiento es deseable para componentes a nivel de aplicación como `FeedStory` o `Comment`, puede ser inconveniente en el caso de componentes “hoja” altamente reutilizables como `FancyButton` o `MyTextInput`. Estos componentes tienden a ser usados a lo largo de las aplicaciones de forma similar a los componentes DOM `button` e `input`, y acceder sus nodos DOM puede resultar inevitable para gestionar el foco, la selección, o animaciones.

**El Reenvío de refs es una característica opcional que permite a algunos componentes tomar una `ref` que reciben, y pasarla (en otras palabras, “reenviarla”) a un hijo.**

En el siguiente ejemplo, `FancyButton` usa `React.forwardRef` para obtener la `ref` que le pasaron, y luego reenviarla al `button` DOM que renderiza:

```jsx
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// Ahora puedes obtener una referencia directa al botón del DOM:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

De esta forma, los componentes que usan `FancyButton` pueden obtener una ref al nodo DOM `button` subyacente, y accederlo si es necesario - tal como si estuvieran usando el `button` DOM directamente.

A continuación un explicación paso a paso de lo que sucede en el ejemplo de arriba:

1.  Creamos una [ref React](https://es.reactjs.org/docs/refs-and-the-dom.html) llamando `React.createRef` y la asignamos a la variable `ref`.
2.  Pasamos nuestra `ref` hacia `<FancyButton ref={ref}>` al especificarla como un atributo JSX.
3.  React pasa la `ref` a la función `(props, ref) => ...` dentro de `forwardRef` como segundo argumento.
4.  Reenviamos este argumento `ref` hacia `<button ref={ref}>` al especificarla como un atributo JSX.
5.  Cuando la ref es adjuntada, `ref.current` apuntará al nodo DOM `<button>`.

> **Nota**: El segundo argumento `ref` solo existe cuando defines un componente con una llamada a `React.forwardRef`. Los componentes normales de función o de clase no reciben el argumento `ref` y ref támpoco está disponible entre sus props.
> 
> El Reenvío de refs no esta limitado únicamente a componentes DOM. También se puede reenviar refs a instancias de componentes de clase.

## Nota para los mantenedores de bibliotecas de componentes

**Una vez empiezas a usar `forwardRef` en una biblioteca de componentes, debes tratarlo como un cambio incompatible y liberar una nueva versión mayor de la biblioteca**. Esto es debido a que probablemente tu biblioteca tendrá un comportamiento observable muy diferente (tal como a que se asignan las refs, y que tipos son exportados), y esto puede romper aplicaciones y otras bibliotecas que dependan del comportamiento anterior.

Aplicar `React.forwardRef` de forma condicional cuando existe tampoco es recomendado por las mismas razones: cambia el comportamiento de tu biblioteca y puede romper las aplicaciones de tus usuarios cuando actualicen React.

## Reenviando refs en componentes de orden superior

Esta técnica puede ser particularmente útil con [componentes de orden superior](https://es.reactjs.org/docs/higher-order-components.html) (también conocidos como `HOCs` por las siglas en inglés de _Higher-Order Components_). Comencemos con un ejemplo de un HOC que imprime los props de un componente a la consola:

```jsx
function logProps(WrappedComponent) {
  class LogProps extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('old props:', prevProps);
      console.log('new props:', this.props);
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  }

  return LogProps;
}
```

El HOC “logProps” pasa todas sus `props` al componente que envuelve, así que la salida renderizada será la misma. Por ejemplo, podemos usar este HOC para imprimir todas las `props` que son pasadas a nuestro componente “FancyButton”:

```jsx
class FancyButton extends React.Component {
  focus() {
    // ...
  }

  // ...
}

// En lugar de exportar FancyButton, exportamos LogProps.
// Esto renderizará un FancyButton igualmente.
export default logProps(FancyButton);
```

Hay un detalle en el ejemplo anterior: las refs no son pasadas. Esto es porque `ref` no es una prop. Al igual que `key`, es manejada de una forma diferente por React. Si añades una ref a un HOC, la ref se referirá al componente contenedor más externo, no al componente envuelto.

Esto significa que las `refs` que queremos para nuestro componente `FancyButton` de hecho estarán adjuntadas al componente `LogProps`:

```jsx
import FancyButton from './FancyButton';

const ref = React.createRef();

// El componente FancyButton que importamos es el HOC LogProps.
// Aun así la salida renderizada será la misma,
// nuestra referencia apuntará a LogProps en lugar del componente FancyButton interno!
// Esto significa que no podemos llamar a por ejemplo: ref.current.focus()
<FancyButton
  label="Click Me"
  handleClick={handleClick}
  ref={ref}
/>;
```

Afortunadamente, podemos reenviar explícitamente refs al componente interno `FancyButton` usando el API `React.forwardRef`. 
`React.forwardRef` acepta una función de renderizado que recibe los parámetros `props` y `ref`, y devuelve un nodo React. Por ejemplo:

```jsx
function logProps(Component) {
  class LogProps extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('old props:', prevProps);
      console.log('new props:', this.props);
    }

    render() {
      const {forwardedRef, ...rest} = this.props;

      // Assign the custom prop "forwardedRef" as a ref
      return <Component ref={forwardedRef} {...rest} />;
    }
  }

  // Mira el segundo parámetro "ref" suministrado por React.forwardRef.
  // Podemos pasarlo a LogProps como una prop regular, por ejemplo: "forwardedRef"
  // Y puede ser agregado al "Component".
  return React.forwardRef((props, ref) => {
    return <LogProps {...props} forwardedRef={ref} />;
  });
}
```

## Mostrar un nombre personalizado en las herramientas de desarrollo

`React.forwardRef` acepta una función de renderizado. Las herramientas de desarrollo de React (_React DevTools_) usan esta función para determinar que nombre mostrar para el componente que hace el reenvio.

Por ejemplo, el siguiente componente aparecerá como ”_ForwardRef_” en _DevTools_:

```jsx
const WrappedComponent = React.forwardRef((props, ref) => {
  return <LogProps {...props} forwardedRef={ref} />;
});
```

Si nombras la función, _DevTools_ también incluirá su nombre (Ej: ”_ForwardRef(myFunction)_”):

```jsx
const WrappedComponent = React.forwardRef(
  function myFunction(props, ref) {
    return <LogProps {...props} forwardedRef={ref} />;
  }
);
```

Puedes incluso asignar la propiedad `displayName` de la función para que incluya el componente que estás envolviendo:

```jsx
function logProps(Component) {
  class LogProps extends React.Component {
    // ...
  }

  function forwardRef(props, ref) {
    return <LogProps {...props} forwardedRef={ref} />;
  }

  // Give this component a more helpful display name in DevTools.
  // e.g. "ForwardRef(logProps(MyComponent))"
  const name = Component.displayName || Component.name;
  forwardRef.displayName = `logProps(${name})`;

  return React.forwardRef(forwardRef);
}
```