#### 

Se crean dos archivos cuando creas una llave pública y privada para SSH, ¿cuál es la extensión de la llave privada?

a

.ssh

b

.ssl

c

Ninguna extensión

d

.pub

e

.rsa

La extensión de la llave privada es "c" Ninguna extensión. La llave privada no tiene una extensión de archivo específica y a menudo se guarda sin una extensión o con la extensión .pem (que significa "privacy enhanced mail"). La llave pública, por otro lado, suele tener la extensión .pub.

La llave privada es un archivo que contiene una clave criptográfica que se utiliza para autenticar la identidad del usuario cuando se conecta a un servidor mediante SSH (Secure Shell). La llave pública, por otro lado, se utiliza para verificar la autenticación de la llave privada y se almacena en el servidor para que pueda utilizarla para verificar la identidad del usuario cuando se conecta.

#### 

Cuando usas git stash, los cambios que “guardas” temporalmente se guardan en:

a

Memoria temporal, volviendo al estado del último commit.

b

Repositorio local, en una rama nueva “stash”.

c

Repositorio remoto, en una rama nueva “stash”.

d

Disco duro, en un nuevo commit.

La respuesta correcta es "a" Memoria temporal, volviendo al estado del último commit.

Git stash es una herramienta de Git que permite guardar temporalmente los cambios que se han realizado en el directorio de trabajo y volver al último estado del commit. Esto es útil cuando necesitas hacer un cambio temporalmente, pero no estás listo para hacer un commit. Los cambios guardados en el stash no se guardan en el repositorio ni en el disco duro, sino que se almacenan temporalmente en la memoria.

Cuando utilizas git stash, los cambios se guardan en una "pila de búfer" o "stash stack", lo que significa que puedes guardar varios conjuntos de cambios diferentes en el stash y recuperarlos más tarde en el orden en que se guardaron. Además, Git no crea una rama especial para el stash, sino que simplemente guarda los cambios en la memoria temporal.

#### 

Cuando hago un _fork_ de un proyecto en GitHub, ¿lo que logro es?

a

Copiar un repositorio público a mis repositorios en GitHub, con todas sus ramas e historia anterior.

b

Copiar la rama master de un repositorio público y toda su historia anterior, pero no otras ramas a menos que las especifique.

c

Copiar la versión más reciente del master de un repositorio, sin su historia anterior y así empezar desde cero mi propio proyecto.

d

Agregarme como colaborador de un repositorio remoto y poder hacer push/pull y modificaciones como colaborador a ese repositorio.

La respuesta correcta es "a" Copiar un repositorio público a mis repositorios en GitHub, con todas sus ramas e historia anterior.

Cuando haces un fork de un proyecto en GitHub, estás creando una copia del repositorio original en tu cuenta de GitHub. Esto significa que obtienes una copia exacta del repositorio original, incluyendo todas sus ramas y su historial completo. Puedes hacer cambios y modificaciones a tu copia del repositorio sin afectar al repositorio original.

Un fork es útil cuando quieres contribuir a un proyecto y necesitas tener tu propia copia del repositorio para trabajar en ella y hacer commits y push a tu copia. También puedes utilizar un fork para crear una versión modificada del proyecto original y hacer un pull request para que tus cambios se incluyan en el repositorio principal.

Nota: Cuando haces un fork, no te conviertes automáticamente en colaborador del repositorio original. Si quieres ser colaborador, deberías solicitarlo al dueño del repositorio y esperar a ser aceptado como colaborador.

#### ¿Para qué sirve GitHub Pages?

a

Es un servicio de GitHub como Azure o AWS que nos permite configurar servidores para desplegar nuestras aplicaciones.

b

Es un servicio de GitHub que nos permite comprar nombres de dominio que terminan en .github.io.

c

GitHub Pages es de pago y no funciona muy bien.

d

Es un servicio de GitHub que nos permite publicar nuestros repositorios en internet (por ejemplo, nombre.github.io o nombre.github.io/proyecto).

La respuesta correcta es "d" Es un servicio de GitHub que nos permite publicar nuestros repositorios en internet (por ejemplo, nombre.github.io o nombre.github.io/proyecto).

GitHub Pages es un servicio gratuito de GitHub que permite publicar páginas web estáticas o dinámicas en internet. Es una forma fácil de compartir tus proyectos y trabajos con otros usuarios de forma sencilla y rápida.

Con GitHub Pages, puedes crear páginas web para tus proyectos, organizaciones o usuarios, y publicarlas en internet utilizando una dirección URL de la forma nombre.github.io o nombre.github.io/proyecto. Puedes utilizar GitHub Pages para mostrar documentación, portafolios, blogs, aplicaciones y más.

GitHub Pages es gratuito y no requiere configuración ni instalación. Simplemente debes crear un repositorio y subir tus archivos HTML, CSS y JavaScript para publicar tu página web. Además, GitHub Pages es compatible con HTML, CSS, JavaScript, Jekyll y otras tecnologías web, por lo que es una opción muy versátil para publicar tus proyectos en internet.

#### 

