Una expresión es la combinación de variables, constantes, operadores, funciones y reglas. Se clasifican en: 

- **Aritméticas**: de tipo numérico
- **Relacionales**: de tipo lógico
- **Lógicas**: de tipo lógico
- **De carácter**: de tipo carácter
### Expresiones aritméticas 

Las expresiones aritméticas son análogas a las que se utilizan en el álgebra. Estas son:

- + (Suma)
- - (Resta)
- * (Multiplicación)
- / (División)
- ^ (Exponenciación)
- div (División entera)
- mod (modulo (Resto de una división entera))

Las reglas de precedencia o prioridad son: 

1) Evaluar primero las expresiones encerradas entre paréntesis. 
2) Las operaciones aritméticas obedecen el siguiente orden de prioridad: 

- Operador exponencial. 
- Operadores de producto y división. 
- Operadores div y mod. 
- Operadores suma y resta.
### Expresiones lógicas

Las expresiones lógicas o booleanas son aquellas cuyo resultado es de tipo lógico, es decir, verdadero o falso. Una expresión lógica se puede formar mediante la combinación de variables o constantes lógicas, operadores lógicos, operadores relacionales u otras expresiones lógicas como llamadas a funciones que retornen un valor lógico.

Los operadores lógicos son:

- **Conjunción** (AND - Y - &).
- **Disyunción** (OR - O - |).
- **Negación** (NOT - NO - !).

Los operadores relacionales (o de comparación) son: 

- = igual que 
- < menor que 
- > mayor que 
- <= menor o igual que 
- = mayor o igual que 
- <> distinto de 

Los operadores relacionales son binarios, ya que necesitan dos operandos para cumplir su función.
### Operación de asignación 

La operación de asignación es utilizada para almacenar/asignar un valor a una variable. La operación de asignación se representa con el símbolo = o <--.

Variable <-- Expresión

La operación A <-- 10, significa que el valor representado por el número entero 10 es asignado a la variable A. 
Los operadores de asignaciones pueden ser de los siguientes tipos:
#### Asignación aritmética

- A <-- 6 + 7 
- B <-- A + B 
- producto <-- con1 * con2 
#### Asignacion logica

- A <-- 5 < 7 
- B <-- A | (3 <> 3) 
- P <-- 10 < 2

Las variables A, B y P tienen los valores verdadero, verdadero y falso, respectivamente.
#### Asignación de caracteres/cadenas

- X <-- "Hola"

Se asigna la cadena de caracteres hola a la variable X de tipo cadena.
### Operación de entrada/salida

Las operaciones de entrada permiten ingresar valores mediante dispositivos de entrada de datos. Se conoce también como operación de lectura.

También los algoritmos de un programa pueden enviar valores a dispositivos de salida de información. Se denominan también operaciones de escritura.

También se pueden utilizar las palabras claves ingresar, en lugar de leer, y mostrar, en lugar de escribir.

Se representan como:

- **leer** (lista de variables de entrada separadas por coma) 
- **escribir** (lista de variables de salida separadas por coma)