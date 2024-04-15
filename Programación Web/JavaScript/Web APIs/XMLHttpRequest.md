`XMLHttpRequest` es un objeto [JavaScript](https://developer.mozilla.org/en-US/JavaScript) que fue diseñado por Microsoft y adoptado por Mozilla, Apple y Google. Actualmente es un [estándar de la W3C](https://www.w3.org/TR/XMLHttpRequest/). Proporciona una forma fácil de obtener información de una URL sin tener que recargar la página completa. Una página web puede actualizar sólo una parte de la página sin interrumpir lo que el usuario está haciendo. `XMLHttpRequest` es ampliamente usado en la programación AJAX.

A pesar de su nombre, `XMLHttpRequest` puede ser usado para recibir cualquier tipo de dato, no solo XML, y admite otros formatos además de [HTTP](https://developer.mozilla.org/en-US/HTTP) (incluyendo `file` y `ftp`).

Para crear una instancia de `XMLHttpRequest`, debes hacer lo siguiente:

```js
var req = new XMLHttpRequest();
```

**Existen 5 estados en un llamado XMLHttpRequest:**  

- **`0`** → Se ha inicializado.
- **`1`** → Loading (cargando).
- **`2`** → Se ha cargado.
- **`3`** → Procesamiento si existe alguna descarga.
- **`4`** → Completado.  

📫 **Métodos y propiedades:**  
  
- **`xmlhttp.open()`** → Prepara la petición para ser enviada tomando tres parámetros: prótocolo, url, asíncrono (true).
- **`xmlhttp.readyState`** → Retorna el estado de la petición.
- **`xmlhttp.onreadystatechange`** → Un eventHandler que es llamado cuando la propiedad readyState cambia.
- **`xmlhttp.status`** → Retorna el estado de la respuesta de la petición. (200,400,500).
- **`xmlhttp.send`()** → Envía la petición.  