Cuando hay un conflicto entre archivos lo mejor es:

a

Crear una rama de experimento, arreglar ahí el conflicto, hacer commit y luego merge con la rama original.

b

Borrar los conflictos, hacer checkout o rebase, cambiar de rama o recuperar un commit anterior.

c

Analizar los conflictos tal como los reportó Git y elegir los cambios finales, luego commit.

d

Sacar de staging los archivos, recuperar de otra rama la versión buena, reagregar a staging y commit.

La respuesta correcta es "c" Analizar los conflictos tal como los reportó Git y elegir los cambios finales, luego commit.

Cuando hay un conflicto entre archivos, significa que Git ha encontrado diferencias entre dos versiones del mismo archivo que no puede resolver automáticamente. Esto puede ocurrir, por ejemplo, cuando dos personas han modificado el mismo archivo en diferentes ramas y luego se han intentado hacer un merge de esas ramas.

En estos casos, Git no puede decidir qué cambios deben mantenerse y cuáles deben descartarse, así que marca los conflictos en el archivo y te deja a ti decidir qué hacer. Lo mejor es analizar los conflictos tal como los reportó Git y elegir los cambios finales que quieres mantener. Luego debes hacer un commit para finalizar el merge y resolver el conflicto.

Es importante tener cuidado al resolver conflictos, ya que debes asegurarte de no perder información importante ni romper el código. Puede ser útil utilizar herramientas de comparación de archivos o incluso pedir ayuda a otros desarrolladores para resolver conflictos complejos.

#### 

El Jefe Freddy despidió a Anita y no piensa volver a contratarla. ¿Qué debe hacer Anita para seguir haciendo contribuciones a los proyectos públicos de Platzi?

a

Demostrarle a Freddy que es sumamente profesional para que la perdone.

b

Anita puede seguir contribuyendo si utiliza su repositorio local para hacer push al repositorio original.

c

Crear un Fork del proyecto y enviar Pull Request al proyecto original.

d

Hacer fork del repositorio de Celis (developer de Platzi que también tiene un fork del proyecto original) y enviarle Pull Requests para que Celis los acepte y los mande como Pull Requests al proyecto original.

La respuesta correcta es "c" Crear un Fork del proyecto y enviar Pull Request al proyecto original.

Si Anita quiere seguir contribuyendo a los proyectos públicos de Platzi después de ser despedida, puede hacerlo creando un fork del proyecto y enviando un pull request al proyecto original. Un fork es una copia del proyecto original que se almacena en tu cuenta de GitHub. Una vez que tienes un fork, puedes hacer cambios y modificaciones a tu copia del proyecto sin afectar al proyecto original.

Para contribuir al proyecto original, debes enviar un pull request desde tu fork. Un pull request es una solicitud para incluir tus cambios en el proyecto original. Los dueños del proyecto original pueden revisar los cambios que has propuesto y decidir si quieren incluirlos en el proyecto o no. Si los cambios son aceptados, se hace un merge del pull request y tus cambios se incluyen en el proyecto original.

Otras opciones como demostrar a Freddy que es profesional o hacer fork del repositorio de otra persona no son opciones viables para contribuir al proyecto original.

#### 

El dueño de un repositorio al ver un pull request puede:

a

Publicarlo en el home de GitHub Pages.

b

Pedir cambios, solicitar autorización de merge.

c

Rechazarlo o aceptarlo, pero nada más.

d

Editarlo, aceptarlo, darle merge, comentarlo para pedir cambios.

La respuesta correcta es "d" Editarlo, aceptarlo, darle merge, comentarlo para pedir cambios.

Cuando un dueño de un repositorio recibe un pull request, tiene varias opciones para manejarlo. Algunas de las opciones disponibles incluyen:

-   Editar el pull request: Si hay algún problema con el pull request o si hay cambios que deben hacerse antes de que se pueda aceptar, el dueño del repositorio puede editar el pull request y solicitar que se realicen los cambios necesarios.
    
-   Aceptar el pull request: Si el dueño del repositorio está de acuerdo con los cambios propuestos en el pull request, puede aceptarlo y hacer un merge para incluir los cambios en el proyecto.
    
-   Comentar el pull request: Si el dueño del repositorio quiere hacer preguntas o pedir más información sobre los cambios propuestos en el pull request, puede dejar un comentario en el pull request.
    
-   Rechazar el pull request: Si el dueño del repositorio no está de acuerdo con los cambios propuestos o si considera que no son adecuados para el proyecto, puede rechazar el pull request.
    

En resumen, el dueño del repositorio tiene varias opciones para manejar un pull request, incluyendo editarlo, aceptarlo, comentarlo o rechazarlo.

#### ¿Qué es un branch o una rama en Git?

a

Un repositorio aparte del master donde puedes trabajar en paralelo.

b

Una etiqueta que le agregas a un estado del repositorio.

c

Una derivación de las ideas que plasmas en la planeación del proyecto.

d

La conexión entre dos repositorios similares.

La respuesta correcta es "a" Un repositorio aparte del master donde puedes trabajar en paralelo.

