Una [`Promise`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Promise) (promesa en castellano) es un objeto que representa la terminación o el fracaso de una operación asíncrona. Dado que la mayoría de las personas consumen `promises` ya creadas, esta guía explicará primero cómo consumirlas, y luego cómo crearlas.

Esencialmente, una promesa es un objeto devuelto al cual se adjuntan funciones `callback`, en lugar de pasar callbacks a una función.

Considera la función `crearArchivoAudioAsync()`, la cual genera de manera asíncrona un archivo de sonido de acuerdo a un archivo de configuración, y dos funciones callback, una que es llamada si el archivo de audio es creado satisfactoriamente, y la otra que es llamada si ocurre un error. El código podría verse de la siguiente forma:

```js
function exitoCallback(resultado) {
  console.log("Archivo de audio disponible en la URL " + resultado);
}

function falloCallback(error) {
  console.log("Error generando archivo de audio " + error);
}

crearArchivoAudioAsync(audioConfig, exitoCallback, falloCallback);
```

... las funciones modernas devuelven un objeto `promise` al que puedes adjuntar funciones de retorno (callbacks). Si `crearArchivoAudioAsync` fuera escrita de manera tal que devuelva un objeto `promise`, usarla sería tan simple como esto:

```js
crearArchivoAudioAsync(audioConfig).then(exitoCallback, falloCallback);
```

Lo cual es la versión corta de:

```js
const promesa = crearArchivoAudioAsync(audioConfig);
promesa.then(exitoCallback, falloCallback);
```

Llamamos a esto una _llamada a función asíncrona_. Esta convención tiene varias ventajas. Exploraremos cada una de ellas.