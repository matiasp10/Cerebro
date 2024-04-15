La firma es idéntica a `useEffect`, pero se dispara de forma síncrona después de todas las mutaciones de DOM. Use esto para leer el diseño del DOM y volver a renderizar de forma sincrónica. Las actualizaciones programadas dentro de `useLayoutEffect` se vaciarán sincrónicamente, antes de que el navegador tenga la oportunidad de pintar.

Prefiera el `useEffect` estándar cuando sea posible para evitar el bloqueo de actualizaciones visuales.

> Consejo
> 
> Si estas migrando código de un componente de clase, recuerda que `useLayoutEffect` se activa en la misma fase que `componentDidMount` y `componentDidUpdate`. Sin embargo, **recomendamos empezar con `useEffect` primero** y solo intentar con `useLayoutEffect` si lo anterior causa problemas.
> 
> Si usas renderizado en el servidor, ten en cuenta que _ni_ `useLayoutEffect` ni `useEffect` pueden ejecutarse hasta que no se haya descargado el código JavaScript. Por eso es que React advierte cuando un componente renderizado en el servidor contiene `useLayoutEffect`. Para corregirlo, puedes o bien mover la lógica a `useEffect` (si no es necesaria para el primer renderizado), o retrasar el momento de mostrar el componente hasta después de que se haya renderizado el cliente (si el HTML luciera roto, hasta que se ejecute `useLayoutEffect`).
> 
> Para excluir del HTML renderizado en el servidor a un componente que necesita efectos de _layout_, renderízalo condicionalmente con `showChild && <Child />` y retrasa mostrarlo con `useEffect(() => { setShowChild(true); }, [])`. De esta manera, la interfaz de usuario no lucirá rota antes de la hidratación.