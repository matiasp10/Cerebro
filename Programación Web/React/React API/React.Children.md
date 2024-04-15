`React.Children` proporciona utilidades para lidiar con la estructura de datos opaca de `this.props.children`.

#### `React.Children.map`

```
React.Children.map(children, function[(thisArg)])
```

Invoca una función en cada hijo inmediato dentro de `children` con `this` establecido a `thisArg`. Si `children` es un array, será recorrido y la función será llamada para cada hijo en el array. Si children es `null` o `undefined`, este método retornará `null` o `undefined` en vez de un array.

> Nota
> 
> Si `children` es un `Fragment` será tratado como un hijo único y no será recorrido.

#### `React.Children.forEach`

```
React.Children.forEach(children, function[(thisArg)])
```

Es como [`React.Children.map()`](https://es.reactjs.org/docs/react-api.html#reactchildrenmap) pero no retorna un array.

#### `React.Children.count`

```
React.Children.count(children)
```

Retorna el número total de componentes en `children`, igual al número de veces que un callback pasado a `map` o `forEach` sería invocado.

#### `React.Children.only`

```
React.Children.only(children)
```

Verifica que `children` solo tenga un hijo (un elemento React) y lo retorna. De otro modo este método lanza un error.

> Nota:
> 
> `React.Children.only()` no acepta el valor retornado de [`React.Children.map()`](https://es.reactjs.org/docs/react-api.html#reactchildrenmap) porque es un array en lugar de un elemento React.

#### `React.Children.toArray`

```
React.Children.toArray(children)
```

Retorna la estructura de datos opaca de `children` como un array plano con keys asignadas a cada hijo. Es útil si se desea manipular colecciones de hijos en los métodos de renderización, particularmente si se desea reordenar o segmentar `this.props.children` antes de pasarlo.

> Nota:
> 
> `React.Children.toArray()` cambia las keys para preservar las semánticas de los array anidados cuando se aplanan listas de hijos. Esto quiere decir que `toArray` antepone cada key en el array retornado de modo que cada elemento de key esté dentro del alcance del array de entrada que lo contiene.
