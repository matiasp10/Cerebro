Como tal vez ya lo sabe, en programación a veces resulta más fácil usar un sistema numérico basado en 8 o 16 en lugar de 10. Al sistema numérico basado en 8 se le llama octal y usa del dígito 0 al 7. En octal, el número 10 es el mismo que el 8 en decimal. Al sistema numérico de base 16 se le llama hexadecimal y usa del dígito 0 al 9 y de las letras A a la F, que representan 10, 11, 12, 13, 14 y 15. Por ejemplo, el número hexadecimal 10 es 16 en decimal. Debido a la frecuencia con que se usan estos dos sistemas numéricos, Java le permite especificar constantes de entero en hexadecimal u octal en lugar de decimal. Una constante hexadecimal debe empezar con 0x (un cero seguido por una x). Una constante octal empieza con un cero. He aquí algunos ejemplos:

```java
hex = 0xFF; // 255 en decimal
oct = 011; // 9 en decimal
```