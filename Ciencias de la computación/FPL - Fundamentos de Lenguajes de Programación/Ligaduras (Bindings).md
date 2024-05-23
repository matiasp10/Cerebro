---
tags:
  - FPL
---
La **ligadura** es el concepto que describe la **asociación entre una entidad y sus atributos, o entre una operación y un símbolo**. Esta conexión es crucial para el correcto funcionamiento de los programas, ya que define cómo se interpretan y utilizan los elementos del código.

- `{java}int precio`;
- _Entidad_: **Variable**.
- _Atributos_:
	- _Nombre_: `precio`
	- _Tipo_: `entero` ← determina el comportamiento de la entidad, el rango de valores que puede tomar y las operaciones que se pueden efectuar.

La ligadura se puede establecer antes de la ejecución (Ligadura Estática) o durante la ejecución (Ligadura Dinámica).

> [!warning] Importante
> Los lenguajes de programación pueden contener y utilizar **ambos tipos de ligaduras, estática y dinámica**, en diferentes contextos y para diferentes propósitos.
> 
> De hecho, muchos lenguajes modernos combinan ambos enfoques para lograr un equilibrio entre **eficiencia, flexibilidad y seguridad**.
___
# Tiempos de ligadura

## Ligadura estática

La **ligadura estática** es un concepto fundamental en la programación que establece la **asociación entre entidades, atributos, operaciones y símbolos antes de la ejecución del programa**. Esta conexión se fija de manera permanente durante la compilación o el enlazado, lo que significa que no cambia durante la ejecución del programa.

### Características de la ligadura estática

- **Predefinición:** Las ligaduras se determinan en tiempo de compilación o enlazado, antes de que el programa se ejecute.
- **Inmutabilidad:** Las ligaduras permanecen sin alteraciones durante la ejecución del programa.
- **Eficiencia:** La ejecución del programa es más eficiente, ya que las asociaciones están predefinidas y no requieren resolución dinámica.
- **Menor flexibilidad:** Los cambios en las ligaduras implican recompilar o reenlazar el programa.

### Tipos de ligadura estática

1. **Ligadura en la definición del lenguaje:** Se establece durante el diseño del lenguaje de programación. Define las reglas básicas para la interpretación de entidades, atributos, operaciones y símbolos. Por ejemplo, el símbolo "+" siempre se asocia con la operación de suma de dos enteros.
2. **Ligadura en tiempo de implementación:** Se establece durante la implementación del lenguaje de programación. Define aspectos específicos de la ligadura, como la precedencia de operadores, los rangos de valores para tipos de datos o las reglas de memoria.
3. **Ligadura en tiempo de compilación:** Se establece durante la compilación del programa. El compilador fija las ligaduras específicas para cada variable, método, operación o símbolo utilizados en el código.

### Ejemplos de ligadura estática

- **Declaración de variable:** En la declaración `{java}int precio;`, se establece una ligadura estática entre la entidad `precio` (_variable_) y el atributo `tipo` (_entero_). El compilador fija esta asociación antes de ejecutar el programa.

```c++
int precio;
```

- **Llamada a método:** Al llamar a un método predefinido, se produce una ligadura estática entre el nombre del método y la implementación del código correspondiente. El compilador ya ha asociado el nombre del método con su implementación durante la compilación.

```C
printf("Hola, mundo!");
```

- **Operaciones sobre variables:** Al realizar operaciones como `{java}precio + 5`, se establece una ligadura estática entre la operación `+`, la variable `precio` y el valor `5`. El compilador ya ha asociado el símbolo **"+"** con la operación de suma y ha determinado el tipo de la variable `precio`.

```C++
int suma = precio + 5;
```

### Ventajas de la ligadura estática

- **Eficiencia:** La ejecución del programa es más eficiente debido a que las ligaduras están predefinidas y no requieren resolución dinámica en tiempo de ejecución.
- **Predictibilidad:** El comportamiento del programa es más predecible, ya que las ligaduras no cambian durante la ejecución.
- **Seguridad:** La ligadura estática puede ayudar a prevenir errores de tipo, ya que el compilador verifica las asociaciones antes de ejecutar el programa.

