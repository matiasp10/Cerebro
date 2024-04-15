**No hace falta ser un programador para tener que haber lidiado en algún caso con las variables de entorno**. Puede ser, por ejemplo, que a la hora de instalar o configurar algún programa para Windows te hayas encontrado con una ruta que, en lugar de seguir la típica estructura ``"C:/Users/YoMismo/carpeta"`` muestre algo como ``"%USERPROFILE%/carpeta"``.

Eso es porque ``%USERPROFILE%`` es una **variable de entorno: es decir, una cadena de texto que sistemas operativos como Windows, Linux o Mac usan para almacenar valores** que pueden variar de un equipo a otro -o, como en este caso, de un usuario a otro- pero que, sin embargo, necesitan de un modo unificado de acceder al mismo.

Normalmente, esos valores hacen referencia a **archivos, directorios y funciones comunes del sistema cuya ruta concreta puede variar**, pero que otros programas necesitan poder conocer.

El ejemplo anterior permite que un programa **sepa acceder a tu carpeta de usuario incluso si no le has indicado el nombre del mismo**. O incluso si no sabe qué versión de Windows usas (recordemos que el ``C:\Users\`` de Windows 10 era ``C:\Document and Settings\`` en Windows XP).

Da igual, porque toda esa información se encuentra definida en las variables de entorno, garantizando que todos los programas para Windows puedan realizar su labor correctamente en cualquier equipo. Porque hay muchas más variables de entorno además de **_%USERPROFILE%_**. Veamos algunas:

-   **_%APPDATA%_** - Remite a la carpeta oculta para datos de programa, dentro de la carpeta de usuario. En Windows 10 la ruta por defecto es ``C:\Users\NombreDeUsuario\AppData\Roaming``.
    
-   **_%COMMONPROGRAMFILES%_** - Remite a la carpeta donde los programas almacenan archivos comunes. En Windows 10 la ruta por defecto es ``C:\Program Files\Common Files``.
    
-   **_%PROGRAMFILES%_** - Remite a la carpeta donde se instalan los programas. En Windows 10 la ruta por defecto es ``C:\Program Files``.
    
-   **_%WINDIR%_** - Remite a la carpeta donde se instala Windows. En Windows 10 la ruta por defecto es ``C:\Windows``.
    

**Pero las variables de entorno no siempre equivalen a rutas de directorios: pueden remitir a otra clase de información**. Así, **_%TIME%_** devuelve la hora actual del sistema, **_%OS%_** la versión del sistema operativo y **_%PATHEXT%_** la lista de extensiones de archivo consideradas ejecutables (lo común es que la lista incluya, además de los .EXE, archivos como los .BAT, los .COM, .CMD, .JS., .JSE, .MSC, .VBE, .VBS, .WSF, .WSH, etc).

Pero quizá la variable de entorno con la que más habitualmente tendremos que lidiar será **_%PATH%_**. ¿Y cuál es su función? ¿Os habéis fijado que, cuando tecleáis un comando propio de Windows (por ejemplo, _Regedit_) **no es necesario teclear la ruta completa del ejecutable**?

Eso es porque, cada vez que tecleamos un comando, el sistema revisa las carpetas contenidas en la variable _%PATH%_ **para comprobar si algún archivo ejecutable coincide con el mismo**.

Es un recurso muy usado, por ejemplo, por los **desarrolladores que desean llamar a un intérprete o compilador desde la carpeta del proyecto** en el que estén trabajando; muchos IDE también recurren al _%PATH%_ para ejecutar dichas herramientas.

![[Pasted image 20221227190111.png]]

## Comprobar y editar nuestras variables de entorno en Windows

Si quieres comprobar si los valores de dichas variables en tu equipo coinciden con los aquí expuestos, puedes abrir una ventana de la línea de comandos (CMD, no el Power Shell) y teclear _"ECHO"_ seguido de la variable en cuestión. **Si prefieres listar todas las variables y sus respectivos valores**, vete (ahora sí) al Power Shell y teclea _"Get-ChildItem Env:"_.

Pero si no te gusta recurrir a la línea de comandos, hay otra herramienta que nos permitirá no sólo comprobar el valor de cada variable, sino también editarlas de forma muy sencilla. **Sólo tenemos que introducir 'Configuración avanzada del sistema' en 'Buscar', y abrir "Variables de entorno"** en la ventana que nos aparezca. Y nos aparecerá algo parecido a esto:

![[Pasted image 20221227190217.png]]

Una vez lleguemos a este punto, sólo deberemos seleccionar la variable que nos interese cambiar y hacer clic en "Evitar". También podemos añadir nuevas variables o eliminarlas.

## Variables de comandos en Linux

**En el caso de Linux, el papel de las variables de entorno es el mismo que en Windows**, aunque no encontraremos exactamente las mismas ni con los mismos nombres.

En este sistema operativo, deberemos **recurrir al comando _'printenv'_ para visualizar tanto la lista completa de variables** como el valor de cada una de ellas individualmente.

![[Pasted image 20221227190241.png]]

Así, en Linux encontremos variables como _'SHELL'_ (shell que interpretará los comandos, en la mayoría de distribuciones será Bash), _'LANG'_ (idioma actual) o _'HOME'_ (directorio de inicio del usuario actual).

Para cambiar sus valores, deberemos recurrir a editar, principalmente, tres archivos de texto:

-   **_"/etc/environment"_** - Para variables independientes del intérprete de comandos.
    
-   **_"etc/profile"_** - Las variables que definamos aquí serán válidas para todas las shells interactivas que exijan login. Su equivalente si queremos definir únicamente variables de usuario es _~/.bash_profile_.
    
-   **_"/etc/bash.bashrc"_** - Igual que el anterior, pero para shells no-login. Su equivalente si queremos definir únicamente variables de usuario es _~/.bashrc_.
