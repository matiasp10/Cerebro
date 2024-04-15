Los elementos pueden colocarse dentro de otros elementos. Esto se llama **anidamiento**. Si quisiéramos decir que nuestro gato es muy gruñón, podríamos envolver la palabra muy en un elemento `<strong>`, lo que significa que la palabra tendrá un formato de texto más fuerte:

```html
<p>Mi gato es <strong>muy</strong> gruñon.</p>
```

Hay una forma **correcta** y otra **incorrecta** de hacer el anidamiento. En el ejemplo anterior, abrimos primero el elemento *p* y luego abrimos el elemento *strong*. Para un anidamiento correcto, deberíamos cerrar primero el elemento *strong*, antes de cerrar el *p*.

A continuación se muestra un ejemplo de la **forma incorrecta** de realizar el anidamiento:

```html
<p>Mi gato es <strong>muy gruñon.</p></strong>
```

Las etiquetas tienen que abrirse y cerrarse de forma que queden una dentro de otra o una fuera de otra. Con el tipo de solapamiento del ejemplo anterior, el navegador tiene que adivinar tu intención. Este tipo de suposición puede dar lugar a resultados inesperados.