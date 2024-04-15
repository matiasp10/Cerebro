
- Tipos de datos abstractos [[SDF-Fundamental Data Structures]] FPL-Types 
	- Operaciones de diccionario (Insert, delete, find)
	- Objetos [[FPL-OOP]]
- Arrays [[SDF-Fundamentals]] [[SDF-Fundamental Data Structures]]
	- Numericos vs No-Numericos, Strings
	- Simples (Vector) vs Multidimensional (Matrix)
- Records/Structs/Tuplas
- Listas enlazadas
	- Simples vs Dobles y Lineales vs Circulares
- Stacks
- Queues y Dequeues 
- Tablas Hash / Maps
	- Resolucion de colision y complejidad
		- Probing 
		- Chaining 
		- Rehash 
- Grafos
	- Listas de adyacencia vs Representaciones Matrix
- Trees 
	- Binarios, n-arios, y arboles de busqueda
	- Balanceado
- Sets
- Algoritmos de busqueda 
	- O(n)
	- O(log2 n)
	- O(logb n)
- Algoritmos de ordenamiento
	- O(n2)
	- O(n log n)
- Algoritmos de grafos 
	- Camino mas corto
	- Arbol de expansion minimo

- Heaps y Queues de prioridad
- Alogritmos de ordenamiento
	- Clausura transitiva
	- Ordenamiento topológico
- Coincidencia 
	- Coincidencia de String eficiente
	- Correspondencia de la subsecuencia común más larga 
	- Coincidencia de expresiones regulares

- Algoritmos Crípticos
- Algoritmos Paralelos
- Algoritmos de consenso
	- Prueba de trabajo vs prueba de participación 
- Algoritmos de computación cuántica
### CS Core:

1. Abstract Data Types (See also: SDF-ADT, FPL-Types: 1)
	a. Dictionary Operations (insert, delete, find)
	b. Objects (See also: FPL-OO: 2a)
2. Arrays (See also: SDF-Fundamentals, SDF-ADT)
	a. Numeric vs. Non-numeric, Character Strings
	b. Single (Vector) vs. Multidimensional (Matrix)
3. Records/Structs/Tuples (See also: FPL-Types: 1)
4. Linked Lists (See also: SDF-ADT)
	a. Single vs. double and Linear vs. Circular
5. Stacks (See also: SDF-ADT, AL-Models)
6. Queues and Dequeues (See also: SDF-ADT)
7. Hash Tables / Maps (See also: SDF-ADT)
	a. Collision Resolution and Complexity (e.g., probing, chaining, rehash)
8. Graphs (e.g., [un]directed, [a]cyclic, [un]connected, and [un]weighted) (See also: MSF-Discrete: 7)
	a. Adjacency list vs. matrix representations
9. Trees (See also: MSF-Discrete: 7)
	a. Binary, n-ary, and search trees
	b. Balanced (e.g., AVL, Red-Black)
10. Sets (See also: MSF-Discrete 1)
11. Search Algorithms (See also: SDF-Algorithms)
	a. O(n) (e.g., linear/sequential search)
	b. O(log2 n) (e.g., binary search)
	c. O(logb n) (e.g. depth/breadth-first tree)
12. Sorting Algorithms (e.g., stable, unstable) (See also: SDF-Algorithms)
	a. O(n2) complexity (e.g., insertion, selection),
	b. O(n log n) complexity (e.g., quicksort, merge, timsort)
13. Graph Algorithms
	a. Shortest Path (e.g., Dijkstra’s, Floyd’s)
	b. Minimal spanning tree (e.g., Prim’s, Kruskal’s)
### KA Core:

14. Heaps and Priority Queues
15. Sorting Algorithms
	a. O(n log n) heapsort
	b. Pseudo O(n) complexity (e.g., bucket, counting, radix)
16. Graph Algorithms
	a. Transitive closure (e.g., Warshall’s Algorithm)
	b. Topological sort
17. Matching
	a. Efficient String Matching (e.g., Boyer-Moore, Knuth-Morris-Pratt)
	b. Longest common subsequence matching
	c. Regular expression matching
### Non Core:

18. Cryptography Algorithms (e.g., SHA-256) (See also: SE-Cryptography, MSF-Discrete: 5)
19. Parallel Algorithms (See also: PDC-Algorithms, FPL-Parallel)
20. Consensus algorithms (e.g., Blockchain) (See also: SE-Cryptography: 14)
	a. Proof of work vs. proof of stake (See also: SEP-Sustainability: 3)
21. Quantum computing algorithms (See also: AR-Quantum: 6)
	a. Oracle-based (e.g. Deutsch-Jozsa, Bernstein-Vazirani, Simn)
	b. Superpolynomial speed-up via QFT (e.g., Shor’s algorithm)
	c. Polynomial speed-up via amplitude amplification (e.g., Grover’s algorithm)
### Illustrative Learning Outcomes:
#### CS Core:

1. For each Fundamental ADT/Data Structure in this unit:
	a. Articulate its definition, properties, representation(s), and associated ADT operations,
	b. Using a real-world example, explain step-by-step how the ADT operations associated with the data structure transform it.
2. For each of the algorithmic in this unit:
	a. Use a real-world example, show step-by-step how the algorithm operates.
3. For each of the algorithmic approach in this unit:
	a. Give a prototypical example of the approach (e.g., Quicksort for Sorting)
4. Given requirements for a real-world application, create multiple design solutions using various data structures and algorithms. Subsequently, evaluate the suitability, strengths, and weaknesses of the selected approach for satisfying the requirements.
5. Explain how collision avoidance and collision resolution is handled in hash tables.
6. Discuss factors other than computational efficiency that influence the choice of algorithms, such as, programming time, maintainability, and the use of application-specific patterns in the input data.
#### KA Core:

7. Describe the heap property and the use of heaps as an implementation of a priority queue.
8. For each of the algorithms and algorithmic approaches in the KA core topics:
	a. Give a prototypical example of the algorithm,
	b. Use a real-world example, show step-by-step how the algorithm operates.