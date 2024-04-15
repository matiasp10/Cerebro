[[Complejidad espacial]] | [[Complejidad temporal]] 
____
![](https://i.imgur.com/oOrmEiX.png)
# ¿Qué es?

Es una forma de saber que tan eficiente es un algoritmo de manera sencilla.

La _complejidad_ del algoritmo se expresa en función del **tamaño de la entrada**, **N**.

Se examinan **sentencias propias del código** por lo cual _no importa la maquina_ que ejecute el algoritmo. 
## Reglas  

1. **Se ignoran las constantes** 

``` title:Ejemplo
3 * 0(1) => O(1)
O(n/2) => 0(n)
```

Tener una multiplicación o una división serán insignificantes en la complejidad. 

2. **Dominancia de términos** 

Siempre nos vamos a quedar con el peor caso o el mas complejo.

$$
\large O(n) < O(n^2)
$$

$$\large O(n\ log_n) < O(2^n)$$

## Complejidades
### Complejidad constante $O(1)$

No depende del tamaño de la entrada 

```js
x = x + 1 
// Asignacion complejidad = O(1)
y = 200 * 3 
// Asignacion complejidad = O(1)
console.log(y)
// funcion complejidad = O(1)
// Esta pieza de codigo todas las lineas tienen complejidad O(1) por lo tanto el peor caso es O(1)
```

### Complejidad lineal $O(n)$

Se obtiene complejidad de tiempo lineal cuando el tiempo de ejecución de un algoritmo aumenta linealmente con el tamaño de la entrada.

```js
for (let i = 0; i <= n; i++) {
    console.log(arr[i]) // O(1)
}
// En este caso como no sabemos cuantas veces va a imprimir el resultado el peor caso seria n * O(1) => O(n)
```

### Complejidad cuadrática $O(n^2)$

Cuando se realiza una iteración anidada, es decir un bucle dentro de otro bucle, la complejidad del tiempo es cuadrática, lo cual es horrible.

```js
for (let i = 0; i < arreglo.length; i++) { // O(n)
    for (let j = 0; j < arreglo.length; j++) { // O(n)
      if (i !== j && arreglo[i] === arreglo[j]) { // O(1)
        return `Encontrado en ${i} y ${j}`;
      }
    }
// El peor caso posible es n * n * O(1) => O(n2)
```

### Complejidad Logarítmica $O(log\ n)$

Esto es similar a la complejidad de tiempo lineal, excepto que el tiempo de ejecución **no depende del tamaño de la entrada sino de la mitad del tamaño de la entrada**. Cuando el tamaño de entrada disminuye en cada iteración o paso, se dice que un algoritmo tiene complejidad logarítmica.

```js
const busquedaBinaria = (arreglo, objetivo) => {
  let primerIndice = 0;
  let ultimoIndice = arreglo.length - 1;
  while (primerIndice <= ultimoIndice) {
    let medioIndice = Math.floor((primerIndice + ultimoIndice) / 2);

    if (array[medioIndice] === objetivo) {
      return medioIndice;
    }

    if (array[medioIndice] > objetivo) {
      ultimoIndice = medioIndice - 1;
    } else {
      primerIndice = medioIndice + 1;
    }
  }
  return -1;
};

let marcadores = [12, 22, 45, 67, 96];
console.log(busquedaBinaria(marcadores, 96));
```

En el código anterior, debido a que es una búsqueda binaria, _primero obtiene el índice medio de su arreglo_, lo compara con el valor objetivo y devuelve el índice medio si es igual. De lo contrario, debe verificar si el valor objetivo es mayor o menor que el valor medio para ajustar el primer y ultimo índice, reduciendo el tamaño de entrada a la mitad.

Debido a que _en cada iteración el tamaño de la entrada se reduce a la mitad_, la complejidad del tiempo es logarítmica con orden O(log n).
### Complejidad exponencial $O(2^n)$

Cuando la tasa de crecimiento se duplica con cada adición a la entrada (n), a menudo iterando a través de todos los subconjuntos de los elementos de entrada. Cada vez que una unidad de entrada aumenta en 1, el número de operaciones ejecutadas se duplica.

```js
const Fibonaccirecursivo = (n) => {
  if (n < 2) {
    return n;
  }
  return Fibonaccirecursivo(n - 1) + Fibonaccirecursivo(n - 2);
};

console.log(Fibonaccirecursivo(6)); // 8
```

El algoritmo especifica una tasa de crecimiento que se duplica cada vez que se agrega el conjunto de datos de entrada. Esto significa que la complejidad del tiempo es exponencial con orden $O (2 ^ n)$.
## Ejercicios

1. Que complejidad tiene el siguiente código:

```js
for(let i = 0; i < 10; i++){
	console.log("Hola")
}
for(let i = 1; i <= 1000; i++){
	for(let j = 0; j < 10; i++){
		console.log(arr[i][j])
	}
}
```

````ad-done
title:Solución
collapse:close 

El peor caso es $O(n2)$
$O(n)$ + $O(n^2)$ => $O(n^2)$

```javascript
for(let i = 0; i < 10; i++){ // Complejidad O(n)
	console.log("Hola")
}

for(let i = 1; i <= 1000; i++){ // Complejidad O(n)
	for(let j = 0; j < 10; i++){ // Complejidad O(n)
		console.log(arr[i][j]) // complejidad O(1)
	}
}
```
````

2. Que complejidad tiene el siguiente código:

```js
if(x === true){
	// codigo O(n)
} else {
	// codigo O(n log n)
}
```

```js
// En la notacion big O siempre se analiza el peor caso asique no importa si x siempre sera true, se analiza el peor caso
// La suma de complejidad seria O(n) + O(n log n) => O(n log n) 
```

3. Escriba una función que tome una matriz de enteros y devuelva la suma de los elementos de la matriz. ¿Cuál es la complejidad temporal de la función?
4. Escribe una función que tome una matriz de enteros y devuelva el entero más grande de la matriz. ¿Cuál es la complejidad temporal de la función?
5. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva el índice del entero objetivo en la matriz. ¿Cuál es la complejidad temporal de la función?
6. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
7. Escriba una función que tome una matriz de enteros y devuelva la matriz ordenada en orden ascendente. ¿Cuál es la complejidad temporal de la función?
8. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?
9. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
10. Escriba una función que tome una matriz de enteros y devuelva la matriz ordenada en orden ascendente. ¿Cuál es la complejidad temporal de la función?
11. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?
12. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
13. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?
14. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
15. Escriba una función que tome una matriz de enteros y devuelva la matriz ordenada en orden ascendente. ¿Cuál es la complejidad temporal de la función?
16. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?
17. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
18. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?
19. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
20. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?
21. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
22. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva el índice del entero objetivo en la matriz, o -1 si el entero objetivo no está en la matriz. ¿Cuál es la complejidad temporal de la función?
23. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
24. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva el índice del entero objetivo en la matriz, o -1 si el entero objetivo no está en la matriz. ¿Cuál es la complejidad temporal de la función?
25. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
26. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva el índice del entero objetivo en la matriz, o -1 si el entero objetivo no está en la matriz. ¿Cuál es la complejidad temporal de la función?
27. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?
