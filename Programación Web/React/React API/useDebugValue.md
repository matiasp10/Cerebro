```
useDebugValue(value)
```

`useDebugValue` puede usarse para mostrar una etiqueta para Hooks personalizados en React DevTools.

Por ejemplo, considera el Hook personalizado `useFriendStatus` descrito en [“Construyendo sus propios Hooks”](https://es.reactjs.org/docs/hooks-custom.html):

```jsx
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  // ...

  // Mostrar una etiqueta en DevTools junto a este Hook
  // por ejemplo: "FriendStatus: Online"
  useDebugValue(isOnline ? 'Online' : 'Offline');

  return isOnline;
}
```

> Consejo
> 
> No recomendamos agregar valores de depuración a cada Hook personalizado. Es más valioso para los Hooks personalizados que forman parte de bibliotecas compartidas.

#### Aplazar el formato de los valores de depuración

En algunos casos, formatear un valor para mostrar puede ser una operación costosa. También es innecesario a menos que un Hook sea realmente inspeccionado.

Por esta razón, `useDebugValue` acepta una función de formato como un segundo parámetro opcional. Esta función solo se llama si se inspeccionan los Hooks. Recibe el valor de depuración como parámetro y debe devolver un valor de visualización formateado.

Por ejemplo, un Hook personalizado que devolvió un valor de `Date` podría evitar llamar a la función `toDateString` innecesariamente al pasar el siguiente formateador:

```jsx
useDebugValue(date, date => date.toDateString());
```