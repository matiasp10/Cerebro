La _pseudo-clase_ **:root** de _CSS_ selecciona el elemento raíz de un árbol que representa el documento. En _HTML_, `:root` representa el elemento `<html>` y es idéntico al selector **html**, excepto que su especificidad es mayor.

```css
/* Selecciona el elemento raíz del documento:
   <html> en el caso de HTML */
:root {
  background: yellow;
}
```
## Sintaxis

```css
:root {
  /* ... */
}
```
## Ejemplos
### Declarando variables globales

`:root` puede ser útil para declarar variables **CSS globales**:

```css
:root {
  --main-color: hotpink;
  --pane-padding: 5px 42px;
}
```