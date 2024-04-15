Java contiene dos categorías generales de tipos de datos integrados: orientados a objetos y no orientados a objetos. Los tipos orientados a objetos de Java están definidos por clases (el análisis de las clases se postergará para después). Sin embargo, en el corazón de Java hay ocho tipos de datos primitivos (también llamados elementales o simples), que se muestran en la tabla 2.1. El término primitivo se usa aquí para indicar que estos tipos no son objetos en el sentido de que están orientados a objetos, sino más bien valores binarios normales. Estos tipos primitivos no son objetos en cuanto a la eficiencia. Todos los otros tipos de datos de Java están construidos a partir de estos tipos primitivos. 

Java especifica estrictamente un rango y un comportamiento para cada tipo primitivo, lo cual todas las implementaciones de la máquina virtual de Java deben soportar. Por ejemplo, un int es lo mismo en todos entornos de ejecución. Esto permite que los programas sean completamente portables. No es necesario reescribir un código para adecuarlo a una plataforma. Aunque la especificación estricta del tamaño de los tipos primitivos puede causar una pequeña pérdida de desempeño en algunos entornos, resulta necesaria para lograr la portabilidad.

| Tipo    | Significado |
| ------- | ----------- |
| Boolean | Representa valores verdaderos/falsos            |
| byte    | Entero de 8 bits            |
| char    |  Carácter           |
| double  |  Punto flotante de doble precisión           |
| float   |  Punto flotante de precisión sencilla           |
| int     |  Entero           |
| long    |   Entero largo          |
| short        |  Entero corto           |

- [[Enteros]]
- [[Punto flotante]]
- [[Caracteres]]
- [[Java/Tipos de datos/Boolean]]
- [[Literales]]