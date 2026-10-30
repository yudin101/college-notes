# BIT152 Discrete Structure: Exam-Ready Answers

Built from the 2078, 2079, 2080, 2081, 2082 papers and the model question. Topics are ordered by how often they repeat, then syllabus topics that haven't been asked yet but could be.

**How to use this:** Discrete Structure is a practice subject. You cannot pass it by reading. Every proof, recurrence, algorithm and numerical below must be written out by hand at least twice. If you only read, you will freeze in the exam.

**Check before the exam:** This is written from standard textbook content (mainly Rosen). Where your teacher's notation or format differs, follow your teacher's. Diagrams are simplified; redraw them neatly with labels.

## What repeats (2078-2082 + model)

| Topic                                                                              | Where it appeared                           |
| ---------------------------------------------------------------------------------- | ------------------------------------------- |
| **Mathematical induction** (sum formulas, divisibility)                            | 2078, 2079, 2081, 2082, model               |
| **Recurrence relations** (solve with characteristic equation)                      | 2078, 2080, 2081, 2082, model (every paper) |
| **Proof methods** (direct, indirect, contradiction, root 2)                        | 2078, 2079, 2080, 2081, 2082, model         |
| **Euler path/circuit conditions**                                                  | 2078, 2079, 2081, 2082                      |
| **Spanning tree, MST, Kruskal**                                                    | 2078, 2081, 2082, model                     |
| **Dijkstra shortest path**                                                         | 2079, 2082, model                           |
| **Graph representation** (adjacency, incidence matrix)                             | 2080, 2081, model                           |
| **Tree traversal**                                                                 | 2080, 2082                                  |
| **Pigeonhole principle** (generalized)                                             | 2079, 2080, 2081, 2082                      |
| **Permutation vs combination, next permutation (362541)**                          | 2080, 2082, model                           |
| **Modular arithmetic, congruence**                                                 | 2078, 2079, 2081                            |
| **Chinese Remainder Theorem**                                                      | 2080, 2082                                  |
| **Euclidean / extended Euclidean algorithm**                                       | 2079, 2081, model                           |
| **Boolean function, exponential function, partial ordering**                       | 2081, 2082, model                           |
| **Floor/ceiling functions**                                                        | 2080, model                                 |
| **One-to-one, onto, identity functions**                                           | 2079, 2080                                  |
| **Relations** (matrix, digraph, equivalence)                                       | 2078, 2079, 2080, model                     |
| **Quantifiers, predicate translation**                                             | 2080, 2081, 2082                            |
| **Rules of inference**                                                             | 2079, 2082                                  |
| **Randomized algorithms**                                                          | 2081, 2082                                  |
| **Recursive definitions, structural induction, recursive algorithm correctness**   | 2079, 2080, 2081, 2082, model               |
| **Sets** (power set, Cartesian product, bit strings, Venn)                         | 2078, 2079, 2080, 2081, model               |
| **Graph basics** (types, isomorphism, connectivity, bipartite, planar, cut vertex) | 2078, 2080, 2081, 2082                      |

## Which long questions to attempt

Each paper gives three long questions and you do two. The long questions are bundles of two or three sub-topics, so you need a spread. The safest bets are:

