#Patron-de-diseño #Objetos

Una de las formas más sencillas de organizar el código es agrupar las cosas en objetos. Toma estos ejemplos de un juego 'tic tac toe':

```javascript
// ejemplo 1
const playerOneName = "tim"
const playerTwoName = "jenn"
const playerOneMarker = "X"
const playerTwoMarker = "O"

// ejemplo 2
const playerOne = {
  name: "tim",
  marker: "X"
}

const playerTwo = {
  name: "jenn",
  marker: "O"
}
```

A primera vista, el primero no parece tan malo... y de hecho se necesitan menos líneas para escribirlo que el ejemplo que utiliza objetos, ¡pero las ventajas del segundo enfoque son enormes! Déjame demostrártelo:

```javascript
function printName(player) {
  console.log(player.name)
}
```

Esto es algo que NO podrías hacer con la configuración del ejemplo uno. En su lugar, cada vez que quisiera imprimir el nombre de un jugador específico, tendría que recordar el nombre correcto de la variable y luego manualmente `console.log`:

```javascript
console.log(playerOneName)
console.log(playerTwoName)
```

De nuevo, esto no es tan malo... pero ¿qué pasa si no sabes qué nombre de jugador quieres imprimir?

```javascript
function gameOver(winningPlayer){
  console.log("Congratulations!")
  console.log(winningPlayer.name + " is the winner!")
}
```

¿Y si no estamos haciendo un juego para 2 jugadores, sino algo más complicado, como un sitio de compras en línea con un gran inventario? En ese caso, el uso de objetos para realizar un seguimiento del nombre de un artículo, el precio, la descripción y otras cosas es la única manera de hacerlo. Desafortunadamente, en este tipo de situaciones, escribir manualmente el contenido de nuestros objetos tampoco es factible. Necesitamos una forma más limpia de crear nuestros objetos, lo que nos lleva a...

[[Funciones constructoras]]