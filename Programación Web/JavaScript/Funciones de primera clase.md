Las funciones de primera clase son funciones que **pueden tratarse como cualquier otro valor del lenguaje**. Esto significa que _pueden asignarse a variables, pasarse como argumentos a otras funciones y devolverlas desde otras funciones_.

Las funciones de primera clase son una característica importante de la **programación funcional**, que es un paradigma de programación que se centra en el uso de funciones. Las funciones de primera clase permiten a los programadores escribir código más conciso y flexible.

En **JavaScript**, todas las funciones son funciones de primera clase. Esto significa que se pueden usar en una variedad de escenarios, como:

- Asignar una función a una variable:

```js
const miFuncion = function () {
  console.log("Hola, mundo!");
};
```

- Pasar una función como argumento a otra función:

```js
function saludar(nombre, funcionSaludo) {
  funcionSaludo(nombre);
}

saludar("Juan", miFuncion); // Imprime "Hola, Juan!"
```

- Devolver una función desde otra función:

```js
function crearFuncionSaludo() {
  return function (nombre) {
    console.log("Hola, " + nombre + "!");
  };
}

const miFuncionSaludo = crearFuncionSaludo();
miFuncionSaludo("Juan"); // Imprime "Hola, Juan!"
```

Las funciones de primera clase son una herramienta poderosa que puede ayudar a los programadores a escribir código más eficiente y flexible.