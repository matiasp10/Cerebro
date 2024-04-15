**-v**
**--versión**
Imprime la versión de la suite Git de la que proviene el programa git.

Esta opción se convierte internamente en git version ... y acepta las mismas opciones que el comando git-version[1]. Si también se da --help, tiene preferencia sobre --version.

**-h**
**--help**
Imprime la sinopsis y una lista de los comandos más utilizados. Si se da la opción --all o -a se imprimen todos los comandos disponibles. Si se nombra un comando Git, esta opción mostrará la página del manual de ese comando.

Hay otras opciones disponibles para controlar cómo se muestra la página del manual. Ver git-help[1] para más información, porque git --help ... se convierte internamente en git help ....

**-C ``<ruta>``**
Se ejecuta como si git se hubiera iniciado en ``<ruta>`` en lugar de en el directorio de trabajo actual. Cuando se dan múltiples opciones -C, cada -C ``<ruta>`` no absoluta subsiguiente se interpreta relativa a la -C ``<ruta>`` precedente. Si ``<ruta>`` está presente pero vacía, por ejemplo -C "", el directorio de trabajo actual no se modifica.

Esta opción afecta a opciones que esperan nombres de ruta como --git-dir y --work-tree en que sus interpretaciones de los nombres de ruta se harían relativas al directorio de trabajo causado por la opción -C. Por ejemplo las siguientes invocaciones son equivalentes:

```bash
git --git-dir=a.git --work-tree=b -C c estado
git --git-dir=c/a.git --árbol-de-trabajo=c/b status
```

**-c ``<nombre>``=``<valor>``**
Pasa un parámetro de configuración al comando. El valor dado anulará los valores de los archivos de configuración. Se espera que ``<nombre>`` tenga el mismo formato que aparece en git config (subclaves separadas por puntos).

Tenga en cuenta que omitir el **=** en **git -c foo.bar** ... está permitido y establece foo.bar al valor booleano true (al igual que ``[foo]bar`` lo haría en un archivo de configuración). Incluyendo la igualdad pero con un valor vacío (como git -c foo.bar= ...) establece foo.bar como una cadena vacía que git config --type=bool convertirá en falsa.

**--config-env=``<nombre>``=``<envvar>``**
Como -c ``<nombre>``=``<valor>``, da a la variable de configuración ``<nombre>`` un valor, donde ``<envvar>`` es el nombre de una variable de entorno de la que recuperar el valor. A diferencia de -c, no existe un método abreviado para establecer directamente el valor en una cadena vacía, sino que la propia variable de entorno debe establecerse en la cadena vacía. Es un error si ``<envvar>`` no existe en el entorno. ``<envvar>`` no puede contener un signo igual para evitar la ambigüedad con ``<nombre>`` que contiene uno.

Esto es útil para casos en los que quiera pasar opciones de configuración transitorias a git, pero lo esté haciendo en SOs en los que otros procesos puedan leer su cmdline (p.e. /proc/self/cmdline), pero no su environ (p.e. /proc/self/environ). Este comportamiento es el predeterminado en Linux, pero puede no serlo en su sistema.

Tenga en cuenta que esto podría añadir seguridad para variables como http.extraHeader donde la información sensible es parte del valor, pero no por ejemplo url.``<base>``.insteadOf donde la información sensible puede ser parte de la clave.

**--exec-ruta``[=<ruta>]``**
Ruta a donde estén instalados tus programas principales de Git. Esto también puede controlarse estableciendo la variable de entorno GIT_EXEC_PATH. Si no se indica ninguna ruta, git mostrará la configuración actual y saldrá.

**--html-ruta**
Imprime la ruta, sin barra al final, donde está instalada la documentación HTML de Git y sale.

**--man-ruta**
Imprime el manpath (ver man(1)) para las páginas man de esta versión de Git y sale.

**--ruta-info**
Imprime la ruta donde están instalados los archivos Info que documentan esta versión de Git y sale.

