El **elemento HTML `<html>`** (o _elemento HTML raiz_) representa la raiz de un documento HTML. El resto de elementos descienden de este elemento.

Dado que el elemento `<html>` es el primero en un documento, aparte de los comentarios, se llama el elemento raíz. A pesar de que esta etiqueta puede ser implícita, o no requerida en HTML, sí es requerida para abrir y cerrar en XHTML.

### Contenido permitido	

Un elemento [`<head>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/head) seguido de un elemento [`<body>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/body).

### Omisión de etiqueta	

La etiqueta de inicio puede omitirse si lo primero que hay en el interior del elemento `<html>` no es un comentario. La etiqueta final puede omitirse si el elemento `<html>` no está inmediatamente seguido por un comentario y contiene un elemento `<body>`, o bien que no esté vacío, o cuya etiqueta de inicio está presente.

### Elementos padres permitidos	

Como elemento raíz de un documento, o donde se permite un fragmento de subdocumento en un documento compuesto.

### Interfaz DOM

[[Programación Web/JavaScript/DOM/HTMLHtmlElement|HTMLHtmlElement]]

## Atributos

- [[Atributos globales]]

### `manifest` 🗑️

Especifica la dirección URL de un manifiesto de recursos que indica los recursos que deben ser almacenados en la caché local.

### `version` 🗑️

Especifica la versión [Document Type Definition (en-US)](https://developer.mozilla.org/en-US/docs/Glossary/Doctype "Currently only available in English (US)") de HTML del documento actual. Este atributo no es necesario, porque es redundante con la información de versión en la declaración de tipo de documento.

### `xmlns` 

Especifica el Espacio de nombres XML del documento. El valor por defecto es `"http://www.w3.org/1999/xhtml"`. En XHTML es requerido y en HTML es opcional.

```html
<!DOCTYPE html>
<html>
  <head>...</head>
  <body>...</body>
</html>
```