**Desventajas de la ligadura estática:**

- **Menor flexibilidad:** Los cambios en las ligaduras implican recompilar o reenlazar el programa, lo que puede ser un proceso costoso y lento.
- **Menor dinamismo:** La ligadura estática limita la capacidad del programa para adaptarse a cambios en tiempo de ejecución.

**En resumen, la ligadura estática es un mecanismo fundamental en la programación que ofrece eficiencia, predictibilidad y seguridad. Sin embargo, su menor flexibilidad y dinamismo pueden ser limitaciones en algunos casos.**

**Lenguajes que utilizan ligadura estática:**

- **C++:** Se caracteriza por su uso extensivo de ligadura estática, lo que le otorga gran eficiencia y rendimiento.
- **Java:** También utiliza ligadura estática para la mayoría de sus entidades, asegurando un alto grado de previsibilidad y seguridad en la ejecución.
- **C:** La ligadura estática es fundamental en C, ya que permite un control preciso sobre la memoria y el rendimiento del programa.

## Ligadura dinamica

La **ligadura dinámica** es un concepto fundamental en la programación que establece la **asociación entre entidades, atributos, operaciones y símbolos durante la ejecución del programa**. Esta conexión no es fija y puede modificarse conforme a ciertas reglas predefinidas por el lenguaje de programación.

```python
def intercambiar(a, b):
  temp = a
  a = b
  b = temp

lista = [10, "Hola", True]

intercambiar(lista[0], lista[2])
print(f"Lista modificada: {lista}")
```

En este ejemplo, la función `{python}intercambiar` intercambia los valores de dos variables, independientemente de su tipo. La ligadura dinámica permite que la función funcione con diferentes tipos de datos sin necesidad de versiones específicas para cada tipo.

**Características de la ligadura dinámica:**

- **Resolución en tiempo de ejecución:** Las ligaduras se determinan en tiempo real durante la ejecución del programa.
- **Mutabilidad:** Las ligaduras pueden cambiar durante la ejecución del programa.
- **Flexibilidad:** Permite mayor adaptabilidad del programa a cambios en tiempo de ejecución.
- **Costo de ejecución:** La resolución dinámica de ligaduras implica un costo adicional en la ejecución del programa.

**Tipos de ligadura dinámica:**

1. **Ligadura en el inicio de la unidad:** Se produce al ingresar a un subprograma o bloque durante la ejecución. Por ejemplo, en C y Pascal, el enlace de parámetros formales a reales y a la localidad de almacenamiento ocurre al entrar al subprograma.
2. **Ligadura en cualquier punto de ejecución:** Ciertos enlaces pueden ocurrir en cualquier momento durante la ejecución del programa. El ejemplo más típico es el enlace de variables a valores a través de la asignación (Ej., `a = 2;`).

### Ejemplos de ligadura dinámica

- **Llamada a método polimórfico:** En la programación orientada a objetos, la ligadura dinámica permite que una misma llamada a método pueda invocar diferentes implementaciones según el tipo del objeto en tiempo de ejecución.

```java
class Animal {
  public void comer() {
    System.out.println("El animal está comiendo.");
  }
}

class Perro extends Animal {
  @Override
  public void comer() {
    System.out.println("El perro está comiendo croquetas.");
  }
}

class Gato extends Animal {
  @Override
  public void comer() {
    System.out.println("El gato está comiendo atún.");
  }
}

public class EjemploPolimorfismo {
  public static void main(String[] args) {
    Animal animal = new Perro();
    animal.comer(); // Imprime: El perro está comiendo croquetas.

    animal = new Gato();
    animal.comer(); // Imprime: El gato está comiendo atún.
  }
}
```

En este ejemplo, la llamada al método `{java}comer()` se resuelve dinámicamente en tiempo de ejecución según el tipo real del objeto (`{java}Perro` o `{java}Gato`). La ligadura dinámica permite que el mismo código se comporte de manera diferente en función del contexto.