**-p**
**--paginate**
Envía toda la salida a less (o si está establecido, $PAGER) si la salida estándar es un terminal. Esto anula las opciones de configuración de pager.``<cmd>`` (ver la sección "Mecanismo de configuración" más abajo).

**-P**
**--no-pager**
No envía la salida de Git a un paginador.

**--git-dir=``<ruta>``**
Establece la ruta al repositorio (directorio ".git"). Esto también puede controlarse estableciendo la variable de entorno GIT_DIR. Puede ser una ruta absoluta o relativa al directorio de trabajo actual.

Especificar la ubicación del directorio ".git" usando esta opción (o la variable de entorno GIT_DIR) desactiva el descubrimiento del repositorio que intenta encontrar un directorio con el subdirectorio ".git" (que es como se descubren el repositorio y el nivel superior del árbol de trabajo), y le dice a Git que estás en el nivel superior del árbol de trabajo. Si no estás en el directorio de nivel superior del árbol de trabajo, debes decirle a Git dónde está el nivel superior del árbol de trabajo, con la opción --work-tree=``<ruta>`` (o la variable de entorno GIT_WORK_TREE)

Si sólo quieres ejecutar git como si se hubiera iniciado en ``<ruta>`` entonces usa git -C ``<ruta>``.

**--árbol-de-trabajo=``<ruta>``.**
Establece la ruta al árbol de trabajo. Puede ser una ruta absoluta o una ruta relativa al directorio de trabajo actual. Esto también puede controlarse estableciendo la variable de entorno GIT_WORK_TREE y la variable de configuración core.worktree (ver core.worktree en ``git-config[1] ``para una discusión más detallada).

**--namespace=``<ruta>``**
Establece el espacio de nombres de Git. Equivale a establecer la variable de entorno GIT_NAMESPACE.

**--super-prefijo=``<ruta>``**
Actualmente sólo para uso interno. Establece un prefijo que da una ruta desde arriba de un repositorio hasta su raíz. Un uso es dar contexto a los submódulos sobre el superproyecto que lo invocó.

**--bare**
Trata el repositorio como un repositorio vacío. Si el entorno GIT_DIR no está definido, se define como el directorio de trabajo actual.

**--no-replace-objects**
No usar refs de reemplazo para reemplazar objetos Git. Vea git-replace[1] para más información.

**--literal-pathspecs**
Trata las especificaciones de ruta literalmente (es decir, sin globbing, sin la magia de las especificaciones de ruta). Esto equivale a establecer la variable de entorno GIT_LITERAL_PATHSPECS a 1.

**--glob-pathspecs**
Añade magia "glob" a todas las especificaciones de ruta. Esto equivale a establecer la variable de entorno GIT_GLOB_PATHSPECS en 1. La desactivación de globbing en pathpecs individuales puede hacerse usando la magia pathpec ":(literal)"

**--noglob-pathspecs**
Añade la magia "literal" a todas las especificaciones de ruta. Esto equivale a poner a 1 la variable de entorno GIT_NOGLOB_PATHSPECS. La activación de globbing en pathpecs individuales puede hacerse usando pathpec magic ":(glob)"

**--icase-pathspecs**
Añade la magia "icase" a todos los pathpecs. Esto equivale a poner a 1 la variable de entorno GIT_ICASE_PATHSPECS.

**--no-optional-locks**
No realizar operaciones opcionales que requieran bloqueos. Equivale a establecer GIT_OPTIONAL_LOCKS en 0.

**--list-cmds=grupo``[,grupo...]``**
Lista los comandos por grupo. Esta es una opción interna/experimental y puede cambiar o ser eliminada en el futuro. Los grupos soportados son: builtins, parseopt (órdenes builtin que usan parse-options), main (todas las órdenes en el directorio libexec), others (todas las demás órdenes en $PATH que tienen el prefijo git-), list-``<category>`` (ver categorías en command-list.txt), nohelpers (excluye órdenes helper), alias y config (recupera la lista de órdenes de la variable config completion.commands).