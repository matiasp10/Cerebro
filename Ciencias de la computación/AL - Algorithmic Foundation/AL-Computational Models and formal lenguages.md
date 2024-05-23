
- Automatas
- Lenguajes formales, gramatica y jerarquia Chomsky
- Relaciones entre autómatas formales, lenguajes y gramáticas
- Decidibilidad, (in)computabilidad y detención
- La tesis de Church-Turing
- Corrección algorítmica
### CS Core:

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
### KA Core:

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
### Non Core:

8. Quantum Computation (See also: AR-Quantum)
	a. Postulates of quantum mechanics
		i. State Space
		ii. State Evolution
		iii. State Composition
		iv. State Measurement
	b. Column vector representations of Qubits
	c. Matrix representations of quantum operations
	d. Quantum Gates (e.g., XNOT, CNOT)
### Illustrative Learning Outcomes
#### CS Core:

1. For each formal automata in this unit:
	a. Articulate its definition comparing its characteristics with this unit’s other automata,
	b. Using an example, explain step-by-step how the automata operates on input including whether it accepts the associated input,
	c. Give an example of inputs that can and cannot be accepted by the automata.
2. Given a real-world problem, design an appropriate automaton that addresses the problem.
3. Design a Regular Expression to accept a sentence from a Regular language.
4. Explain the difference between Regular Expressions (Type-3 acceptors) and Re-Ex pattern matchers (Type-2 acceptors) used in programming languages.
5. For each formal language/grammar in this unit
	a. Articulate its definition comparing its characteristics with the others in this unit,
	b. Give an example of inputs that can and cannot be accepted by the language/grammar.
6. Describe a univTuring Machine.
7. Explain how decidability and computability for various automata are related.
8. Explain the Halting problem, why it has no algorithmic solution, and its significance for realworld algorithmic computation.
9. Give examples of classic uncomputable problems.
10. Explain the Church-Turing Thesis and its significance for algorithmic computation.
11. Explain how invariants assist in proving the correctness of an algorithm as a formal model.
#### KA Core:

12. For each formal automata in this unit
	a. Compare/contrast its deterministic and nondeterministic capabilities.
13. Use a pumping lemma to prove the limitations of Finite State and Pushdown automata.
14. Use arithmetization and diagonalization to prove Turing Machine Halting/Undecidability.
15. Explain a reduction such as between Halting and Undecidability of the language accepted by a Turing Machine, where one has been previously proven by diagonalization.
16. Convert among equivalently powerful notations for a language, including among DFAs, NFAs, and regular expressions, and between PDAs and CFGs
17. Explain Rice’s Theorem and its significance.
18. Give an example proof of a problem that is uncomputable by reducing a classic known uncomputable problem to it
19. Explain the Primitive and General Recursive functions (zero, successor, selection, primitive recursion, composition, and Mu), their significance, and Turing Machine implementations.
20. Explain how computation is performed in Lambda Calculus (e.g., Alpha Conversion and Beta-Reduction)
#### Non Core:

21. For a quantum system give examples that explain the following postulates:
	a. State Space: system state represented as a unit vector in Hilbert space,
	b. State Evolution: the use of unitary operators to evolve system state,
	c. State Composition: the use of tensor product to compose systems states,
	d. State Measurement: the probabilistic output of measuring a system state.
22. Explain the operation of a quantum XNOT or CNOT gate on a quantum bit represented as a matrix and column vector respectively