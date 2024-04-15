### Unir cadenas de texto (cat)

Si queremos crear una lista de los archivos de varias carpetas, podemos usar cat para concatenar la salida de varios de ellos.

Por ejemplo, vamos a crear uno que tenga la lista de los archivos contenidos en la carpeta “Images” y “SecretosDeEstado”.

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28110%29.png)

### Crear un archivo con base en una salida (tee)

Si queremos guardar la lista creada anteriormente, podemos pasar esa salida por medio de un pipe operator al comando tee, el cual creará un archivo con esa salida.

```
cat images.txt secretosDeEstado.txt | tee archivos.txt
```

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28111%29.png)

De momento parece lo mismo, pero si inspeccionamos el archivo “archivos.txt” veremos esto:

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28112%29.png)

Por cierto, para ver los archivos usa el comando `head` , para que puedas ver la línea de comandos. Para inspeccionar archivos el comando `less` es mucho más efectivo.

### Organizar archivos con sort

Puede ser algo complicado encontrar un archivo dentro de la lista, por lo que lo podemos organizar alfabéticamente una salida con el comando sort.

```
ls | sort | tee archivosHome.txt
```

![image.png](https://cdn.document360.io/da52b302-22aa-4a71-9908-ba18e68ffee7/Images/Documentation/image%28113%29.png)

Aquí lo que estamos haciendo es:

-   Listar los archivos
-   Organizar los archivos
-   Crear un archivo llamado archivosHome.txt, con las salidas anteriores

## Tabla de comandos pipe operator

| Comando |                Función                |
| ------- |:-------------------------------------:|
| sort    | Organiza allfabéticamente una salida  |
| cat     |        Concatena dos entradas         |
| tee     | Crea un archivo en base a una entrada |
