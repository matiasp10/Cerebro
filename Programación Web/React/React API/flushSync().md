```jsx
flushSync(callback)
```

Obliga a React a ejecutar síncronamente todas las actualizaciones dentro del _callback_ proporcionado. Así se asegura que el DOM se actualiza inmediatamente.

````jsx
// Obliga a que esta actualización del estado sea síncrona.
flushSync(() => {
  setCount(count + 1);
});
// En este punto, el DOM está actualizado.
````

> Nota:
> 
> `flushSync` puede afectar significativamente el rendimiento. Úsalo con moderación.
> 
> `flushSync` puede obligar a las barreras Suspense pendientes a que muestren su estado `fallback`.
> 
> `flushSync` puede también ejecutar los efectos pendientes y aplicar sincrónicamente cualquier actualización que estas contengan antes de retornar.
> 
> `flushSync` también puede ejecutar actualizaciones fuera del *callback* cuando sea necesario para ejecutar la actualizaciones dentro del *callback*. Por ejemplo, si hay actualizaciones pendientes de un clic, React puede ejecutar esas antes de ejecutar las actualizaciones dentro del *callback*.