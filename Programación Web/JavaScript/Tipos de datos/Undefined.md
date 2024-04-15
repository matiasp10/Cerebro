Al igual que null, el valor especial _undefined_ forma un tipo propio y su único valor es `undefined`.

El significado de `undefined` es “_valor no asignado_”.

Si una variable es declarada, pero no asignada, entonces su valor es `undefined`:

```js
let age;

alert(age); // muestra "undefined"
```

> [!caution] Asignar undefined a las variables
> Técnicamente, es posible asignar undefined a cualquier variable
> 
> ```js
> let age = 100;
> 
> // cambiando el valor a undefined
> age = undefined;
> 
> alert(age); // "undefined"
> ```
> …Pero no se recomienda hacer eso. Normalmente, usamos null para asignar un valor “_vacío_” o “_desconocido_” a una variable, mientras undefined es un _valor inicial reservado para cosas que no han sido asignadas_.



