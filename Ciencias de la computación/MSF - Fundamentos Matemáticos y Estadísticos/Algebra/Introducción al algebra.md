# Conjuntos

Un conjunto es una colección de objetos, llamados elementos, que tiene la propiedad que dado un objeto cualquiera, se puede decidir si ese objeto es un elemento del conjunto o no.

Ejemplos:

  - A = {1, 2, 3}, B = {△, ◻}, C = {1, {1}, {2, 3}}
  - ℕ = {1, 2, 3, 4, . . . } el conjunto de los números naturales.
  - ℤ = {. . . , −2, −1, 0, 1, 2, . . . } el conjunto de los números enteros.
  - ℚ = {a/b; a ∈ ℤ, b ∈ ℕ} el conjunto de los números racionales.
  - ℝ el conjunto de los números reales, ℂ el conjunto de los números complejos.
  - ∅ o { } el conjunto vacío.

```ad-note
title: Observacion
collapse:
El orden de los elementos no importa en un conjunto, y en un conjunto no se tiene en cuenta repeticiones de elementos.

Se dice que cada elemento a de un conjunto A pertenece al conjunto A, y se nota a ∈ A. Si un objeto b no pertenece al conjunto A, se nota b ∉ A.
```

Ejemplos:

- Sea A = {1, 2, 3}: 1 ∈ A, 2 ∈ A, 4 ∉ A, {1, 2} ∉ A, ∅ ∉ A.
- Sea B = {2, {1}, {2, 3}}: {1} ∈ B, {2, 3} ∈ B, 1 ∉ B, 3 ∉ B.

Para notar los conjuntos se suele reservar letras mayúsculas: A, B, ... , X, Y , ... , U, V , ...

Definición: (Cardinal de un conjunto.) Sea A un conjunto, se llama cardinal de A a la cantidad de elementos distintos que tiene A, y se nota #A. Cuando el conjunto no tiene un numero finito de elementos, se dice que es infinito, y se nota #A = ∞.

Ejemplos:

`#∅ = 0, #{a, b, c} = 3 = #{1, 2, 3}, #ℕ = ∞.`

Notar que si A es un conjunto finito, `#A ∈ N ∪ {0} =: N0`.

Las definiciones comunes de un conjunto son por extensión (listando todos los elementos del conjunto entre las llaves `{` y `}`, cuando es posible hacerlo, o sea cuando el conjunto es finito) y por comprensión (a través de una propiedad que describe los elementos del conjunto, pero usualmente para eso se necesita la noción de subconjunto porque hay que dar un conjunto referencial, de donde se eligen los elementos). También presentamos en forma informal los conjuntos infinitos ℕ y ℤ usando los puntos suspensivos ... , aunque esto no es muy riguroso: se puede dar una definición formal del conjunto ℕ sin usar ... , y a partir de ello definir ℤ y ℚ. El conjunto ℝ se supone “conocido”, aunque para el también se puede dar una construcción rigurosa, y a través de ℝ se puede definir ℂ fácilmente.

Los conjuntos se suelen representar gráficamente por los llamados diagramas de Venn (por el lógico y filosofo británico John Archibald Venn, 1834–1923), que son simplemente de la forma:

<img
  src="https://support.content.office.net/es-es/media/97a3d11c-7c48-4912-a11a-815c8cd220b5.png"
  alt="diagrama de venn"
/>

```ad-abstract
title: Definición
(Subconjuntos e Inclusion.) Sea A un conjunto. Se dice que un conjunto
B esta contenido en A, y se nota B ⊆ A (o tambien B ⊂ A), si todo elemento de B es un elemento
de A. En ese caso decimos tambien que b esta incluido en A, o que B es un subconjunto de A.
Si B no es un subconjunto de A se nota B ̸⊆ A (o B ̸⊂ A).
```

```ad-example
title: Ejemplos
collapse:
- Sea A = {1, 2, 3}: {1} ⊆ A, {2, 3} ⊆ A, ∅ ⊆ A, A ⊆ A, {3, 4} ̸⊆ A.
- ℕ ⊆ ℤ ⊆ ℚ ⊆ ℝ ⊆ ℂ.
- A ⊆ A y ∅ ⊆ A cualquiera sea el conjunto A.
```

