En Java, los caracteres no son cantidades de 8 bits como en casi todos los demás lenguajes de cómputo. En cambio, Java usa Unicode. Unicode define un conjunto de caracteres que puede representar todos los caracteres encontrados en el lenguaje humano. Por lo tanto, en Java, char es un tipo de 16 bytes sin signo que tiene un rango de 0 a 65,536. El conjunto de caracteres ASCII estándar de 8 bites es un subconjunto de Unicode y va de 0 a 127. Por consiguiente, los caracteres ASCII aún son caracteres válidos de Java. Es posible asignar un valor a una variable de carácter al encerrar éste entre comillas. Por ejemplo, para asignar a la variable carácter la letra X:

```java
char ch; 
ch = ‘X’;
```

Puede dar salida a un valor char empleando la instrucción println( ). Por ejemplo, esta línea da salida al valor de ch:

```java
System.out.println(“Este es ch: “ + ch);
```

Debido a que char es un tipo de 16 bits sin signo, es posible realizar varias manipulaciones aritméticas en una variable char. Por ejemplo, considere el siguiente programa:

```java
// Las variables de carácter se manejan como enteros.
class CarAritDemo {
	 public static void main(String args[]) {
	 char ch;
	 ch = ‘X’;
	 System.out.println(“ch contiene “ + ch);
	 ch++; // incrementa ch Es posible incrementar char
	 System.out.println(“ch es ahora “ + ch);
	 ch = 90; // da a ch el valor Z A char puede asignársele un valor entero.
	 System.out.println(“ch es ahora “ + ch);
	 }
}
```

Aquí se muestra la salida generada por este programa:

```bash
ch contiene X
ch es ahora Y
ch es ahora Z
```

En el programa, a ch se la da primero el valor X. Luego se aumenta ch. El resultado es que ahora contiene Y, el siguiente carácter en la secuencia ASCII (y Unicode). Aunque char no es un tipo entero, en algunos casos puede manejarse como si lo fuera. A continuación, se le asigna a ch el valor 90, que es el valor de ASCII (y Unicode) que corresponde a la letra Z. Debido a que el conjunto de caracteres de ASCII ocupa los primeros 127 valores en el conjunto de caracteres de Unicode, todos los “viejos trucos” que ha usado con caracteres en el pasado funcionarán también en Java.