Crea un nuevo objeto Map.

# Sintaxis

```js
new Map()
new Map(iterable)
```

> [!warning] Nota
> Map() sólo puede construirse con new. Si se intenta llamar sin new se produce un TypeError.

## Parametros

### Iterable (Opcional)

Un array u otro objeto iterable cuyos elementos son pares clave-valor. (Por ejemplo, arrays con dos elementos, como ``[[ 1, 'uno' ],[ 2, 'dos' ]]``.) Cada par clave-valor se añade al nuevo Mapa.

# Propiedades estáticas

## get Map`[@@species]`

La función constructora que se utiliza para crear objetos derivados.

# Propiedades de instancia

Estas propiedades se definen en Map.prototype y son compartidas por todas las instancias de Map.

## Map.prototype.constructor

La función constructora que creó el objeto instancia. Para instancias Map, el valor inicial es el constructor Map.

## Map.prototype.size

Devuelve el número de pares clave/valor del objeto Map.

## Map.prototype`[@@toStringTag]`

El valor inicial de la propiedad @@toStringTag es la cadena "Map". Esta propiedad se utiliza en Object.prototype.toString().

# Métodos de instancia

## Map.prototype.clear()

Elimina todos los pares clave-valor del objeto Map.

## Map.prototype.delete()

Devuelve true si un elemento del objeto Map existía y ha sido eliminado, o false si el elemento no existe. map.has(key) devolverá false después.

## Map.prototype.get()

Devuelve el valor asociado a la clave pasada, o indefinido si no hay ninguno.

## Map.prototype.has()

Devuelve un booleano que indica si se ha asociado o no un valor a la clave pasada en el objeto Map.

## Map.prototype.set()

Establece el valor de la clave pasada en el objeto Map. Devuelve el objeto Map.

## Map.prototype`[@@iterator]()`

Devuelve un nuevo objeto Iterator que contiene un array de dos miembros `[clave, valor]` para cada elemento del objeto Map en orden de inserción.

## Map.prototype.keys()

Devuelve un nuevo objeto Iterator que contiene las claves de cada elemento del objeto Map en orden de inserción.

## Map.prototype.values()

Devuelve un nuevo objeto Iterator que contiene los valores de cada elemento del objeto Map en orden de inserción.

## Map.prototype.entries()

Devuelve un nuevo objeto Iterator que contiene un array de dos miembros `[clave, valor]` para cada elemento del objeto Map en orden de inserción.

## Map.prototype.forEach()

Llama a `callbackFn` una vez por cada par clave-valor presente en el objeto Map, en orden de inserción. Si se proporciona un parámetro thisArg a forEach, se utilizará como valor this para cada llamada de retorno.



