En Git, una rama o branch es una línea de desarrollo separada del proyecto principal. Es una forma de trabajar en paralelo en un proyecto y hacer cambios sin afectar al código principal.

Cuando trabajas en una rama, tienes una copia del código principal en la que puedes hacer cambios y commits sin afectar al código principal. Luego, cuando estés listo para fusionar tus cambios con el código principal, puedes hacer un merge de la rama en la rama principal (también conocida como "rama maestra" o "master").

Las ramas son útiles para trabajar en varias características o correcciones de errores al mismo tiempo, o para probar nuevas ideas sin arriesgar el código principal. Puedes crear tantas ramas como necesites y cambiar entre ellas fácilmente para trabajar en diferentes tareas.


#### ¿Cuál es la diferencia entre git rm y git reset HEAD?

a

git rm saca los archivos del repositorio y (opcionalmente) del disco duro. git reset head saca los archivos de Staging, pero no del disco duro.

b

Son lo mismo. git rm solo es un alias de git reset head.

c

git rm borra todos los commits y el historial donde aparezcan los archivos. git reset head también, pero guarda los últimos cambios en Staging.

d

git reset head saca los archivos del repositorio. git rm saca los archivos de Staging.

e

git reset head borra el último commit. git rm también, pero guarda los últimos cambios en Staging.

La respuesta correcta es:

a git rm saca los archivos del repositorio y (opcionalmente) del disco duro. git reset head saca los archivos de Staging, pero no del disco duro.

git rm es una herramienta de Git que se utiliza para eliminar archivos del repositorio y del árbol de trabajo (el directorio de trabajo local). Si se usa con la opción `--cached`, git rm eliminará el archivo del repositorio pero no del árbol de trabajo. Si se usa sin esta opción, git rm eliminará el archivo tanto del repositorio como del árbol de trabajo.

Por otro lado, git reset head es una herramienta de Git que se utiliza para deshacer cambios en el área de preparación (también conocida como "Staging Area"). La opción `HEAD` hace referencia al commit más reciente en el repositorio. Cuando se ejecuta git reset head, se eliminan los archivos de la área de preparación, pero no se eliminan del árbol de trabajo ni del repositorio. Los cambios realizados en el árbol de trabajo siguen estando presentes y pueden ser vistos con `git status`.

#### 

Es mejor aprender a manejar Git con la terminal antes de hacerlo con herramientas visuales como Gitk porque:

a

No todos los sistemas operativos soportan Gitk. Si queremos que todo el equipo pueda trabajar debemos usar Git.

b

Incorrecto: Gitk es una herramienta sumamente profesional que nos ayuda a aprender Git más rápido y sin necesidad de comandos complejos.

c

A los desarrolladores profesionales les gusta más Git que Gitk (cuestión de gustos).

d

Debemos aprender Git con sus comandos de la terminal para resolver problemas o conflictos más avanzados. Gitk funciona bien, pero no nos permite realizar operaciones tan complejas.

La respuesta correcta es "d" Debemos aprender Git con sus comandos de la terminal para resolver problemas o conflictos más avanzados. Gitk funciona bien, pero no nos permite realizar operaciones tan complejas.

Aunque Gitk es una herramienta visual que puede ser útil para aprender Git y realizar tareas básicas, es mejor aprender a manejar Git con la terminal si quieres tener un control más completo sobre el sistema. La terminal te permite acceder a todas las opciones y comandos de Git, lo que te permite realizar operaciones más avanzadas y resolver problemas o conflictos más complejos.

Además, la terminal es la forma más universal de acceder a Git, ya que está disponible en todos los sistemas operativos y es independiente de cualquier herramienta visual. Esto significa que puedes usar la terminal para trabajar con Git en cualquier sistema, lo que es especialmente útil si quieres trabajar en diferentes plataformas o si necesitas trabajar con un equipo que utiliza diferentes sistemas operativos.

En resumen, es recomendable aprender a manejar Git con la terminal para tener un control más completo sobre el sistema y poder realizar operaciones avanzadas y resolver problemas más complejos. Sin embargo, si prefieres una interfaz gráfica, Gitk o cualquier otra herramienta visual puede ser útil para aprender Git y realizar tareas básicas.

#### 

¿Qué crean los tags en Git?

a

Versiones descargables y puntos únicos en una rama de un repositorio.

b

Etiquetas para luego buscar qué tipo de archivos estaba usando y sus categorías.

c

Ramas separadas de la master en el repositorio donde trabajas.

La respuesta correcta es:

a Versiones descargables y puntos únicos en una rama de un repositorio.

Los tags en Git son etiquetas que se usan para marcar un commit específico en el repositorio. Se pueden utilizar para marcar versiones de un software o para hacer un seguimiento de cambios importantes en el proyecto. Los tags son útiles porque proporcionan una forma de acceder a un commit específico en el repositorio de forma rápida y sencilla. Los tags son inmutables, lo que significa que una vez que se han creado, no pueden ser modificados ni eliminados. Es común utilizar tags para marcar versiones de software y para hacer un seguimiento de cambios importantes en un proyecto.

