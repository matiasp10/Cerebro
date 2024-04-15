```jsx
useInsertionEffect(didUpdate);
```

The signature is identical to `useEffect`, but it fires synchronously _before_ all DOM mutations. Use this to inject styles into the DOM before reading layout in [`useLayoutEffect`](https://es.reactjs.org/docs/hooks-reference.html#uselayouteffect). Since this hook is limited in scope, this hook does not have access to refs and cannot schedule updates.

> Note:
> 
> `useInsertionEffect` should be limited to css-in-js library authors. Prefer [`useEffect`](https://es.reactjs.org/docs/hooks-reference.html#useeffect) or [`useLayoutEffect`](https://es.reactjs.org/docs/hooks-reference.html#uselayouteffect) instead.