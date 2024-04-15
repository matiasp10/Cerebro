Vamos a introducir el concepto de sustitución e ilustrar su aplicación en el razonamiento con igualdades y asignaciones en los lenguajes de programación. También introducimos la definición de Leibniz de igualdad y la formalizaremos en términos de la sustitución, además damos un formato de demostración que nos permitirá probar la igualdad entre dos expresiones
___
En la vida cotidiana es corriente considerar colecciones de objetos o conjunto de objetos, como por ejemplo el conjunto de alumnos que están inscriptos en el primer año de esta facultad, el conjunto de líneas de colectivo que cubren el tramo Rosario–San Lorenzo, etc. En Informática llamaremos **conjunto** a _cualquier colección de objetos que compartan ciertas características_, y un **elemento de un conjunto** es _cualquiera de sus objetos_. En particular consideraremos ciertos conjuntos de números que tienen una importancia especial.

- El conjunto $N = \{0, 1, 2, 3, . . .\}$ al que llamaremos **conjunto de los números naturales**.
- El conjunto $Z = \{. . . , −3, −2, −1, 0, 1, 2, 3, . . .\}$ es el **conjunto de los números enteros**.
- El conjunto $Z += \{1, 2, 3, . . .\}$ es el **conjunto de los números enteros positivos**.
- El conjunto $Z −= \{−1, −2, −3, . . .\}$ es el **conjunto de los números enteros negativos**.

Una forma muy usual de definir conjuntos es **establecer las propiedades que deben satisfacer sus elementos**. Por ejemplo, mediante la frase: “_Sea A el conjunto de todos los números enteros mayores que −1 y menores que 100_”; estamos señalando a todos los elementos del conjunto A, una lista exhaustiva de ellos es también una definición del conjunto pero no es necesario explicar que sería extensa y tediosa, por ello es que en matemática es común recurrir a la siguiente definición:
$$
A = \{x ∈ Z : −1 < x < 100\}
$$
aquí, mediante x estamos representando a cualquier número que cumpla con la propiedad de ser entero, mayor que $−1$ y menor que $100$. Claramente cualquier número que satisfaga esta propiedad pertenecerá a $A$ y con la letra $x$ estamos simbolizando a cualquiera de las posibilidades. Cuando se utiliza de esta forma, $x$ recibe el nombre de variable, puesto que su valor puede variar entre diversas alternativas posibles, 100 para ser precisos en el caso de nuestro ejemplo. 

Una de las nociones fundamentales en Informática es el concepto de variable. Una **variable** es un mecanismo de notación que se toma prestado de la matemática que aporta concisión y precisión cuando es necesario representar ideas complejas, en resumen podemos decir que: _Una variable es un símbolo que se asocia a cualquier elemento de un conjunto predefinido_. 
Las expresiones aritméticas son muy utilizadas en la matemática básica que se enseña en la escuela secundaria, por lo tanto consideraremos cierta familiaridad con ellas. Con frecuencia aparecen variables en las expresiones aritméticas, como por ejemplo:
$$(−5) · (3 + x)\ O \ (4 + x) /2.$$
A continuación presentamos una definición axiomática de expresión aritmética:

> [!definition] Expresiones aritméticas
> %% label: expresiones-aritmticas %%
> 1. Una constante es una expresión aritmética. 
> 2. Una variable es una expresión aritmética. 
> 3. Si E es una expresión aritmética, (E) también es una expresión aritmética. 
> 4. Si E es una expresión aritmética, −E también es una expresión aritmética. 
> 5. Si E y F son expresiones aritméticas, (E + F), (E − F), (E · F) y (E/F) también son expresiones aritméticas

A partir de esta definición sólo son **expresiones aritméticas** _aquellas construidas utilizando las reglas anteriores_. Es decir, hemos establecido la sintaxis de las expresiones aritméticas, con el término sintaxis nos estamos refiriendo a las leyes o reglas que aseguran que una determinada sucesión de símbolos pertenece a una determinada clase o tiene cierta estructura. Por lo tanto para reconocer si estamos frente a una expresión aritmética debemos analizar si tal sucesión de símbolos aritméticos puede construirse siguiendo las reglas.

> [!example] ¿Es $((3 + x) · 2)$ una expresión aritmética?
> %% label: es---x---una-expresin-aritmtica %%
> Para contestar esta pregunta, comenzamos observando que por la regla 1, el número 3 es una expresión aritmética y por la regla 2, también lo es x. Ahora usando la regla 5, sigue que $(3+x)$ es una expresión aritmética y otra vez la regla 5 y la regla 1 nos garantizan que $((3 + x) · 2)$ **es una expresión aritmética**.

> [!example] ¿Es $(·2)$ una expresión aritmética?
> %% label: es--una-expresin-aritmtica %%
> La regla 1 nos dice que 2 es una expresión aritmética, pero de acuerdo a la regla 5 el símbolo $·$ correspondiente a la multiplicación es un operador binario, es decir necesita dos operandos, aquí sólo tenemos uno. Observemos además que la única expresión que puede construirse usando un operando es mediante el símbolo $−$ que corresponde al operador unario de la negación. Concluimos que la expresión $(·2)$ **no es una expresión aritmética**.

> [!tip] **Precedencia**
> Los paréntesis en las expresiones aritméticas se utilizan en general para indicar qué operaciones preceden a otras. En matemática existen reglas que permiten quitar paréntesis en las expresiones sin dar lugar a interpretaciones ambiguas, esta reglas establecen una jerarquía entre las operaciones que tienen como objetivo abreviar la escritura y que adoptaremos para las expresiones aritméticas. Por ejemplo $7 · 5 + 3$ es la misma expresión que $(7 · 5) + 3$, es decir la operación producto · tiene mayor precedencia que la suma +.

**Evaluar** una expresión aritmética _consiste en realizar las operaciones que se indican sobre los operandos que en ella aparecen_, está claro en el caso en que sólo existan constantes como operandos, pero como ya mencionamos anteriormente una expresión puede contener variables, en este caso evaluar una expresión requiere conocer que valores deben considerarse para esas variables, para esto introducimos el concepto de **estado**.

> [!definition] Sea E una expresión aritmética, y sean las variables $x1, x2, . . . , xn$ en E. Un estado de estas variables es una lista de ellas con sus valores asociados.
> %% label: sea-e-una-expresin-aritmtica-y-sean-las-variables-x1-x-----xn-en-e-un-estado-de-estas-variables-es-una-lista-de-ellas-con-sus-valores-asociados %%
> Por ejemplo, en el estado $(x, 5)$,$(y, 6)$ la variable x está asociada al valor 5 y la variable y está asociada al valor 6. Ahora entonces podemos definir qué entendemos por evaluar una expresión E en un estado.

> [!definition] Dada una expresión E y un estado de las variables de E, evaluar a E en ese estado significa calcular el valor que se obtiene al realizar las operaciones de E sobre los valores asociados a las variables
> %% label: dada-una-expresin-e-y-un-estado-de-las-variables-de-e-evaluar-a-e-en-ese-estado-significa-calcular-el-valor-que-se-obtiene-al-realizar-las-operaciones-de-e-sobre-los-valores-asociados-a-las-variables %%
> Si $E = x · 5 + y$ y el estado es $(x, 8)$,$(y, 2)$, la evaluación de la expresión en este estado da como resultado el número $42$.

[[Sustitución]]