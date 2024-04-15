## ¿Qué es la terminal?

Las razones para aprender a usarla son:

1. Tenemos mucha **flexibilidad** ya que podemos hacer procesos dentro de nuestra computadora de una forma más eficiente, mover grandes volúmenes de datos de forma rápida, así como hacer copias e incluso programar procesos que se ejecuten en cierto tiempo
2. Normalmente hacer cosas en la terminal como copiar archivos o buscarlos tiende a ser mucho más rápido que hacerlo a través de una interfaz gráfica. Por lo tanto podemos decir que tenemos una **velocidad** mayor al realizar dichos procesos en la terminal.
3. **No siempre contaremos con una interfaz gráfica** o puede llegar a fallar.

### Pero qué es...

Es una **interfaz gráfica que simula una linea de comandos** y cuando hablamos de una línea de comandos nos referimos a una `shell`.

- **Terminal**: es la ventanita que nos muestra el prompt. Este aloja la shell.
- **Linea de comandos**: programa que toma comandos y los pasa al sistema operativo para hacer algo.
- **Comando**: es una acción escrita, generalmente, a través de una terminal y emulada por una shell para ser ejecutada por nuestro sistema operativo.

![[Pasted image 20221115111547.png]]

### ¿Que es un comando?

Un **comando** es un mensaje enviado al ordenador que provoca una respuesta en este sistema y se comporta como una orden, pues informa al dispositivo informático que debe ejecutar una acción según la indicación que pueda enviarse.

Cada sistema operativo incorpora un determinado número de comandos básicos, que permiten ejecutar las tareas más simples con órdenes directas. A continuación conocerás todo lo relacionado con sistemas operativos basados en UNIX y sus comandos basicos en la terminal.

**Un comando pueden significar cuatro cosas:**

1.  Un programa ejecutable
2.  Un comando de utilidad de la shell. Esto es un programa en sí mismo, que puede tener funciones. Ejemplo `cd`
3.  Una función de shell. Son funciones de shell externas al comando de utilidad. Ejemplo `mkdir`
4.  Un alias. Un ejemplo es `ls`

![que-es-un-comando.jpg](https://static.platzi.com/media/user_upload/que-es-un-comando-7115bdf1-045c-4ff2-84bf-3e2d10a9bcb5.jpg)

## Ejemplos de comandos básicos de la terminal

Ahora conocerás varios tipos de comandos que puedes aplicar en el proyecto que estás realizando.

-   `type <comando>`: Nos permite conocer que tipo de comando es 🤔.
-   `alias l="<secuencia de comandos>"`: Nos permite crear comandos. Son temporales, se borran al cerrar la terminal 👶🏼.
-   `help <comando>`: Nos permite consultar un poco de documentación de un comando 📄.
-   `man <comando>`: De _manual_, nos permite conocer mucha más información de un comando.
-   `info <comando>`: Similar al anterior, pero un poco resumido y con otro formato.
-   `whatis <comando>`: Describe un comando en una sola línea ☺️. No funciona con todos.

## ¿**Cómo puedo saber qué comando estoy utilizando?**

Puedes introducir `type ls` para ver qué tipo de comando es `ls.`

Ahora, podemos crear nuestro propio comando con un alias llamado `l`:

```
alias l="ls -lh"

```

Podemos invocar a nuestro nuevo comando `l`cada vez que lo necesitemos y se ejecutará lo que está entre comillas, **¿cuál es el problema?**

Si cerramos y volvemos a abrir la terminal, este alias **se pierde.**

Puedes implementar **zsh,** y pues ni el comando `help` ni `man` con `cd`, pero el comando `man` **sí me funciona con** `git` y otros comandos.


### Tipos de lineas de comandos

-   Bourne Shell
-   Bash Shell
-   Z Shell
-   C Shell
-   Korn Shell
-   Fish Shell
-   PowerShell

### Las más populares

> 💡 Un comando de manera sencilla es un programa que se puede ejecutar desde la terminal. Este puede recibir parámetros y opciones.

### Comandos

- **pwd**: Saber donde estoy ubicado.
- **mkdir**: Creación de carpeta.
- **cd**: Moverse a carpetas
- **git init** : Inicias Git.
- **npm init**: Le da nombre, versión, entre otras cosas al proyecto.
- **code .**: Inicia el editor de códigos en la carpeta donde estoy parado.
- **ls**: Listar archivos.
	- **-a** :todos los archivos, incluso los que comienzan con punto (.).
	- **-A** :Lista todos los ficheros en los directorios, excepto los que comienzan con punto . (.) y los que comienzan con doble punto (…).
	- **-F** :indica tipo: / directorio, * ejecutable, @ enlace simbólico.
	- **-h** :indicará el tamaño en KB, MB, etc.
	- **-l** :listado en formato largo (o detallado).
	- **-S** :clasifica los contenidos de los directorios por tamaños, con los ficheros más grandes en primer lugar.
	- **-r** :invierte el orden de la salida.
	- **-R** :Lista recursivamente los subdirectorios encontrados.
	- **-t** :ordenar por fecha de última modificación.
	- **-u** :ordenar por fecha de último acceso.
	- **-x** :presenta los ficheros por columnas.
	- **-i** :precede la salida con el número de i-node
- **ls -lh**: Listar archivos para ver su peso de una manera mas mas legible.
- **ls -a**: Listar archivos ocultos.
- **pwd**: Identificar la ruta en la que estamos en nuestro sistema.
- **cp**: copiar archivo.
- **rm**: borrar un archivo.
- **mv**: mover un archivo.
- **rmdir**: remover un directorio.
- **clear**: limpiar la terminal.
- **touch**: crea un archivo, si no indicas la extension por defecto sera .txt

## Otros temas

- [[Wildcards]]