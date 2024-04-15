Los Hooks te permiten utilizar diferentes características de React desde tus componentes. Puedes usar los Hooks incorporados o combinarlos para crear los tuyos propios. 
____
## Hooks de estado

El estado permite que un componente "**recuerde**" información como la introducida por el usuario. Por ejemplo, un componente de formulario puede utilizar el estado para almacenar el valor de la entrada, mientras que un componente de galería de imágenes puede utilizar el estado para almacenar el índice de la imagen seleccionada.  

Para añadir estado a un componente, utilice uno de estos ganchos:  
  
- **`useState`** declara una variable de estado que puede actualizar directamente.  
- **`useReducer`** declara una variable de estado con la lógica de actualización dentro de una función reductora.

```jsx
function ImageGallery() {
  const [index, setIndex] = useState(0);
  // ...
```
## Hooks de contexto

El contexto permite que un componente _reciba información de componentes padre distantes sin pasarla como `props`_. Por ejemplo, el componente de nivel superior de tu aplicación puede pasar el tema de interfaz de usuario actual a todos los componentes inferiores, independientemente de su profundidad.  

- **`useContext`** lee y se suscribe a un contexto.

```jsx
function Button() {
  const theme = useContext(ThemeContext);
  // ...
```
## Hooks de referencia

Las referencias permiten que un componente _contenga información que no se utiliza para el renderizado_, como un nodo DOM o un ID de tiempo de espera. A diferencia del estado, la actualización de una referencia no vuelve a renderizar el componente. Los `Refs` son una "**escotilla de escape**" del paradigma `React`. Son útiles cuando necesitas trabajar con sistemas que no son `React`, como las `APIs` integradas del navegador.  
  
- **`useRef`** declara una `ref`. Puedes guardar cualquier valor en ella, pero la mayoría de las veces se usa para guardar un nodo DOM.  
- **`useImperativeHandle`** te permite personalizar la `ref` expuesta por tu componente. Rara vez se utiliza.

```jsx
function Form() {
  const inputRef = useRef(null);
  // ...
```
## Hooks de efecto

Los efectos permiten que un componente _se conecte y sincronice con sistemas externos_. Esto incluye el manejo de la red, el DOM del navegador, las animaciones, los widgets escritos con una biblioteca de interfaz de usuario diferente y otro código que no sea de `React`.  

- **`useEffect`** conecta un componente a un sistema externo.

```jsx
function ChatRoom({ roomId }) {
  useEffect(() => {
    const connection = createConnection(roomId);
    connection.connect();
    return () => connection.disconnect();
  }, [roomId]);
  // ...
```

Los efectos son una "**escotilla de escape**" del paradigma `React`. No uses Efectos para orquestar el flujo de datos de tu aplicación. Si no estás interactuando con un sistema externo, puede que no necesites un efecto.  
  
Hay dos variaciones de `useEffect` poco utilizadas con diferencias en la temporización:  
  
- **`useLayoutEffect`** se dispara antes de que el navegador repinte la pantalla. Puedes medir el layout aquí.  
- **`useInsertionEffect`** se activa antes de que React haga cambios en el DOM. Las bibliotecas pueden insertar CSS dinámico aquí.
## Hooks de rendimiento

Una forma común de optimizar el rendimiento del re renderizado es **omitir el trabajo innecesario**. Por ejemplo, puedes indicarle a `React` que reutilice un cálculo almacenado en caché o que omita una nueva renderización si los datos no han cambiado desde la renderización anterior.  
  
Para omitir cálculos y re renderizaciones innecesarias, utiliza uno de estos Hooks:  
  
- **`useMemo`** te permite almacenar en caché el resultado de un cálculo costoso.  
- **`useCallback`** permite almacenar en caché la definición de una función antes de pasarla a un componente optimizado.

```jsx
function TodoList({ todos, tab, theme }) {
  const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
  // ...
}
```

A veces, no se puede omitir el re renderizado porque la pantalla necesita actualizarse. En ese caso, puedes mejorar el rendimiento separando las actualizaciones bloqueantes que deben ser síncronas (como escribir en una entrada) de las actualizaciones no bloqueantes que no necesitan bloquear la interfaz de usuario (como actualizar un gráfico).  

Para priorizar el renderizado, utilice uno de estos ganchos:  

- **`useTransition`** le permite marcar una transición de estado como no bloqueante y permitir que otras actualizaciones la interrumpan.  
- **`useDeferredValue`** le permite aplazar la actualización de una parte no crítica de la interfaz de usuario y dejar que otras partes se actualicen primero.
## Hooks de recursos

Un componente puede **acceder a los recursos sin que formen parte de su estado**. Por ejemplo, un componente puede leer un mensaje de una promesa o leer información de estilo de un contexto.  
  
Para leer un valor de un recurso, utiliza este Hook:  
  
- **`use`** le permite leer el valor de un recurso como una Promesa o un contexto.

```jsx
function MessageComponent({ messagePromise }) {
  const message = use(messagePromise);
  const theme = use(ThemeContext);
  // ...
}
```
## Otros hooks

Estos ganchos son útiles sobre todo para los autores de bibliotecas y no se utilizan habitualmente en el código de la aplicación.  
  
- **`useDebugValue`** te permite personalizar la etiqueta que `React DevTools` muestra para tu Hook personalizado.  
- **`useId`** permite a un componente asociar un ID único consigo mismo. Típicamente usado con `APIs` de accesibilidad.  
- **`useSyncExternalStore`** permite a un componente suscribirse a un almacén externo.