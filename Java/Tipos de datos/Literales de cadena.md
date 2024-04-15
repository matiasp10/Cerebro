Java soporta otro tipo de literal: la cadena. Una cadena es un conjunto de caracteres encerrados entre comillas dobles. 

Por ejemplo: 

```java
“esto es una prueba”
```

| Secuencia de escape                                              | Descripcion                                        |
| ---------------------------------------------------------------- | -------------------------------------------------- |
| \’                      | Comilla sencilla                                   |
| \”                                                               | Comillas dobles                                    |
| \\                                                               | Diagonal invertida                                 |
| \r                                                               | Retorno de carro                                   |
| \n                                                               | Nueva línea                                        |
| \f                                                               | Avanzar línea                                      |
| \t                                                               | Tabulador horizontal                               |
| \b                                                               | Retroceso                                          |
| \ddd                                                             | Constante octal (donde ddd es una constante octal) |
| \uxxxx                                                           | Constante hexadecimal (donde xxxx es una constante hexadecimal)                             |

es una cadena. 

Usted ha visto ejemplos de cadenas en muchas instrucciones ``println( )`` en los programas anteriores de ejemplo. 

Además de los caracteres normales, una literal de cadena también puede contener una o más de las secuencias de escape que se han descrito. Por ejemplo, tome en cuenta el siguiente programa: éste utiliza las secuencias de escape ``\n`` y ``\t.``