O sea, B esta incluido en A si para todo b, se tiene que si b pertenece a B entonces b pertenece a A, y B no esta incluido en A si existe b perteneciendo a B tal que b no pertenece a A.

Matemáticamente se escribe:

$$\large B ⊆ A si ∀ b, b ∈ B ⇒ b ∈ A , B ̸⊆ A si ∃ b ∈ B : b ̸∈ A$$

Aquí el símbolo “∀” significa “para todo”: la construcción “∀ b, . . . ”se lee “para todo b, se tiene
... ”, y el símbolo “∃” significa “existe”: la construcción “∃ b ∈ B : ... ”se lee “existe b en B
tal que ... ”. El símbolo “⇒” significa “implica”: la construcción “b ∈ B ⇒ b ∈ A” se lee “b en
B implica b en A”, o también “si b en B, entonces b en A” (significa que si ocurre lo primero,
entonces obligatoriamente tiene que ocurrir lo segundo).

Ejemplos de conjuntos dados por comprensión:

- A = {x ∈ ℝ : x ≥ −2}, B = {k ∈ ℤ : k ≥ −2}.
- P = {n ∈ ℕ : n es par}, I = {k ∈ ℤ : k es impar}.

Representación de Venn de B ⊆ A:

<img src="https://i.imgur.com/d0exH2s.png" alt="Representacion de Venn" />

```ad-note
title: Observacion (Igualdad de conjuntos.)
collapse:
A = B ⇐⇒ A ⊆ B y B ⊆ A.

Es decir A = B si tienen exactamente los mismos elementos (sin importar el orden y sin tener en cuenta repeticiones de elementos). (Aqui, el simbolo “⇔” es el simbolo de la bi-implicacion, que se lee “si y s´olo si”.)
```

```ad-note
title: Observacion (Combinatoria, o el arte de contar.)
collapse:
Sea A es un conjunto finito y sea B ⊆ A. Entonces #B ≤ #A. (Esto vale tambien para conjuntos infinitos)
```

Ejemplo 1.1.7. (Conjunto de partes.)

Sea A un conjunto. El conjunto de partes de A, que se nota P(A), es el conjunto formado por todos los subconjuntos de A, o sea el conjunto cuyos elementos son los subconjuntos de A. Es decir

`P(A) = {B : B ⊆ A} o tambien B ∈ P(A) ⇐⇒ B ⊆ A.`

Ejemplos:


- Sea A = {1, 2, 3}: P(A) = {∅, {1}, {2}, {3}, {1, 2}, {1, 3}, {2, 3}, A}.
- Cualquiera sea el conjunto A, ∅ ∈ P(A), A ∈ P(A).
- P(∅) = {∅}, o sea el conjunto que tiene como único elemento al conjunto vacío.

## Operaciones entre conjuntos

Supondremos en todo lo que sigue que los conjuntos A, B, C, ... que se consideran son subconjuntos de un mismo conjunto referencial (o de referencia) U (para poder “operar”). Esto también es generalmente indispensable al definir un conjunto por comprensión, como por ejemplo `P = {n ∈ ℕ : n es un numero par }`, o `I = {x ∈ ℝ : x ≤ 2} = [−∞, 2)`, que no es lo mismo que `J = {x ∈ ℕ : x ≤ 2} = {1, 2}`.

### Complemento

Sea A subconjunto de un conjunto referencial U. El complemento de A (en U) es el conjunto A′ de los elementos de U que no pertenecen a A. Es decir

`A′ = {b ∈ U : b /∈ A}, o tambien ∀ b ∈ U, b ∈ A′ ⇐⇒ b /∈ A.`

Ejemplos:

- Si U = {1, 2, 3} y A = {2}, entonces A′ = {1, 3}.
- Si U = ℕ y A = {2}, entonces A′ = {n ∈ ℕ, n ̸= 2}. O sea el complemento de un conjunto depende del conjunto referencial U.
- Si U = ℕ y P = {n ∈ ℕ : n es un numero par }, entonces P′ = {n ∈ ℕ :n es un numero impar }.
- Se tiene ∅′ = U y U′ = ∅.
- (A′)′ = A.

Representación de Venn del complemento:

<img
  src="https://i.imgur.com/fIyEuBj.png"
  alt="Diagrama de venn del complemento"
