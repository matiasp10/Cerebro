## Algoritmos y Estructuras de Datos: Conceptos Fundamentales

Los algoritmos y las estructuras de datos son fundamentales para la informática y la ingeniería de software, ya que toda computación teórica y programa del mundo real consiste en algoritmos que operan con elementos de datos que poseen una estructura subyacente. La selección de soluciones computacionales apropiadas para problemas del mundo real se beneficia de la comprensión de las capacidades teóricas y prácticas, así como las limitaciones, de los algoritmos y paradigmas disponibles, incluido su impacto en el medio ambiente y la sociedad. Además, esta comprensión proporciona una visión de la naturaleza intrínseca de la computación, los problemas computacionales y la resolución de problemas computacionales, así como posibles técnicas de solución independientes del lenguaje de programación, el paradigma de programación, el hardware informático u otros aspectos de implementación.

Esta área de conocimiento se centra en la naturaleza de la computación algorítmica, incluidos los conceptos y habilidades necesarios para diseñar y analizar algoritmos para resolver problemas computacionales del mundo real. Complementa la implementación de algoritmos y estructuras de datos que se encuentran en el área de conocimiento Fundamentos del Desarrollo de Software (SDF). Dado que los algoritmos y las estructuras de datos son esenciales en todas las áreas avanzadas de la informática, esta área proporciona los fundamentos algorítmicos que se espera que conozca todo graduado en informática. La exposición a la amplitud de estos temas fundamentales de AL está diseñada para proporcionar a los estudiantes una base para estudiar temas adicionales en computación algorítmica con mayor profundidad y para aprender algoritmos avanzados en diversas áreas de conocimiento y disciplinas.
### AL-Foundational: Foundational Data Structures and Algorithms

CS Core:
1. Tipos de datos abstractos 
	A. Operaciones de diccionario (insert, delete, find)	
	B. Objetos
2. Arrays
	1. Numeric vs Non-numeric, Character Strings
	2. Single (Vector) vs Multidimensional (Matrix)
3. Records/Structs/Tuples
4. Linked lists
	1. Single vs double and linear vs circular
5. Stacks
6. Queues y Dequeues
7. Hash Tables / Maps
	1. Collision resolution y Complejidad (ej., probing, chaining, rehash)
8. Graphs
	1. Adjacency list vs matrix representations
9. Trees
	1. Binary, n-ary, y search trees
	2. Balanced
10. Sets
11. Search Algorithms
	1. O(n) (ej,. linear/sequential search)
	2. O(log2 n) (ej binary search)
	3. O(logb n) (ej depth/breadth-first tree)
12. Sorting Algorithms
	1. O(n2) Complexity (ej insertion, selection)
	2. O(n log n) complexity (ej quicksort, merge, timsort)
13. Graph Algorithms
	1. Shortest Path (ej Dijkstra's, Floyd's)
	2. Minimal spanning tree (ej, Prim's, Kruskal's)

KA Core:

1. Heaps and Priority Queues
2. Sorting Algorithms
	a. O(n log n) heapsort
	b. Pseudo O(n) complexity (e.g., bucket, counting, radix)
3. Graph Algorithms
	a. Transitive closure (e.g., Warshall’s Algorithm)
	b. Topological sort
4. Matching
	a. Efficient String Matching (e.g., Boyer-Moore, Knuth-Morris-Pratt)
	b. Longest common subsequence matching
	c. Regular expression matching 

Non Core:
1. Cryptography Algorithms (e.g., SHA-256) (See also: SE-Cryptography, MSF-Discrete: 5)
2. Parallel Algorithms (See also: PDC-Algorithms, FPL-Parallel)
3. Consensus algorithms (e.g., Blockchain) (See also: SE-Cryptography: 14)
	a. Proof of work vs. proof of stake (See also: SEP-Sustainability: 3)
4. Quantum computing algorithms (See also: AR-Quantum: 6)
	a. Oracle-based (e.g. Deutsch-Jozsa, Bernstein-Vazirani, Simn)
	b. Superpolynomial speed-up via QFT (e.g., Shor’s algorithm)
	c. Polynomial speed-up via amplitude amplification (e.g., Grover’s algorithm) 

