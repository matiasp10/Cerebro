## Qué son las entradas y salidas de la terminal

En la consola nosotros generamos una entrada cuando escribimos y una salida casi siempre que ejecutamos un comando.

A las entradas típicamente se les suele llamar **Standard Input** y a las salidas **Standard Output**, además se les suele abreviar como **stdin** y **stdout** respectivamente.

### Qué son file descriptors

Los file descriptors son números que identifican un recurso. Funciona asociando un número con una acción, archivo o programa, en el caso de la shell tenemos 3 file descriptors:

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28100%29.png)

El 2 es **Standard Error**.

## Cómo usar el operador de redirección (>)

A veces queremos guardar la información de una salida porque nos puede interesar almacenar lo que esa salida contiene. Veamos el siguiente ejemplo, si utilizas el comando:

```
ls -l
```

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28102%29.png)

Lo que sucede aquí es que le diste un **Standard Input** (el comando) y obtuviste un **Standard Output** (la lista de archivos).

Si quieres que el **Standard Output** no vaya a la consola sino hacia un archivo, entonces puedes usar el operador **>** seguido del nombre del archivo en el que quieres guardar la salida.

```
ls -l > output.txt
```

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28103%29.png)

### Cómo concatenar (>>)

Suponiendo que ya tienes el archivo output.txt y ahora también quieres guardar la información de la carpeta de documentos, entonces no puedes volver a ejecutar:

```
ls -l > output.txt
```

Esto lo que hará es reescribir el contenido del documento, lo que necesitas es concatenar el contenido del documento con el de la salida, para eso ejecutas:

```
ls -l >> output.txt
```

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28104%29.png)

Como puedes ver, la salida del comando `ls -l` se concatenó con la salida del comando `ls -l ./SecretosDeEstado`. Te puedes dar cuenta porque la palabra total se repite dos veces.

Por cierto, esa palabra total es el tamaño total de la carpeta en kilobytes y dice que la carpeta SecretosDeEstado pesa 0, porque los archivos y carpetas vacías no ocupan espacio.

### Redirección de errores (2>|2>&1)

El operador de redirección por defecto solo redirecciona el file descriptor 1 (es decir, el **Standard Output**). Pero, ¿qué tal si queremos redirigir un error? Pues tenemos que especificar que queremos el **Standar Error**, que tiene el file descriptor 2.

Vamos a generar un error ejecutando un comando que saldrá mal para redirigirlo a un archivo llamado “error.txt”.

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28105%29.png)

En este caso la opción “ñ” no existe, por lo que produce un error.

También podemos especificar que no importa lo que pase si me da un **Standar Ouput** o un **Standar Error**, igual tiene que guardar la salida en un archivo. Esto lo hacemos así:

```
ls -l > output.txt 2>&1
```

La orden `2>&1` significa que debe redirigir el file descriptor 2 y el file descriptor 1.

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28106%29.png)

En la primera ejecución del comando, se ejecuta correctamente y guarda el **Standar Output**, pero en la segunda ejecución, el comando falla y guarda el **Standar Error**.

## Tabla de operadores

| Operador |                                          Funcion                                          |
| -------- |:-----------------------------------------------------------------------------------------:|
| >        |          Redirecciona la salida. Por defecto redirecciona el **Standar Output**           |
| >>       | Concatena la salida con lo que ya tenga el archivo a donde se está redirigiendo la salida |
| 2>&1     |                           Redirecciona el file descriptor 2 y 1                           |