- **Procesamiento de listas de datos heterogéneos:** Un programa puede trabajar con una lista de datos de diferentes tipos, ya que las variables se ligan al tipo correcto en el momento de la asignación.

```python
def procesar_lista(lista):
  for elemento in lista:
    if isinstance(elemento, str):
      print(f"Cadena: {elemento}")
    elif isinstance(elemento, int):
      print(f"Número: {elemento}")
    else:
      print(f"Tipo desconocido: {elemento}")

lista = ["Hola", 10, True, 3.14]
procesar_lista(lista)
```

En este ejemplo, la función `{python}procesar_lista` itera sobre una lista y verifica el tipo de cada elemento en tiempo de ejecución. La ligadura dinámica permite que la función se adapte a cualquier tipo de dato presente en la lista.

- **Reflexión:** La ligadura dinámica permite inspeccionar y modificar la estructura y el comportamiento de objetos en tiempo de ejecución.

```python
class Persona:
  def __init__(self, nombre, edad):
    self.nombre = nombre
    self.edad = edad

def obtener_atributos(objeto):
  for atributo in dir(objeto):
    if not atributo.startswith("_"):
      valor = getattr(objeto, atributo)
      print(f"Atributo: {atributo}, Valor: {valor}")

persona = Persona("Juan", 30)
obtener_atributos(persona)
```

> [!info]- Reflexión
> La **reflexión** es una técnica que permite inspeccionar y modificar la estructura y el comportamiento de objetos en tiempo de ejecución.

En este ejemplo, la función `{python}obtener_atributos` utiliza la reflexión para inspeccionar los atributos de un objeto `{python}Persona`. La ligadura dinámica permite que la función acceda dinámicamente a los atributos del objeto sin necesidad de conocerlos de antemano.

### Ventajas de la ligadura dinámica

- **Flexibilidad:** Permite mayor adaptabilidad del programa a cambios en tiempo de ejecución, como la recepción de datos de diferentes tipos o la ejecución de código dinámico.
- **Dinamismo:** Facilita la implementación de características como el polimorfismo y la reflexión.
- **Programación genérica:** Permite programar con variables que pueden trabajar con cualquier tipo de datos.

### Desventajas de la ligadura dinámica

- **Costo de ejecución:** La resolución dinámica de ligaduras implica un costo adicional en la ejecución del programa.
- **Menor predictibilidad:** El comportamiento del programa puede ser menos predecible, ya que las ligaduras pueden cambiar durante la ejecución.
- **Dificultad para detectar errores:** La ligadura dinámica puede dificultar la detección de errores de tipo, ya que la verificación se realiza en tiempo de ejecución.

### Lenguajes que utilizan ligadura dinámica

- **JavaScript:** Se caracteriza por su uso extensivo de ligadura dinámica, lo que le otorga gran flexibilidad y adaptabilidad.
- **Python:** También utiliza ligadura dinámica en gran medida, permitiendo un desarrollo más rápido y dinámico.
- **Smalltalk:** Un lenguaje de programación orientado a objetos puro que utiliza ligadura dinámica para todas sus entidades.

**En resumen, la ligadura dinámica es un mecanismo fundamental en la programación que ofrece flexibilidad, dinamismo y capacidad para la programación genérica. Sin embargo, su costo de ejecución y menor predictibilidad pueden ser limitaciones en algunos casos.**

**La elección entre ligadura estática y dinámica depende de las necesidades y características del proyecto en desarrollo.** Si se prioriza la eficiencia, la predictibilidad y la seguridad, la ligadura estática puede ser una buena opción. Sin embargo, si se requiere mayor flexibilidad, dinamismo y capacidad para la programación genérica, la ligadura dinámica puede ser más adecuada.

# Ligadura estática vs ligadura dinámica 

