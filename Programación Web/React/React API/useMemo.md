```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

Devuelve un valor [memorizado](https://en.wikipedia.org/wiki/Memoization).

Pasa una función de “crear” y un arreglo de dependencias. `useMemo` solo volverá a calcular el valor memorizado cuando una de las dependencias haya cambiado. Esta optimización ayuda a evitar cálculos costosos en cada render.

Recuerde que la función pasada a `useMemo` se ejecuta durante el renderizado. No hagas nada allí que normalmente no harías al renderizar. Por ejemplo, los efectos secundarios pertenecen a `useEffect`, no a`useMemo`.

Si no se proporciona un arreglo, se calculará un nuevo valor en cada renderizado.

**Puede confiar en `useMemo` como una optimización del rendimiento, no como una garantía semántica.** En el futuro, React puede elegir “olvidar” algunos valores previamente memorizados y recalcularlos en el próximo renderizado, por ejemplo para liberar memoria para componentes fuera de pantalla. Escribe tu código para que aún funcione sin `useMemo` - y luego agrégalo para optimizar el rendimiento.

> Nota
> 
> El arreglo de dependencias no se pasa como argumentos a la función. Sin embargo, conceptualmente, eso es lo que representan: cada valor al que se hace referencia dentro de la función también debe aparecer en el arreglo de dependencias. En el futuro, un compilador lo suficientemente avanzado podría crear este arreglo automáticamente.
> 
> Recomendamos usar la regla [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) que forma parte de nuestro paquete [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation). Esta regla advierte cuando las dependencias se especifican incorrectamente y sugiere una solución.