/>

Tabla de verdad:

| A   | A'  |
| --- | --- |
| V   | F   |
| F   | V    |
### Unión:

Sean A, B subconjuntos de un conjunto referencial U. La unión de A y B es el conjunto A ∪ B de los elementos de U que pertenecen a A o a B. Es decir

$A ∪ B = {c ∈ U : c ∈ A y c ∈ B}$, o tambien $∀ c ∈ U, c ∈ A ∪ B ⇐⇒ c ∈ A o c ∈ B.$

Notemos que este “o” involucrado en la definición de la unión es no excluyente, es decir si un elemento esta en A y en B, esta en la unión por estar en al menos alguno de los dos.

Ejemplos:

- Si $A = {1, 2, 3, 5, 8}$ y $B = {3, 4, 5, 10} ⊆ U = {1, . . . , 10}$, entonces $A ∪ B = {1, 2, 3, 4, 5, 8, 10}$.
- $Si I = {x ∈ ℝ : x ≤ 2} = (−∞, 2] y J = {x ∈ ℝ : −10 ≤ x < 10} = [−10, 10) ⊆ U = ℝ$, entonces $I ∪ J = {x ∈ ℝ : x < 10} = (−∞, 10)$.
- Cualesquiera sean $A$ y $B$, se tiene $A ∪ B = B ∪ A$ (conmutatividad), $A ∪ ∅ = A$, $A ∪ U = U$, $A ∪ A′ = U$. Probemos por ejemplo la afirmación $A ∪ A′ = U$: Hay que probar las dos inclusiones $A ∪ A′ ⊆ U$ y $U ⊆ A ∪ A′$. $A ∪ A′ ⊆ U$: Sea $a ∈ A ∪ A′$ ; si $a ∈ A$ entonces $a ∈ U$ pues $A ⊆ U$, y si $a ∈ A′$, entonces $a ∈ U$ pues $A′ ⊆ U$; por lo tanto $A ∪ A′ ⊆ U$. $U ⊆ A ∪ A′$: Sea $a ∈ U$; entonces $a ∈ A$ o $a /∈ A$. Si $a ∈ A$, entonces $a ∈ A ∪ A′$, y si $a /∈ A$, por definición $a ∈ A′$ y luego $a ∈ A ∪ A′$; por lo tanto $U ⊂ A ∪ A′$.

Representación de Venn de la unión:

<img src="https://i.imgur.com/4k3BPeY.png" alt="Diagrama de venn de la union" />

Además en la unión de conjuntos se cumple las siguientes propiedades:

<List
  items={[
    'Conmutativa: por lo tanto A ∪ B = B ∪ A',
    'Asociativa: es decir que dados tres o mas conjuntos tendremos (A ∪ B) ∪ C = A ∪ (B ∪ C)',
  ]}
/>

Tabla de verdad:

| A   | A'  | A ∪ B |
| --- | --- | ----- |
| V   | V   | V     |
| F   | V   | V     |
| V   | F   | V     |
| F   | F   | F      |

### Intersección.

Sean A, B subconjuntos de un conjunto referencial U. La intersección de A y B es el conjunto A ∩ B de los elementos de U que pertenecen tanto a A como a B. Es decir
`A ∩ B = {c ∈ U : c ∈ A y c ∈ B}, o tambien c ∈ A ∩ B ⇐⇒ c ∈ A y c ∈ B.`

Ejemplos:

- Sean A = {1, 2, 3, 5, 8}, B = {3, 4, 5, 10} ⊆ U = {1, . . . , 10}. Entonces A ∩ B = {3, 5}.
- Sean ``I = {x ∈ R : x ≤ 2} = (−∞, 2], J = {x ∈ R : −10 ≤ x < 10} = [−10, 10) ⊆ U = R.`` Entonces ``I ∩ J = {x ∈ R : −10 ≤ x ≤ 2} = [−10, 2]``.
- Cualesquiera sean A y B, se tiene A ∩ B = B ∩ A (conmutatividad), A ∩ ∅ = ∅, A ∩ U = A, A ∩ A′ = ∅. Cuando A ∩ B = ∅, se dice que A y B son conjuntos disjuntos.

Representación de Venn de la intersección:

