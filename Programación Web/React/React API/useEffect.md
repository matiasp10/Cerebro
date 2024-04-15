```
useEffect(didUpdate);
```

Acepta una función que contiene código imperativo, posiblemente código efectivo.

Las mutaciones, suscripciones, temporizadores, registro y otros efectos secundarios no están permitidos dentro del cuerpo principal de un componente de función (denominado como _render phase_ de React). Si lo hace, dará lugar a errores confusos e inconsistencias en la interfaz de usuario.

En su lugar, use `useEffect`. La función pasada a `useEffect` se ejecutará después de que el renderizado es confirmado en la pantalla. Piense en los efectos como una escotilla de escape de React del mundo puramente funcional al mundo imperativo.

Por defecto, los efectos se ejecutan después de cada renderizado completado, pero puede elegir ejecutarlo [solo cuando ciertos valores han cambiado](https://es.reactjs.org/docs/hooks-reference.html#conditionally-firing-an-effect).

#### Limpiando un efecto

A menudo, los efectos crean recursos que deben limpiarse antes de que el componente salga de la pantalla, como una suscripción o un ID de temporizador. Para hacer esto, la función pasada a `useEffect` puede devolver una función de limpieza. Por ejemplo, para crear una suscripción:

```jsx
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Limpiar la suscripción
    subscription.unsubscribe();
  };
});
```

La función de limpieza se ejecuta antes de que el componente se elimine de la interfaz de usuario para evitar pérdidas de memoria. Además, si un componente se procesa varias veces (como suele hacer), el **efecto anterior se limpia antes de ejecutar el siguiente efecto**. En nuestro ejemplo, esto significa que se crea una nueva suscripción en cada actualización. Para evitar disparar un efecto en cada actualización, consulte la siguiente sección.

#### Tiempo de los efectos

A diferencia de `componentDidMount` y`componentDidUpdate`, la función enviada a `useEffect` se inicia **después** de la disposición y pintada de la página, durante un evento diferido. Esto lo hace adecuado para los muchos efectos secundarios comunes, como la configuración de suscripciones y los controladores de eventos, porque la mayoría de los tipos de trabajo no deben impedir que el navegador actualice la pantalla.

Sin embargo, no todos los efectos pueden ser diferidos. Por ejemplo, una mutación de DOM que es visible para el usuario debe ejecutarse de manera sincrónica antes del siguiente render para que el usuario no perciba una inconsistencia visual. (La distinción es conceptualmente similar a la de los listeners de eventos pasivos y de los activos). Para estos tipos de efectos, React proporciona un Hook adicional llamado [`useLayoutEffect`](https://es.reactjs.org/docs/hooks-reference.html#uselayouteffect). Tiene la misma firma que `useEffect` y solo difiere de este último en cuándo se ejecuta.

Adicionalmente, a partir de React 18, la función que se pasa a `useEffect` se ejecutará sincrónicamente **antes** de las etapas de _layout_ y pintura cuando es el resulta de una entrada discreta del usuario como un clic, o cuando el resultado de una actualización envuelta en [`flushSync`](https://es.reactjs.org/docs/react-dom.html#flushsync). Este comportamiento permite que el resultado del efecto sea observado por un sistema de eventos o por quien llama a [`flushSync`](https://es.reactjs.org/docs/react-dom.html#flushsync).

> Nota
> 
> Esto solo afecta el tiempo de llamada de la función pasada a `useEffect` - las actualizaciones que se programan dentro de estos efectos aún se difieren. Esto es diferente a [`useLayoutEffect`](https://es.reactjs.org/docs/hooks-reference.html#uselayouteffect), que invoca la función y procesa las actualizaciones dentro de ella inmediatamente.

Aún en los casos en que `useEffect` se aplaza hasta después de que el navegador haya pintado, se garantiza que se activará antes de cualquier nuevo render. React siempre eliminará los efectos de un render anterior antes de comenzar una nueva actualización.

#### Disparar un efecto condicionalmente.

El comportamiento predeterminado para los efectos es ejecutar el efecto después de cada renderizado que se completa. De esa manera, siempre se recrea un efecto si cambia una de sus dependencias.

Sin embargo, esto puede ser excesivo en algunos casos, como el ejemplo de suscripción de la sección anterior. No necesitamos crear una nueva suscripción en cada actualización, solo si las propiedades de `source` han cambiado.

Para implementar esto, pase un segundo argumento a `useEffect` que es el conjunto de valores de los que depende el efecto. Nuestro ejemplo actualizado se verá así:

```jsx
useEffect(
  () => {
    const subscription = props.source.subscribe();
    return () => {
      subscription.unsubscribe();
    };
  },
  [props.source],
);
```

Ahora la suscripción solo se volverá a crear cuando cambie `props.source`.

> Nota
> 
> Si usas esta optimización, asegúrate de que incluyes **todos los valores del ámbito del componente (como props y estado) que cambien a lo largo del tiempo y que sean usados por el efecto**. De otra forma, tu código referenciará valores obsoletos de renderizados anteriores. Aprende más [cómo tratar con funciones](https://es.reactjs.org/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) y [qué hacer cuando el array cambia con mucha frecuencia](https://es.reactjs.org/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often).
> 
> Si quieres ejecutar un efecto y sanearlo solamente una vez (al montar y desmontar), puedes pasar un array vacío (`[]`) como segundo argumento. Esto le indica a React que el efecto no depende de _ningún_ valor proviniente de las props o el estado, de modo que no necesita volver a ejecutarse. Esto no se gestiona como un caso especial, obedece directamente al modo en el que siempre funcionan los arrays.
> 
> Si pasas un array vacío (`[]`), las props y el estado dentro del efecto siempre tendrán sus valores iniciales. Si bien pasar `[]` como segundo argumento se acerca al conocido modelo mental de `componentDidMount` y `componentWillUnmount`, a menudo hay [mejores](https://es.reactjs.org/docs/hooks-faq.html#is-it-safe-to-omit-functions-from-the-list-of-dependencies) [soluciones](https://es.reactjs.org/docs/hooks-faq.html#what-can-i-do-if-my-effect-dependencies-change-too-often) para evitar volver a ejecutar los efectos con demasiada frecuencia. Además, no olvides que React pospone la ejecución de `useEffect` hasta que el navegador finaliza el trazado, de modo que hacer algún trabajo extra no es tan problemático.
> 
> Recomendamos usar la regla [`exhaustive-deps`](https://github.com/facebook/react/issues/14920) que forma parte de nuestro paquete [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks#installation). Esta regla advierte cuando las dependencias se especifican incorrectamente y sugiere una solución.

El arreglo de entradas no se pasa como argumentos a la función de efecto. Sin embargo, conceptualmente, eso es lo que representan: cada valor al que se hace referencia dentro de la función de efecto también debería aparecer en el arreglo de entradas. En el futuro, un compilador lo suficientemente avanzado podría crear este arreglo automáticamente.