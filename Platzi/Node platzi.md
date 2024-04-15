1.

¿Cuál es el motor de JavaScript sobre el que corre Node?

V8

2.

Cuando un evento llega al Event Loop, ¿dónde lo manda Node?

Al thread pool

3.

¿Cómo accedemos a una variable de entorno llamada NOMBRE?

process.env.NOMBRE

4.

¿Qué pasa si salta un error no capturado en el hilo principal?

El proceso se detiene

5.

¿Cual es la herramienta más adecuada para ejecutar nuestros procesos de Node en producción?

PM2

6.

¿Cómo se le llama a la función que se ejecuta cuando termina otra función asíncrona?

Callback

<mark style="background: #FF5582A6;">7.

¿Cuál es la mejor forma de evitar un Callback Hell?

No anidar callbacks

REPASAR CLASE</mark>

Crear funciones intermedias
Una estrategia para trabajar con estas estructuras lógicas tan monolíticas es usar estructuras de control y funciones recursivas.

Las funciones recursivas se llaman así mismas y mediante la estructura de control le digo cuantas veces voy a necesitar llamar la función así misma.

<mark style="background: #FF5582A6;">8.

¿Cuántos parámetros puede recibir el then de una promesa?</mark>

```
promise
    .then()
    .catch()
```

<mark style="background: #FF5582A6;">Todos los que quieras

REPASAR CLASE</mark>

Para poder obtener los valores que retorna una función debemos utilizar su propiedad .then, esta propiedad es una función que recibe un callback el cual tendrá como parámetro el valor retornado con resolve o reject.  
Siempre que usemos una promesa además de realizar la propiedad .then debemos invocar la propiedad .catch, la cual es un callback que recibe como parámetro el error ocurrido en caso de haber sucedió uno.

9.

¿Se puede usar la palabra reservada "await" en cualquier sitio?

No, solo en funciones declaradas con async

10.

¿Cuál de los siguientes módulos **NO** está en los módulos globales?

crypto

<mark style="background: #FF5582A6;">11.

¿Cómo indentamos un nivel los logs de consola?

console.table

REPASAR CLASE</mark>

Con console podemos imprimir todo tipo de valores por  
nuestra terminal.

