Java define cuatro tipos de enteros: <mark style="background: #FFB86CA6;">byte, short, int y long. </mark>A continuación se muestran:

| Tipo  | Ancho en bits | Rango                          |
| ----- | ------------- | ------------------------------ |
| byte  | 8             | -128 a 127                     |
| short | 16            | -32,768 a 32,767               |
| int   | 32            | -2,147,483,648 a 2,147,483,647 |
| long  | 64            | −9,223,372,036,854,775,808 a 9,223,372,036,854,775,807                               |

Como se muestra en la tabla, todos los tipos de enteros tienen valores de signo positivo y negativo. **Java no soporta enteros sin signo** (sólo positivos). Muchos otros lenguajes de cómputo soportan enteros con signo y sin signo. Sin embargo, los diseñadores de Java sintieron que los enteros sin signo eran innecesarios.

> Técnicamente, el sistema en tiempo de ejecución de Java puede usar cualquier tamaño que quiera para almacenar un tipo primitivo. Sin embargo, en todos los casos, los tipos deben actuar como está especificado.

El tipo de entero más usado es **int**. Las variables de tipo **int** suelen emplearse para _bucles de control, para indicar matrices y para realizar operaciones matemáticas de propósito general_. Cuando necesite un entero que tenga un rango mayor que **int**, use **long**.

El tipo de entero más pequeño es el **byte**. Las variables del tipo byte resultan especialmente útiles _cuando se trabaja con datos binarios_ que tal vez no sean compatibles directamente con otros tipos integrados de Java. 

El tipo **short** crea un entero corto que tiene primero su byte de orden mayor (al que se le llama big-endian).