Escribe un constructor para crear objetos "Libro". Volveremos sobre esto en el proyecto al final de esta lección. Tus objetos libro deben tener el título del libro, el autor, el número de páginas, y si has leído o no el libro.

Ponga una función en el constructor que pueda reportar la información del libro así:

```javascript
theHobbit.info() // "The Hobbit by J.R.R. Tolkien, 295 pages, not read yet"
```

>[!note] Nota
>Casi siempre es mejor devolver cosas que poner console.log() directamente en la función. En este caso, devuelva la cadena de información y regístrela después de llamar a la función:
>```js
>console.log(theHobbit.info());
>```

# Mi solución

```js
function Libro(title, author, pages, isRead){
  this.title = title,
    this.author = author,
    this.pages = pages,
    this.isRead = isRead,
    this.info = function(){
    	return `${this.title} escrito por ${this.author}, tiene ${this.pages} paginas, ${isRead ? "Ya lo has leido" : "No lo has leido"}`}
} 


const hobbit = new Libro("The Hobbit", "J.R.R. Tolkien", 295, true)

console.log(hobbit.info())

// The Hobbit escrito por J.R.R. Tolkien, tiene 295 paginas, Ya lo has leido
```

