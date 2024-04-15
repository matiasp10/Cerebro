```
unmountComponentAtNode(contenedor)
```

> Nota:
> 
> `unmountComponentAtNode` ha sido reemplazado con `root.unmount()` en React 18. Consulta [createRoot](https://es.reactjs.org/docs/react-dom-client.html#createroot) para más información.

Elimina un componente React ya montado en el DOM, y limpia sus manejadores de eventos y estado. Si ningún componente fue montado en el contenedor, llamar a esta función no hará nada. Retorna `true` si un componente fue desmontado, y `false` si no hay algún componente para desmontar.