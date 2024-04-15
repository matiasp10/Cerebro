```
UNSAFE_componentWillMount()
```

> Nota
> 
> Este ciclo de vida se llamaba anteriormente `componentWillMount`. Ese nombre seguirá funcionando hasta la versión 17. Usa la [`rename-unsafe-lifecycles` codemod](https://github.com/reactjs/react-codemod#rename-unsafe-lifecycles) para actualizar automaticamente tus componentes.

`UNSAFE_componentWillMount()` se invoca justo antes de que el montaje ocurra. Es llamado antes de `render()`, por lo tanto, al llamar a `setState()` de forma síncrona en este método no se activará una representación adicional. En general, recomendamos usar el `constructor()` en lugar de inicializar el estado.

Evite introducir efectos secundarios o suscripciones en este método. Para estos casos de uso, use `componentDidMount()` en su lugar.

Este ciclo de vida es el único método que se llama en el renderizado en el lado de servidor.