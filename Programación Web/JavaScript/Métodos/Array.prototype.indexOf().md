El método **indexOf()** retorna el primer índice en el que se puede encontrar un elemento dado en el array, ó retorna _-1_ si el elemento no esta presente.

# Sintaxis

```js
array.indexOf(searchElement[, fromIndex])
```

## Parámetros

### searchElement

Elemento a encontrar en el array.

### fromIndex (Opcional)

Indica el índice por el que se comienza la búsqueda. Por defecto es 0, por lo que se busca en todo el array. Si el índice es mayor o igual a la longitud del array, devuelve -1, ya que no se buscaría en el array. Si el valor es negativo, se toma restando posiciones desde el final del array. Hay que tener en cuenta que aunque el índice sea negativo, la búsqueda seguirá realizándose en un orden incremental. Si el índice calculado es menor de 0, la búsqueda se realizará por todo el array.

## Valor de retorno

El primer índice del elemento en la matriz; -1 si no se encuentra.

# Descripción 

`indexOf()` compara `searchElement` con los elementos del array usando _igualdad estricta_ (el mismo método que cuando se usa` === `, o el operador igualdad-triple).