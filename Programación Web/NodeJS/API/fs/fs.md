El módulo `node:fs` permite interactuar con el sistema de archivos siguiendo el modelo de las funciones POSIX estándar.

Para utilizar las API basadas en **promesas**:

```js
import * as fs from 'node:fs/promises';
// o
const fs = require('node:fs/promises');
```

Para utilizar las API de **callback** y **sincronización**:

```js
import * as fs from 'node:fs';
// o
const fs = require('node:fs');
```

Todas las operaciones del sistema de archivos tienen formas síncronas, de devolución de llamada y basadas en promesas, y son accesibles utilizando tanto la sintaxis CommonJS como los módulos ES6 (ESM).

## Ejemplo de promesa

Las operaciones basadas en promesas devuelven una promesa que se cumple cuando se completa la operación asíncrona.

```js
import { unlink } from 'node:fs/promises';

try {
  await unlink('/tmp/hello');
  console.log('successfully deleted /tmp/hello');
} catch (error) {
  console.error('there was an error:', error.message);
}
```

## Ejemplo de una callback

La forma callback toma como último argumento una función callback de finalización e invoca la operación de forma asíncrona. Los argumentos que se pasan a la llamada de retorno dependen del método, pero el primer argumento siempre se reserva para una excepción. Si la operación se completa con éxito, entonces el primer argumento es `null` o `undefined`.

```js
import { unlink } from 'node:fs';

unlink('/tmp/hello', (err) => {
  if (err) throw err;
  console.log('successfully deleted /tmp/hello');
});
```

Las versiones basadas en callbacks de las APIs del módulo `node:fs` son preferibles al uso de las APIs promise cuando se requiere el máximo rendimiento (tanto en términos de tiempo de ejecución como de asignación de memoria).

## Ejemplo de sincronía

Las APIs síncronas bloquean el bucle de eventos de Node.js y la ejecución posterior de JavaScript hasta que se completa la operación. Las excepciones se lanzan inmediatamente y pueden ser manejadas usando `try...catch`, o se puede permitir que burbujeen.

```js
import { unlinkSync } from 'node:fs';

try {
  unlinkSync('/tmp/hello');
  console.log('successfully deleted /tmp/hello');
} catch (err) {
  // handle the error
}
```