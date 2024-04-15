A veces verá atributos **escritos sin valores**. Esto es totalmente aceptable. Se denominan _atributos booleanos_. Los atributos booleanos sólo pueden tener un valor, que suele ser el mismo que el nombre del atributo. Por ejemplo, considere el atributo *disabled*, que puede asignar a elementos de entrada de formularios. (Se utiliza para desactivar los elementos de entrada del formulario para que el usuario no pueda realizar entradas. Los elementos desactivados suelen tener un aspecto grisáceo). Por ejemplo:

```html
<input type="text" disabled="disabled" />
```

Como abreviatura, es aceptable escribir esto de la siguiente manera:

```html
<!-- el uso del atributo disabled impide que el usuario final introduzca texto en el cuadro de entrada -->
<input type="text" disabled />

<!-- la entrada de texto está permitida, ya que no contiene el atributo disabled -->
<input type="text" />
```

Como referencia, el ejemplo anterior también incluye un elemento de entrada de formulario no desactivado. El HTML del ejemplo anterior produce este resultado:

![[Pasted image 20230717175532.png|center|600]]