<img
  src="https://i.imgur.com/fQSywek.png"
  alt="Diagrama de venn de la interseccion"
/>

En la intersección de conjuntos se cumple las siguientes propiedades:

- Asociativa: es decir que, R ∩ S ∩ T = (R ∩ S) ∩ T = =R ∩ (S ∩ T).
- Conmutativa: de modo tal que, R ∩ S ∩ T = R ∩ T ∩ S = T ∩ R ∩ S.
- Distributiva: La unión es distributiva con respecto a la intersección, (R ∩ S) ∪ T = (R ∪ T) ∩ (S ∪ T). La intersección de conjuntos es distributiva con respecto a la unión, (R ∪ S) ∩ T = (R ∩ T) ∪ (S ∩ T).

Tabla de verdad:

| A   | A'  | A ∩ B |
| --- | --- | ----- |
| V   | V   | V     |
| F   | V   | F     |
| V   | F   | F     |
| F   | F   | F      |

Podemos notar que a diferencia del complemento, la unión y la intersección no dependen del conjunto referencial U.
Otra forma de visualizar esas operaciones es por medio de las tablas de verdad de la lógica proposicional aplicadas a las operaciones de conjuntos: Dado un conjunto A ⊆ U, un elemento a ∈ U puede pertenecer a A o no, notaremos en la tabla siguiente el hecho que a ∈ A con una V (de Verdadero) o con un 1, y el hecho que a /∈ A con una F (de Falso) o con un 0 (abajo de la letra A). Esto describe las dos posibilidades para todos los elementos de U. Ahora bien, si tenemos dos conjuntos A, B ⊆ U, hay 4 posibilidades: estar en A y en B, no en A pero s´ı en B, en A pero no en B, y finalmente ni en A ni en B.

### Diferencia de conjuntos

Operación en la cual dos conjuntos, A y B, especifican cuales elementos de uno no están en el otro, formando un nuevo conjunto llamado diferencia. La diferencia del conjunto A y el conjunto B, se representa como: A-B. La diferencia del conjunto B y el conjunto A, se representa como: B-A. Ambas operaciones arrojan resultados distintos, cuando los conjuntos no son iguales.
En la diferencia de conjuntos se cumple las siguientes propiedades: la diferencia de conjuntos no es asociativa, y no es conmutativa.
La diferencia es distributiva con respecto a la unión: (R ∪ S) – T = (R – T) ∪ (S – T); y a la intersección de conjuntos: (R ∩ S) – T = (R – T) ∩ (S – T).

Representación de Venn de la Diferencia de conjuntos:

<img
  src="https://i.imgur.com/jU2Iobf.png"
  alt="Diagrama de venn de la Diferencia de conjuntos"
/>

### Diferencia simétrica de conjuntos.

Dados dos conjuntos A y B, su diferencia simétrica, A Δ B, es un conjunto que contiene los elementos de A y los de B, menos los que son comunes a ambos.
En la diferencia simétrica de conjuntos se cumple las siguientes propiedades:

- Asociativa: (A Δ B) Δ C = A Δ (B Δ C).
- Conmutativa: A Δ B = B Δ A.
- Distributiva respecto a la intersección: A ∩ (B Δ C) = (A ∩ B) Δ (A ∩ C).

Representación de Venn de la Diferencia simétrica de conjuntos:

<img
  src="https://i.imgur.com/auhypmR.png"
  alt="Diagrama de venn de la Diferencia simétrica de conjuntos"
/>

Tabla de verdad:

| A   | A'  | A ∩ B |
| --- | --- | ----- |
| V   | V   | V     |
| F   | V   | F     |
| V   | F   | F     |
| F   | F   | F      |

# Producto cartesiano

El nombre producto cartesiano fue puesto en honor al matemático, físico y filosofo francés Rene Descartes, 1596-1650. El plano euclídeo `ℝ² = {(x, y); x, y ∈ ℝ}` representado mediante los ejes cartesianos es el plano donde constantemente dibujamos los gráficos de las funciones.

<img
  src="https://i.imgur.com/BH4PsFN.png"
  alt="Eje de coordenadas cartesianas"
/>

Sean A, B conjuntos. El producto cartesiano de A con B, que se nota `A x B`, es el conjunto de pares ordenados
`A x B := {(a, b) : a ∈ A, b ∈ B}`.

