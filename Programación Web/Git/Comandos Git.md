Dividimos Git en comandos de alto nivel ("porcelana") y comandos de bajo nivel ("fontanería").

## **Comandos de alto nivel (porcelana)**

Separamos los comandos de porcelana en comandos principales y algunas utilidades auxiliares para el usuario.

### Comandos principales de porcelana

**git-add**
Añade el contenido del archivo al índice

**git-am**
Aplicar una serie de parches desde un buzón

**git-archive**
Crear un archivo de ficheros a partir de un árbol con nombre

**git-bisect**
Utiliza la búsqueda binaria para encontrar la confirmación que introdujo un error

**git-branch**
Listar, crear o borrar ramas

**git-bundle**
Mover objetos y referencias por archivo

**git-checkout**
Cambiar de rama o restaurar archivos del árbol de trabajo

**git-cherry-pick**
Aplicar los cambios introducidos por algunos commits existentes

**git-citool**
Alternativa gráfica a git-commit

**git-clean**
Eliminar del árbol de trabajo los archivos sin seguimiento

**git-clone**
Clonar un repositorio en un nuevo directorio

**git-commit**
Registrar los cambios en el repositorio

**git-describe**
Da a un objeto un nombre legible por humanos basado en una referencia disponible

**git-diff**
Muestra los cambios entre commits, commit y árbol de trabajo, etc

**git-fetch**
Descargar objetos y referencias de otro repositorio

**git-format-patch**
Preparar parches para su envío por correo electrónico

**git-gc**
Limpia archivos innecesarios y optimiza el repositorio local

**git-grep**
Imprime las líneas que coinciden con un patrón

**git-gui**
Una interfaz gráfica portátil para Git

**git-init**
Crea un repositorio Git vacío o reinicia uno existente

**git-log**
Muestra los registros de commits

**git-maintenance**
Ejecutar tareas para optimizar los datos del repositorio Git

**git-merge**
Unir dos o más historiales de desarrollo

**git-mv**
Mover o renombrar un archivo, un directorio o un enlace simbólico

**git-notes**
Añadir o inspeccionar notas de objetos

**git-pull**
Obtener de e integrar con otro repositorio o una rama local

**git-push**
Actualizar referencias remotas junto con los objetos asociados

**git-range-diff**
Compara dos rangos de confirmaciones (por ejemplo, dos versiones de una rama)

**git-rebase**
Reaplicar commits sobre otra base

**git-reset**
Restablecer el HEAD actual al estado especificado

**git-restore**
Restaurar los archivos del árbol de trabajo

**git-revert**
Revertir algunos commits existentes

**git-rm**
Eliminar archivos del árbol de trabajo y del índice

**git-shortlog**
Resume la salida del log de git

**git-show**
Mostrar varios tipos de objetos

**git-sparse-checkout**
Reduce tu árbol de trabajo a un subconjunto de archivos rastreados

**git-stash**
Almacena los cambios en un directorio de trabajo sucio

**git-status**
Mostrar el estado del árbol de trabajo

**git-submodule**
Inicializar, actualizar o inspeccionar submódulos

**git-switch**
Cambiar de rama

**git-tag**
Crear, listar, borrar o verificar un objeto tag firmado con GPG

**git-árbol-de-trabajo**
Gestiona múltiples árboles de trabajo

**gitk**
El navegador de repositorios Git

**scalar**
Herramienta para gestionar grandes repositorios Git

### Comandos auxiliares

#### Manipuladores:

**git-config**
Obtener y establecer opciones globales o del repositorio

**git-fast-export**
Exportador de datos Git

**git-fast-import**
Backend para importadores rápidos de datos Git

**git-filter-branch**
Reescribir ramas

**git-mergetool**
Ejecuta herramientas de resolución de conflictos para resolver conflictos de fusión

**git-pack-refs**
Empaqueta encabezados y etiquetas para un acceso eficiente al repositorio

**git-prune**
Elimina todos los objetos inalcanzables de la base de datos de objetos

**git-reflog**
Gestiona la información reflog

**git-remote**
Gestiona el conjunto de repositorios rastreados

**git-repack**
Empaquetar objetos desempaquetados en un repositorio

**git-replace**
Crear, listar, borrar refs para reemplazar objetos

#### Interrogadores:

**git-annotate**
Anota líneas de archivo con información de confirmación

**git-blame**
Muestra qué revisión y autor modificaron por última vez cada línea de un archivo

**git-bugreport**
Recopila información para que el usuario pueda enviar un informe de error

**git-count-object**
Contar el número de objetos desempaquetados y su consumo de disco

**git-diagnose**
Genera un archivo zip con información de diagnóstico

**git-difftool**
Muestra los cambios usando herramientas comunes de diff

**git-fsck**
Verifica la conectividad y validez de los objetos de la base de datos

**git-help**
Muestra información de ayuda sobre Git

**git-instaweb**
Navega instantáneamente por tu repositorio de trabajo en gitweb

**git-merge-tree**
Realiza la fusión sin tocar el índice o el árbol de trabajo

**git-rerere**
Reutiliza la resolución registrada de fusiones conflictivas

**git-show-branch**
Mostrar ramas y sus confirmaciones

**git-verify-commit**
Comprueba la firma GPG de los commits

**git-verify-tag**
Comprueba la firma GPG de las etiquetas

**git-version**
Muestra información sobre la versión de Git

**git-whatchanged**
Mostrar logs con la diferencia que introduce cada commit

**gitweb**
Interfaz web de Git (interfaz web para repositorios Git)

#### Interactuar con otros

Estos comandos sirven para interactuar con SCM ajenos y con otras personas a través de parches por correo electrónico.

**git-archimport**
Importa un repositorio GNU Arch a Git

**git-cvsexportcommit**
Exporta una única confirmación a una comprobación CVS

**git-cvsimport**
Salva tus datos de otro SCM que la gente odia

**git-cvsserver**
Un emulador de servidor CVS para Git

**git-imap-send**
Envía una colección de parches desde stdin a una carpeta IMAP

**git-p4**
Importa desde y envía a repositorios Perforce

**git-quiltimport**
Aplica un conjunto de parches quilt a la rama actual

**git-request-pull**
Genera un resumen de los cambios pendientes

**git-send-email**
Envía una colección de parches como correos electrónicos

**git-svn**
Operación bidireccional entre un repositorio Subversion y Git

#### Resetear, restaurar y revertir

Hay tres comandos con nombres similares: **git reset**, **git restore** y **git revert**.

**git-revert** consiste en hacer un nuevo commit que revierte los cambios hechos por otros commits.

**git-restore** consiste en restaurar archivos en el árbol de trabajo desde el índice o desde otra confirmación. Este comando no actualiza tu rama. El comando también puede usarse para restaurar archivos en el índice desde otra confirmación.

**git-reset** consiste en actualizar tu rama, moviendo la punta para añadir o eliminar confirmaciones de la rama. Esta operación cambia el historial de commits.

git reset también puede usarse para restaurar el índice, solapándose con git restore.