#### 

¿Las llaves públicas son?

a

Fáciles de compartir y sus mensajes imposibles de descifrar.

b

Sistemas de cifrado básicos donde la misma llave puede cifrar y descifrar un mensaje.

c

Imposibles de descifrar e imposibles de compartir.

d

No compartibles y fáciles de descifrar.

La respuesta correcta es "a" Fáciles de compartir y sus mensajes imposibles de descifrar.

Las llaves públicas son una parte fundamental de los sistemas de cifrado asimétrico, que se utilizan para proteger la información y asegurar la privacidad de las comunicaciones. En un sistema de cifrado asimétrico, hay dos llaves: una llave pública y una llave privada.

La llave pública es fácil de compartir y se utiliza para cifrar mensajes o archivos. Los mensajes cifrados con la llave pública solo pueden descifrarse con la llave privada correspondiente, por lo que son imposibles de descifrar para cualquier otra persona que no tenga la llave privada. Esto significa que puedes compartir tu llave pública con cualquier persona sin preocuparte por la seguridad de la información.

La llave privada, por otro lado, es importante mantenerla en secreto y se utiliza para descifrar los mensajes cifrados con la llave pública. Es importante proteger la llave privada y no compartirla con nadie, ya que es la única forma de descifrar los mensajes cifrados con la llave pública.

#### 

Si usas:

`git config --global alias.platzi "shortlog"`

¿Cómo invocar ese comando?

a

```
./platzi
```
b

```
git alias.platzi
```
c

```
git platzi
```
d

```
git shortlog platzi
```

e

```
git global platzi
```

La respuesta correcta es:

c git platzi

Cuando se ejecuta el comando `git config --global alias.platzi "shortlog"`, se está creando un alias global llamado `platzi` para el comando `shortlog`. Esto significa que cuando se quiera ejecutar el comando `shortlog`, se puede usar el alias `platzi` en su lugar.

Para invocar el alias, se debe ejecutar `git platzi`. Este comando ejecutará el comando `shortlog` en realidad, ya que el alias `platzi` ha sido configurado para que sea un alias del comando `shortlog`.

Otras opciones no son correctas porque no son la forma correcta de invocar el alias. Por ejemplo, `./platzi` no es un comando válido en Git, ya que Git no busca en el directorio actual para encontrar comandos. Además, `git alias.platzi` y `git global platzi` son también formas incorrectas de invocar el alias, ya que no es necesario incluir `alias` o `global` al usar el alias.

# REHACER

#### ¿Qué guarda Git?

a

Los cambios de los archivos de un proyecto.

b

Los textos de mensajes a los que hago “commit”.

c

Git no guarda nada. Es sólo una referencia.

d

Los archivos completos por cada versión de un proyecto.

La respuesta correcta es:

d Los archivos completos por cada versión de un proyecto.

Git es un sistema de control de versiones que se utiliza para llevar un seguimiento de los cambios realizados en los archivos de un proyecto a lo largo del tiempo. Cada vez que se hace un commit (guardar cambios) en Git, se guarda una copia completa de los archivos del proyecto en ese momento. Esto permite volver atrás a versiones anteriores de los archivos si es necesario, y también permite comparar cambios entre diferentes versiones.

Git también guarda información sobre los cambios realizados en los archivos, como quién los realizó y cuándo se hicieron. Además, Git guarda el mensaje de commit que se escribió cuando se hizo el commit, lo que permite entender el propósito de los cambios realizados.

#### 

En un repositorio público en GitHub, ¿qué puede hacer los colaboradores?

a

Crear ramas y trabajar sobre ellas, pero no sobre master.

b

Solo hacer pull requests y con permiso del dueño hacer push/pull, crear ramas, etc.

c

Hacer cambios al repositorio, hacer push/pull, crear ramas, etc.

d

Ver el código y clonarlo, pero no editarlo.

En un repositorio público en GitHub, los colaboradores pueden hacer cambios al repositorio, hacer push/pull, crear ramas, etc. Los colaboradores pueden contribuir al proyecto realizando cambios y enviando solicitudes de extracción (pull requests) para que los cambios sean revisados y fusionados al repositorio principal. Sin embargo, es importante tener en cuenta que el dueño del repositorio tiene la última palabra sobre qué cambios se fusionan y cuáles no.

#### 

¿Con amend puedo?

a

Cambiar el staging de un archivo erróneo al archivo correcto.

b

Solucionar conflictos ante un merge que generó errores.

c

Corregir los mensajes de un commit que hice mal sin que quede en la historia del repositorio.

d

Agregar un nuevo commit que repare el anterior, quedando en la historia del repo.


El comando `git commit --amend` permite modificar el último commit realizado en el repositorio. Con este comando, puedes realizar las siguientes acciones:

-   Cambiar el mensaje del commit: puedes usar este comando para corregir errores o agregar información adicional al mensaje del commit.
    
-   Agregar o eliminar archivos del commit: puedes usar este comando para agregar archivos que se olvidaron de incluir en el commit anterior o eliminar archivos que no debieron ser incluidos.
    