1. **Induction + recursion/recurrence** (formulaic, high marks if you've practiced)
2. **Dijkstra / Kruskal / spanning tree** (pure algorithm, step-by-step marks)
3. **Proof methods + logic** (direct/indirect/contradiction, rules of inference)

## Errors in the papers (state your assumption in the exam)

- **2078 Q2:** the recurrence is garbled in the scan. I've assumed `a_n = 4a_(n-1) + n`.
- **2079 Q6:** "7 + 119" is almost certainly `7 +11 9` (addition in Z11). Answers below cover that.
- **2081 Q1:** the graph is too blurry for me to read reliably, so I have not solved it. Follow the Kruskal steps in Section 7.
- **2082 Q1 and 2079 Q8:** details are ambiguous; see the notes in those answers.

## Contents

1. [Mathematical Induction](#1-mathematical-induction)
2. [Recurrence Relations](#2-recurrence-relations)
3. [Proof Methods](#3-proof-methods)
4. [Graph Fundamentals](#4-graph-fundamentals)
5. [Euler and Hamilton Paths](#5-euler-and-hamilton-paths)
6. [Dijkstra's Shortest Path](#6-dijkstras-shortest-path)
7. [Trees, Spanning Trees, Kruskal, Traversals](#7-trees-spanning-trees-kruskal-traversals)
8. [Counting](#8-counting)
9. [Number Theory](#9-number-theory)
10. [Sets and Functions](#10-sets-and-functions)
11. [Relations](#11-relations)
12. [Logic and Rules of Inference](#12-logic-and-rules-of-inference)
13. [Recursion and Structural Induction](#13-recursion-and-structural-induction)
14. [Randomized Algorithms and Probability](#14-randomized-algorithms-and-probability)
15. [Syllabus Extras (not yet asked)](#15-syllabus-extras-not-yet-asked)

---

## 1. Mathematical Induction

### Principle

To prove `P(n)` is true for all integers `n >= n0`:

1. **Basis step:** show `P(n0)` is true.
2. **Inductive step:** assume `P(k)` is true for an arbitrary `k >= n0` (the **inductive hypothesis**) and show that `P(k+1)` is true.
3. **Conclusion:** by the principle of mathematical induction, `P(n)` is true for all `n >= n0`.

It works like dominoes: the basis knocks over the first, and the inductive step guarantees each falling domino knocks over the next.

### a) Sum of the first n odd positive integers is n² (2079, 2082, model)

`P(n): 1 + 3 + 5 + ... + (2n-1) = n²`

- **Basis:** n = 1: LHS = 1, RHS = 1² = 1. True.
- **Inductive step:** Assume `1 + 3 + ... + (2k-1) = k²`. Then
  `1 + 3 + ... + (2k-1) + (2k+1) = k² + (2k+1) = (k+1)²`.
  So `P(k+1)` is true.
- **Conclusion:** `P(n)` holds for all n >= 1. ∎

### b) Sum of the first n positive integers is n(n+1)/2 (2078)

- **Basis:** n = 1: LHS = 1, RHS = 1·2/2 = 1.
- **Step:** Assume `1 + 2 + ... + k = k(k+1)/2`. Then
  `1 + ... + k + (k+1) = k(k+1)/2 + (k+1) = (k+1)(k/2 + 1) = (k+1)(k+2)/2`. ∎

### c) 1³ + 2³ + ... + n³ is a perfect square (2081)

Claim: `1³ + 2³ + ... + n³ = [n(n+1)/2]²`. Since `n(n+1)/2` is an integer, the sum is a perfect square.

- **Basis:** n = 1: LHS = 1, RHS = (1·2/2)² = 1.
- **Step:** Assume the sum to k equals `[k(k+1)/2]²`. Then
  `[k(k+1)/2]² + (k+1)³ = (k+1)² [k²/4 + (k+1)] = (k+1)² (k+2)²/4 = [(k+1)(k+2)/2]²`. ∎

### d) 3ⁿ - 1 is a multiple of 2 for n >= 1 (2079)

- **Basis:** n = 1: 3 - 1 = 2, a multiple of 2.
- **Step:** Assume `3^k - 1 = 2m` for some integer m. Then
  `3^(k+1) - 1 = 3·3^k - 1 = 3(2m + 1) - 1 = 6m + 2 = 2(3m + 1)`, a multiple of 2. ∎

### e) Other forms you may get

**Divisibility:** n³ - n is divisible by 3.
Basis: n = 1 gives 0. Step: `(k+1)³ - (k+1) = (k³ - k) + 3(k² + k)`, both terms divisible by 3. ∎

**Inequality:** n < 2ⁿ for n >= 1.
Basis: 1 < 2. Step: if `k < 2^k`, then `k + 1 < 2^k + 1 <= 2^k + 2^k = 2^(k+1)`. ∎

### Strong induction and well-ordering

- **Strong induction:** to prove `P(n)` for all n >= n0, show `P(n0)` is true and that if `P(n0), ..., P(k)` are **all** true then `P(k+1)` is true. Use it when the step needs more than just the previous case.
- **Well-ordering property:** every non-empty set of positive integers has a least element. It is equivalent to induction and is used to prove things by contradiction (assume a smallest counterexample exists).

---

## 2. Recurrence Relations

### Definitions

- **Recurrence relation:** an equation that expresses `a_n` in terms of one or more earlier terms (`a_0, ..., a_(n-1)`) for all `n >= n0`. **Initial conditions** specify the first few terms.
- **Linear homogeneous recurrence relation of degree k with constant coefficients:**
  `a_n = c1·a_(n-1) + c2·a_(n-2) + ... + ck·a_(n-k)`, with `c1, ..., ck` real constants and `ck != 0`.
  - _Linear:_ previous terms appear only to the first power.
  - _Homogeneous:_ no extra term that doesn't involve a previous `a`.
  - _Constant coefficients:_ the c's don't depend on n.
  - _Degree k:_ `a_n` depends on the previous k terms.
- **Linear non-homogeneous:** `a_n = c1·a_(n-1) + ... + ck·a_(n-k) + F(n)`, where `F(n) != 0` depends only on n.

### Solving a homogeneous relation

1. Write the **characteristic equation:** `r^k - c1·r^(k-1) - ... - ck = 0`.
2. Find the roots.
3. **Distinct roots** `r1, ..., rk`: `a_n = α1·r1^n + α2·r2^n + ... + αk·rk^n`.
   **Repeated root** r of multiplicity m: use `(α0 + α1·n + ... + α(m-1)·n^(m-1))·r^n` for that root.
4. Use the initial conditions to find the constants α.

### Solving a non-homogeneous relation

`a_n = a_n^(h) + a_n^(p)`: the solution of the associated homogeneous relation plus any particular solution.

Form of the particular solution for `F(n)`:

| F(n)                                                                  | Try                           |
| --------------------------------------------------------------------- | ----------------------------- |
| Polynomial of degree t (e.g. n, n², constant) and 1 is **not** a root | `p_t·n^t + ... + p_1·n + p_0` |
| `c·s^n` and s is **not** a root                                       | `p·s^n`                       |
| `c·s^n` and s **is** a root of multiplicity m                         | `n^m·p·s^n`                   |

Substitute into the recurrence to find the coefficients p.

### a) Fibonacci: `a_n = a_(n-1) + a_(n-2)`, a0 = 0, a1 = 1 (2082, model)

Characteristic equation: `r² - r - 1 = 0`, so `r = (1 ± √5)/2`.
`a_n = α1·((1+√5)/2)^n + α2·((1-√5)/2)^n`

- n = 0: `α1 + α2 = 0`, so `α2 = -α1`.
- n = 1: `α1(1+√5)/2 + α2(1-√5)/2 = 1`, so `α1·√5 = 1`, giving `α1 = 1/√5`, `α2 = -1/√5`.

**`a_n = (1/√5)[((1+√5)/2)^n - ((1-√5)/2)^n]`**

### b) `a_n = 7a_(n-1) - 10a_(n-2)`, a0 = 2, a1 = 3 (2080)

Characteristic equation: `r² - 7r + 10 = 0`, so `(r-5)(r-2) = 0`, giving r = 5, 2.
`a_n = α1·5^n + α2·2^n`

- n = 0: `α1 + α2 = 2`
- n = 1: `5α1 + 2α2 = 3`

Substituting `α2 = 2 - α1`: `5α1 + 4 - 2α1 = 3`, so `α1 = -1/3`, `α2 = 7/3`.

**`a_n = -(1/3)·5^n + (7/3)·2^n`**. Check: a1 = -5/3 + 14/3 = 3 ✓.

### c) `a_n = 6a_(n-1) - 11a_(n-2) + 6a_(n-3)`, a0 = 2, a1 = 5, a2 = 15 (2081)

Characteristic equation: `r³ - 6r² + 11r - 6 = 0`, which factors as `(r-1)(r-2)(r-3) = 0`.
`a_n = α1 + α2·2^n + α3·3^n`

- n = 0: `α1 + α2 + α3 = 2`
- n = 1: `α1 + 2α2 + 3α3 = 5`
- n = 2: `α1 + 4α2 + 9α3 = 15`

Subtracting consecutive equations: `α2 + 2α3 = 3` and `2α2 + 6α3 = 10`, so `α2 + 3α3 = 5`. Hence `α3 = 2`, `α2 = -1`, `α1 = 1`.

**`a_n = 1 - 2^n + 2·3^n`**. Check: a3 = 6·15 - 11·5 + 6·2 = 47 and `1 - 8 + 54 = 47` ✓.

### d) Non-homogeneous: `a_n = 4a_(n-1) + n` (2078, assumed form)

- **Homogeneous part:** `a_n = 4a_(n-1)` has root r = 4, so `a_n^(h) = α·4^n`.
- **Particular solution:** F(n) = n is a degree-1 polynomial and 1 is not a root, so try `a_n^(p) = c1·n + c0`.
  Substituting: `c1·n + c0 = 4[c1(n-1) + c0] + n`.
  Matching n terms: `c1 = 4c1 + 1`, so `c1 = -1/3`.
  Matching constants: `c0 = -4c1 + 4c0`, so `c0 = 4c1/3 = -4/9`.
  So `a_n^(p) = -n/3 - 4/9`.
- **General solution (all solutions):** `a_n = α·4^n - n/3 - 4/9`.
- **With a1 = 1:** `1 = 4α - 1/3 - 4/9 = 4α - 7/9`, so `α = 4/9`.

  **`a_n = (4^(n+1) - 3n - 4)/9`**. Check: a1 = (16 - 3 - 4)/9 = 1 ✓; a2 = 4·1 + 2 = 6 and (64 - 6 - 4)/9 = 6 ✓.

- If the condition is `a0 = 1` instead: `α = 13/9`, so `a_n = (13·4^n - 3n - 4)/9`.

---

## 3. Proof Methods

### Terminology

- **Theorem:** a statement proven true. **Lemma:** a helper theorem. **Corollary:** follows directly from a theorem. **Axiom:** assumed true. **Conjecture:** unproven statement.

### Methods

| Method                              | Idea                                                                                       |
| ----------------------------------- | ------------------------------------------------------------------------------------------ |
| **Direct proof**                    | Assume p is true and show q follows, for `p → q`                                           |
| **Indirect proof (contraposition)** | Prove `¬q → ¬p`, which is equivalent to `p → q`                                            |
| **Proof by contradiction**          | Assume the statement is false and derive a contradiction (`p ∧ ¬p`)                        |
| **Vacuous proof**                   | `p → q` is true because p is always false                                                  |
| **Trivial proof**                   | `p → q` is true because q is always true                                                   |
| **Proof by cases / exhaustive**     | Split into cases that cover everything and prove each                                      |
| **Proof of equivalence**            | To prove `p ↔ q`, prove both `p → q` and `q → p`                                           |
| **Existence proof**                 | Show that an object exists (constructive: give one; non-constructive: argue it must exist) |
| **Uniqueness proof**                | Show existence, then show any two such objects are equal                                   |
| **Counterexample**                  | Disprove a universal claim with one example                                                |

### Direct proofs

**If n is odd, then n² is odd** (2078, model):
Let n = 2k + 1 for some integer k. Then `n² = 4k² + 4k + 1 = 2(2k² + 2k) + 1`, which is odd. ∎

**The sum of two even numbers is even** (2079):
Let a = 2m and b = 2n. Then `a + b = 2m + 2n = 2(m + n)`, which is even. ∎

**The sum of an odd and an even number is odd** (2081):
Let a = 2m + 1 (odd) and b = 2n (even). Then `a + b = 2(m + n) + 1`, which is odd. ∎

### Indirect proof (2078)

**If n is an integer and n² is odd, then n is odd.**
Contrapositive: if n is even, then n² is even.
Let n = 2k. Then `n² = 4k² = 2(2k²)`, which is even. The contrapositive is true, so the original statement is true. ∎

### Proof by contradiction: √2 is irrational (2080, 2082)

Assume √2 is rational. Then `√2 = a/b` where a, b are integers with no common factor (lowest terms), b != 0.

1. Squaring: `2 = a²/b²`, so `a² = 2b²`.
2. So a² is even, which means a is even. Let `a = 2c`.
3. Then `4c² = 2b²`, so `b² = 2c²`, meaning b² is even, so b is even.
4. Now both a and b are even, so they have a common factor 2. This contradicts "lowest terms".

So the assumption is false. **√2 is irrational.** ∎

### Counterexample

"Every prime number is odd" is false. Counterexample: 2 is prime and even.

### Common mistakes in proofs

- **Affirming the conclusion:** from `p → q` and q, concluding p.
- **Circular reasoning (begging the question):** using the thing you are proving.
- **Proving one example** and calling it a general proof.
- **Dividing by zero** hidden inside the algebra.

---

## 4. Graph Fundamentals

### Definition

A graph `G = (V, E)` consists of a non-empty set V of **vertices (nodes)** and a set E of **edges**, each connecting two vertices.

### Types of graphs

| Type                         | Edges                        | Multiple edges?                                 | Loops?               |
| ---------------------------- | ---------------------------- | ----------------------------------------------- | -------------------- |
| **Simple graph**             | Undirected                   | No                                              | No                   |
| **Multigraph**               | Undirected                   | Yes                                             | No                   |
| **Pseudograph**              | Undirected                   | Yes                                             | Yes                  |
| **Directed graph (digraph)** | Directed (arcs)              | Not between same ordered pair in simple digraph | Loops may be allowed |
| **Mixed graph**              | Both directed and undirected | Possible                                        | Possible             |

**Simple graph example:** vertices {a, b, c}, edges {a-b, b-c, c-a}. No loops, no repeated edges.
**Pseudograph example:** vertices {a, b}, edges: a-b twice and a loop at a.

### Terminology

- **Adjacent:** two vertices joined by an edge. **Incident:** an edge and its endpoint.
- **Degree** `deg(v)`: number of edges incident to v (a loop counts 2).
- **Handshaking theorem:** `sum of deg(v) = 2|E|`. So the number of odd-degree vertices is always even.
- **Directed graph:** in-degree and out-degree. The sum of in-degrees = sum of out-degrees = |E|.

### Special graphs

- **Complete graph Kn:** every pair of vertices is adjacent. Edges = n(n-1)/2.
- **Cycle Cn** (n >= 3): n vertices in a single cycle.
- **Wheel Wn:** Cn plus one hub vertex joined to all.
- **n-cube Qn:** 2ⁿ vertices (bit strings of length n); two are adjacent if they differ in exactly one bit.
- **Bipartite graph:** vertices split into two sets V1, V2 such that every edge joins V1 to V2. **Complete bipartite K(m,n):** every vertex in V1 is adjacent to every vertex in V2; has mn edges.
- **Subgraph:** a graph whose vertices and edges are subsets of G's. **Union** of G1 and G2 has vertex set V1 ∪ V2 and edge set E1 ∪ E2.

### Representing graphs

Example graph: vertices a, b, c, d; edges e1 = ab, e2 = bc, e3 = ca, e4 = cd.

**Adjacency list** (each vertex with its neighbours):

```
a: b, c
b: a, c
c: a, b, d
d: c
```

**Adjacency matrix** (rows and columns are vertices; entry = 1 if adjacent):

```
     a  b  c  d
 a [ 0  1  1  0 ]
 b [ 1  0  1  0 ]
 c [ 1  1  0  1 ]
 d [ 0  0  1  0 ]
```

- Undirected graph: the matrix is symmetric.
- A loop gives 1 on the diagonal; for a multigraph, the entry is the number of edges.
- For a digraph, entry (i, j) = 1 if there is an arc from vi to vj.
- Needs n² space; good for dense graphs.

**Incidence matrix** (rows = vertices, columns = edges; entry = 1 if the vertex is an endpoint of the edge):

```
     e1 e2 e3 e4
 a [  1  0  1  0 ]
 b [  1  1  0  0 ]
 c [  0  1  1  1 ]
 d [  0  0  0  1 ]
```

In a simple undirected graph, each column has exactly two 1s. A loop gives a single 1 in its column.

### Graph isomorphism (2081)

Graphs G1 = (V1, E1) and G2 = (V2, E2) are **isomorphic** if there is a one-to-one and onto function `f: V1 → V2` such that a and b are adjacent in G1 **if and only if** f(a) and f(b) are adjacent in G2.

**Invariants (must be equal, but equality alone doesn't prove isomorphism):** number of vertices, number of edges, degree sequence, number of cycles of each length. If any invariant differs, the graphs are **not** isomorphic.

**Example:** G1 has edges ab, bc, cd, da (a 4-cycle). G2 has edges 1-3, 3-2, 2-4, 4-1. Define `f(a) = 1, f(b) = 3, f(c) = 2, f(d) = 4`. Then ab → 1-3, bc → 3-2, cd → 2-4, da → 4-1; all are edges of G2. So G1 ≅ G2.

### Connectivity (2080, 2082)

- **Path:** a sequence of edges moving from one vertex to another. **Circuit (cycle):** a path that starts and ends at the same vertex.
- **Connected graph:** there is a path between every pair of distinct vertices. Otherwise the graph is **disconnected** and splits into **connected components**.
- **Directed graphs:** **strongly connected** (a directed path exists from a to b _and_ b to a for all a, b) or **weakly connected** (connected when directions are ignored).
- **Cut vertex:** a vertex whose removal (with its edges) disconnects the graph (increases the number of components).
- **Cut edge (bridge):** an edge whose removal disconnects the graph.

Connectivity matters for networks: it tells you whether every node can reach every other node, and which nodes or links are critical points of failure.

### Bipartite graphs (2082)

A graph is bipartite if its vertices can be partitioned into two disjoint sets so that no two vertices in the same set are adjacent (equivalently, it can be coloured with two colours).

**Test:** a graph is bipartite if and only if it contains **no odd-length cycle**. Example: C4 is bipartite, C3 (a triangle) is not. K(m,n) is bipartite.

### Planar graphs (2082)

A graph is planar if it can be drawn in the plane with **no edges crossing**.

- **Euler's formula:** for a connected planar graph, `v - e + f = 2`, where f is the number of regions (faces).
- For a simple connected planar graph with v >= 3: `e <= 3v - 6`. If it also has no triangles, `e <= 2v - 4`.
- **K5** is not planar (10 edges > 3·5 - 6 = 9). **K(3,3)** is not planar (9 edges > 2·6 - 4 = 8).
- **Kuratowski's theorem:** a graph is non-planar if and only if it contains a subdivision of K5 or K(3,3).

---

## 5. Euler and Hamilton Paths

### Definitions

- **Euler circuit:** a circuit that uses **every edge exactly once** and returns to the start.
- **Euler path:** a path that uses every edge exactly once (it need not return to the start).
- **Hamilton circuit / path:** a circuit / path that visits **every vertex exactly once**.

### Necessary and sufficient conditions (2078, 2079, 2081, 2082)

For a **connected** undirected multigraph:

- **Euler circuit exists if and only if every vertex has even degree.**
- **Euler path (but no circuit) exists if and only if exactly two vertices have odd degree.** The path starts at one odd vertex and ends at the other.

For a directed graph with a connected underlying graph:

- **Euler circuit** if and only if in-degree = out-degree for every vertex.
- **Euler path** if and only if the graph has at most one vertex with out-in = 1 (start), at most one with in-out = 1 (end), and all others balanced.

**How to determine (2081):** (1) check the graph is connected, (2) count the vertices of odd degree: 0 means Euler circuit, 2 means Euler path, otherwise neither.

**Examples:**

- K3 (triangle): all degrees 2, so it has an Euler circuit.
- Path graph a-b-c: deg(a) = 1, deg(b) = 2, deg(c) = 1; two odd vertices, so an Euler path (a to c) but no circuit.
- K4: all degrees 3 (four odd vertices), so neither.

### Hamilton conditions

No simple necessary and sufficient condition is known. Only **sufficient** conditions exist:

- **Dirac:** a simple graph with n >= 3 vertices where `deg(v) >= n/2` for every v has a Hamilton circuit.
- **Ore:** if `deg(u) + deg(v) >= n` for every pair of non-adjacent vertices, then it has a Hamilton circuit.

### Euler vs Hamilton (2078)

| Point       | Euler path/circuit              | Hamilton path/circuit                            |
| ----------- | ------------------------------- | ------------------------------------------------ |
| Visits      | Every **edge** exactly once     | Every **vertex** exactly once                    |
| Vertices    | May be revisited                | Not revisited (except start = end for a circuit) |
| Test        | Simple: check vertex degrees    | No simple criterion (NP-complete)                |
| Example use | Route inspection, mail delivery | Travelling salesman problem                      |

---

## 6. Dijkstra's Shortest Path

### Problem

The **shortest path problem** is to find a path of least total weight between two vertices in a weighted graph. Used in routing, GPS, and network protocols.

### Algorithm (Dijkstra, for positive weights)

1. Set `L(a) = 0` for the source a and `L(v) = ∞` for all other vertices. Let S = empty (visited set).
2. Choose the vertex u **not in S** with the smallest label L(u). Add u to S.
3. For every vertex v **not in S** adjacent to u: if `L(u) + w(u,v) < L(v)`, set `L(v) = L(u) + w(u,v)` and record u as v's predecessor.
4. Repeat steps 2-3 until the destination z is in S. `L(z)` is the shortest distance.
5. Trace predecessors back from z to get the path.

### Worked example (2082 Q8 / model Q3)

Graph as read from the scan; verify against your paper. Edges: a-b = 2, a-c = 3, b-d = 5, b-e = 2, c-e = 5, d-e = 1, d-z = 2, e-z = 4.

| Step | Vertex added to S | L(a) | L(b) | L(c) | L(d) | L(e)                 | L(z)  |
| ---- | ----------------- | ---- | ---- | ---- | ---- | -------------------- | ----- |
| Init |                   | 0    | ∞    | ∞    | ∞    | ∞                    | ∞     |
| 1    | a (0)             | 0    | 2    | 3    | ∞    | ∞                    | ∞     |
| 2    | b (2)             | 0    | 2    | 3    | 7    | 4                    | ∞     |
| 3    | c (3)             | 0    | 2    | 3    | 7    | 4 (via c would be 8) | ∞     |
| 4    | e (4)             | 0    | 2    | 3    | 5    | 4                    | 8     |
| 5    | d (5)             | 0    | 2    | 3    | 5    | 4                    | 7     |
| 6    | z (7)             |      |      |      |      |                      | **7** |

**Shortest path: a → b → e → d → z, length 2 + 2 + 1 + 2 = 7.**

---

## 7. Trees, Spanning Trees, Kruskal, Traversals

### Trees

A **tree** is a connected undirected graph with **no simple circuits**. A tree with n vertices has **n - 1 edges**. A **rooted tree** has one vertex designated the root; terms: parent, child, leaf (no children), internal vertex, subtree, level, height.

**Applications:** binary search trees (searching/sorting), decision trees (modelling choices), prefix codes (e.g., Huffman coding: no code is a prefix of another).

### Spanning tree and minimum spanning tree

- **Spanning tree** of a connected graph G: a subgraph that is a tree and contains **all vertices** of G. A connected graph with n vertices gives a spanning tree with n - 1 edges.
- **Minimum spanning tree (MST)** of a connected weighted graph: a spanning tree with the **smallest possible total weight**.

**Example:** a triangle with vertices A, B, C and edge weights AB = 1, BC = 2, AC = 3. Spanning trees: {AB, BC} weight 3, {AB, AC} weight 4, {BC, AC} weight 5. The MST is {AB, BC} with weight 3.

**Use:** laying cable, pipelines, roads, or network links to connect all sites at minimum total cost.

### Kruskal's algorithm

1. Sort all edges by weight, smallest first.
2. Pick the smallest edge. Add it to the tree **if it does not form a cycle** with the edges already chosen; otherwise reject it.
3. Repeat until the tree has n - 1 edges.

### Worked example (2078 Q3)

Graph as read from the scan; verify against your paper. Edges: a-b = 7, e-g = 8, c-e = 10, d-g = 11, f-g = 13, d-f = 15, b-f = 17, a-c = 18, c-d = 19.

| Step | Edge | Weight | Decision                                                    |
| ---- | ---- | ------ | ----------------------------------------------------------- |
| 1    | a-b  | 7      | Accept                                                      |
| 2    | e-g  | 8      | Accept                                                      |
| 3    | c-e  | 10     | Accept                                                      |
| 4    | d-g  | 11     | Accept                                                      |
| 5    | f-g  | 13     | Accept                                                      |
| 6    | d-f  | 15     | **Reject** (d and f are already connected through g: cycle) |
| 7    | b-f  | 17     | Accept (joins {a, b} to the rest)                           |

All 7 vertices are connected with 6 edges, so stop (a-c and c-d would form cycles).

**MST edges: ab, eg, ce, dg, fg, bf. Total weight = 7 + 8 + 10 + 11 + 13 + 17 = 66.**

For the 2081 graph, apply exactly the same steps: sort edges, add smallest first, skip any that create a cycle, stop at n - 1 edges.

### Tree traversal (2080, 2082)

**Tree traversal** is the process of visiting every vertex of an ordered rooted tree exactly once in a systematic order.

Example tree:

```
        A
       / \
      B   C
     / \   \
    D   E   F
```

| Traversal     | Rule                                        | Result      |
| ------------- | ------------------------------------------- | ----------- |
| **Preorder**  | Root, then left subtree, then right subtree | A B D E C F |
| **Inorder**   | Left subtree, then root, then right subtree | D B E A C F |
| **Postorder** | Left subtree, then right subtree, then root | D E B F C A |

**Preorder explained:** visit the root first, then recursively do preorder on each subtree from left to right. Here: visit A; then the subtree rooted at B (B, D, E); then the subtree rooted at C (C, F). Preorder is used to copy a tree and to produce prefix notation. Inorder gives sorted order for a binary search tree. Postorder is used to delete a tree and produce postfix notation.

---

## 8. Counting

### Basic rules

- **Product rule:** if a task can be done in a sequence of two steps, with n1 ways for the first and n2 ways for the second, the task can be done in `n1 × n2` ways.
- **Sum rule:** if a task can be done in one of two ways that cannot happen together, with n1 ways or n2 ways, then there are `n1 + n2` ways.
- **Subtraction rule (inclusion-exclusion for 2 sets):** `|A ∪ B| = |A| + |B| - |A ∩ B|`.

### Inclusion-exclusion (2079)

**Why needed:** when the cases overlap, the sum rule counts the common elements twice. Inclusion-exclusion corrects the overcount.
`|A ∪ B ∪ C| = |A| + |B| + |C| - |A ∩ B| - |A ∩ C| - |B ∩ C| + |A ∩ B ∩ C|`

### Worked counting questions from past papers

**Strings of four lowercase letters containing at least one x (2078):**
Total strings = 26⁴ = 456,976. Strings with no x = 25⁴ = 390,625. So with x: 456,976 - 390,625 = **66,351**.

**Four-character words: first three are lowercase letters, last is a digit, no character repeated (2079):**
26 × 25 × 24 × 10 = **156,000**. (Letters and the digit come from different sets, so the digit can never repeat a letter.)

**Four-digit integers with no repeated digit (2081):**
First digit: 9 choices (1-9, not 0). Then 9, 8, 7. Total = 9 × 9 × 8 × 7 = **4,536**. (If leading zero were allowed, 10 × 9 × 8 × 7 = 5,040; state your assumption.)

### Pigeonhole principle (2079, 2080, 2081, 2082)

**Pigeonhole principle:** if k + 1 or more objects are placed into k boxes, then at least one box contains two or more objects.

**Generalized pigeonhole principle:** if N objects are placed into k boxes, then at least one box contains at least `⌈N/k⌉` objects.

**Examples:**

- Among 100 people, at least ⌈100/12⌉ = 9 were born in the same month.
- **2079 (24 students):** with k possible grades, two students must share a grade whenever 24 > k. So the maximum number of different grades for which a repeat is still guaranteed is **23**. (The wording is ambiguous; state this interpretation.)

**2082: ten natural numbers between 1 and 99; show two disjoint non-empty subsets have equal sums.**

- A set of 10 elements has 2¹⁰ - 1 = **1023 non-empty subsets**.
- The sum of any subset is at least 1 and at most 90 + 91 + ... + 99 = **945**. So there are only 945 possible sums.
- 1023 subsets (pigeons) into 945 possible sums (boxes): by the pigeonhole principle, two different subsets A and B have the same sum.
- If A and B overlap, remove the common elements from both. The sums remain equal, and the subsets are now disjoint. Neither becomes empty: if A ⊂ B with equal sums, then B - A would have sum 0, impossible for positive numbers. ∎

### Permutation vs combination (2080, 2082, model)

| Point                               | Permutation                             | Combination                             |
| ----------------------------------- | --------------------------------------- | --------------------------------------- |
| Meaning                             | Ordered arrangement of r objects from n | Unordered selection of r objects from n |
| Order                               | Matters (abc != bac)                    | Does not matter ({a,b,c} = {b,a,c})     |
| Formula                             | `P(n, r) = n! / (n - r)!`               | `C(n, r) = n! / (r! (n - r)!)`          |
| Relation                            | `P(n, r) = C(n, r) × r!`                |                                         |
| Example (n = 3, r = 2 from a, b, c) | 6: ab, ba, ac, ca, bc, cb               | 3: {a,b}, {a,c}, {b,c}                  |

### Generalized permutations and combinations (2082)

- **Permutations with repetition allowed:** `n^r`.
- **Combinations with repetition allowed:** `C(n + r - 1, r)`.
- **Permutations with indistinguishable objects:** `n! / (n1! n2! ... nk!)`. Example: arrangements of SUCCESS (S×3, C×2, U, E): 7! / (3! 2!) = **420**.

### Next permutation in lexicographic order (2080, model)

**Question: next permutation after 362541.**

Algorithm:

1. From the right, find the first position j where `a_j < a_(j+1)`.
2. Find the smallest digit to the right of j that is larger than `a_j`.
3. Swap them.
4. Reverse (sort ascending) the digits to the right of position j.

Working: `3 6 2 5 4 1`. Scanning from the right: 4 > 1, 5 > 4, then 2 < 5, so j is the position of 2. Digits to its right: 5, 4, 1. The smallest larger than 2 is **4**. Swap 2 and 4: `3 6 4 5 2 1`. Reverse the tail `5 2 1` to get `1 2 5`.

**Next permutation = 364125.**

### Binomial coefficients and Pascal's identity (2080)

**Pascal's identity:** `C(n+1, k) = C(n, k-1) + C(n, k)` for n >= k.

**Algebraic proof:**

```
C(n,k-1) + C(n,k) = n!/[(k-1)!(n-k+1)!] + n!/[k!(n-k)!]
                  = n!/[k!(n-k+1)!] · [k + (n-k+1)]
                  = n!(n+1)/[k!(n+1-k)!]
                  = (n+1)!/[k!(n+1-k)!]  = C(n+1, k)   ∎
```

**Combinatorial proof:** count the k-element subsets of a set with n + 1 elements. Fix one element x. Subsets **containing x**: choose the other k - 1 from n, which is `C(n, k-1)`. Subsets **not containing x**: choose k from n, which is `C(n, k)`. The total is `C(n+1, k)`. ∎

**Pascal's triangle** (each entry = sum of the two above it):

```
1
1 1
1 2 1
1 3 3 1
1 4 6 4 1
```

**Binomial theorem:** `(x + y)^n = Σ C(n, k) x^(n-k) y^k` for k = 0 to n.

---

## 9. Number Theory

### Division algorithm (2082: "division theory")

If a is an integer and d is a positive integer, there exist **unique** integers q (quotient) and r (remainder) such that
`a = d·q + r, 0 <= r < d`.
Examples: `101 = 11 × 9 + 2`; `-11 = 3 × (-4) + 1` (the remainder is never negative).

### Congruence and modular arithmetic (2078, 2079, 2081)

- `a mod m` = the remainder when a is divided by m (always in 0 to m-1).
- **a ≡ b (mod m)** if and only if m divides (a - b).
- If `a ≡ b` and `c ≡ d (mod m)`, then `a + c ≡ b + d` and `ac ≡ bd (mod m)`.
- **Arithmetic modulo m** (in Zm = {0, 1, ..., m-1}): `a +m b = (a + b) mod m`, `a ·m b = (a·b) mod m`.

**2078: is 20 ≡ 8 (mod 6)? Is 25 ≡ 17 (mod 5)?**

- 20 - 8 = 12, divisible by 6. **Yes.**
- 25 - 17 = 8, not divisible by 5. **No.**

**2079: 7 +11 9 and 7 ·11 9 in Z11** (the paper's "7 + 119" is this):

- 7 +11 9 = 16 mod 11 = **5**
- 7 ·11 9 = 63 mod 11 = **8**

**2081: compute each mod value**

- 8 mod 8 = **0**
- -9 mod 4: -9 = 4(-3) + 3, so **3**
- 7 mod 17 = **7**
- 6 mod 7 = **6**
- -8 mod 3: -8 = 3(-3) + 1, so **1**

### Primes, trial division, prime factorization (2078)

- A **prime** is an integer > 1 whose only positive divisors are 1 and itself.
- **Fact:** a composite number n has a prime divisor <= √n.
- **Trial division:** to test whether n is prime, divide by every prime <= √n. If none divides n, it is prime.

**Show 101 is prime:** √101 ≈ 10.05, so test the primes 2, 3, 5, 7.

- 101 is odd, so not divisible by 2.
- Digit sum 1 + 0 + 1 = 2, not divisible by 3.
- Doesn't end in 0 or 5, so not divisible by 5.
- 101 = 7 × 14 + 3, not divisible by 7.

No prime <= 10 divides 101, so **101 is prime.**

### GCD, LCM, relatively prime

- **gcd(a, b):** the largest integer dividing both. **lcm(a, b):** the smallest positive integer divisible by both.
- **Relatively prime:** gcd(a, b) = 1. **Pairwise relatively prime:** gcd(ai, aj) = 1 for every pair.
- **Using prime factorization:** take the minimum exponents for gcd and the maximum for lcm. Example: 120 = 2³·3·5 and 500 = 2²·5³, so gcd = 2²·5 = 20, lcm = 2³·3·5³ = 3000. (Check: gcd × lcm = 60,000 = 120 × 500.)

### Euclidean algorithm (model)

`gcd(a, b) = gcd(b, a mod b)`. Repeat until the remainder is 0; the last non-zero remainder is the gcd.

**gcd(414, 662):**

```
662 = 1 × 414 + 248
414 = 1 × 248 + 166
248 = 1 × 166 + 82
166 = 2 × 82  + 2
 82 = 41 × 2  + 0
```

**gcd(414, 662) = 2.**

### Extended Euclidean algorithm

**Bézout's theorem:** gcd(a, b) can be written as `s·a + t·b` for integers s, t. The extended Euclidean algorithm finds s and t by back-substituting through the Euclid steps.

**gcd(12, 18) (2079):**

```
18 = 1 × 12 + 6
12 = 2 × 6  + 0
```

gcd = 6. Back-substitute: `6 = 18 - 1×12 = (-1)×12 + 1×18`.
**gcd(12, 18) = 6 = (-1)(12) + (1)(18).**

### Modular inverse (2081)

If gcd(a, m) = 1, then a has an inverse modulo m: an integer ā with `a·ā ≡ 1 (mod m)`; it comes from Bézout's coefficient.

**Inverse of 6 in Z25:**
`25 = 4 × 6 + 1`, so `1 = 25 - 4×6`. Therefore `(-4)·6 ≡ 1 (mod 25)`, and `-4 ≡ 21`.
**The inverse of 6 in Z25 is 21.** Check: 6 × 21 = 126 = 5×25 + 1 ✓.

### Linear congruences

To solve `ax ≡ b (mod m)` with gcd(a, m) = 1: find the inverse ā, then `x ≡ ā·b (mod m)`.
Example: `3x ≡ 4 (mod 7)`. The inverse of 3 mod 7 is 5 (15 ≡ 1). So `x ≡ 5 × 4 = 20 ≡ 6 (mod 7)`. Check: 18 mod 7 = 4 ✓.

### Chinese Remainder Theorem (2080, 2082)

**Statement:** let `m1, ..., mn` be pairwise relatively prime positive integers. The system `x ≡ a1 (mod m1), ..., x ≡ an (mod mn)` has a **unique solution modulo M = m1·m2·...·mn**.

**Steps:**

1. Compute `M = m1·m2·...·mn`.
2. For each k, compute `Mk = M / mk`.
3. Find `yk`, the inverse of `Mk` modulo `mk`.
4. `x = a1·M1·y1 + a2·M2·y2 + ... + an·Mn·yn`, then reduce mod M.

**2080: x ≡ 2 (mod 3), x ≡ 3 (mod 5), x ≡ 2 (mod 7)**

- M = 3 × 5 × 7 = 105. M1 = 35, M2 = 21, M3 = 15.
- y1: 35 ≡ 2 (mod 3), and 2 × 2 = 4 ≡ 1, so y1 = 2.
- y2: 21 ≡ 1 (mod 5), so y2 = 1.
- y3: 15 ≡ 1 (mod 7), so y3 = 1.
- x = 2·35·2 + 3·21·1 + 2·15·1 = 140 + 63 + 30 = 233, and 233 mod 105 = 23.

**x ≡ 23 (mod 105).** Check: 23 mod 3 = 2 ✓, 23 mod 5 = 3 ✓, 23 mod 7 = 2 ✓.

**2082: add 13578 and 45730 using CRT**
The sum is 59308. Choose pairwise relatively prime moduli whose product exceeds the sum: **99, 100, 101** (product M = 999,900).

|       | mod 99                   | mod 100                   | mod 101                    |
| ----- | ------------------------ | ------------------------- | -------------------------- |
| 13578 | 15                       | 78                        | 44                         |
| 45730 | 91                       | 30                        | 78                         |
| Sum   | (15 + 91) mod 99 = **7** | (78 + 30) mod 100 = **8** | (44 + 78) mod 101 = **21** |

Solve `x ≡ 7 (mod 99)`, `x ≡ 8 (mod 100)`, `x ≡ 21 (mod 101)`.

- M1 = 999,900 / 99 = 10,100; 10,100 mod 99 = 2, and the inverse of 2 mod 99 is 50, so y1 = 50.
- M2 = 999,900 / 100 = 9,999; 9,999 mod 100 = 99 ≡ -1, so y2 = 99 (since (-1)(-1) = 1).
- M3 = 999,900 / 101 = 9,900; 9,900 mod 101 = 2, and the inverse of 2 mod 101 is 51, so y3 = 51.

x = 7·10,100·50 + 8·9,999·99 + 21·9,900·51 = 3,535,000 + 7,919,208 + 10,602,900 = 22,057,108.
22,057,108 mod 999,900 = 22,057,108 - 22 × 999,900 = **59,308** ✓.

(Any other pairwise coprime set with product > 59,308 works. Your teacher may use 99, 98, 97, 95.)

**Why CRT matters:** it lets a computer do arithmetic on very large integers by working with several small residues in parallel, then combining them.

---

## 10. Sets and Functions

### Sets: representation (2082)

- **Roster (tabular) form:** list the elements: `A = {1, 2, 3, 4}`.
- **Set-builder form:** `A = {x | x is a positive integer less than 5}`.
- **Venn diagram:** circles inside a rectangle (the universal set U).
- **Computer representation (bit string):** order the elements of U; use 1 if the element is in the set, 0 otherwise.

Key terms: **empty set** ∅; **subset** A ⊆ B; **proper subset**; **cardinality** |A|; **equal sets** (same elements).

### Set operations with Venn diagrams (2080)

Example: U = {1, 2, 3, 4, 5, 6, 7, 8}, A = {1, 2, 3, 4}, B = {3, 4, 5, 6}.

| Operation                      | Meaning                | Venn region                    | Result             |
| ------------------------------ | ---------------------- | ------------------------------ | ------------------ |
| **Union** A ∪ B                | In A or B or both      | Both circles shaded            | {1, 2, 3, 4, 5, 6} |
| **Intersection** A ∩ B         | In both A and B        | Overlap only                   | {3, 4}             |
| **Difference** A - B           | In A but not in B      | Circle A minus the overlap     | {1, 2}             |
| **Complement** A'              | In U but not in A      | Everything outside circle A    | {5, 6, 7, 8}       |
| **Symmetric difference** A ⊕ B | In exactly one of A, B | Both circles minus the overlap | {1, 2, 5, 6}       |

### Power set and Cartesian product

- **Power set P(A):** the set of all subsets of A. If |A| = n, then |P(A)| = 2ⁿ.
- **Cartesian product A × B:** all ordered pairs (a, b) with a ∈ A and b ∈ B. |A × B| = |A|·|B|. Order matters: A × B != B × A in general.

**2079: power set of A = {1, 2, 3, 4}** (2⁴ = 16 subsets):

```
∅,
{1}, {2}, {3}, {4},
{1,2}, {1,3}, {1,4}, {2,3}, {2,4}, {3,4},
{1,2,3}, {1,2,4}, {1,3,4}, {2,3,4},
{1,2,3,4}
```

**2078: A³ = A × A × A for A = {a, b, c}** (3³ = 27 ordered triples):

```
(a,a,a) (a,a,b) (a,a,c) (a,b,a) (a,b,b) (a,b,c) (a,c,a) (a,c,b) (a,c,c)
(b,a,a) (b,a,b) (b,a,c) (b,b,a) (b,b,b) (b,b,c) (b,c,a) (b,c,b) (b,c,c)
(c,a,a) (c,a,b) (c,a,c) (c,b,a) (c,b,b) (c,b,c) (c,c,a) (c,c,b) (c,c,c)
```

### Bit-string operations (model, 2081)

Complement = flip all bits. Union = bitwise **OR**. Intersection = bitwise **AND**.

**Model Q6:** U = {1, ..., 10}, A = {1, 2, 3, 4, 5}, B = {1, 3, 5, 7, 9}.

```
A     = 1 1 1 1 1 0 0 0 0 0
B     = 1 0 1 0 1 0 1 0 1 0
A ∪ B = 1 1 1 1 1 0 1 0 1 0  →  {1, 2, 3, 4, 5, 7, 9}
A ∩ B = 1 0 1 0 1 0 0 0 0 0  →  {1, 3, 5}
```

**2081 Q3: U = {0, 1, ..., 9}, positions for 0 through 9:**

| Set               | Elements        | Bit string   |
| ----------------- | --------------- | ------------ |
| a. Even numbers   | {0, 2, 4, 6, 8} | `1010101010` |
| b. Multiples of 5 | {0, 5}          | `1000010000` |
| c. Greater than 7 | {8, 9}          | `0000000011` |
| d. Prime numbers  | {2, 3, 5, 7}    | `0011010100` |

(If your teacher excludes 0 as a multiple of 5, then b = `0000010000`.)

### Functions

A function `f: A → B` assigns to each element of A (domain) exactly one element of B (codomain). The **range** is the set of actual outputs; `f(a) = b` means b is the **image** of a and a is a **pre-image** of b.

| Type                                      | Definition                                                              | Example                                                              |
| ----------------------------------------- | ----------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **One-to-one (injective)**                | `f(a) = f(b)` implies `a = b` (different inputs give different outputs) | `f(x) = x + 1` on integers                                           |
| **Onto (surjective)**                     | Every element of B is the image of some element of A (range = codomain) | `f: {a,b,c,d} → {1,2,3}` with f(a) = 1, f(b) = 2, f(c) = 3, f(d) = 3 |
| **One-to-one correspondence (bijection)** | Both one-to-one and onto                                                | `f(x) = x + 1` from Z to Z                                           |
| **Identity function**                     | `i_A(x) = x` for every x in A                                           | `i(5) = 5`                                                           |

**Counterexamples:**

- Not one-to-one: `f(x) = x²` on integers, since f(2) = f(-2) = 4.
- One-to-one but not onto: `f: {a,b,c} → {1,2,3,4}`, f(a) = 1, f(b) = 2, f(c) = 3 (4 has no pre-image).

**Inverse function** `f⁻¹` exists only if f is a bijection. **Composite function:** `(f ∘ g)(x) = f(g(x))`.

### Floor and ceiling functions (2080, model)

- **Floor ⌊x⌋:** the largest integer less than or equal to x.
- **Ceiling ⌈x⌉:** the smallest integer greater than or equal to x.

| x    | ⌊x⌋ | ⌈x⌉ |
| ---- | --- | --- |
| 3.7  | 3   | 4   |
| 3.2  | 3   | 4   |
| -2.5 | -3  | -2  |
| 5    | 5   | 5   |

Uses: number of bytes needed for n bits is ⌈n/8⌉; pigeonhole principle uses ⌈N/k⌉.

### Boolean function (2081, 2082, model)

Let B = {0, 1}. A **Boolean function of degree n** is a function `f: Bⁿ → B`. It takes n binary inputs and gives a binary output. Built from the operations: **complement** x' (NOT), **Boolean sum** x + y (OR), **Boolean product** x·y (AND).

**Example:** `F(x, y) = x·y'`

| x   | y   | y'  | F = x·y' |
| --- | --- | --- | -------- |
| 0   | 0   | 1   | 0        |
| 0   | 1   | 0   | 0        |
| 1   | 0   | 1   | **1**    |
| 1   | 1   | 0   | 0        |

Another: `F(x, y, z) = x·y + z'` is a Boolean function of degree 3. Boolean functions model logic circuits.

### Exponential function (2081, 2082)

A function of the form `f(x) = a^x` with a base a > 0, a != 1. Examples: `f(n) = 2ⁿ`. Properties: `a^x · a^y = a^(x+y)`, `(a^x)^y = a^(xy)`. Its inverse is the **logarithm**. It grows faster than any polynomial, which is why exponential-time algorithms are infeasible for large n (the power set of an n-element set has 2ⁿ elements).

---

## 11. Relations

### Basics

A **relation R from A to B** is a subset of A × B. A **relation on A** is a subset of A × A. Notation: `(a, b) ∈ R` or `a R b`. A function is a special relation where every a appears as the first element of exactly one pair.

### Properties of a relation on set A

| Property          | Definition                                         |
| ----------------- | -------------------------------------------------- |
| **Reflexive**     | `(a, a) ∈ R` for every a ∈ A                       |
| **Symmetric**     | If `(a, b) ∈ R` then `(b, a) ∈ R`                  |
| **Antisymmetric** | If `(a, b) ∈ R` and `(b, a) ∈ R` then `a = b`      |
| **Transitive**    | If `(a, b) ∈ R` and `(b, c) ∈ R` then `(a, c) ∈ R` |

### Representing relations using a matrix (2078, 2080)

For a relation R from `A = {a1, ..., am}` to `B = {b1, ..., bn}`, the **zero-one matrix** `M_R = [m_ij]` has `m_ij = 1` if `(ai, bj) ∈ R` and 0 otherwise.

**2078 example:** A = {1, 2, 3}, B = {1, 2}, R = {(a, b) | a > b}.
R = {(2, 1), (3, 1), (3, 2)}. Rows = a1, a2, a3; columns = b1, b2:

```
        b1 b2
 a1=1 [  0  0 ]
 a2=2 [  1  0 ]
 a3=3 [  1  1 ]
```

For a relation on a single set, the matrix is square. Reflexive: all 1s on the diagonal. Symmetric: the matrix equals its transpose.

### Representing relations using a directed graph (model)

Draw each element as a vertex. For every pair `(a, b) ∈ R`, draw an **arrow from a to b**. A pair `(a, a)` is drawn as a **loop**.

**Model Q8:** R = {(1,1), (1,3), (2,1), (2,3), (2,4), (3,1), (3,2), (4,1)} on {1, 2, 3, 4}.
Draw four vertices 1, 2, 3, 4 and these arrows:

```
loop at 1
1 → 3
2 → 1,  2 → 3,  2 → 4
3 → 1,  3 → 2
4 → 1
```

Matrix (rows = from, columns = to):

```
      1  2  3  4
 1 [  1  0  1  0 ]
 2 [  1  0  1  1 ]
 3 [  1  1  0  0 ]
 4 [  1  0  0  0 ]
```

### Equivalence relation (2079)

A relation that is **reflexive, symmetric, and transitive**.

**Example:** on the integers, `a R b` if and only if `a ≡ b (mod 3)`.

- Reflexive: `a - a = 0`, divisible by 3.
- Symmetric: if 3 divides `a - b`, then 3 divides `b - a`.
- Transitive: if `a - b = 3k` and `b - c = 3l`, then `a - c = 3(k + l)`.

**Equivalence classes:** `[a] = {x | x R a}`. Here: `[0] = {..., -3, 0, 3, 6, ...}`, `[1] = {..., -2, 1, 4, ...}`, `[2] = {..., -1, 2, 5, ...}`. The classes partition the integers into three disjoint sets.

### Partial ordering (2081, 2082)

A relation that is **reflexive, antisymmetric, and transitive**. The set with the relation is a **partially ordered set (poset)**.

**Examples:** `≤` on integers; "divides" on positive integers; `⊆` on subsets of a set.

- Elements a, b are **comparable** if `a ≼ b` or `b ≼ a`; otherwise **incomparable** (e.g., 2 and 3 under "divides").
- If every pair is comparable, it is a **total order** (e.g., `≤`).
- A **Hasse diagram** draws a poset: remove loops, remove edges implied by transitivity, and draw all arrows pointing upward (omit arrowheads).

### Closures

- **Reflexive closure:** add `(a, a)` for all a.
- **Symmetric closure:** `R ∪ R⁻¹` (add the reverse of every pair).
- **Transitive closure:** add pairs until the relation is transitive (the union of R, R², R³, ...).

---

## 12. Logic and Rules of Inference

### Propositions (2079, 2081)

A **proposition** is a declarative sentence that is either **true or false, but not both**.

**Four examples that are NOT propositions (2079):**

1. "What time is it?" (a question)
2. "Close the door." (a command)
3. "x + 2 = 5" (depends on x; open sentence)
4. "What a beautiful day!" (an exclamation)

### Logical connectives and precedence

| Connective    | Symbol | Meaning                                                |
| ------------- | ------ | ------------------------------------------------------ |
| Negation      | ¬p     | not p                                                  |
| Conjunction   | p ∧ q  | p and q                                                |
| Disjunction   | p ∨ q  | p or q (inclusive)                                     |
| Exclusive or  | p ⊕ q  | p or q but not both                                    |
| Conditional   | p → q  | if p then q (false only when p is true and q is false) |
| Biconditional | p ↔ q  | p if and only if q                                     |

**Precedence (highest to lowest):** ¬, ∧, ∨, →, ↔.

### Converse, inverse, contrapositive (model)

For `p → q`:

- **Converse:** `q → p`
- **Inverse:** `¬p → ¬q`
- **Contrapositive:** `¬q → ¬p`

The contrapositive is **logically equivalent** to the original. The converse and inverse are equivalent to each other but **not** to the original.

**Show "if it is hot today then today is Sunday" ≡ "if it is not Sunday then today is not hot":**
Let p = "it is hot today", q = "today is Sunday". The first statement is `p → q`. The second is `¬q → ¬p`, the contrapositive.

| p   | q   | p → q | ¬q → ¬p |
| --- | --- | ----- | ------- |
| T   | T   | T     | T       |
| T   | F   | F     | F       |
| F   | T   | T     | T       |
| F   | F   | T     | T       |

The columns are identical, so they are logically equivalent. ∎

### Tautology (2078)

A **tautology** is a compound proposition that is true for **all** truth values of its variables. A **contradiction** is always false. A **contingency** is neither.

**Show `(p ∧ q) → (p ∨ q)` is a tautology:**

| p   | q   | p ∧ q | p ∨ q | (p ∧ q) → (p ∨ q) |
| --- | --- | ----- | ----- | ----------------- |
| T   | T   | T     | T     | T                 |
| T   | F   | F     | T     | T                 |
| F   | T   | F     | T     | T                 |
| F   | F   | F     | F     | T                 |

The last column is all T, so it is a tautology. ∎

**Symbolic proof:** `(p ∧ q) → (p ∨ q) ≡ ¬(p ∧ q) ∨ (p ∨ q) ≡ ¬p ∨ ¬q ∨ p ∨ q ≡ (p ∨ ¬p) ∨ (q ∨ ¬q) ≡ T ∨ T ≡ T`. ∎

### Key equivalences

- **De Morgan:** `¬(p ∧ q) ≡ ¬p ∨ ¬q`; `¬(p ∨ q) ≡ ¬p ∧ ¬q`
- **Conditional:** `p → q ≡ ¬p ∨ q ≡ ¬q → ¬p`
- **Double negation:** `¬¬p ≡ p`
- **Distributive:** `p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)`
- **Identity/domination:** `p ∧ T ≡ p`, `p ∨ F ≡ p`, `p ∨ T ≡ T`, `p ∧ F ≡ F`
- **Absorption:** `p ∨ (p ∧ q) ≡ p`

### Predicates and quantifiers (2080, 2081, 2082)

**Why we need quantifiers (2082):** propositional logic can't express statements about _all_ or _some_ members of a collection, or statements with variables, such as "every student in the class passed". Quantifiers do this.

- **Predicate** `P(x)`: a statement with a variable that becomes a proposition when x is given a value.
- **Universal quantifier** `∀x P(x)`: P(x) is true for **all** x in the domain.
- **Existential quantifier** `∃x P(x)`: P(x) is true for **at least one** x.
- **Negation:** `¬∀x P(x) ≡ ∃x ¬P(x)` and `¬∃x P(x) ≡ ∀x ¬P(x)`.
- **Nested quantifiers:** e.g., `∀x ∃y (x + y = 0)` is true over integers; `∃y ∀x (x + y = 0)` is false. **Order matters.**
- A variable that is bound by a quantifier is a **bound** variable; otherwise it is **free**.

### Translating to logical expressions

**2080:**

- (a) "Not all good people are heroes": with G(x): x is good, H(x): x is a hero: `¬∀x (G(x) → H(x)) ≡ ∃x (G(x) ∧ ¬H(x))`.
- (b) "Every person in our country is loyal": with P(x): x is a person in our country, L(x): x is loyal: `∀x (P(x) → L(x))`.
- (c) "Some people hate good people": with P(x): x is a person, G(y): y is good, Hate(x, y): x hates y: `∃x ∃y (P(x) ∧ G(y) ∧ Hate(x, y))`.

**2081:**

- (a) "Some kind-hearted people do still exist": with K(x): x is a kind-hearted person: `∃x K(x)`.
- (b) "Students who study hard and do the homework get good marks": with S(x): x studies hard, H(x): x does the homework, M(x): x gets good marks (domain: students): `∀x ((S(x) ∧ H(x)) → M(x))`.

### Rules of inference

| Rule                       | Form                  |
| -------------------------- | --------------------- |
| **Modus ponens**           | p, p → q ∴ q          |
| **Modus tollens**          | ¬q, p → q ∴ ¬p        |
| **Hypothetical syllogism** | p → q, q → r ∴ p → r  |
| **Disjunctive syllogism**  | p ∨ q, ¬p ∴ q         |
| **Addition**               | p ∴ p ∨ q             |
| **Simplification**         | p ∧ q ∴ p             |
| **Conjunction**            | p, q ∴ p ∧ q          |
| **Resolution**             | p ∨ q, ¬p ∨ r ∴ q ∨ r |

**Quantifier rules:**

- **Universal instantiation (UI):** `∀x P(x)` ∴ `P(c)` for any c in the domain.
- **Universal generalization (UG):** `P(c)` for an arbitrary c ∴ `∀x P(x)`.
- **Existential instantiation (EI):** `∃x P(x)` ∴ `P(c)` for some element c.
- **Existential generalization (EG):** `P(c)` for some c ∴ `∃x P(x)`.

**Fallacies:** _affirming the conclusion_ (from `p → q` and q, concluding p) and _denying the hypothesis_ (from `p → q` and ¬p, concluding ¬q). Both are invalid.

### 2079: "Sam is naughty"

Let O(x): x is oversmart, S(x): x is stupid, C(x, y): x is a child of y, N(x): x is naughty.

Premises:

1. `∀x (O(x) → S(x))`
2. `∀x ∀y ((S(y) ∧ C(x, y)) → N(x))`
3. `O(John)`
4. `C(Sam, John)`

Proof:

| Step | Statement                           | Reason              |
| ---- | ----------------------------------- | ------------------- |
| 1    | `∀x (O(x) → S(x))`                  | Premise             |
| 2    | `O(John) → S(John)`                 | UI on 1             |
| 3    | `O(John)`                           | Premise             |
| 4    | `S(John)`                           | Modus ponens (2, 3) |
| 5    | `∀x ∀y ((S(y) ∧ C(x, y)) → N(x))`   | Premise             |
| 6    | `(S(John) ∧ C(Sam, John)) → N(Sam)` | UI on 5             |
| 7    | `C(Sam, John)`                      | Premise             |
| 8    | `S(John) ∧ C(Sam, John)`            | Conjunction (4, 7)  |
| 9    | `N(Sam)`                            | Modus ponens (6, 8) |

**Sam is naughty.** ∎

---

## 13. Recursion and Structural Induction

### Recursive definitions (2079, model)

A recursive definition has a **basis** (initial values) and a **recursive step** (rule using earlier values).

**Recursively defined function:** a function whose value at n is defined using its values at smaller arguments.

- Factorial: `f(0) = 1`, `f(n+1) = (n+1)·f(n)`.
- Fibonacci: `f(0) = 0`, `f(1) = 1`, `f(n) = f(n-1) + f(n-2)`.

**2079: f(0) = 3, f(n+1) = 2f(n) + 3**

- f(1) = 2·3 + 3 = **9**
- f(2) = 2·9 + 3 = **21**
- f(3) = 2·21 + 3 = **45**
- f(4) = 2·45 + 3 = **93**

**Recursively defined set:** Let S be defined by: (1) `3 ∈ S`; (2) if `x ∈ S` and `y ∈ S`, then `x + y ∈ S`. Then S = {3, 6, 9, 12, ...}.

### Structural induction (2081)

Used to prove properties of recursively defined sets/structures.

1. **Basis step:** show the property holds for the initial elements.
2. **Recursive step:** show that if the property holds for the elements used to build a new element, it holds for the new element.

**Example:** every element of the set S above (3 ∈ S; x, y ∈ S ⟹ x + y ∈ S) is divisible by 3.

- Basis: 3 is divisible by 3.
- Recursive step: if x and y are divisible by 3, then x + y is divisible by 3.
  So every element of S is divisible by 3. ∎

### Proving a recursive algorithm correct (2080, 2082)

Use ordinary induction on the input size, mirroring the algorithm's structure: the base case is the stopping case; the inductive step assumes the recursive call is correct and shows the full call is correct.

**2082: `Power(a, n)`**

```
Power(a, n) {
    if (n == 0) return 1;
    else return a * Power(a, n-1);
}
```

**Claim:** `Power(a, n)` returns `a^n` for all integers n >= 0.

- **Basis (n = 0):** the algorithm returns 1 = a⁰. Correct.
- **Inductive step:** assume `Power(a, k)` correctly returns a^k. Then `Power(a, k+1)` (since k+1 > 0) returns `a * Power(a, k) = a · a^k = a^(k+1)`. Correct.

By induction, `Power(a, n)` is correct for all n >= 0. ∎

(The same template proves a recursive factorial correct: basis `fact(0) = 1`; step `fact(k+1) = (k+1)·fact(k) = (k+1)·k! = (k+1)!`.)

---

## 14. Randomized Algorithms and Probability

### Randomized algorithms (2081, 2082)

A **randomized algorithm** makes random choices (e.g., coin flips, random numbers) during execution, so its behaviour can differ from run to run, even on the same input.

**Uses / advantages:**

- **Simplicity:** often much simpler than the best deterministic algorithm.
- **Speed:** good _expected_ running time (e.g., randomized quicksort picks a random pivot, avoiding the worst case on bad inputs).
- **Defeats adversarial inputs:** no single input is consistently bad.
- **Solves hard problems efficiently:** e.g., primality testing (Miller-Rabin), hashing, load balancing, approximate counting.
- Well suited to parallel and distributed computing.

**Disadvantages:** _Monte Carlo_ algorithms may give a wrong answer with small probability; _Las Vegas_ algorithms are always correct but have a random running time.

### Discrete probability

- **Probability of an event E** in a finite sample space S with equally likely outcomes: `P(E) = |E| / |S|`.
- **Complement:** `P(E') = 1 - P(E)`.
- **Union:** `P(E1 ∪ E2) = P(E1) + P(E2) - P(E1 ∩ E2)`.
- **Conditional probability:** `P(E | F) = P(E ∩ F) / P(F)`.
- **Independent events:** `P(E ∩ F) = P(E)·P(F)`.
- **Random variable:** a function from the sample space to the real numbers.
- **Expected value:** `E(X) = Σ P(s)·X(s)`. **Variance:** `V(X) = E(X²) - [E(X)]²`.

**Example:** for a fair die, `E(X) = (1+2+3+4+5+6)/6 = 3.5`. The probability of getting an even number is 3/6 = 1/2.

**Hashing:** a hash function such as `h(k) = k mod m` maps keys to m slots; a **collision** occurs when two keys map to the same slot. With k keys and m slots, the probability that no collisions occur is `(m/m)·((m-1)/m)·...·((m-k+1)/m)`.

---

## 15. Syllabus Extras (not yet asked)

These are on the syllabus but didn't appear in the past papers. Read them only after everything above is solid.

### Boolean (zero-one) matrices

For zero-one matrices A and B of the same size:

- **Join** `A ∨ B`: entry-wise OR.
- **Meet** `A ∧ B`: entry-wise AND.
- **Boolean product** `A ⊙ B`: `c_ij = (a_i1 ∧ b_1j) ∨ (a_i2 ∧ b_2j) ∨ ... ∨ (a_ik ∧ b_kj)`. It is like matrix multiplication, but using AND for multiplication and OR for addition.
- **Boolean power** `A^[r]`: the Boolean product of A with itself r times.

Example: A = [[1, 0], [1, 1]], B = [[0, 1], [1, 0]].

- A ∨ B = [[1, 1], [1, 1]]. A ∧ B = [[0, 0], [1, 0]].
- A ⊙ B: c11 = (1∧0) ∨ (0∧1) = 0; c12 = (1∧1) ∨ (0∧0) = 1; c21 = (1∧0) ∨ (1∧1) = 1; c22 = (1∧1) ∨ (1∧0) = 1. So A ⊙ B = [[0, 1], [1, 1]].

### Integer representations

- **Binary** (base 2), **octal** (base 8), **hexadecimal** (base 16, digits 0-9 and A-F).
- **Decimal to base b:** repeatedly divide by b and read the remainders from last to first. Example: 156 → 156/2 = 78 r0, 39 r0, 19 r1, 9 r1, 4 r1, 2 r0, 1 r0, 0 r1, giving `(10011100)₂`.
- **Binary to octal / hex:** group bits in 3s / 4s from the right. `(10011100)₂ = (234)₈ = (9C)₁₆`.

### Graph colouring

A **colouring** assigns colours to vertices so that no two adjacent vertices share a colour. The **chromatic number** χ(G) is the minimum number of colours needed. Examples: χ(Kn) = n; χ(bipartite graph) = 2 (if it has an edge); χ(C_n) = 2 (n even) or 3 (n odd). **Four colour theorem:** every planar graph can be coloured with at most 4 colours. **Applications:** map colouring, exam scheduling (courses that share students must have different time slots), register allocation.

### Other graph topics

- **Travelling salesman problem:** find the shortest Hamilton circuit in a weighted complete graph. NP-hard; solved by brute force for small n, heuristics otherwise.
- **Matching:** a set of edges with no shared vertices. In a bipartite graph, a **complete matching** from V1 to V2 matches every vertex of V1. **Hall's theorem:** a complete matching exists if and only if `|N(A)| >= |A|` for every subset A of V1.

### Trees: applications

- **Binary search tree:** left subtree values < node < right subtree values; supports fast search, insertion and deletion.
- **Decision tree:** each internal node is a decision, each leaf is an outcome (e.g., minimum comparisons for sorting is ⌈log₂ n!⌉).
- **Prefix codes:** no code word is a prefix of another; represented as a binary tree with symbols at leaves (Huffman coding builds the optimal one).