Ejemplos:

- Sean A = {1, 2, 3}, B = {a, b}. Entonces A x B = {(1, a),(1, b),(2, a),(2, b),(3, a),(3, b)}, B x A = {(a, 1),(a, 2),(a, 3),(b, 1),(b, 2),(b, 3)} y B x B = {(a, a),(a, b),(b, a),(b, b)}.
- Si A = B = R, entonces R x R es el espacio euclideo R².
- Si A ̸= B, entonces A x B ̸= B x A.
- A x ∅ = ∅, ∅ x B = ∅.
- Sean A ⊆ U, B ⊆ V entonces A x B ⊆ U x V . Analizar si vale (A x B)′ = A′ x B′.

De la misma forma se puede definir el producto cartesiano de n conjuntos A₁, ... , Aₙ como el conjunto de n-uplas ordenadas:

`A₁ x ... x Aₙ := {(a₁, ... , aₙ) : a₁ ∈ A₁, ... , aₙ ∈ Aₙ}.`

# Particiones

El siguiente concepto nos permite hablar de «partir» un conjunto en distintos subconjuntos. En términos simples, una partición será una forma de dividir un conjunto en subconjuntos que no comparten elementos en común entre sí. Por ejemplo, considera a los números enteros. Podemos dividir el conjunto en dos particiones: el de los número pares y el de los impares. Denotemos al conjunto de los números pares como 𝑷 y al de los impares como 𝑰 entonces:

$𝑷 ⋂ 𝑰 = ∅$
$𝑷 ⋃ 𝑰 = ℤ$

Entonces podemos observar algunos puntos para definir qué es una partición:

- Cada uno de los subconjuntos que forman la partición son no vacíos. Nota que tanto 𝑷 como 𝑰 tienen al menos un elemento.
- La intersección entre cada una de los subconjuntos de la partición es vacía. Esto significa que las particiones no comparten elementos, en el ejemplo, es claro que ningún número par es impar y viceversa.
- La unión de los subconjuntos de la partición forman de nuevo el conjunto. Esto significa que todo elemento del conjunto pertenece a una única partición, en nuestro ejemplo esto significa que cualquier número entero es impar o es par, no ambos al mismo tiempo.

Estas son las tres propiedades que pediremos para definir una **partición**.

Definición. Sea X un conjunto y $F = {Xᵢ}ᵢ∈𝖿$ una colección de subconjuntos, entonces diremos que F es una partición de X si:

- Para cada $Xᵢ ∈ 𝖿, Xᵢ ≠ ∅$.
- Para $Xᵢ, Xⱼ ∈ 𝖿$ dos subconjuntos distintos, $Xᵢ ⋂ Xⱼ = ∅$.
- $⋃F = X$.

Resulta que esta definición no es al azar, pues cada relación de equivalencia induce una partición.

Proposición. Sea $∼$ una relación de equivalencia sobre un conjunto X. Entonces las distintas clases de equivalencia forman una partición.

Demostración. Denotemos a 𝑷 como el conjunto de todas las clases de equivalencia de X, es decir

$$𝑷 = {[x]: x ∈ X}$$

Ahora demostraremos que $𝑷$ es una partición. Para ello, notemos que:

1. Cada elemento de la partición $𝑷$ es distinta al vacío. Observemos que si $[x] ∈ 𝑷$ entonces existe al menos un elemento en esa clase de equivalencia, de manera explícita, `x ∈ [x]`.
2. Si `[x]`, `[y]` son dos clases distintas, entonces `[x] ⋂ [y]` es vacía. Este punto sale directamente del corolario demostrado anteriormente, pues `[x] = [y]` o `[x] ⋂ [y] ≠ ∅`.
3. `⋃𝑷 = X`. De manera clara sucede que `⋃𝑷 ⊂ X`, pues cada elemento de 𝑷 es un subconjunto de X, y la unión de subconjuntos de un conjunto siempre está contenida en el conjunto. Para demostrar que `X ⊂ ⋃𝑷`, notemos que si `x ∈ X`, entonces `x ∈ [x]` y `[x] ∈ 𝑷`, de esta manera, `x ∈ ⋃𝑷`.

De esta manera, 𝑷 es una partición.