-   Corregir conflictos de fusión: si un merge generó conflictos, puedes usar este comando para solucionarlos y crear un nuevo commit con los cambios corregidos.
    

Es importante tener en cuenta que al utilizar `git commit --amend`, se crea un nuevo commit que reemplaza al commit anterior, lo que significa que el commit original desaparece de la historia del repositorio. Esto puede ser útil para corregir errores o hacer ajustes menores al último commit, pero se deben tener precaución al utilizar este comando, ya que los cambios realizados no pueden deshacerse.

#### 

Por defecto, GitHub usa la rama main como la rama principal. ¿Podemos cambiar la rama principal?

a

Verdadero

b

Falso

Es verdad que por defecto, GitHub usa la rama main como la rama principal de un repositorio. Sin embargo, es posible cambiar la rama principal de un repositorio en GitHub.

Para cambiar la rama principal de un repositorio en GitHub, debes seguir los siguientes pasos:

1.  Accede al repositorio en GitHub y selecciona la pestaña "Settings" (Configuración).
2.  En la sección "Options" (Opciones), encontrarás una opción llamada "Default branch" (Rama principal por defecto).
3.  Haz clic en el menú desplegable y selecciona la rama que quieres que sea la rama principal.
4.  Haz clic en el botón "Save" (Guardar) para guardar los cambios.

Es importante tener en cuenta que cambiar la rama principal de un repositorio puede tener consecuencias en otras ramas y en las solicitudes de extracción (pull requests) existentes. Es recomendable proceder con precaución y asegurarse de que se entienden las implicaciones de cambiar la rama principal antes de hacerlo.

#### 

Con checkout puedo:

a

Enviar todos los cambios al repositorio.

b

Ver todos los archivos de mi proyecto como los dejé en otras ramas.

c

Enviar todos los cambios al servidor.

d

Borrar los errores que cometí en un archivo.

Con `checkout` puedes realizar las siguientes acciones:

a) Cambiar de rama en un repositorio Git.

b) Descargar una versión específica de un archivo o de todo el repositorio desde el servidor.

c) Deshacer cambios en un archivo o en todo el repositorio.

d) Crear una nueva rama a partir de un commit específico.

En resumen, `checkout` es una herramienta muy útil en Git que te permite cambiar entre ramas y revertir cambios en tu proyecto. Sin embargo, no permite enviar cambios al repositorio ni al servidor. Para hacerlo, debes utilizar otras operaciones de Git, como `commit` y `push`.

#### 

Si ya hiciste el desafío de “Hazme un pull request,” ¿dentro de cuál etiqueta tenías que agregar el cambio?

a

```
<div id="footer"> 
``` 
b

```
<divid="cabecera">
```
c

```
<divid="post">
```
d

```
<divid="desafio"> 
```

El cambio debía hacerse dentro de la etiqueta <divid="desafio">. Esta es la respuesta correcta.

#### 

Un pull request es:

a

Un merge opcional entre repositorios locales.

b

Una petición de traer a mi local el contenido de un repositorio remoto.

c

Un cambio sugerido a un repositorio que el dueño del repositorio puede autorizar y hacer merge a la rama que elija.

d

Un merge forzado de mi master al master de producción.

La respuesta correcta es: c

Un pull request es una solicitud de integración de cambios que se realiza en un repositorio de código. Es una forma de sugerir cambios a un repositorio y pedir a los dueños del repositorio que revisen y acepten esos cambios para que se integren en el repositorio. Un pull request es una característica comúnmente utilizada en el desarrollo de software y en proyectos de colaboración en línea. Los dueños del repositorio tienen la opción de revisar y comparar los cambios propuestos, realizar cambios adicionales o rechazar la solicitud de integración de cambios.


####
¿GitHub es? a Un sistema online de manejo de repositorios de Git. b Un software de control de versiones. c Un sitio web de descarga de librerías y proyectos open source. d Una red social de programadores.

a. Un sistema online de manejo de repositorios de Git.

GitHub es una plataforma online que ofrece almacenamiento y control de versiones para proyectos de software, utilizando el sistema de control de versiones Git. Es utilizado principalmente por desarrolladores de software para alojar y colaborar en proyectos de código abierto, pero también puede ser utilizado para proyectos privados. GitHub ofrece una amplia variedad de herramientas y características para colaboración y desarrollo de proyectos, como seguimiento de errores, gestión de tareas y herramientas de revisión de código. También es una plataforma popular para descubrir y descargar proyectos de código abierto.


#### 

Un repositorio remoto y un repositorio local:

a

Tienen ramas similares dependiendo de cuáles haya enviado entre uno y otro.

b

Tienen las mismas ramas dado que uno es un reflejo del otro.

c

Tienen ramas 100% diferentes dado que cada uno es distinto.

###

¿Cómo llaman GitHub y GitLab a los "merges" (propuestas de cambios desde otra rama o repositorio)? a Merge Request b Pull Request c GitHub los llama Pull Request y GitLab Merge Request.

