Uno de los mayores retos para un programador es **resolver problemas utilizando el algoritmo adecuado**. Si importar la cantidad de lenguajes que el programador conozca, es muy importante saber **resolver problemas lógicos de la forma correcta**.
### ¿Cuáles son los pasos para resolver un problema de programación?

Para esto vamos a seguir cinco pasos que nos ayudarán a acercarnos a la solución lo mas posible.

1. Entender el problema.
2. Explorar ejemplos concretos.
3. Descomponer el problema.
4. Solucionar/Simplificar.
5. Retroceder y refactorizar.
## I. Entender el problema
### ¿Cuáles son las preguntas que debes realizar para resolver un problema de programación?

Imaginemos que estamos participando en una entrevista y el problema no es alguno que hayamos preparado durante nuestra fase de estudio de preparación. Antes de iniciar realiza las siguientes preguntas.

1. ¿Puedo describir el problema con mis propias palabras?
2. ¿Cuáles son las entradas que involucra el problema?
3. ¿Cuáles son las salidas que retorna el problema?
4. ¿Las salidas pueden ser determinadas a partir de las entradas? (Tenemos la suficiente información para resolver el problema)
### Ejemplo del planteamiento de un problema de programación

Por ejemplo, para el siguiente problema… “Escriba una función que tome dos números y retorne la suma de estos.”

```txt
1. Describir el problema con tus propias palabras.
Realizar una suma de dos números.

2. Cuáles son las entradas que involucra el problema?
num1 y num2 (int, float?)

3. Cuáles son las salidas que retorna el problema?
int, float, ?

4. Las salidas pueden ser determinadas a partir de las entradas?
```
## II. Problemas en Concreto

Este es el segundo paso a realizar para entender el problema. El plantear problemas concretos ayuda entendiendo mejor el problema. Los ejemplos también ayudan de forma que podemos validar que el la solución al problema funciona como se espera ya que en ese punto conocemos las entradas y salidas del programa.

Esto aplica en una escala mas grande como:

- Utilizando user stories.
- Unit tests (pruebas unitarias).

Al explorar ejemplos posibles…

1. Inicia con ejemplos sencillos.
2. Avanza a ejemplos mas complejos.
3. Explora ejemplos con entradas vacías.
4. Explora ejemplos con entradas inválidas.
### 1. Inicia con ejemplos sencillos

Ejemplo… _Crea una función que tome un string y retorne el número de caracteres dentro del string_.

```js
contarCaracteres("aaaa"); // { a: 4, b: c }
contarCaracteres("hola"); // { a: 1, o: 1, l: 1, a: 1 }
```

En este primer ejemplo preguntamos si debemos indicar para los caracteres que no existen el valor igual a 0, esto simplificaría el incrementar el valor cuando este aparezca en lugar de validar si esta presente o no.
### 2. Avanza a ejemplos mas complejos

Ahora supongamos que la entrada es mas larga.

```js
contarCaracteres("mi dirección es Calle siempre viva #");
```

¿Debemos contar espacios o si los valores acentuados como la **ó** son un valor mas al contar la **o**? ¿Qué pasa con mayúsculas y minúsculas?
### 3. Explora ejemplos con entradas vacías

Al momento de explorar las entradas vacías tenemos que preguntarnos que sucede con las salidas.

```js
contarCaracteres(""); // {}
```

¿Para una entrada vacía, la salida debería ser 0, null, un objeto vacío o una excepción?
### 4. Explora ejemplos con entradas inválidas

Plantea que es lo que sucede cuando el valor de entrada es no valido.

```js
contarCaracteres(true); // ?
```

¿Si no es proporcionado un string se debe generar un error o una excepción?
## III. Descomponer el problema en partes

Antes de empezar a escribir código es recomendable descomponer el problema a resolver agregando comentarios acerca del enfoque que vamos a tomar para solucionar el problema.

