
- Análisis de complejidad 
- Análisis de complejidad asintótica 
- Medidas empíricas del rendimiento
- Trazabilidad e intratabilidad
- Compromisos de tiempo y espacio en los algoritmos

- Notación Little-o y Little-Omega 
- Analisis recursivo
- Analisis Amortizado
- Modelos de complejidad basados en la máquina de Turing
### CS Core:

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
### KA Core:

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
### Illustrative Learning Outcomes
#### CS Core:

1. Explain what is meant by “best”, “average”, and “worst” case behavior of an algorithm.
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
#### KA Core:

14. Use recurrence relations to determine the time complexity of recursively defined algorithms.
15. Solve elementary recurrence relations using some form of the Master Theorem.
16. Use Big-O notation to give upper case bounds on time/space complexity of algorithms.
17. Explain the Cook-Levin Theorem and the NP-Completeness of SAT.
18. Define the classes P and NP.
19. Prove that a problem is NP-Complete by reducing a classic known NP-C problem to it (e.g., 3SAT and Clique)
20. Define the P-space class and its relation to the EXP class.