La respuesta correcta es: c

GitHub y GitLab tienen diferentes términos para referirse a las "propuestas de cambios" que se realizan desde otra rama o repositorio. En GitHub, estos cambios se llaman "Pull Requests". En GitLab, estos cambios se llaman "Merge Requests". Aunque los términos son diferentes, ambos servicios ofrecen una forma similar de solicitar la integración de cambios en un repositorio de código.

Un Pull Request o Merge Request es una solicitud de integración de cambios que se realiza en un repositorio de código. Es una forma de sugerir cambios a un repositorio y pedir a los dueños del repositorio que revisen y acepten esos cambios para que se integren en el repositorio. Los dueños del repositorio tienen la opción de revisar y comparar los cambios propuestos, realizar cambios adicionales o rechazar la solicitud de integración de cambios.

#### 

¿Qué puedes hacer con gitk?

a

Ver en la linea de comandos las ramas y el log de tu repositorio.

b

Ver el reflog en linea de comandos de tu historia.

c

Abrir en GitHub las ramas y log de tu repositorio.

d

Ver en una interfaz visual las ramas y el log de tu repositorio.

e

Ver el reflog en una interfaz visual.

La respuesta correcta es: d, e

Gitk es una herramienta de visualización de repositorios de Git que se ejecuta desde la línea de comandos. Con gitk, puedes ver el log de tu repositorio y las ramas existentes de forma visual, en lugar de tener que revisar el log o las ramas en la línea de comandos. Además, gitk te permite ver el reflog, que es un registro de todas las operaciones que se han realizado en tu repositorio, incluyendo operaciones de merge, revert, cherry-pick y más. Gitk es una herramienta útil para explorar y entender la historia de un repositorio de Git y para ver cómo se han realizado cambios en el repositorio a lo largo del tiempo.

###

Un repositorio remoto y un repositorio local: a Tienen ramas similares dependiendo de cuáles haya enviado entre uno y otro. b Tienen las mismas ramas dado que uno es un reflejo del otro. c Tienen ramas 100% diferentes dado que cada uno es distinto.

a y b son incorrectas.

c es correcta. Un repositorio remoto es un repositorio que se encuentra en un servidor externo y se puede acceder a él a través de Internet. Por otro lado, un repositorio local es un repositorio que se encuentra en tu propia computadora y solo es accesible desde ella. Por lo tanto, pueden tener ramas totalmente diferentes, ya que cada uno puede tener su propio conjunto de cambios y archivos.

Es posible sincronizar los repositorios remoto y local para mantenerlos al día, pero incluso en ese caso, pueden tener diferencias en las ramas y en los cambios que se hayan realizado en cada uno de ellos. Por ejemplo, puedes tener una rama en tu repositorio local que no exista en el repositorio remoto, o viceversa.

#### ¿Puedes conectar tu repositorio local con más de un repositorio remoto?

a

Verdadero

b

Falso

a es correcto. Es posible conectar tu repositorio local con más de un repositorio remoto. Esto se llama tener múltiples remotos y puede ser útil en varias situaciones, como por ejemplo:

-   Si quieres colaborar con diferentes proyectos que se encuentran en diferentes repositorios remotos.
-   Si quieres tener una copia de seguridad de tu repositorio local en varios repositorios remotos diferentes.
-   Si quieres sincronizar tu repositorio local con diferentes servidores o servicios de almacenamiento, como por ejemplo GitHub y GitLab.

Para conectar tu repositorio local con múltiples remotos, puedes usar el comando `git remote add` y especificar un nombre y una dirección URL para cada repositorio remoto al que quieras conectarte. Luego, puedes usar los comandos `git push` y `git pull` para enviar y recibir cambios de y hacia cualquiera de los repositorios remotos a los que estés conectado.

#### 

