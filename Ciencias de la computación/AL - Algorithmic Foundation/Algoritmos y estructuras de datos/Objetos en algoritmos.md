Los `objects` ([[Objetos]]) son estructuras de datos no ordenadas que poseen conjuntos de pares de `keys` (llaves) y `values`. Por ejemplo.

```js
const persona = {
    edad: 20,
    nombre: "Mario",
    profesion: "Arquitecto",
    esGraduado: true,
};
```
## ¿Cuándo se deben utilizar objetos para construir algoritmos?

Los objetos son utilizados cuando:

- No se necesita mantener un orden.
- Se necesita acceder acceder, insertar y eliminar valores rápidamente.
## Big O de los objetos

Las operaciones con objetos tienen los siguientes Big O.

- Insertar valor **O(1)**
- Eliminar valor **O(1)**
- Buscar valor **O(N)**
- Acceder un valor **O(1)**
### ¿Cuáles son las ventajas y desventajas del Big O de los objetos?

Cuando no se requiere mantener un orden, los objetos son una solución excelente. Cuando se requiere buscar un valor dentro de uno de los `values` (no de las `keys`) no hay una forma sencilla de realizar la búsqueda, posiblemente se requiera buscar dentro de cada uno de los pares `key/value` que conforman el objeto.
## Big O de los métodos de un objeto

Los siguientes son los Big O correspondientes para cada uno de los métodos de `Object`.

- [[Object()#Object.keys()|Object.keys()]] $O(N)$
- [[Object()#Object.values()|Object.values()]] $O(N)$
- [[Object()#Object.entries()|Object.entries()]] $O(N)$
- [[Object()#Object.prototype.hasOwnProperty()|Object.prototype.hasOwnProperty()]] $O(1)$