Illustrative Learning Outcomes:
CS Core:
1. For each Fundamental ADT/Data Structure in this unit:
	a. Articulate its definition, properties, representation(s), and associated ADT operations,
	b. Using a real-world example, explain step-by-step how the ADT operations associated
	with the data structure transform it.
2. For each of the algorithmic in this unit:
	a. Use a real-world example, show step-by-step how the algorithm operates. 
3. For each of the algorithmic approach in this unit:
	a. Give a prototypical example of the approach (e.g., Quicksort for Sorting)
4. Given requirements for a real-world application, create multiple design solutions using various data structures and algorithms. Subsequently, evaluate the suitability, strengths, and weaknesses of the selected approach for satisfying the requirements.
5. Explain how collision avoidance and collision resolution is handled in hash tables.
6. Discuss factors other than computational efficiency that influence the choice of algorithms, such as, programming time, maintainability, and the use of application-specific patterns in the input data. 

KA Core:
7. Describe the heap property and the use of heaps as an implementation of a priority queue.
8. For each of the algorithms and algorithmic approaches in the KA core topics:
	a. Give a prototypical example of the algorithm,
	b. Use a real-world example, show step-by-step how the algorithm operates. 
### AL-Strategies: Algorithmic Strategies

CS Core:
1. Paradigms
	a. Brute-Force (e.g., linear search, selection sort, traveling salesperson, knapsack)
	b. Decrease-and-Conquer
		i. By a Constant (e.g., insertion sort, topological sort),
		ii. By a Constant Factor (e.g., binary search),
		iii. By a Variable Size (e.g., Euclid’s algorithm)
	c. Divide-and-Conquer (e.g., Binary Search, Quicksort, Mergesort, Strassen’s)
	d. Greedy (e.g., Dijkstra’s, Kruskal’s)
	e. Transform-and-Conquer
		i. Instance simplification (e.g. find duplicates via list presort)
		ii. Representation change (e.g., heapsort)
		iii. Problem reduction (e.g., least-common-multiple, linear programming)
		iv. Dynamic Programming (e.g., Floyd’s)
	f. Space vs. Time Tradeoffs (e.g., hashing) (See also: AL-Fundamentals)
2. Handling Exponential Growth (e.g., heuristics, A*, branch-and-bound, backtracking)
3. Iteration vs. Recursion (e.g., factorial) (See also: MSF-Discrete: 2)

KA Core:
4. Paradiams
	a. Approximation Algorithms
	b. Iterative improvement (e.g., Ford-Fulkerson, Simplex)
	c. Randomized/Stochastic Algorithms (e.g., Max-Cut, Balls and Bins) 

Non Core:
5. Quantum computing (See also AL-Fundamentals: 8, AL-Models: 8)

Illustrative Learning Outcomes
CS Core:
1. For each of the paradigms in this unit
	a. Articulate its definitional characteristics,
	b. Give an example that demonstrates the paradigm including explaining how this example satisfies the paradigm’s characteristics
2. For each of the algorithms in the AL-Fundamentals unit:
	a. Describe the paradigm used by the algorithm and how it exemplifies this paradigm
3. Given an algorithm, describe the paradigm used by the algorithm and how it exemplifies this paradigm
4. Give a real-world problem, determine appropriate algorithmic paradigms and algorithms from these paradigms that address the problem including considering the tradeoffs among the paradigms and algorithms selected.
5. Give an example of an iterative and a recursive algorithm that solves the same problem including explaining the benefits and disadvantages of each approach.
6. Determine if a greedy approach leads to an optimal solution.
7. Explain at least one approach for addressing a computational problem whose algorithmic solution is exponential. 
### AL-Complexity: Complexity

CS Core:
1. Complexity Analysis Framework
	a. Best, average, and worst case performance of an algorithm
	b. Empirical and Relative (Order of Growth) Measurements
	c. Input Size and Primitive Operations
	d. Time and Space Efficiency
