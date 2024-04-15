# Document.doctype

Devuelve la Declaración de tipo de documento (_Document Type Declaration (DTD)_), asociada al documento actual. El objeto devuelto implementa la interfaz _DocumentType_. Utilice _DOMImplementation.createDocumentType()_ para crear un _DocumentType_.

```js
doctype = document.doctype;
```

> [!hint] 
> doctype es una propiedad de sólo lectura.

La propiedad devuelve `null` si no hay DTD asociada al documento actual.