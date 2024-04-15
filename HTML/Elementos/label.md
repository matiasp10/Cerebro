El **Elemento HTML `<label>`** representa una etiqueta para un elemento en una interfaz de usuario. Este puede estar asociado con un control ya sea mediante la utilizacion del atributo _for_, o ubicando el control dentro del elemento _label_. Tal control es llamado "el control etiquetado" del elemento _label_.

## Atributos

### accesskey

Una tecla de atajo para acceder a este elemento desde el teclado.

### for

El ID del elemento de formulario etiquetable relacionado en el mismo documento que el elemento label. El primer elemento en el documento con tal ID que coincida con el dispuesto en el atributo for será el control etiquetado para este elemento.

> **Nota**: Un elemento label puede contener ambos; El atributo for y el elemento de control anidado, siempre y cuando el atributo for apunte al mismo elemento.

### form

El formulario con el cual el label está asociado (su formulario dueño). El valor de este atributo debe ser un ID del elemento <form> en el mismo documento. Si este atributo no es especificado, este elemento <label> deberia ser descendiente de un elemento <form>. Este atributo permite ubicar el elemento label en cualquier lugar dentro del documento y no solo como descendiente de su respectivo formulario.

