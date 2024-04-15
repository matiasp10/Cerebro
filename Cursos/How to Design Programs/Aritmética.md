A modo de recordatorio, he aquí una **expresión primitiva**:

```sml
(+ 1 2)
```

Utiliza **+**, la operación para sumar dos números, seguida de dos argumentos, que son números planos. Pero he aquí otro ejemplo:

```sml
(+ 1 (+ 1 (+ 1 1) 2) 3 4 5)
```

Este segundo ejemplo aprovecha dos puntos de la descripción anterior que son susceptibles de interpretación. En primer lugar, las operaciones primitivas pueden consumir más de dos argumentos. En segundo lugar, los argumentos no tienen por qué ser números en sí; también pueden ser expresiones.
La evaluación de expresiones también es sencilla. En primer lugar, BSL evalúa todos los argumentos de una operación primitiva. En segundo lugar, "alimenta" los datos resultantes a la operación, que produce un resultado. Así,

```sml
(+ 1 2)
==
3
```

> [!attention] 
> Usamos == para decir **"es igual a"** según las leyes del cálculo.

```sml
(+ 1 (+ 1 (+ 1 1) 2) 3 (+ 2 2) 5)
==
(+ 1 (+ 1 2 2) 3 4 5)
==
(+ 1 5 3 4 5)
==
18
```

Es fundamental que un programador comprenda cómo calcula el lenguaje que utiliza. Si no es así, existe el riesgo de que los programas realicen cálculos incorrectos que puedan afectar a las personas que los utilizan.

Se presentan cuatro formas de datos atómicos en BSL:

- **Números:** Enteros, decimales, etc.
- **Cadenas:** Secuencias de caracteres, como texto.
- **Imágenes:** Representaciones visuales.
- **Valores booleanos:** Verdadero o falso.

## Analogía con la física

La palabra "atómico" se usa por analogía con la física. Al igual que los átomos son las unidades básicas de la materia, las formas de datos atómicas son las unidades básicas de información en BSL.

## Operaciones primitivas

No se puede acceder al contenido interno de las formas de datos atómicas, pero existen funciones que permiten combinarlas, obtener propiedades de ellas y realizar otras operaciones. Estas funciones se denominan operaciones primitivas u operaciones predefinidas.