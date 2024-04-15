Son llamados tipos de datos primitivos porque solo pueden contener una cosa.

- [[Programación Web/JavaScript/Tipos de datos/String]]
- [[Number]]
- [[Programación Web/JavaScript/Tipos de datos/Boolean|Booleanos]]
- [[Null]]
- [[Symbol]]
- [[Undefined]]
- [[BigInt]]

# Métodos de tipos primitivos

JavaScript nos permite trabajar con tipos de datos primitivos (string, number, etc.) como si fueran objetos. Los primitivos también ofrecen métodos que podemos llamar.

Los tipos null y undefined no poseen métodos.

## Primitivos como objetos

Aquí el dilema que enfrentó el creador de JavaScript:

- Hay muchas cosas que uno querría hacer con los tipos primitivos, como un string o un number. Sería grandioso accederlas usando _métodos_.
- Los Primitivos deben ser tan _rápidos_ y _livianos_ como sea posible.

La solución es algo enrevesada, pero aquí está:

1. Los primitivos _son aún primitivos_. Con un valor único, como es deseable.
2. El lenguaje permite el acceso a _métodos_ y _propiedades_ de strings, numbers, booleans y symbols.
3. Para que esto funcione, se crea una envoltura especial, un “**object wrapper**” (objeto envoltorio) que provee la funcionalidad extra y luego es destruido.

Los “**object wrappers**” son diferentes para cada primitivo y son llamados: `String`, [[Number()|Number]], `Boolean`, `Symbol` y `BigInt`. Así, proveen diferentes sets de métodos.

> [!example]- Ejemplo
> ```js
> let str = "Hello"; 
> alert( str.toUpperCase() ); // HELLO
> ``` 
> Lo que ocurre es lo siguiente:
> 1. El string str es primitivo. Al momento de acceder a su propiedad, un objeto especial es creado, uno que conoce el valor del string y tiene métodos útiles como toUpperCase().
> 2. Ese método se ejecuta y devuelve un nuevo string (mostrado con alert).
> 3. El objeto especial es destruido, dejando solo el primitivo str.



