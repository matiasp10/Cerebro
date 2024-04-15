El objeto Map contiene pares clave-valor y recuerda el orden original de inserción de las claves. Cualquier valor (tanto objetos como valores primitivos) puede utilizarse como clave o como valor.

# Descripción

Los objetos Map son colecciones de pares clave-valor. Una clave del mapa sólo puede aparecer una vez; es única en la colección del mapa. Un objeto Map se itera por pares clave-valor: un bucle `for...of` devuelve una matriz de 2 miembros `[clave, valor]` en cada iteración. La iteración se produce en orden de inserción, que corresponde al orden en que cada par clave-valor fue insertado por primera vez en el mapa por el método `set()` (es decir, no había ya una clave con el mismo valor en el mapa cuando se llamó a set()).

La especificación exige que se implementen mapas "que, por término medio, proporcionen tiempos de acceso que sean sublineales con respecto al número de elementos de la colección". Por tanto, podría representarse internamente como una tabla hash (con consulta O(1)), un árbol de búsqueda (con consulta O(log(N))) o cualquier otra estructura de datos, siempre que la complejidad sea mejor que O(N).

## Igualdad de claves

La igualdad de valores se basa en el [[Algoritmo SameValueZero]]. (Antes se utilizaba SameValue, que trataba 0 y -0 como diferentes). Esto significa que NaN se considera igual que NaN (aunque NaN !== NaN) y todos los demás valores se consideran iguales según la semántica del operador === .

## Objetos vs Map

Object es similar a Map: ambos permiten establecer claves a valores, recuperar esos valores, eliminar claves y detectar si algo está almacenado en una clave. Por esta razón (y porque no había alternativas integradas), Object se ha utilizado históricamente como Map.

Sin embargo, hay diferencias importantes que hacen que Map sea preferible en algunos casos:

|                                     | Map                                                                                                                                              | Object                                                                                                                                                                                                                                                                                                                               |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Claves accidentales                 | Un Mapa no contiene claves por defecto. Sólo contiene lo que se introduce explícitamente en él.                                                  | Un Objeto tiene un prototipo, por lo que contiene claves por defecto que podrían colisionar con tus propias claves si no tienes cuidado. Esto puede evitarse utilizando Object.create(null), pero rara vez se hace.                                                                                                               |
| Seguridad                           | Un Mapa es seguro de usar con claves y valores proporcionados por el usuario.                                                                    | Establecer pares clave-valor proporcionados por el usuario en un objeto puede permitir a un atacante anular el prototipo del objeto, lo que puede conducir a ataques de inyección de objetos . Al igual que el problema de las claves accidentales, esto también se puede mitigar mediante el uso de un objeto de prototipo nulo. |
| Tipos claves                        | Las claves de un Mapa pueden ser cualquier valor (incluyendo funciones, objetos o cualquier primitiva).                                          | Las claves de un objeto deben ser cadenas o símbolos.                                                                                                                                                                                                                                                                             |
| Orden de claves                     | Las claves de Map se ordenan de forma sencilla y directa: Un objeto Map itera entradas, claves y valores en el orden de inserción de la entrada. | Aunque ahora las claves de un objeto ordinario están ordenadas, no siempre ha sido así, y el orden es complejo. Como resultado, es mejor no confiar en el orden de las propiedades.                                                                                                                                               |
| Tamaño                              | El número de elementos de un Mapa se obtiene fácilmente a partir de su propiedad `size`.                                                         | Determinar el número de elementos de un objeto es más indirecto y menos eficiente. Una forma común de hacerlo es a través de la longitud del array devuelto por Object.keys().                                                                                                                                                    |
| Iteración                           | Un Mapa es un iterable, por lo que puede ser iterado directamente.                                                                               | Object no implementa un protocolo de iteración, por lo que los objetos no son directamente iterables utilizando la sentencia JavaScript for...of (por defecto).                                                                                                                                                                   |
| Performance                         | Funciona mejor en situaciones en las que se añaden y eliminan con frecuencia pares clave-valor.                                                  | No está optimizado para adiciones y eliminaciones frecuentes de pares clave-valor.                                                                                                                                                                                                                                                |
| Serialización y análisis sintáctico | No hay soporte nativo para la serialización o el análisis sintáctico.                                                                            | Soporte nativo para la serialización de Object a JSON, utilizando JSON.stringify(). Soporte nativo para el análisis sintáctico de JSON a Object, utilizando JSON.parse().                                                                                                                                                         |

## Establecer las propiedades de los objetos

La configuración de las propiedades de los objetos también funciona para los objetos Map, y puede causar bastante confusión.  
  
Por lo tanto, esto parece funcionar de alguna manera:

> [!failure] 
> ```js
> const wrongMap = new Map();
> wrongMap['bla'] = 'blaa';
> wrongMap['bla2'] = 'blaaa2';
> console.log(wrongMap); // Map { bla: 'blaa', bla2: 'blaaa2' }
> ```

Pero esa forma de establecer una propiedad no interactúa con la estructura de datos del Map. Utiliza la característica del objeto genérico. El valor de 'bla' no se almacena en el Mapa para las consultas. Otras operaciones sobre los datos fallan:

> [!failure] 
> ```js
> wrongMap.has('bla')    // false
> wrongMap.delete('bla') // false
> console.log(wrongMap)  // Map { bla: 'blaa', bla2: 'blaaa2' }
> ```

El uso correcto para almacenar datos en el Mapa es a través del método set(key, value).

> [!check] 
> ```js
> const contacts = new Map()
> contacts.set('Jessie', {phone: "213-555-1234", address: "123 N 1st Ave"})
> contacts.has('Jessie') // true
> contacts.get('Hilary') // undefined
> contacts.set('Hilary', {phone: "617-555-4321", address: "321 S 2nd St"})
> contacts.get('Jessie') // {phone: "213-555-1234", address: "123 N 1st Ave"}
> contacts.delete('Raymond') // false
> contacts.delete('Jessie') // true
> console.log(contacts.size) // 1
> ```

# Constructor

[[Map()]]
