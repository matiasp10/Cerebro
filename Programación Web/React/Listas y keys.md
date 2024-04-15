Primero, vamos a revisar como transformar listas en Javascript.

Dado el código de abajo, usamos la función [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) para tomar un array de `numbers` y duplicar sus valores. Asignamos el nuevo array devuelto por `map()` a la variable `doubled` y la mostramos:

```jsx
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
```

Este código muestra `[2, 4, 6, 8, 10]` a la consola.

En React, transformar arrays en listas de [elementos](https://es.reactjs.org/docs/rendering-elements.html) es casi idéntico.

### Renderizado de Múltiples Componentes

Puedes hacer colecciones de elementos e [incluirlos en JSX](https://es.reactjs.org/docs/introducing-jsx.html#embedding-expressions-in-jsx) usando llaves `{}`.

Debajo, recorreremos el array `numbers` usando la función [`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) de Javascript. Devolvemos un elemento `<li>` por cada ítem . Finalmente, asignamos el array de elementos resultante a `listItems`:

```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>  <li>{number}</li>);
```

Entonces, podemos incluir el array `listItems` completo dentro de un elemento `<ul>`:

```jsx
<ul>{listItems}</ul>
```

[**Pruébalo en CodePen**](https://codepen.io/gaearon/pen/GjPyQr?editors=0011)

Este código muestra una lista de números entre 1 y 5.

### Componente básico de lista

Usualmente renderizarías listas dentro de un **componente**.

Podemos refactorizar el ejemplo anterior en un componente que acepte un array de `numbers` e imprima una lista de elementos.

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<NumberList numbers={numbers} />);
```

Cuando ejecutes este código, serás advertido que una key debería ser proporcionada para ítems de lista. Una “**key**” es un atributo especial string que debes incluir al crear listas de elementos.

Vamos a asignar una `key` a nuestra lista de ítems dentro de `numbers.map()` y arreglar el problema de la falta de key.

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}
```

[**Pruébalo en CodePen**](https://codepen.io/gaearon/pen/jrXYRR?editors=0011)

## Keys

Las keys ayudan a React a identificar que ítems han **cambiado**, son **agregados**, o son **eliminados**. Las keys deben ser dadas a los elementos dentro del array para darle a los elementos una identidad estable:

```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

La mejor forma de elegir una key es usando un string que identifique únicamente a un elemento de la lista entre sus hermanos. Habitualmente vas a usar **IDs** de tus datos como key:

```jsx
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

Cuando no tengas IDs estables para renderizar, puedes usar el índice del ítem como una key como último recurso:

```jsx
const todoItems = todos.map((todo, index) =>
  // Solo hacer esto si los items no tienen un ID estable.
  <li key={index}>
    {todo.text}
  </li>
);
```

No recomendamos usar índices para keys si el orden de los ítems puede cambiar. Esto puede impactar negativamente el rendimiento y puede causar problemas con el estado del componente. Revisa el artículo de Robin Pokorny para una [explicación en profundidad de los impactos negativos de usar un índice como key](https://robinpokorny.com/blog/index-as-a-key-is-an-anti-pattern/). Si eliges no asignar una key explícita a la lista de ítems, React por defecto usará índices como keys.

[[Reconciliacion]]

### Extracción de componentes con keys

Las keys **solo tienen sentido en el contexto del array que las envuelve**.

Por ejemplo, si [extraes](https://es.reactjs.org/docs/components-and-props.html#extracting-components) un componente `ListItem`, deberías mantener la key en los elementos `<ListItem />` del array en lugar de en el elemento `<li>` del propio `ListItem`.

**Ejemplo: Uso Incorrecto de Key**

```jsx
function ListItem(props) {
  const value = props.value;
  return (
    // Mal! No hay necesidad de especificar la key aquí:
    <li key={value.toString()}>
      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Mal! La key debería haber sido especificada aquí:
    <ListItem value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

**Ejemplo: Uso Correcto de Key**

```jsx
function ListItem(props) {
  // Correcto! No hay necesidad de especificar la key aquí:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correcto! La key debería ser especificada dentro del array.
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

[**Pruébalo en CodePen**](https://codepen.io/gaearon/pen/ZXeOGM?editors=0010)

Una buena regla es que los elementos dentro de `map()` **necesitan keys**.

### Las keys deben ser únicas solo entre hermanos

Las keys usadas dentro de arrays deberían ser únicas entre sus hermanos. Sin embargo, **no necesitan ser únicas globalmente**. Podemos usar las mismas keys cuando creamos dos arrays diferentes:

```jsx
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Blog posts={posts} />);
```

[**Pruébalo en CodePen**](https://codepen.io/gaearon/pen/NRZYGN?editors=0010)

Las keys sirven como una sugerencia para React pero no son pasadas a tus componentes. Si necesitas usar el mismo valor en tu componente, pásasela explícitamente como una propiedad con un nombre diferente:

```jsx
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

Con el ejemplo de arriba, el componente `Post` puede leer `props.id`, pero no `props.key`.

### Integrar map() en JSX

En los ejemplos de arriba declaramos una variable separada `listItems` y la incluimos en JSX:

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

JSX permite [integrar cualquier expresión](https://es.reactjs.org/docs/introducing-jsx.html#embedding-expressions-in-jsx) en llaves así que podemos alinear el resultado de `map()`:

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

[**Pruébalo en CodePen**](https://codepen.io/gaearon/pen/BLvYrB?editors=0010)

Algunas veces esto resulta más claro en código, pero este estilo también puede ser abusado. Como en JavaScript, depende de ti decidir cuando vale la pena extraer una variable por legibilidad. Ten en mente que si el cuerpo de `map()` está muy anidado, puede ser un buen momento para [extraer un componente](https://es.reactjs.org/docs/components-and-props.html#extracting-components).