Si en el .gitignore agrego esto: images/*.js. ¿Cuál de los siguientes archivos sería ignorado?

a

images/jquery.js

b

images/jquery.jpg

c

images/java.jsp

d

javascript/jquery.js

La respuesta correcta es: a

El archivo .gitignore es un archivo que se utiliza para indicar a Git qué archivos o carpetas deben ser ignorados y no deben ser incluidos en el control de versiones. Si en el .gitignore agregas la línea "images/*.js", esto indicaría a Git que ignore todos los archivos con la extensión .js que se encuentren en la carpeta images.

En este caso, el archivo "images/jquery.js" sería ignorado, ya que cumple con el patrón de búsqueda especificado en el .gitignore. Los demás archivos mencionados (images/jquery.jpg, images/java.jsp y javascript/jquery.js) no serían ignorados, ya que no cumplen con el patrón de búsqueda especificado en el .gitignore.

Es importante tener en cuenta que el .gitignore solo afecta a archivos o carpetas que aún no han sido agregados a tu repositorio de Git. Si un archivo o carpeta ha sido agregado a tu repositorio y luego es especificado en el .gitignore, ese archivo o carpeta seguirá siendo controlado por Git y no será ignorado.

#### 

Los cambios a un archivo que están en “staging” están en:

a

Un área temporal en memoria antes de llegar al repositorio.

b

Solo en tu disco, no están siendo rastreados por Git.

c

En un servidor temporal de pruebas.

d

Ya en el repositorio, rastreados y confirmados.

La respuesta correcta es a: Un área temporal en memoria antes de llegar al repositorio.

Cuando haces cambios a un archivo y los colocas en el área de "staging" con el comando `git add`, estos cambios se guardan temporalmente en un área de memoria conocida como el área de "staging". Estos cambios todavía no han sido confirmados y no se han agregado al repositorio de Git. Para confirmar los cambios y agregarlos al repositorio, debes usar el comando `git commit`.

Es importante tener en cuenta que los cambios en el área de "staging" solo están disponibles en tu sistema local y no se han compartido con otros repositorios o servidores.

#### 

¿El HEAD en una rama es?

a

El apuntador al estado actual del repositorio basado en la rama en la que estoy trabajando.

b

El apuntador al estado inicial de un repositorio en la rama master.

c

El inicio de una rama.

d

El inicio de un repositorio.

a) El apuntador al estado actual del repositorio basado en la rama en la que estoy trabajando.

El HEAD es un apuntador especial en Git que siempre se refiere al último commit realizado en el repositorio. Se puede considerar como el "estado actual" del repositorio. Cuando se trabaja en una rama en particular, el HEAD se refiere al último commit de esa rama. Por lo tanto, la respuesta correcta es la opción a).

Es importante tener en cuenta que el HEAD no es necesariamente el último commit en la rama master, sino que se refiere al último commit en la rama en la que estás trabajando.

#### 

Para transmitir cambios seguros entre tu repositorio local y GitHub, ¿qué se recomienda?

a

Usar una llave SSH.

b

Usar el cliente oficial de GitHub.

c

Usar una contraseña fuerte.

d

Usar una llave SSL.

La respuesta correcta es a: Usar una llave SSH.

Para transmitir cambios de forma segura entre tu repositorio local y un repositorio remoto en GitHub, se recomienda utilizar una llave SSH (Secure Shell). Las llaves SSH son una forma segura de autenticar tu acceso a un servidor remoto y proteger tus comunicaciones.

Para usar una llave SSH con tu repositorio en GitHub, debes generar una llave SSH en tu sistema local y agregarla a tu cuenta de GitHub. Luego, puedes usar el protocolo SSH para conectarte a tu repositorio y realizar operaciones de push y pull de forma segura.

Otras opciones como usar una contraseña fuerte o el cliente oficial de GitHub también pueden ser útiles, pero no ofrecen la misma seguridad que las llaves SSH.

#### 

Git funciona para muchos tipos de archivo, ¿Qué tal funciona Git con archivos binarios?

a

Git está optimizado para archivos binarios, no tiene ningún problema con todas sus herramientas.

b

Git no funciona con archivos binarios, pero GitHub sí.

c

Los puede agregar y versionar pero es mejor usar Git con texto plano.

d

Git no puede usar archivos binarios, solo texto plano.

c) Los puede agregar y versionar pero es mejor usar Git con texto plano.

Git puede manejar archivos binarios, pero es mejor usar Git con archivos de texto plano debido a ciertas limitaciones de Git al trabajar con archivos binarios. Los archivos binarios son archivos que no son de texto plano, como imágenes, audio o vídeo. Aunque Git puede almacenar y versionar estos tipos de archivos, puede tener dificultades para detectar y resolver conflictos en ellos. Además, los archivos binarios suelen ser más grandes que los archivos de texto, lo que puede aumentar el tamaño del repositorio y hacer que sea más difícil de trabajar. Por lo tanto, es mejor usar Git con archivos de texto plano y utilizar otras herramientas para manejar archivos binarios.

Es importante tener en cuenta que Git y GitHub son dos cosas diferentes. GitHub es una plataforma de desarrollo de código que utiliza Git como su sistema de control de versiones, pero Git es un sistema de control de versiones en sí mismo y puede usarse sin GitHub.




#################



<mark style="background: #BBFABBA6;">
Git funciona para muchos tipos de archivo, ¿Qué tal funciona Git con archivos binarios?

Los puede agregar y versionar pero es mejor usar Git con texto plano.
</mark>

<mark style="background: #FF5582A6;">2.

¿Qué guarda Git?

Los archivos completos por cada versión de un proyecto.

REPASAR CLASE</mark>

<mark style="background: #BBFABBA6;">3.

Los cambios a un archivo que están en “staging” están en:

Un área temporal en memoria antes de llegar al repositorio.</mark>

<mark style="background: #BBFABBA6;">4.

¿Qué es un branch o una rama en Git?

Un repositorio aparte del master donde puedes trabajar en paralelo.</mark>

<mark style="background: #BBFABBA6;">5.

Con checkout puedo:

Ver todos los archivos de mi proyecto como los dejé en otras ramas.</mark>

<mark style="background: #FF5582A6;">6.

Un repositorio remoto y un repositorio local:

Tienen ramas 100% diferentes dado que cada uno es distinto.

REPASAR CLASE</mark>

<mark style="background: #BBFABBA6;">7.

¿El HEAD en una rama es?

El apuntador al estado actual del repositorio basado en la rama en la que estoy trabajando.</mark>

<mark style="background: #BBFABBA6;">8.

Cuando hay un conflicto entre archivos lo mejor es:

Analizar los conflictos tal como los reportó Git y elegir los cambios finales, luego commit.</mark>

<mark style="background: #BBFABBA6;">9.

¿GitHub es?

Un sistema online de manejo de repositorios de Git.</mark>

<mark style="background: #BBFABBA6;">10.

¿Las llaves públicas son?

Fáciles de compartir y sus mensajes imposibles de descifrar.</mark>

<mark style="background: #BBFABBA6;">11.

Para transmitir cambios seguros entre tu repositorio local y GitHub, ¿qué se recomienda?

Usar una llave SSH.</mark>

<mark style="background: #BBFABBA6;">12.

Se crean dos archivos cuando creas una llave pública y privada para SSH, ¿cuál es la extensión de la llave privada?

Ninguna extensión</mark>

<mark style="background: #BBFABBA6;">13.

¿Qué crean los tags en Git?

Versiones descargables y puntos únicos en una rama de un repositorio.</mark>

<mark style="background: #FF5582A6;">14.

En un repositorio público en GitHub, ¿qué puede hacer los colaboradores?

Crear ramas y trabajar sobre ellas, pero no sobre master.

REPASAR CLASE</mark>

<mark style="background: #BBFABBA6;">15.

Un pull request es:

Un cambio sugerido a un repositorio que el dueño del repositorio puede autorizar y hacer merge a la rama que elija.</mark>

<mark style="background: #BBFABBA6;">16.

El dueño de un repositorio al ver un pull request puede:

Editarlo, aceptarlo, darle merge, comentarlo para pedir cambios.</mark>

<mark style="background: #BBFABBA6;">17.

Cuando hago un _fork_ de un proyecto en GitHub, ¿lo que logro es?

Copiar un repositorio público a mis repositorios en GitHub, con todas sus ramas e historia anterior.</mark>

<mark style="background: #FF5582A6;">18.

Si ya hiciste el desafío de “Hazme un pull request,” ¿dentro de cuál etiqueta tenías que agregar el cambio? REPASAR CLASE</mark>

```
<divid="desafio"> 
```

<mark style="background: #BBFABBA6;">19.

Si en el .gitignore agrego esto: images/*.js. ¿Cuál de los siguientes archivos sería ignorado?

images/jquery.js</mark>

<mark style="background: #BBFABBA6;">20.

Cuando usas git stash, los cambios que “guardas” temporalmente se guardan en:

Memoria temporal, volviendo al estado del último commit.</mark>

<mark style="background: #BBFABBA6;">21.

¿Con amend puedo?

Corregir los mensajes de un commit que hice mal sin que quede en la historia del repositorio.</mark>

<mark style="background: #BBFABBA6;">22.

¿Qué puedes hacer con gitk?

Ver en una interfaz visual las ramas y el log de tu repositorio.</mark>

<mark style="background: #BBFABBA6;">23.

Si usas:

`git config --global alias.platzi "shortlog"`

¿Cómo invocar ese comando?</mark>

```
git platzi
```

<mark style="background: #BBFABBA6;">24.

Es mejor aprender a manejar Git con la terminal antes de hacerlo con herramientas visuales como Gitk porque:

Debemos aprender Git con sus comandos de la terminal para resolver problemas o conflictos más avanzados. Gitk funciona bien, pero no nos permite realizar operaciones tan complejas.</mark>

<mark style="background: #BBFABBA6;">25.

¿Cómo llaman GitHub y GitLab a los "merges" (propuestas de cambios desde otra rama o repositorio)?

GitHub los llama Pull Request y GitLab Merge Request.</mark>

<mark style="background: #BBFABBA6;">26.

¿Puedes conectar tu repositorio local con más de un repositorio remoto?

Verdadero</mark>

<mark style="background: #BBFABBA6;">27.

¿Cuál es la diferencia entre git rm y git reset HEAD?

git rm saca los archivos del repositorio y (opcionalmente) del disco duro. git reset head saca los archivos de Staging, pero no del disco duro.</mark>

<mark style="background: #BBFABBA6;">28.

Por defecto, GitHub usa la rama main como la rama principal. ¿Podemos cambiar la rama principal?

Verdadero</mark>

<mark style="background: #BBFABBA6;">29.

¿Para qué sirve GitHub Pages?

Es un servicio de GitHub que nos permite publicar nuestros repositorios en internet (por ejemplo, nombre.github.io o nombre.github.io/proyecto).</mark>

<mark style="background: #BBFABBA6;">30.

El Jefe Freddy despidió a Anita y no piensa volver a contratarla. ¿Qué debe hacer Anita para seguir haciendo contribuciones a los proyectos públicos de Platzi?

Crear un Fork del proyecto y enviar Pull Request al proyecto original.</mark>