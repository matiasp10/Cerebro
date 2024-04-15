Considera la declaración de esta variable:

```jsx
const element = <h1>Hello, world!</h1>;
```

Esta curiosa sintaxis de etiquetas no es **ni un string ni HTML**.

Se llama **JSX**, y es una **extensión de la sintaxis de JavaScript**. Recomendamos usarlo con React para describir cómo debería ser la interfaz de usuario. JSX puede recordarte a un lenguaje de plantillas, pero viene con todo el poder de JavaScript.

JSX produce “**elementos**” de React.

### ¿Por qué JSX?

React acepta el hecho de que la lógica de renderizado está intrínsecamente unida a la lógica de la interfaz de usuario: cómo se manejan los eventos, cómo cambia el estado con el tiempo y cómo se preparan los datos para su visualización.

En lugar de separar artificialmente _tecnologías_ poniendo el **maquetado** y la **lógica** en archivos separados, React separa intereses con unidades ligeramente acopladas llamadas “**componentes**” que contienen ambas.

React no requiere usar **JSX**, pero la mayoría de la gente lo encuentra útil como ayuda visual cuando trabajan con interfaz de usuario dentro del código Javascript. Esto también permite que React muestre mensajes de error o advertencia más útiles.

### Insertando expresiones en JSX

En el ejemplo a continuación, declaramos una variable llamada `name` y luego la usamos dentro del JSX envolviéndola dentro de llaves:

```jsx
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;
```

Puedes poner cualquier **expresion de JavaScript** dentro de llaves en JSX. Por ejemplo, `2 + 2`, `user.firstName`, o `formatName(user)` son todas expresiones válidas de Javascript.

En el ejemplo a continuación, insertamos el resultado de llamar la función de JavaScript, `formatName(user)`, dentro de un elemento `<h1>`.

```jsx
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
	<h1>
	    Hello, {formatName(user)}!  
    </h1>
);
```

Dividimos JSX en varias líneas para facilitar la lectura. Aunque no es necesario, cuando hagas esto también te recomendamos envolverlo entre paréntesis para evitar errores por la **insercion automatica del punto y coma**.

### JSX también es una expresión

Después de **compilarse**, las **expresiones** JSX se convierten en **llamadas a funciones JavaScript regulares y se evalúan en objetos JavaScript**.

Esto significa que puedes usar JSX dentro de declaraciones `if` y bucles `for`, asignarlo a variables, aceptarlo como argumento, y retornarlo desde dentro de funciones:

```jsx
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;  
    }
  return <h1>Hello, Stranger.</h1>;
}
```

### Especificando atributos con JSX

Puedes utilizar **comillas** para especificar strings literales como atributos:

```jsx
const element = <a href="https://www.reactjs.org"> link </a>;
```

También puedes usar **llaves** para insertar una expresión JavaScript en un atributo:

```jsx
const element = <img src={user.avatarUrl}></img>;
```

**No pongas comillas rodeando llaves** cuando insertes una expresión JavaScript en un atributo. Debes utilizar **comillas** (para los valores de los strings) o **llaves** (para las expresiones), pero no ambas en el mismo atributo.

> **Advertencia:** Dado que JSX es más cercano a JavaScript que a HTML, React DOM usa la convención de nomenclatura `camelCase` en vez de nombres de atributos HTML. Por ejemplo, `class` se vuelve `className` en JSX, y `tabindex` se vuelve `tabIndex`.

### Especificando hijos con JSX

Si una etiqueta está vacía, **puedes cerrarla inmediatamente** con `/>`, como en XML:

```jsx
const element = <img src={user.avatarUrl} />;
```

Las etiquetas de Javascript pueden contener hijos:

```jsx
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

### JSX previene ataques de inyección

Es seguro insertar datos ingresados por el usuario en JSX:

```jsx
const title = response.potentiallyMaliciousInput;
// Esto es seguro:
const element = <h1>{title}</h1>;
```

Por defecto, React DOM escapa cualquier valor insertado en JSX antes de renderizarlo. De este modo, **se asegura de que nunca se pueda insertar nada que no esté explícitamente escrito en tú aplicación**. Todo es convertido en un string antes de ser renderizado. Esto ayuda a prevenir vulnerabilidades [XSS (cross-site-scripting)](https://es.wikipedia.org/wiki/Cross-site_scripting).

### JSX representa objetos

Babel compila JSX a llamadas de `React.createElement()`.

Estos dos ejemplos son idénticos:

```jsx
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```jsx
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

`React.createElement()` realiza algunas comprobaciones para ayudarte a escribir código libre de errores, pero, en esencia crea un **objeto** como este:

```jsx
// Nota: Esta estructura está simplificada
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

Estos objetos son llamados “**Elementos de React**”. Puedes pensar en ellos como descripciones de lo que quieres ver en pantalla. React lee estos objetos y los usa para construir el DOM y mantenerlo actualizado.