-   **console.log**: recibe cualquier tipo y lo muestra en el consola.
-   **[console.info](http://console.info/)**: es equivalente a log pero es usado para informar.
-   **console.error**: es equivalente a log pero es usado para errores.
-   **console.warn**: es equivalente a log pero es usado para warning.
-   **console.table**: muestra una tabla a partir de un objeto.
-   **console.count**: inicia un contador autoincremental.
-   **console.countReset**: reinicia el contador a 0.
-   **console.time**: inicia un cronometro en ms.
-   **console.timeEnd**: Finaliza el cronometro.
-   **console.group**: permite agrupar errores mediante identación.
-   **console.groupEnd**: finaliza la agrupación.
-   **console.clear**: Limpia la consola.

<mark style="background: #FF5582A6;">12.

Por defecto, ¿cómo detectamos que un fichero se ha escrito con fs.writeFile?

Con una promesa

REPASAR CLASE</mark>

La respuesta correcta es la opción a, con el callback.

La función `fs.writeFile` de NodeJS es un método asíncrono que escribe datos en un archivo y toma un callback como último parámetro. Este callback se ejecuta cuando se ha completado la operación de escritura y recibe dos argumentos: un error (si se ha producido) y un resultado (si la operación se ha completado correctamente).

Es importante tener en cuenta que `fs.writeFile` no devuelve una promesa, por lo que no es posible utilizar el método `then` para detectar cuándo se ha completado la operación de escritura. En su lugar, se debe utilizar el callback para detectar el resultado de la operación.

El **file system** provee una API para interactuar con el sistema de archivos cerca del estándar POSIX.  
POSIX es el estándar para interfaces de comando y shell, las siglas las significan: “Interfaz de sistema operativo portátil” la X de POSIX es por UNIX.

El file system nos permite acceder archivo del sistema, leer, modificar., escribirlos, es muy útil para precompiladores, para lo que requiera hacer grabados de disco, o bases de datos en node requieren un uso intensivo de Node.Todo lo que hagamos con modulos por buenas prácticas son asincronos, pero tienen una version sincrona no recomendada pues pordría bloquear el event loop con más facilidad.

13.

Cuando se lanzan excepciones, ¿cómo las capturamos?

Con try / catch

14.

¿Se pueden ejecutar comandos del sistema desde NodeJS? ¿Cómo?

Si, con procesos hijo

15.

¿En qué lenguajes se pueden desarrollar módulos nativos para NodeJS?

JavaScript y C++

16.

¿En qué puerto se puede iniciar un servidor HTTP en Node?

En cualquiera

17.

¿Podemos acceder a la memoria disponible y total del sistema operativo desde NodeJS?

Si, con el módulo OS

18.

¿Podemos controlar cuando se cierra el proceso de Node, y ejecutar código antes de que muera?

Si, con el módulo Process

19.

¿Dónde se listan las dependencias de nuestro proyecto?

En el package.json

<mark style="background: #FF5582A6;">20.

Cuando creamos un módulo, ¿podemos exportar mas de una entidad?

No, sólo se puede exportar una entidad

REPASAR CLASE</mark>

La respuesta correcta es la opción c, sí, tantas como queramos.

Cuando creamos un módulo en NodeJS, podemos exportar tantas entidades como queramos utilizando la sintaxis de módulos de CommonJS. Esto se puede hacer de varias maneras, como por ejemplo utilizando la palabra clave `module.exports` para asignar un objeto que contenga todas las entidades que queremos exportar. También se pueden utilizar las palabras clave `exports.nombreDeLaEntidad` para exportar entidades individuales.

21.

¿Qué módulo nos permite trabajar con imágenes desde NodeJS?

Sharp

22.

¿Cuál es la principal ventaja de trabajar en memoria frente a la lectura y escritura en disco?

La velocidad es mayor

23.

¿Qué es un Buffer?

Un conjunto de datos crudos

24.

¿Puede un stream transformar datos?

Si, usando un stream de transformación

25.

¿Cómo sabemos lo que tarda un trozo de código en ejecutarse?

Usando console.time

<mark style="background: #FF5582A6;">26.

¿Podemos parar el código en un punto determinado mientras se ejecuta?

Si, con un evento de proccess

REPASAR CLASE</mark>

Node.js viene integrado con un modo de debug para poder conectarnos desde cualquier herramienta de inspección de código a nuestro código de node.js.

Podemos utilizar en la terminal el flag de `--inspect` con **nodemon**

<mark style="background: #FF5582A6;">27.

En un callback, ¿cuál debería ser el primer parámetro?

El dato

REPASAR CLASE</mark>

Error First Callbacks

28.

¿Podemos usar NodeJS para acceder al DOM de un sitio externo y extraer información de él?

Si, con puppeteer

<mark style="background: #FF5582A6;">29.

¿Qué herramienta nos permite crear tareas en NodeJS para automatizar procesos?

Nodemon

REPASAR CLASE</mark>

**Que es gulp.js?** 📖🖥💥

Es una herramienta de construcción en JavaScript construida sobre flujos de nodos . Estos flujos facilitan la conexión de operaciones de archivos a través de canalizaciones . Gulp lee el sistema de archivos y canaliza los datos disponibles de un complemento de un solo propósito a otro a través del .pipe()operador, haciendo una tarea a la vez. Los archivos originales no se ven afectados hasta que se procesan todos los complementos. Se puede configurar para modificar los archivos originales o para crear nuevos. Esto otorga la capacidad de realizar tareas complejas mediante la vinculación de sus numerosos complementos. Los usuarios también pueden escribir sus propios complementos para definir sus propias tareas.

30.

¿Se puede usar NodeJS para crear aplicaciones de escritorio?

Si, con Electron