El **DOM virtual** (**VDOM**) es un concepto de programación donde una representación ideal o “virtual” de **la IU se mantiene en memoria** y en **sincronía con el DOM “real”**, mediante una biblioteca como **ReactDOM**. Este proceso se conoce como [reconciliación](https://es.reactjs.org/docs/reconciliation.html).

[[Reconciliacion]]

Este enfoque hace posible la **API declarativa de React**: le dices a React en qué estado quieres que esté la IU, y se hará cargo de llevar el DOM a ese estado. Esto abstrae la manipulación de atributos, manejo de eventos y actualización manual del DOM que de otra manera tendrías que usar para construir tu aplicación.

Ya que “DOM virtual” **es más un patrón que una tecnología específica**, las personas a veces le dan significados diferentes. En el mundo de React, el término “DOM virtual” es normalmente asociado con [elementos de React](https://es.reactjs.org/docs/rendering-elements.html) ya que son **objetos representando la interfaz de usuario**. Sin embargo, React también usa objetos internos llamados “**fibers**” para mantener información adicional acerca del árbol de componentes. Éstos pueden ser también considerados como parte de la implementación de “DOM virtual” de React.

