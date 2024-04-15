Al ejecutar un programa los procesadores entienden únicamente lenguaje máquina. Por ello para poder ejecutar el lenguaje de alto nivel debe ser traducido al lenguaje máquina.

### Interprete 

Lee e interpreta las instrucciones de un programa fuente a medida que son encontradas y las ejecuta. A este proceso se lo llama interpretar y a los programas que lo hacen se los conoce como intérpretes.

Programa fuente --> Intérprete --> Traducción y ejecución
### Compilador

El compilador traduce el **código fuente** de un programa (lenguaje de alto nivel) en lenguaje máquina. El código que se escribe en lenguaje de alto nivel se lo denomina código fuente y el traducido selo denomina código objeto. El programa objeto que resulta luego de ejecutar la compilación no coincide con el lenguaje máquina. Por ello se utiliza un **enlazador o montador**, el cual junta el código objeto obtenido para convertirlo en lenguaje máquina y poder ser ejecutado por el procesador.

Programa fuente --> compilador --> programa objeto --> montador --> programa ejecutable en lenguaje maquina