Escribe los pasos que vas a tomar para solucionar el problema, solo incluyendo los componentes básicos del problema. Esto te lleva a pensar en el código antes de empezar a escribirlo y detectar problemas o malentendidos antes de que te adentres y te tengas que preocupar acerca de detalles como el uso de la sintaxis.

```js
function contarCaracteres(str) {
  // convertir a minusculas
  // construir objeto
  // recorrer cada caracter del string
    // si el caracter no es valido continuar con la siguiente iteracion
    // si el caracter no existe en el objeto, crearlo
    // incrementar
  }
  // retornar el objeto
}
```

Una de las ventajas de realizar este proceso durante una entrevista es que incluso si no logras completar la implementación, el enfoque provisto puede beneficiarte a la hora de ser evaluado, ya que describe la manera en que pretendes solucionar el problema.
## IV. Solucionar el problema

Soluciona el problema, y si es posible soluciona el problema de forma sencilla. Es decir, trata de ignorar las partes complicadas, es decir, en lugar de gastar el tiempo en las partes complicadas enfocate en la parte que puedas solucionar. Cuando termines con este ataca aquella que consideres mas complicada.

1. Encuentra la parte mas complicada.
2. Ignora esta parte de forma temporal.
3. Escribe una solución simplificada.
4. Después incorpora la parte completa.

```js
function contarCaracteres(str) {
    // convertir a minusculas
    str = str.toLowerCase();
    // construir objeto
    let salida = {};
    // recorrer cada caracter del string
    for (let i = 0; i < str.length; i++) {
        const char = str[i];
        // si el caracter no es valido continuar con la siguiente iteracion
        if (char.match(/[^a-z0-9]/)) {
            continue;
        }
        // si el caracter no existe en el objeto, crearlo
        if (salida[char] === undefined) {
            salida[char] = 0;
        }
        // incrementar
        salida[char]++;
    }
    // retornar el objeto
    return salida;
}

console.log(contarCaracteres("Hola Mundo"));
```

Salida.

```txt
{ H: 1, o: 2, l: 1, a: 1, M: 1, u: 1, n: 1, d: 1 }
```
## V. Retroceder / Refactorizar

Al refactorizar el código asegúrate de realizar las siguientes preguntas.

- ¿Es posible revisar el resultado?
- ¿Es posible obtener el resultado de una forma diferente?
- ¿Es posible entender el algoritmo con una mirada?
- ¿Es posible reutilizar el método para otro problema?
- ¿Es posible mejorar el performance de la solución propuesta?
- ¿Existen otras formas de refactorizar?
- ¿Este problema ha sido solucionado por otras personas?

> [!definition]
> En el caso del algoritmo propuesto tiene mucho valor el hacer mención a una posible ineficiencia o demanda adicional de recursos cuando se utilizan expresiones regulares en lenguajes como JavaScript.
## ¿Cómo mejorar las habilidades para resolver problemas de programación?

Ya sea en una entrevista o en un proyecto que estamos realizando, la manera de mejorar la resolución de problemas es aplicar un enfoque que implique:

- Desarrollar un plan para solucionar problemas.
- Adquirir las habilidades para usar patrones para la solución de problemas de programación.

> [!definition]
> Aun cuando se desarrolla un plan para solucionar problemas y se conocen los patrones para solucionar problemas de programación, nos llegaremos a enfrentar con múltiples escenarios en los cuales para solucionar un problema estos pasos anteriores no serán suficiente.

## ¿Cuáles son los patrones mas comunes para solucionar problemas de programación?

Algunos de los patrones mas comunes para solucionar problemas de programación son los siguientes.

- [[Frequency counter]]
- [[Multiple pointers]]
- [[Sliding window]]
- [[Divide and conquer]]
- Dynamic Programming
- Greedy Algorithms
- Backtracking

> [!definition]
> A los llamados patrones podemos considerarlos también como mecanismos de programación o blueprints.