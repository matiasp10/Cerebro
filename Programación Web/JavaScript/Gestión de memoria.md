Los lenguajes de bajo nivel, como C, tienen primitivos de bajo nivel como `malloc()` y `free()` para la gestión de memoria. Por otro lado, para los valores en JavaScript se reserva memoria cuando "cosas" (objetos, strings, etc.) son creados y "automáticamente" liberados cuando ya no son utilizados. El proceso anterior es conocido como _Recolección de basura_ (garbage collection). Su forma "automática" es fuente de confusión, y da la impresión a los desarrolladores de JavaScript (y de otros lenguajes de alto nivel) de poder ignorar el proceso de gestión de memoria. Esto es erróneo.

# Ciclo de vida de memoria

Sin importar el lenguaje de programación, el ciclo de memoria es casi siempre parecido al siguiente:

1. **Reservar** la memoria necesaria.
2. **Utilizarla** (lectura, escritura).
3. **Liberar** la memoria una vez ya no es necesaria.

El primer y el segundo paso son explícitos en todos los lenguajes. El último paso es explícito en lenguajes de bajo nivel, pero es mayormente implícito en lenguajes de alto nivel como JavaScript

[[Recolector de basura]]