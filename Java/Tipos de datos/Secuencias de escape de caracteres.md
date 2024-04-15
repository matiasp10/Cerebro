Encerrar constantes de carácter entre comillas sencillas funciona para con casi todos los caracteres de impresión; sin embargo, unos cuantos caracteres, como los retornos de carro, plantean un problema especial cuando se usa un editor de textos. Además, otros caracteres, como las comillas sencillas y las dobles, tienen un significado especial en Java, de modo que no puede usarlos directamente. Por estas razones, Java proporciona las _secuencias de escape especiales_ (en ocasiones denominadas constantes de carácter de diagonal invertida). Estas secuencias se usan en lugar de los caracteres que representan.

Por ejemplo, lo siguiente asigna a **ch** el carácter de tabulador:

```java
ch = ‘\t’;
```

El siguiente ejemplo asigna una comilla sencilla a **ch**:

```java
ch = ‘\’’;
```