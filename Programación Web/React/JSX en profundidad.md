Fundamentalmente, JSX solo proporciona azúcar sintáctica para la función `React.createElement(component, props, ...children)`. El código JSX:

```jsx
<MyButton color="blue" shadowSize={2}>
  Haz click en mí
</MyButton>
```

se compila en:

```jsx
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Haz click en mí'
)
```

También puedes utilizar la forma de cierre automático de la etiqueta si no hay hijos. Así:

```jsx
<div className="sidebar" />
```

se compila en:

```jsx
React.createElement(
  'div',
  {className: 'sidebar'}
)
```

Si deseas probar cómo cierto código JSX en específico se convierte a JavaScript, puedes probar [el compilador de Babel en línea](https://babeljs.io/repl/#?presets=react&code_lz=GYVwdgxgLglg9mABACwKYBt1wBQEpEDeAUIogE6pQhlIA8AJjAG4B8AEhlogO5xnr0AhLQD0jVgG4iAXyJA).

## Especificando el tipo de elemento React

La primera parte de una etiqueta JSX determina el tipo del elemento React.

Los tipos en mayúsculas indican que la etiqueta JSX se refiere a un componente React. Estas etiquetas se compilan en una referencia directa a la variable nombrada, por lo que si usas la expresión JSX `<Foo />`, `Foo` debe estar dentro del alcance.

### React debe estar al alcance

Como JSX se compila en llamadas a `React.createElement`, la biblioteca`React` también debe estar siempre dentro del alcance de tu código JSX.

Por ejemplo, ambas importaciones son necesarias en este código, a pesar de que `React` y `CustomButton` no están directamente referenciados desde JavaScript:

```jsx
import React from 'react';
import CustomButton from './CustomButton';

function WarningButton() {
  // retorna React.createElement(CustomButton, {color: 'red'}, null);
  return <CustomButton color="red" />;
}
```

Si no usas un _bundler_ de JavaScript y cargas React desde una etiqueta `<script>`, ya está dentro del alcance como el elemento global `React`.

### Usando la notación de punto para el tipo JSX

También puedes referirte a un componente React usando notación de punto desde JSX. Esto es conveniente si tienes un solo módulo que exporta muchos componentes de React. Por ejemplo, si `MyComponents.DatePicker` es un componente, puede usarlo directamente desde JSX con:

```jsx
import React from 'react';

const MyComponents = {
  DatePicker: function DatePicker(props) {
    return <div>Imagine a {props.color} datepicker here.</div>;
  }
}

function BlueDatePicker() {
  return <MyComponents.DatePicker color="blue" />;
}
```

### Los componentes definidos por el usuario deben estar en mayúsculas

Cuando un tipo de elemento comienza con una letra minúscula, se refiere a un componente incorporado como `<div>` o `<span>` y da como resultado una cadena `'div'` o `'span'` que se pasa a `React.createElement`. Los tipos que comienzan con una letra mayúscula como `<Foo />` compilan a `React.createElement(Foo)` y corresponden a un componente definido o importado en tu archivo JavaScript.

Recomendamos nombrar los componentes con una letra mayúscula. Si tienes un componente que comienza con una letra minúscula, asígnalo a una variable en mayúscula antes de usarlo en JSX.

Por ejemplo, este código no se ejecutará como se esperaba:

```jsx
import React from 'react';

// ¡Incorrecto! Este es un componente y debería comenzar con mayúscula:
function hello(props) {
  // ¡Correcto! Este uso de <div> es legítimo porque div es una etiqueta HTML válida:
  return <div>Hello {props.toWhat}</div>;
}

function HelloWorld() {
  // ¡Incorrecto! React piensa que <hola /> es una etiqueta HTML porque no está en mayúscula:
  return <hello toWhat="World" />;
}
```

Para solucionar este problema, cambiaremos el nombre de `hello` a `Hello` y usaremos `<Hello />` cuando nos refiramos a el:

```jsx
import React from 'react';

// ¡Correcto! Este es un componente y debe comenzar con mayúscula:
function Hello(props) {
  // ¡Correcto! Este uso de <div> es legítimo porque div es una etiqueta HTML válida:
  return <div>Hello {props.toWhat}</div>;
}

function HelloWorld() {
  // ¡Correcto! React sabe que <Hello /> es un componente porque está en mayúsculas.
  return <Hello toWhat="World" />;
}
```

### Elegir el tipo en tiempo de ejecución

No puedes utilizar una expresión general como el tipo de elemento React. Si deseas usar una expresión general para indicar el tipo de elemento, primero asígnala a una variable en mayúscula. Esto ocurre a menudo cuando se desea generar un componente diferente basado en un prop:

```jsx
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  // ¡Incorrecto! El tipo JSX no puede ser una expresión.
  return <components[props.storyType] story={props.story} />;
}
```

Para solucionar esto, primero asignaremos el tipo a una variable en mayúscula:

```jsx
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  // ¡Correcto! El tipo JSX puede ser una variable en mayúscula.
  const SpecificStory = components[props.storyType];
  return <SpecificStory story={props.story} />;
}
```

## Props en JSX

Hay varias formas diferentes de especificar props en JSX.

### Expresiones JavaScript como props

Puede pasar cualquier expresión de JavaScript como prop, al rodearla con `{}`. Por ejemplo, en este JSX:

```
<MyComponent foo={1 + 2 + 3 + 4} />
```

Para `MyComponent`, el valor de `props.foo` será `10` porque se evalúa la expresión `1 + 2 + 3 + 4`.

Las sentencias `if` y los bucles `for` no son expresiones en JavaScript, por lo que no se pueden usar directamente en JSX. En su lugar, puede poner estos en el código circundante. Por ejemplo:

```jsx
function NumberDescriber(props) {
  let description;
  if (props.number % 2 == 0) {
    description = <strong>even</strong>;
  } else {
    description = <i>odd</i>;
  }
  return <div>{props.number} is an {description} number</div>;
}
```

Puedes obtener más información sobre [renderizado condicional](https://es.reactjs.org/docs/conditional-rendering.html) y [bucles](https://es.reactjs.org/docs/lists-and-keys.html) en las secciones correspondientes.

### Literales _string_

Puede pasar un literal _string_ como prop. Estas dos expresiones JSX son equivalentes:

```jsx
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

Cuando se pasa un literal _string_, su valor es HTML sin escapar. Así que estas dos expresiones JSX son equivalentes:

```jsx
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />
```

Este comportamiento no suele ser relevante. Sólo se menciona aquí en aras de ser exhaustivos.

### Los props son por defecto “true”

Si no pasas ningún valor para un prop, el valor predeterminado es `true`. Estas dos expresiones JSX son equivalentes:

```jsx
<MyTextBox autocomplete />

<MyTextBox autocomplete={true} />
```

En general, no recomendamos usarlo porque puede confundirse con la [notación simplificada de objetos ES6](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015) `{foo}` que es la abreviatura de `{foo: foo}` en lugar de `{foo: true}`. Este comportamiento está para que coincida con el de HTML.

### Atributos de propagación

Si ya tienes `props` como objeto, y quiere pasarlo en JSX, puedes usar `...` como sintaxis de “propagación” para pasar el objeto de props completo. Estos dos componentes son equivalentes:

```jsx
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

También puedes elegir props específicos que su componente consumirá al pasar todos los demás props utilizando la sintaxis de propagación.

```jsx
const Button = props => {
  const { kind, ...other } = props;
  const className = kind === "primary" ? "PrimaryButton" : "SecondaryButton";
  return <button className={className} {...other} />;
};

const App = () => {
  return (
    <div>
      <Button kind="primary" onClick={() => console.log("clicked!")}>
        Hello World!
      </Button>
    </div>
  );
};
```

En el ejemplo anterior, el prop `kind` se consume de forma segura _y no_ se pasa al elemento `<button>` en el DOM. Todos los demás props se pasan a través del objeto `...other` que hace que este componente sea realmente flexible. Puedes ver que pasa un `onClick` y `children` props.

Los atributos de propagación pueden ser útiles, pero también facilitan la transferencia de propiedades innecesarias a los componentes que no les interesan o la transferencia de atributos HTML no válidos al DOM. Recomendamos utilizar esta sintaxis con moderación.

## Hijos en JSX

En las expresiones JSX que contienen una etiqueta de apertura y una etiqueta de cierre, el contenido entre esas etiquetas se pasa como un elemento especial: `props.children`. Hay varias maneras diferentes de pasar a los hijos:

### Cadenas de Literales

Puede poner un _string_ entre las etiquetas de apertura y cierre y `props.children` será solo ese _string_. Esto es útil para muchos de los elementos HTML integrados. Por ejemplo:

```jsx
<MyComponent>Hello world!</MyComponent>
```

Esto es JSX válido, y `props.children` en `MyComponent` simplemente será el _string_ `Hello world!`. El código HTML no se ha escapado, por lo que generalmente puedes escribir JSX de la misma manera que escribirías HTML de esta manera:

```jsx
<div>This is valid HTML &amp; JSX at the same time.</div>
```

JSX elimina los espacios en blanco al principio y al final de una línea. También elimina las líneas en blanco. Se eliminan las nuevas líneas adyacentes a las etiquetas, las nuevas líneas que se producen en medio de literales de _string_ se condensan en un solo espacio. Así que todo esto se traduce en lo mismo:

```jsx
<div>Hello World</div>

<div>
  Hello World
</div>

<div>
  Hello
  World
</div>

<div>

  Hello World
</div>
```

### Los hijos JSX

Puedes proporcionar más elementos JSX como hijos. Esto es útil para mostrar componentes anidados:

```jsx
<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
```

Puedes mezclar diferentes tipos de hijos, así que puedes usar literales de _string_ junto con hijos JSX. Esta es otra forma en la que JSX es como HTML, de modo que es tanto JSX válido como HTML válido:

```jsx
<div>
  Here is a list:
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
  </ul>
</div>
```

Un componente de React también puede retornar un array de elementos:

```jsx
render() {
  // ¡No es necesario envolver los elementos de la lista en un elemento adicional!
  return [
    // No olvides las llaves :)
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}
```

### Expresiones de JavaScript como hijos

Puedes pasar cualquier expresión de JavaScript como hijos, encerrándola dentro de `{}`. Por ejemplo, estas expresiones son equivalentes:

```jsx
<MyComponent>foo</MyComponent>

<MyComponent>{'foo'}</MyComponent>
```

Esto suele ser útil para representar una lista de expresiones JSX de longitud arbitraria. Por ejemplo, esto renderiza una lista HTML:

```jsx
function Item(props) {
  return <li>{props.message}</li>;
}

function TodoList() {
  const todos = ['finish doc', 'submit pr', 'nag dan to review'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
    </ul>
  );
}

```

Las expresiones de JavaScript se pueden mezclar con otros tipos de hijos. Esto suele ser útil en lugar de _string templates_:

```jsx
function Hello(props) {
  return <div>Hello {props.addressee}!</div>;
}
```

### Funciones como hijos

Normalmente, las expresiones de JavaScript insertadas en JSX se evaluarán como una cadena, un elemento React o una lista de esas cosas. Sin embargo, `props.children` funciona igual que cualquier otro prop, ya que puede pasar cualquier tipo de datos, no solo los tipos que React sabe cómo procesar. Por ejemplo, si tienes un componente personalizado, puedes hacer que tome un _callback_ como `props.children`:

```jsx
// Llama al *callback* `numTimes` veces para producir un componente repetido
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>This is item {index} in the list</div>}
    </Repeat>
  );
}
```

Los hijos pasados a un componente personalizado pueden ser cualquier cosa, siempre que ese componente los transforme en algo que React pueda entender antes de renderizar. Este uso no es común, pero funciona si desea ampliar lo que JSX es capaz de hacer.

### Los booleanos, `null` y `undefined` se ignoran

`false`, `null`, `undefined` y `true` son hijos válidos. Simplemente no se renderizan. Estas expresiones JSX se renderizan todas a la misma forma:

```jsx
<div />

<div></div>

<div>{false}</div>

<div>{null}</div>

<div>{undefined}</div>

<div>{true}</div>
```

Esto puede ser útil para renderizar condicionalmente elementos React. Este JSX renderiza el componente `<Header />` solo si `showHeader` es`true`:

```jsx
<div>
  {showHeader && <Header />}
  <Content />
</div>
```

Una advertencia es que algunos [valores que se comportan como falsos](https://developer.mozilla.org/es/docs/Glossary/Falsy), como el número `0`, todavía son renderizados por React. Por ejemplo, este código no se comportará como se espera porque se imprimirá `0` cuando `props.messages` sea una arreglo vacío:

```jsx
<div>
  {props.messages.length &&
    <MessageList messages={props.messages} />
  }
</div>
```

Para solucionar esto, asegúrate de que la expresión antes de `&&` sea siempre booleana:

```jsx
<div>
  {props.messages.length > 0 &&
    <MessageList messages={props.messages} />
  }
</div>
```

Por el contrario, si desea que aparezca un valor como `false`, `true`, `null` o `undefined` en la salida, debes primero [convertirlo en una cadena](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/String#String_conversion):

```jsx
<div>
  My JavaScript variable is {String(myVariable)}.
</div>
```