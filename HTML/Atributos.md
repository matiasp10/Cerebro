Los atributos contienen **información adicional sobre el elemento** que no aparecerá en el contenido.

Un atributo debe tener:  
  
- Un **espacio entre él y el nombre del elemento**. (En el caso de un elemento con más de un atributo, los atributos también deben ir separados por espacios). 
- El **nombre del atributo**, seguido de un signo igual.  
- El **valor del atributo**, entre comillas de apertura y cierre.

![[Pasted image 20230717173741.png|center]]

### Véase también

- [[Atributos booleanos]]
- [[Atributos globales]]

### Omitir las comillas alrededor de los valores de los atributos

Si echa un vistazo al código de muchos otros sitios, es posible que se encuentre con una serie de extraños estilos de marcado, incluidos valores de atributos sin comillas. Esto está permitido en determinadas circunstancias, pero también puede romper el marcado en otras circunstancias. Por ejemplo, podríamos escribir una versión básica con sólo el atributo `href`, así:

```html
<a href=https://www.mozilla.org/>favorite website</a>
```

Sin embargo, en cuanto añadimos el atributo `title` de esta forma, surgen problemas:

```html
<a href=https://www.mozilla.org/ title=The Mozilla homepage>favorite website</a>
```

Como se ha escrito anteriormente, el navegador malinterpreta el marcado, confundiendo el atributo `title` con tres atributos: un atributo **`title`** con el valor `The`, y **dos atributos booleanos**, `Mozilla` y `homepage`. Obviamente, ¡esto no está previsto! Provocará errores o comportamientos inesperados.

Incluya siempre las comillas de atributo. Evita este tipo de problemas y resulta en un código más legible.

### ¿Comillas simples o dobles?

Sin embargo, es posible que vea comillas simples en algunos códigos HTML. Es una cuestión de estilo. Puedes elegir la que prefieras. Ambas líneas son equivalentes:

```html
<a href='https://www.example.com'>A link to my example.</a>

<a href="https://www.example.com">A link to my example.</a>
```

Asegúrate de no mezclar comillas simples y dobles. Este ejemplo (abajo) muestra un tipo de mezcla de comillas que irá mal:

```html
<a href="https://www.example.com'>A link to my example.</a>
```

Sin embargo, si utiliza un tipo de cita, puede incluir el otro tipo de cita dentro de los valores de sus atributos:

```html
<a href="https://www.example.com" title="Isn't this fun?">
  A link to my example.
</a>
```

Para utilizar comillas dentro de otras comillas del mismo tipo (simples o dobles), utilice entidades HTML. Por ejemplo, esto se romperá:

```html
<a href="https://www.example.com" title="An "interesting" reference">A link to my example.</a>
```

En su lugar, tienes que hacer esto:

```html
<a href="https://www.example.com" title="An &quot;interesting&quot; reference">A link to my example.</a>
```