|Característica|Ligadura Estática|Ligadura Dinámica|
|---|---|---|
|**Establecimiento**|Se fija antes de la ejecución del programa.|Se resuelve durante la ejecución del programa.|
|**Mutabilidad**|Inmutable: las ligaduras no cambian durante la ejecución.|Mutable: las ligaduras pueden cambiar durante la ejecución.|
|**Eficiencia**|Más eficiente: las ligaduras están predefinidas y no requieren resolución dinámica.|Menos eficiente: la resolución dinámica de ligaduras implica un costo adicional.|
|**Predictibilidad**|Más predecible: el comportamiento del programa es más previsible.|Menos predecible: el comportamiento del programa puede variar según las ligaduras dinámicas.|
|**Flexibilidad**|Menos flexible: los cambios en las ligaduras implican recompilar o reenlazar el programa.|Más flexible: las ligaduras pueden cambiar en tiempo de ejecución.|
|**Dinamismo**|Menos dinámico: el programa se comporta de manera predeterminada.|Más dinámico: el programa puede adaptarse a cambios en tiempo de ejecución.|
|**Detección de errores**|Mejor detección de errores de tipo en tiempo de compilación.|Menor detección de errores de tipo en tiempo de ejecución.|
|**Costos de implementación**|Costos de implementación más bajos.|Costos de implementación más altos debido al chequeo de tipo en tiempo de ejecución.|
|**Lenguajes de programación**|C++, Java, C|JavaScript, Python, Smalltalk|
|**Ejemplos**|Declaración de variables, llamadas a métodos predefinidos.|Llamadas a métodos polimórficos, procesamiento de listas heterogéneas, reflexión, programación genérica.|
___
# Declaraciones

**Las declaraciones** son una parte fundamental de la programación, ya que permiten **establecer una conexión entre entidades, nombres y tipos de datos** dentro de un programa. Esta conexión, conocida como **ligadura**, es crucial para que el compilador o intérprete pueda entender y ejecutar el código correctamente.

> [!warning] Importante
> Las _declaraciones_ son **instrucciones en el código que establecen una conexión entre una entidad, un nombre y un tipo de dato**.
> Y las _ligaduras_ son la **asociación real entre la entidad, el nombre y el tipo de dato** que se establece durante la ejecución del programa.

## Tipos de declaraciones

### Declaraciones implícitas

- **Definición:** No requieren una declaración explícita en el programa. La ligadura se establece automáticamente la primera vez que se utiliza la entidad.
- **Ventajas:**
    - Simplifican la escritura del código en algunos casos.
- **Desventajas:**
    - **Disminuyen la legibilidad del código:** Al no tener una declaración explícita, puede ser difícil comprender el tipo y propósito de una entidad a simple vista.
    - **Perjudican la fiabilidad:** Impiden al proceso de compilación detectar errores tipográficos o lógicos, ya que no se realiza una verificación previa de tipos.
    - **No permiten el control del almacenamiento:** El compilador asigna automáticamente memoria a las entidades implícitas, lo que puede ser ineficiente o no adecuado en algunos casos.

#### Ejemplos

##### Asignaciones directas

En algunos lenguajes, como Python o JavaScript, es posible asignar un valor a una variable sin necesidad de una declaración previa. La ligadura se establece automáticamente en la primera asignación.

```python
numero = 5  # Declaración implícita de la variable "numero" como entero
otroNumero = 10.5  # Declaración implícita de "otroNumero" como flotante
```

##### Argumentos de funciones

En lenguajes dinámicos, como Python, no es necesario declarar explícitamente el tipo de los argumentos de una función. El tipo se infiere a partir del valor asignado en la llamada a la función.

```python
def sumar(a, b):
  return a + b

resultado = sumar(3, 2.5)  # Argumentos implícitos: "a" como entero, "b" como flotante
```

##### Bucle for

En algunos lenguajes, la variable de iteración en un bucle `for` no requiere una declaración previa. Su tipo se infiere del elemento iterado.

```python
for numero in [1, 2, 3, 4, 5]:
  print(numero)  # Variable "numero" implícita como entero
```

### Declaraciones explícitas

