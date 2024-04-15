```
useImperativeHandle(ref, createHandle, [deps])
```

`useImperativeHandle` personaliza el valor de instancia que se expone a los componentes padres cuando se usa`ref`. Como siempre, el código imperativo que usa refs debe evitarse en la mayoría de los casos. `useImperativeHandle` debe usarse con [`forwardRef`](https://es.reactjs.org/docs/react-api.html#reactforwardref):

```jsx
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />;
}
FancyInput = forwardRef(FancyInput);
```

En este ejemplo, un componente padre que muestra `<FancyInput ref={inputRef} />` podría llamar a `inputRef.current.focus()`.

### [](https://es.reactjs.org/docs/hooks-reference.html#uselayouteffect)`   `