2. Asymptotic complexity analysis (average and worst case bounds)
	a. Big-O, Big-Omega, and Big-Theta formal notations
	b. Foundational complexity classes and representative examples/problems
		i. O(1) Constant (e.g., Array Access)
		ii. O(log2 n) Logarithmic (e.g., Binary Search)
		iii. O(n) Linear (e.g., Linear Search)
		iv. O(n log2 n) Log Linear (e.g., Mergesort
		v. O(n2) Quadratic (e.g., Selection Sort)
		vi. O(n3) Cubic (e.g., Gaussian Elimination)
		vii. O(2n) Exponential (e.g., Knapsack, SAT, TSP, All Subsets)
		viii. O(n!) Factorial (e.g., Hamiltonian Circuit, All Permutations)
3. Empirical measurements of performance
4. Tractability and Intractability
	a. P, NP and NP-Complete complexity classes
	b. NP-Complete problems (e.g., SAT, Knapsack, TSP)
	c. Reductions
5. Time and space trade-offs in algorithms. 

KA Core:
6. Little-o and Little-Omega notations
7. Recursive Analysis: (e.g., recurrence relations, Master theorem, substitution)
8. Amortized Analysis
9. Turing Machine-Based Models of Complexity
	a. Time complexity (See also: AL-Models)
		i. P, NP, NP-C, and EXP classes
		ii. Cook-Levin Theorem
	b. Space Complexity
		i. NSpace and PSpace
		ii. Savitch’s Theorem

Illustrative Learning Outcomes
CS Core:
1. Explain what is meant by “best”, “average”, and “worst” case behavior of an algorithm..
2. State and explain the formal definitions of Big-O, Big-Omega, and Big-Theta notations and how they are used to describe the amount of work done by an algorithm.
3. Compare and contrast each of the foundational complexity classes listed in this unit.
4. For each foundational complexity class in this unit:
	a. Give an algorithm that demonstrates the associated runtime complexity.
5. For each algorithm in the AL-Fundamentals unit:
	a. Give its runtime complexity class and explain why it belongs to this class.
6. Determine informally the foundational complexity class of simple algorithms.
7. Perform empirical studies to determine and validate hypotheses about the runtime complexity of various algorithms by running algorithms on input of various sizes and comparing actual performance to the theoretical analysis.
8. Give examples that illustrate time-space trade-offs of algorithms.
9. Explain how tree balance affects the efficiency of various binary search tree operations.
10. Explain to a non-technical audience the significance of tractable versus intractable algorithms using an intuitive explanation of Big-O complexity.
11. Explain the significance of NP-Completeness.
12. Describe NP-Hard as a lower bound and NP as an upper bound for NP-Completeness.
13. Provide examples of NP-complete problems. 

KA Core:
14. Use recurrence relations to determine the time complexity of recursively defined algorithms.
15. Solve elementary recurrence relations using some form of the Master Theorem.
16. Use Big-O notation to give upper case bounds on time/space complexity of algorithms.
17. Explain the Cook-Levin Theorem and the NP-Completeness of SAT.
18. Define the classes P and NP.
19. Prove that a problem is NP-Complete by reducing a classic known NP-C problem to it (e.g., 3SAT and Clique)
20. Define the P-space class and its relation to the EXP class.

### AL-Models: Computational Models and Formal Languages

CS Core:
1. Formal Automata
	a. Finite State
	b. Pushdown (See also: AL-Fundamentals: 5, SDF-ADT)
	c. Linear Bounded
	d. Turing Machine
2. Formal Languages, Grammars and Chomsky Hierarchy (See also: FPL-H Translation, FPL-J Syntax)
	a. Regular (Type-3)
		i. Regular Expressions
	b. Context-Free (Type-2)
	c. Context-Sensitive (Type-1)
	d. Recursively Enumerable (Type-0)
3. Relations among formal automata, languages, and grammars
4. Decidability, (un)computability, and halting
5. The Church-Turing Thesis
6. Algorithmic Correctness
	a. Invariants (e.g., in: iteration, recursion, tree search)

KA Core:
1. Deterministic and nondeterministic automata
2. Pumping Lemma Proofs (See also: MSF-Discrete: 3)
	a. Finite State/Regular
	b. Pushdown Automata/Context-Free
3. Decidability
	a. Arithmetization and Diagonalization (See also: MSF-Discrete: 1)
4. Reducibility and reductions
5. Time Complexity based on Turing Machine
6. Space Complexity (e.g., PSPACE, Savitch’s Theorem)
7. Equivalent Models of Algorithmic Computation
	a. Turing Machines and Variations (e.g., multi-tape, non-deterministic)
	b. Lambda Calculus (See also: FPL-Functional)
	c. Mu-Recursive Functions 

Non Core:
8. Quantum Computation (See also: AR-Quantum)
	a. Postulates of quantum mechanics
		i. State Space
		ii. State Evolution
		iii. State Composition
		iv. State Measurement
	b. Column vector representations of Qubits
	c. Matrix representations of quantum operations
	d. Quantum Gates (e.g., XNOT, CNOT) 

Illustrative Learning Outcomes
CS Core:
1. For each formal automata in this unit:
	a. Articulate its definition comparing its characteristics with this unit’s other automata,
	b. Using an example, explain step-by-step how the automata operates on input including whether it accepts the associated input,
	c. Give an example of inputs that can and cannot be accepted by the automata.
2. Given a real-world problem, design an appropriate automaton that addresses the problem.
3. Design a Regular Expression to accept a sentence from a Regular language.
4. Explain the difference between Regular Expressions (Type-3 acceptors) and Re-Ex pattern matchers (Type-2 acceptors) used in programming languages.
5. For each formal language/grammar in this unit
	a. Articulate its definition comparing its characteristics with the others in this unit,
	b. Give an example of inputs that can and cannot be accepted by the
	language/grammar.
6. Describe a univTuring Machine.
7. Explain how decidability and computability for various automata are related.
8. Explain the Halting problem, why it has no algorithmic solution, and its significance for realworld algorithmic computation.
9. Give examples of classic uncomputable problems.
10. Explain the Church-Turing Thesis and its significance for algorithmic computation.
11. Explain how invariants assist in proving the correctness of an algorithm as a formal model. 

Illustrative Learning Outcomes
KA Core:
1. For each formal automata in this unit
	a. Compare/contrast its deterministic and nondeterministic capabilities.
2. Use a pumping lemma to prove the limitations of Finite State and Pushdown automata.
3. Use arithmetization and diagonalization to prove Turing Machine Halting/Undecidability.
4. Explain a reduction such as between Halting and Undecidability of the language accepted by a Turing Machine, where one has been previously proven by diagonalization.
5. Convert among equivalently powerful notations for a language, including among DFAs, NFAs, and regular expressions, and between PDAs and CFGs
6. Explain Rice’s Theorem and its significance. 
7. Give an example proof of a problem that is uncomputable by reducing a classic known uncomputable problem to it
8. Explain the Primitive and General Recursive functions (zero, successor, selection, primitive recursion, composition, and Mu), their significance, and Turing Machine implementations.
9. Explain how computation is performed in Lambda Calculus (e.g., Alpha Conversion and Beta-Reduction)

Non Core:
10. For a quantum system give examples that explain the following postulates:
	a. State Space: system state represented as a unit vector in Hilbert space,
	b. State Evolution: the use of unitary operators to evolve system state,
	c. State Composition: the use of tensor product to compose systems states,
	d. State Measurement: the probabilistic output of measuring a system state.
11. Explain the operation of a quantum XNOT or CNOT gate on a quantum bit represented as a matrix and column vector respectively
### AL-SEP: Society, Ethics, and Professionalism

CS Core: (See also: SEP-Context, SEP-Sustainability)
1. Social, Ethical, and Secure Algorithms
2. Algorithmic Fairness (e.g., Differential Privacy)
3. Accountability/Transparency
4. Responsible algorithms
5. Economic and other impacts of inefficient algorithms
6. Sustainability

Illustrative Learning Outcomes

CS Core:
1. Devise algorithmic solutions to real-world societal problems, such as routing an ambulance to a hospital
2. Predict and explain the impact that an algorithm may have on the environment and society when used to solve real-world problems taking into account that it can affect different societal groups in different ways and the algorithm’s sustainability.
3. Prepare a presentation that justifies the selection of appropriate data structures and/or algorithms to solve a given real-world industry problem.
4. Give an example that articulates how differential privacy protects knowledge of an individual’s data.
5. Describe the environmental impacts of design choices that relate to algorithm design.
6. Discuss the tradeoffs involved in proof-of-work and proof-of-stake algorithms. 