- **Definición:** Requieren una instrucción específica en el código para definir la entidad, su nombre y su tipo de dato.
- **Ventajas:**
    - **Mejoran la legibilidad del código:** Al tener una declaración explícita, se aclara el tipo y propósito de cada entidad, facilitando la comprensión del programa.
    - **Aumentan la fiabilidad:** Permiten al compilador realizar una verificación de tipos en tiempo de compilación, detectando errores potenciales antes de la ejecución.
    - **Ofrecen mayor control del almacenamiento:** El programador puede especificar cómo y dónde se debe almacenar la información de la entidad, optimizando el uso de la memoria.

#### Ejemplos

##### Definición de variables

La forma más común de declaración explícita es utilizar una instrucción específica para definir la variable, su nombre y su tipo de dato.

```C
int numeroEntero = 10;  // Declaración explícita de "numeroEntero" como entero
double numeroDecimal = 3.14;  // Declaración explícita de "numeroDecimal" como flotante
```

##### Declaración de tipo de dato

En algunos lenguajes, se pueden declarar tipos de datos personalizados para agrupar características comunes de variables.

```Delphi
type TColor = (rojo, verde, azul);
var colorFondo: TColor;
```

##### Declaraciones de funciones

Las declaraciones explícitas de funciones permiten definir el nombre, los parámetros, el tipo de retorno y el cuerpo de la función.

```java
public static int sumar(int a, int b) {
  return a + b;
}
```

#### Tipos de declaraciones explícitas

- **Definiciones:** Son las declaraciones más simples y su único efecto es establecer la ligadura entre la entidad, el nombre y el tipo de dato. Ejemplos: `const pi = 3.14;` o `int a;`.
- **Secuenciales:** Permiten agrupar varias declaraciones relacionadas en un solo bloque, facilitando la organización y legibilidad del código. Por ejemplo: `type cadena = array [1..30] of char; cliente = record; nombre: cadena; saldo: real; end;`.
- **Recursivas:** Se utilizan para definir entidades que se componen a sí mismas, creando estructuras de datos jerárquicas. Árboles, colas y listas enlazadas son ejemplos comunes de estructuras recursivas.

La declaración de una **Celda** en una lista enlazada, como la que se presenta en el ejemplo, es un caso paradigmático de declaración recursiva:

```
type Celda = record
  Elemento : integer;
  Siguiente : Celda;
end;
```

## Propósitos de las declaraciones

### Selección de la representación de almacenamiento

Las declaraciones explícitas permiten al compilador elegir la mejor forma de representar la entidad en memoria, considerando su tipo de dato, tamaño y uso previsto. Esto optimiza el uso de la memoria y mejora el rendimiento del programa.

### Gestión de almacenamiento

Las declaraciones permiten al compilador gestionar la asignación y liberación de memoria de manera eficiente durante la ejecución del programa. Esto evita la fragmentación de la memoria y asegura que los recursos se utilicen de forma óptima.

### Operaciones polimórficas

En lenguajes con polimorfismo, las declaraciones permiten al compilador determinar en tiempo de compilación qué operación específica debe aplicarse a un operador homónimo, según el tipo de datos involucrados. Esto mejora la eficiencia y la flexibilidad del código.

### Verificación de tipos

Las declaraciones explícitas permiten realizar una verificación de tipos estática, antes de la ejecución del programa. El compilador analiza las declaraciones para detectar posibles errores de tipo, como asignaciones incompatibles o llamadas a métodos con argumentos incorrectos. Esto ayuda a prevenir errores en tiempo de ejecución y mejora la confiabilidad del programa.

**En resumen, las declaraciones son elementos fundamentales en la programación que permiten establecer ligaduras, controlar el almacenamiento, gestionar la memoria, posibilitar operaciones polimórficas y realizar verificaciones de tipos. Su uso correcto contribuye a la legibilidad, fiabilidad, eficiencia y seguridad del código.**

**Recuerda que la elección entre declaraciones implícitas y explícitas depende del lenguaje de programación, el estilo de codificación y las necesidades específicas del proyecto.**