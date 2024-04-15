El encapsulamiento es un mecanismo de programación que une al código y a los datos que manipula y que los mantiene a salvo de interferencias y de un mal uso externo. **En un lenguaje orientado a objetos, el código y los datos pueden unirse de tal manera que pueda crearse una caja negra de contenido independiente**. Dentro de la caja están todos los datos y el código necesarios. Cuando el código y los datos están vinculados de esta manera, se crea un objeto. En otras palabras, un objeto es el dispositivo que soporta el encapsulamiento.

Dentro de un objeto, el código, los datos, o ambos, pueden ser _privados_, o _públicos_, en relación con dicho objeto. El código o los datos privados son conocidos para la otra parte del objeto, y sólo ésta puede tener acceso a ellos. Es decir, una parte del programa que se encuentra fuera del objeto no puede acceder al código o los datos privados. Cuando el código o los datos son públicos, otras partes de su programa pueden acceder a ellos aunque estén definidos dentro del objeto. Por lo general, las partes públicas de un objeto se usan para proporcionar una interfaz controlada a los elementos privados de un objeto.

<mark style="background: #FFB86CA6;">La unidad básica de encapsulamiento de Java es la clase.</mark> Una clase define la forma de un objeto; especifica los datos y el código que operarán sobre los datos. Java usa una especificación de clase para construir objetos. Los objetos son instancias de una clase. Por consiguiente, **una clase es, en esencia, un conjunto de planos que especifican la manera de construir un objeto**.

Al **código** y los **datos** que constituyen una clase se les denomina <mark style="background: #ADCCFFA6;">miembros de la clase</mark>. De manera específica, los datos definidos por la clase son denominados <mark style="background: #ADCCFFA6;">variables de miembro o variables de instancia</mark>. **Método** es el término que usa Java para una <mark style="background: #FF5582A6;">subrutina</mark>.