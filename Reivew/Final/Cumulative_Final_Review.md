# Theory of Computation - Cumulative Final Review

**Course Coverage:** All topics from Regular Languages through Time Complexity  
**Reference Materials:** Exam 1 & 2 reviews, Class slides, Notes

---

## Table of Contents

1. [Language Hierarchy Overview](#1-language-hierarchy-overview)
2. [Regular Languages](#2-regular-languages)
3. [Context-Free Languages](#3-context-free-languages)
4. [Turing Machines](#4-turing-machines)
5. [Decidability](#5-decidability)
6. [Reducibility](#6-reducibility)
7. [Time Complexity](#7-time-complexity)
8. [Key Theorems and Results](#8-key-theorems-and-results)
9. [Problem-Solving Strategies](#9-problem-solving-strategies)
10. [Quick Reference](#10-quick-reference)

---

## 1. Language Hierarchy Overview

### The Chomsky Hierarchy

```
Recursively Enumerable (RE) Languages
    ↑
Context-Sensitive Languages
    ↑
Context-Free Languages (CFL)
    ↑
Regular Languages
```

### Computational Models

| Language Class | Automaton | Grammar | Closure Properties |
|----------------|-----------|---------|-------------------|
| **Regular** | DFA, NFA | Regular Grammar | Union, Concatenation, Star, Complement, Intersection |
| **Context-Free** | PDA (nondeterministic) | CFG | Union, Concatenation, Star (NOT Complement, Intersection) |
| **Turing-Recognizable** | Turing Machine | - | Union, Intersection (NOT Complement) |
| **Turing-Decidable** | Decider TM | - | Union, Intersection, Complement |

### Key Relationships

- **Regular ⊆ Context-Free ⊆ Turing-Recognizable**
- Every DFA is a PDA (ignoring stack)
- Every PDA is a TM (using tape as stack)
- Deterministic PDAs ⊂ Nondeterministic PDAs
- Turing-Decidable ⊆ Turing-Recognizable

---

## 2. Regular Languages

### 2.1 Finite Automata

#### Deterministic Finite Automaton (DFA)

**Formal Definition:** $M = (Q, \Sigma, \delta, q_0, F)$
- $Q$: Finite set of states
- $\Sigma$: Input alphabet
- $\delta: Q \times \Sigma \rightarrow Q$: Transition function
- $q_0 \in Q$: Start state
- $F \subseteq Q$: Accept states

**Acceptance:** String $w$ is accepted if $\delta^*(q_0, w) \in F$

#### Nondeterministic Finite Automaton (NFA)

**Formal Definition:** $N = (Q, \Sigma, \delta, q_0, F)$
- $\delta: Q \times \Sigma_\varepsilon \rightarrow \mathcal{P}(Q)$: Transition function
- Can have multiple transitions, $\varepsilon$-transitions, or no transition

**Acceptance:** String $w$ is accepted if **any** computation path leads to an accept state

#### Equivalence: DFA = NFA

**Theorem 1.39:** Every NFA has an equivalent DFA.

**Subset Construction:**
- DFA states = subsets of NFA states
- If NFA has $n$ states, DFA has at most $2^n$ states
- This bound is tight (exponential blowup can occur)

### 2.2 Regular Expressions

**Operations:**
- Union: $R_1 \cup R_2$ (or $R_1 | R_2$)
- Concatenation: $R_1 R_2$
- Kleene Star: $R^*$ (zero or more repetitions)

**Precedence:** Star > Concatenation > Union

**Equivalence:** Regular Expressions = DFAs = NFAs = Regular Grammars

**Converting DFA → Regular Expression:** GNFA method
1. Convert DFA to GNFA (add start/accept states)
2. Remove states one by one
3. Final edge label is the regular expression

### 2.3 Regular Grammars

**Right-Linear Form:**
- $A \to xB$ or $A \to x$ where $x \in \Sigma^*$

**Left-Linear Form:**
- $A \to Bx$ or $A \to x$

**Conversion:**
- DFA → Regular Grammar: Each state becomes nonterminal, transitions become productions
- Regular Grammar → DFA: Each nonterminal becomes state, productions become transitions

### 2.4 Pumping Lemma for Regular Languages

**Statement:** If $L$ is regular, then there exists pumping length $p$ such that for any string $s \in L$ with $|s| \geq p$, we can write $s = xyz$ where:
1. $|y| > 0$
2. $|xy| \leq p$
3. For all $i \geq 0$, $xy^iz \in L$

**Use:** Prove languages are **NOT regular** by contradiction

**Strategy:**
1. Assume $L$ is regular
2. Choose string $s \in L$ with $|s| \geq p$ (cleverly!)
3. Show for all splits $s = xyz$ (satisfying conditions), some $xy^iz \notin L$
4. Contradiction → $L$ is not regular

**Common Choices:** $0^p1^p$, $0^{p!}$, $1^{2^p}$

### 2.5 Closure Properties

**Regular languages are closed under:**
- Union (NFA with $\varepsilon$-transitions)
- Concatenation (NFA with $\varepsilon$-transitions)
- Star (NFA with loops)
- Complement (swap accept/reject in DFA)
- Intersection (product construction)
- Set Difference (product construction)

---

## 3. Context-Free Languages

### 3.1 Context-Free Grammars (CFG)

**Formal Definition:** $G = (V, \Sigma, R, S)$
- $V$: Nonterminals (variables)
- $\Sigma$: Terminals
- $R$: Production rules of form $A \to w$ where $A \in V$, $w \in (V \cup \Sigma)^*$
- $S$: Start symbol

**Language:** $L(G) = \{w \in \Sigma^* \mid S \Rightarrow^* w\}$

**Derivations:**
- Leftmost: Always expand leftmost nonterminal
- Rightmost: Always expand rightmost nonterminal
- Parse tree: Tree representation of derivation

**Example:** Consider grammar $G$ with productions:
- $S \to aSb \mid ab$

**Leftmost derivation for string "aabb":**
$S \Rightarrow aSb \Rightarrow aabb$

(Step 1: Apply $S \to aSb$. Step 2: Apply $S \to ab$ to the middle $S$. At each step, the leftmost nonterminal is expanded.)

**Rightmost derivation for string "aabb":**
$S \Rightarrow aSb \Rightarrow aabb$

(For this grammar, leftmost and rightmost derivations are the same because there is only one nonterminal at each step)

**Parse tree for "aabb":**
```
    S
   /|\
  a S b
   / \
  a   b
```

**Example with different leftmost/rightmost derivations:** Grammar:
- $E \to E + T \mid T$
- $T \to T * F \mid F$
- $F \to (E) \mid id$

**Leftmost derivation for "id + id * id":**
$E \Rightarrow E + T \Rightarrow T + T \Rightarrow F + T \Rightarrow id + T \Rightarrow id + T * F \Rightarrow id + F * F \Rightarrow id + id * F \Rightarrow id + id * id$

**Rightmost derivation for "id + id * id":**
$E \Rightarrow E + T \Rightarrow E + T * F \Rightarrow E + T * id \Rightarrow E + F * id \Rightarrow E + id * id \Rightarrow T + id * id \Rightarrow F + id * id \Rightarrow id + id * id$

**Notice:** For each step in the left or rightmost derivation, it strictly expands the left or right nonterminal until the nonterminal is replaced by a terminal before moving on to the next nonterminal.

**Chomsky Normal Form (CNF):**
- All productions: $A \to BC$ or $A \to a$
- Every CFL has a grammar in CNF

**Conversion to CNF (5 steps):**
1. Add new start variable (if $S$ appears on RHS)
2. Eliminate $\varepsilon$-rules ($A \to \varepsilon$)
3. Eliminate unit rules ($A \to B$)
4. Patch up grammar
5. Convert to CNF form (introduce terminal nonterminals, break long sequences)

**Ambiguity:**
- Grammar is ambiguous if some string has multiple leftmost derivations
- Some languages are inherently ambiguous

**Example of Ambiguous Grammar:** Consider grammar $G$ with productions:
- $E \to E + E \mid E * E \mid id$

This grammar is ambiguous because the string "id + id * id" has two different leftmost derivations:

**Leftmost Derivation 1** (addition before multiplication):
$E \Rightarrow E + E \Rightarrow id + E \Rightarrow id + E * E \Rightarrow id + id * E \Rightarrow id + id * id$

**Leftmost Derivation 2** (multiplication before addition):
$E \Rightarrow E * E \Rightarrow E + E * E \Rightarrow id + E * E \Rightarrow id + id * E \Rightarrow id + id * id$

These correspond to two different parse trees:
- **Tree 1:** $(id + id) * id$ (addition grouped first)
- **Tree 2:** $id + (id * id)$ (multiplication grouped first)

**To remove ambiguity:** Use a grammar with precedence rules:
- $E \to E + T \mid T$ (addition at outer level)
- $T \to T * F \mid F$ (multiplication at inner level)
- $F \to (E) \mid id$ (parentheses and identifiers)

This unambiguous grammar forces multiplication to bind tighter than addition.

### 3.2 Pushdown Automata (PDA)

**Formal Definition:** $P = (Q, \Sigma, \Gamma, \delta, q_0, F)$
- $Q$: States
- $\Sigma$: Input alphabet
- $\Gamma$: Stack alphabet
- $\delta: Q \times \Sigma_\varepsilon \times \Gamma_\varepsilon \rightarrow \mathcal{P}(Q \times \Gamma_\varepsilon)$
- $q_0$: Start state
- $F$: Accept states

**Acceptance Methods:**
- **Final State:** End in accept state after reading input
- **Empty Stack:** Stack empty after reading input
- **Equivalence:** Both methods are equivalent

**Transition Notation:** $a, b \to c$
- $a$: Input symbol to read ($\varepsilon$ = no read)
- $b$: Stack symbol to pop ($\varepsilon$ = no pop)
- $c$: Stack symbol to push ($\varepsilon$ = no push)

**Equivalence:** CFG = Nondeterministic PDA

**CFG → PDA (Standard Construction):**
- **Key Idea:** Simulate leftmost derivations using the stack
- **Construction:**
  1. Push start symbol $S$ onto stack
  2. For each production $A \to w$ in grammar:
     - Add transition: $\varepsilon, A \to w$ (pop $A$, push $w$ in reverse)
  3. For each terminal $a$:
     - Add transition: $a, a \to \varepsilon$ (read $a$ from input, pop $a$ from stack)
  4. Accept by empty stack (or final state)
- **How it works:** Stack holds the sentential form of leftmost derivation. When nonterminal is on top, expand it. When terminal is on top, match it with input.
- **Example:** For grammar $S \to aSb \mid ab$, PDA:
  - $\varepsilon, S \to bSa$ (for $S \to aSb$, reversed)
  - $\varepsilon, S \to ba$ (for $S \to ab$, reversed)
  - $a, a \to \varepsilon$ and $b, b \to \varepsilon$ (match terminals)

**PDA → CFG (State Pair Construction):**
- **Key Idea:** Variables $A_{pq}$ represent "path from state $p$ to state $q$ that empties stack"
- **Construction:**
  1. For each transition $\delta(p, a, A) \ni (q, B_1B_2\ldots B_k)$:
     - Create variables for intermediate states
     - Add productions: $A_{pq} \to a B_{1,r_1} B_{2,r_2} \ldots B_{k,r_k}$ for all state sequences
  2. For each transition $\delta(p, a, A) \ni (q, \varepsilon)$:
     - Add production: $A_{pq} \to a$
  3. Start variable: $S = A_{q_0,q_{accept}}$ (or all accept states)
- **Intuition:** $A_{pq}$ generates strings that take PDA from state $p$ to $q$ while popping $A$ from stack
- **Complexity:** Requires considering all possible intermediate state sequences, leading to many variables

**Deterministic PDAs:** Recognize proper subset of CFLs (deterministic CFLs)

### 3.3 Pumping Lemma for Context-Free Languages

**Statement:** If $L$ is context-free, then there exists pumping length $p$ such that for any string $w \in L$ with $|w| \geq p$, we can write $w = uvxyz$ where:
1. $|vxy| \leq p$
2. $|vy| \geq 1$
3. For all $i \geq 0$, $uv^ixy^iz \in L$

**Key Difference from Regular:** 5 parts instead of 3 (due to branching in parse trees)

**Use:** Prove languages are **NOT context-free**

**Common Choices:** $a^pb^pc^p$, $a^pc^pb^pd^p$

**Case Analysis:** Since $|vxy| \leq p$, consider:
- $vxy$ contained in one block
- $vxy$ straddles boundaries

### 3.4 Closure Properties

**Context-free languages are closed under:**
- Union (CFG: $S \to S_1 \mid S_2$)
- Concatenation (CFG: $S \to S_1 S_2$)
- Star (CFG: $S \to S_1 S \mid \varepsilon$)

**Context-free languages are NOT closed under:**
- Complement (would imply closure under intersection)
- Intersection (counterexample: $\{a^nb^nc^n\}$)

**Regular ⊆ Context-Free:**
- Every DFA is a PDA (ignore stack)
- Every regular language is context-free

---

## 4. Turing Machines

### 4.1 Formal Definition

**Turing Machine:** $M = (Q, \Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject})$
- $Q$: States
- $\Sigma$: Input alphabet (does not contain $\sqcup$)
- $\Gamma$: Tape alphabet ($\sqcup \in \Gamma$, $\Sigma \subseteq \Gamma$)
- $\delta: Q \times \Gamma \rightarrow Q \times \Gamma \times \{L, R\}$
- $q_0$: Start state
- $q_{accept}$: Accept state
- $q_{reject}$: Reject state

**Transition:** $\delta(q, a) = (r, b, D)$
- In state $q$, reading $a$
- Go to state $r$, write $b$, move direction $D$ (Left/Right)

**Configuration:** $uqv$ (tape content, current state, head position)

### 4.2 Language Classes

#### Turing-Recognizable (Recursively Enumerable)
- Language $L$ is recognizable if some TM accepts all strings in $L$
- TM may loop forever on strings not in $L$

#### Turing-Decidable (Recursive)
- Language $L$ is decidable if some TM:
  - Accepts all strings in $L$
  - Rejects all strings not in $L$
- TM **always halts** on every input

**Relationship:** Decidable ⊆ Recognizable

### 4.3 Variants of Turing Machines

**All variants are equivalent:**
- Multitape TM = Single-tape TM
- Nondeterministic TM = Deterministic TM
- Enumerator = Turing-recognizable languages

**Simulation Techniques:**
- Multitape: Use separators and marked symbols
- Nondeterministic: BFS on computation tree

### 4.4 The Church-Turing Thesis

**Statement:** "The intuitive notion of algorithms equals Turing machine algorithms"

**Implications:**
- TMs capture all computable functions
- If no TM can solve a problem, no algorithm can
- Establishes TMs as formal model of computation

---

## 5. Decidability

### 5.1 Decidable Languages

**Definition:** A language $L$ is **decidable** if there exists a Turing machine $M$ (called a **decider**) that:
- Accepts all strings in $L$
- Rejects all strings not in $L$
- **Always halts** on every input

**Key Examples:**

**$A_{DFA}$ = $\{\langle M, w \rangle \mid M$ is a DFA that accepts $w\}$** ✓ Decidable
- **Decider:** Simulate $M$ on input $w$ step by step
- Since DFAs always halt (finite computation), simulation terminates
- Accept if $M$ ends in accept state, reject otherwise
- **Time complexity:** $O(|w|)$
  - **Derivation:** Process each symbol of $w$ exactly once
  - For each symbol $w[i]$, perform one transition lookup: $\delta(\text{current\_state}, w[i])$
  - Total operations: $|w|$ transitions, each taking constant time
  - Therefore: $O(|w|)$

**$A_{NFA}$ = $\{\langle N, w \rangle \mid N$ is an NFA that accepts $w\}$** ✓ Decidable
- **Decider:** Convert NFA to equivalent DFA (subset construction), then simulate
- Or: Simulate NFA by tracking all possible states simultaneously
- **Time complexity:** $O(2^{|Q|} \cdot |w|)$ where $Q$ is set of states
  - **Derivation (Subset Construction Method):**
    - **Step 1:** Convert NFA to DFA using subset construction
      - DFA states are subsets of NFA states
      - Worst case: $2^{|Q|}$ possible subsets (exponential blowup)
      - Construction time: $O(2^{|Q|} \cdot |\Sigma|)$ where $\Sigma$ is alphabet
    - **Step 2:** Simulate resulting DFA on $w$
      - DFA has at most $2^{|Q|}$ states
      - Process $|w|$ symbols, each requiring transition lookup
      - Simulation time: $O(2^{|Q|} \cdot |w|)$
    - **Total:** $O(2^{|Q|} \cdot |\Sigma|) + O(2^{|Q|} \cdot |w|) = O(2^{|Q|} \cdot |w|)$ (assuming $|w| \geq |\Sigma|$)
  - **Alternative (Direct Simulation):** Track set of possible states, update for each symbol: also $O(2^{|Q|} \cdot |w|)$

**$A_{REX}$ = $\{\langle R, w \rangle \mid R$ is a regex that matches $w\}$** ✓ Decidable
- **Decider:** Convert regex to equivalent NFA, then use $A_{NFA}$ decider
- **Time complexity:** Exponential in worst case (due to NFA conversion)
  - **Derivation:**
    - **Step 1:** Convert regex $R$ to NFA
      - Regex to NFA conversion: $O(|R|)$ states (linear in regex length)
      - However, regex can be exponentially more concise than equivalent NFA
    - **Step 2:** Convert NFA to DFA (subset construction)
      - NFA from regex has $O(|R|)$ states
      - DFA can have up to $2^{O(|R|)}$ states (exponential blowup)
      - Example: Regex $(0|1)^*0(0|1)^{n-1}$ requires DFA with $2^n$ states
    - **Step 3:** Simulate DFA on $w$: $O(2^{|R|} \cdot |w|)$
    - **Total:** Exponential in $|R|$ due to subset construction

**$A_{CFG}$ = $\{\langle G, w \rangle \mid G$ is a CFG that generates $w\}$** ✓ Decidable
- **Decider:** Use CYK algorithm or convert to CNF and check all derivations
- For CNF: Check all possible parse trees of length $2|w|-1$ (since CNF trees are binary)
- **Time complexity:** $O(|w|^3 \cdot |G|)$ for CYK algorithm
  - **Derivation (CYK Algorithm):**
    - **Prerequisite:** Grammar must be in Chomsky Normal Form (CNF)
    - **Algorithm:** Fill dynamic programming table $T[i,j]$ = set of nonterminals generating substring $w[i..j]$
    - **Table size:** $|w| \times |w| = |w|^2$ cells
    - **For each cell $T[i,j]$:**
      - Consider all splits: $k$ from $i$ to $j-1$ (at most $|w|$ splits)
      - For each split, check all productions $A \to BC$ in grammar
      - If $B \in T[i,k]$ and $C \in T[k+1,j]$, add $A$ to $T[i,j]$
      - Work per cell: $O(|w| \cdot |G|)$ where $|G|$ is number of productions
    - **Total cells:** $O(|w|^2)$
    - **Total time:** $O(|w|^2) \times O(|w| \cdot |G|) = O(|w|^3 \cdot |G|)$
  - **Note:** Converting to CNF adds polynomial overhead, but doesn't change asymptotic complexity

**$E_{DFA}$ = $\{\langle M \rangle \mid M$ is a DFA and $L(M) = \emptyset\}$** ✓ Decidable
- **Decider:** Check if any accept state is reachable from start state
- Use graph reachability (BFS/DFS) on DFA's state diagram
- Accept if no accept state reachable, reject otherwise
- **Time complexity:** $O(|Q| + |\delta|)$ where $Q$ is states, $\delta$ is transitions
  - **Derivation:**
    - Model DFA as directed graph: states = vertices, transitions = edges
    - **Graph representation:** Adjacency list (each state stores its outgoing transitions)
    - **BFS/DFS traversal:**
      - Visit each state at most once: $O(|Q|)$
      - Traverse each transition (edge) at most once: $O(|\delta|)$
      - Check if visited state is accepting: $O(1)$ per state
    - **Total:** $O(|Q| + |\delta|)$
  - **Note:** $|\delta| = |Q| \times |\Sigma|$ for complete DFA, so complexity is $O(|Q| \cdot |\Sigma|)$

**$EQ_{DFA}$ = $\{\langle M_1, M_2 \rangle \mid M_1, M_2$ are DFAs and $L(M_1) = L(M_2)\}$** ✓ Decidable

**Method 1: Symmetric Difference (Standard Method)**
- **Key Idea:** $L(M_1) = L(M_2)$ if and only if their symmetric difference is empty
- **Symmetric difference:** $L(M_1) \triangle L(M_2) = (L(M_1) \cap \overline{L(M_2)}) \cup (\overline{L(M_1)} \cap L(M_2))$
- **Algorithm:**
  1. Construct DFA $C$ for symmetric difference using closure properties:
     - Complement $L(M_2)$ to get $\overline{L(M_2)}$
     - Intersect $L(M_1)$ with $\overline{L(M_2)}$ to get $L(M_1) \cap \overline{L(M_2)}$
     - Complement $L(M_1)$ to get $\overline{L(M_1)}$
     - Intersect $\overline{L(M_1)}$ with $L(M_2)$ to get $\overline{L(M_1)} \cap L(M_2)$
     - Union the two intersections to get $C$
  2. Use $E_{DFA}$ decider on $C$
  3. If $L(C) = \emptyset$, then $L(M_1) = L(M_2)$ (accept)
  4. Otherwise, $L(M_1) \neq L(M_2)$ (reject)
- **Why it works:** Two languages are equal iff their symmetric difference is empty
- **Time complexity:** Polynomial (product construction + reachability)
  - **Derivation:**
    - Let $M_1$ have $n$ states, $M_2$ have $m$ states, alphabet size $|\Sigma|$
    - **Step 1: Complement operations** (2 operations)
      - Complement DFA: Swap accept/reject states
      - Time: $O(1)$ (just relabeling)
    - **Step 2: Intersection operations** (2 operations)
      - Product construction: Create DFA with $n \times m$ states
      - Each state $(q_1, q_2)$ has transitions for each symbol in $\Sigma$
      - Construction time: $O(n \cdot m \cdot |\Sigma|)$
    - **Step 3: Union operation** (1 operation)
      - Union of two DFAs: Similar product construction
      - Result has at most $n \cdot m \times n \cdot m = (nm)^2$ states
      - Construction time: $O((nm)^2 \cdot |\Sigma|)$
    - **Step 4: Emptiness check** on resulting DFA $C$
      - $C$ has at most $(nm)^2$ states
      - Reachability check: $O((nm)^2 \cdot |\Sigma|)$
    - **Total:** $O((nm)^2 \cdot |\Sigma|)$ = polynomial in input size

**Method 2: Testing All Strings Up to a Certain Size**
- **Key Idea:** If $L(M_1) \neq L(M_2)$, there exists a distinguishing string of bounded length
- **Bound:** If $M_1$ has $n$ states and $M_2$ has $m$ states, test all strings up to length $n \cdot m - 1$
- **Reasoning:**
  - Construct product DFA $P$ for $L(M_1) \triangle L(M_2)$ (symmetric difference)
  - $P$ has at most $n \times m$ states
  - If $L(P)$ is nonempty, by pumping lemma (or shortest path property), there exists a string $w \in L(P)$ with length $< n \cdot m$
  - This $w$ distinguishes $M_1$ and $M_2$ (accepted by exactly one)
- **Algorithm:**
  1. For each string $w$ of length $0$ to $n \cdot m - 1$:
     - Test if $M_1$ accepts $w$ and $M_2$ rejects $w$, or vice versa
     - If such $w$ found, **reject** (languages differ)
  2. If no distinguishing string found, **accept** (languages equal)
- **Number of strings to test:** $\sum_{i=0}^{n \cdot m - 1} |\Sigma|^i$ where $\Sigma$ is alphabet
- **Time complexity:** Exponential in $n \cdot m$
  - **Derivation:**
    - Number of strings of length $i$: $|\Sigma|^i$
    - Total strings to test: $\sum_{i=0}^{nm-1} |\Sigma|^i = \frac{|\Sigma|^{nm} - 1}{|\Sigma| - 1} = O(|\Sigma|^{nm})$
    - For each string $w$:
      - Simulate $M_1$ on $w$: $O(|w|) = O(nm)$
      - Simulate $M_2$ on $w$: $O(|w|) = O(nm)$
      - Compare results: $O(1)$
    - **Total:** $O(|\Sigma|^{nm} \cdot nm)$ = exponential in $nm$
  - **Note:** This method is exponentially worse than Method 1 but demonstrates the bound on distinguishing string length

**Techniques for Proving Decidability:**
1. **Simulation:** Directly simulate the automaton/grammar on input
2. **Reachability:** Use graph algorithms to check state/configuration reachability
3. **Closure Properties:** Build new automata using closure operations (union, intersection, complement)
4. **Algorithmic Methods:** Use known algorithms (CYK, minimization, etc.)

### 5.2 Undecidable Languages

**Definition:** A language $L$ is **undecidable** if no Turing machine can decide it (i.e., no TM always halts and correctly accepts/rejects all inputs).

**Key Examples:**

**$A_{TM}$ = $\{\langle M, w \rangle \mid M$ is a TM that accepts $w\}$** ✗ Undecidable
- **Why undecidable:** TMs can loop forever. We cannot determine if a TM will accept without running it, but running it might never halt.
- **Proof sketch (Diagonalization):**
  1. Assume $A_{TM}$ is decidable by decider $H$
  2. Construct TM $D$ that: On input $\langle M \rangle$, runs $H$ on $\langle M, \langle M \rangle \rangle$
  3. $D$ accepts if $H$ rejects, $D$ rejects if $H$ accepts
  4. Consider $D$ on input $\langle D \rangle$: Contradiction!
  5. Therefore, $H$ cannot exist
- **Key insight:** Self-reference creates paradox (like "This statement is false")

**$HALT_{TM}$ = $\{\langle M, w \rangle \mid M$ is a TM that halts on $w\}$** ✗ Undecidable
- **Why undecidable:** If we could decide halting, we could decide $A_{TM}$ (run TM, if it halts, check if it accepted)
- **Proof:** Reduction from $A_{TM}$
  - Assume $HALT_{TM}$ is decidable by decider $H$
  - To decide $A_{TM}$ on $\langle M, w \rangle$:
    1. Run $H$ on $\langle M, w \rangle$ (check if $M$ halts on $w$)
    2. If no, reject (doesn't accept)
    3. If yes, simulate $M$ on $w$ until it halts, then check if it accepted
  - This would decide $A_{TM}$, contradiction!
  - Therefore, $HALT_{TM}$ is undecidable

**$E_{TM}$ = $\{\langle M \rangle \mid M$ is a TM and $L(M) = \emptyset\}$** ✗ Undecidable
- **Why undecidable:** To check if language is empty, we'd need to check all possible inputs (infinite), or determine if TM accepts anything (which is $A_{TM}$)
- **Proof:** Reduction from $A_{TM}$
  - Given $\langle M, w \rangle$, construct $M'$ that: ignores input, simulates $M$ on $w$, accepts if $M$ accepts $w$
  - $L(M') = \Sigma^*$ if $M$ accepts $w$, else $L(M') = \emptyset$
  - If $E_{TM}$ were decidable, we could decide $A_{TM}$: check if $L(M') = \emptyset$

**$EQ_{TM}$ = $\{\langle M_1, M_2 \rangle \mid M_1, M_2$ are TMs and $L(M_1) = L(M_2)\}$** ✗ Undecidable
- **Why undecidable:** Special case: check if TM equals fixed TM (e.g., one that accepts nothing)
- **Proof:** Reduction from $E_{TM}$
  - Given $\langle M \rangle$, check if $L(M) = L(M_\emptyset)$ where $M_\emptyset$ rejects everything
  - If $EQ_{TM}$ were decidable, $E_{TM}$ would be decidable, contradiction

**Proof Techniques:**

**1. Diagonalization:**
- Create a "diagonal" TM that differs from every TM on the diagonal
- Self-reference leads to contradiction
- Example: $A_{TM}$ proof

**2. Reduction:**
- Show that if problem $B$ were decidable, then known undecidable problem $A$ would be decidable
- Since $A$ is undecidable, $B$ must be undecidable
- Example: $HALT_{TM}$, $E_{TM}$, $EQ_{TM}$ proofs

**The Halting Problem ($HALT_{TM}$):**
- **Most famous undecidable problem** - foundational result in computability
- **Statement:** No algorithm can determine if an arbitrary TM halts on arbitrary input
- **Implications:**
  - Cannot write perfect program analyzer (detect infinite loops)
  - Cannot write perfect compiler optimizer
  - Fundamental limit of computation
- **Proof outline:**
  1. Assume decider $H$ exists for $HALT_{TM}$
  2. Construct contradictory TM $D$ using $H$
  3. $D$ on $\langle D \rangle$ creates logical paradox
  4. Therefore, $H$ cannot exist

### 5.3 Recognizable but Not Decidable

**Definition:** A language $L$ is **Turing-recognizable** (recursively enumerable) if there exists a TM $M$ that:
- Accepts all strings in $L$
- May loop forever on strings not in $L$
- Does **not** need to reject (only needs to accept strings in $L$)

**Key Relationship:** Decidable ⊆ Recognizable
- Every decidable language is recognizable (decider is also recognizer)
- But not every recognizable language is decidable

**Examples:**

**$A_{TM}$ is recognizable but not decidable:**
- **Recognizable:** TM $U$ (universal TM) simulates $M$ on $w$
  - If $M$ accepts $w$, $U$ accepts
  - If $M$ rejects or loops, $U$ loops
  - This recognizes $A_{TM}$ (accepts when $M$ accepts)
- **Not decidable:** Proved by diagonalization (see 5.2)
- **Key insight:** We can recognize acceptance, but cannot always detect rejection/looping

**$E_{TM}$ is not recognizable (and not decidable):**
- **Not recognizable:** To recognize $E_{TM}$, we'd need to verify that TM accepts nothing
- But checking all inputs is impossible (infinite)
- If we find one accepting input, we know language is non-empty
- But if we never find one, we can't tell if it's empty or we haven't checked enough
- **Proof:** If $E_{TM}$ were recognizable, then $\overline{E_{TM}}$ would be recognizable
  - But then both would be recognizable, making $E_{TM}$ decidable (contradiction)

**Complement of recognizable language may not be recognizable:**
- **Example:** $A_{TM}$ is recognizable, but $\overline{A_{TM}}$ is not recognizable
- **Proof:** If $\overline{A_{TM}}$ were recognizable, then both $A_{TM}$ and $\overline{A_{TM}}$ would be recognizable
- By key fact below, $A_{TM}$ would be decidable (contradiction!)

**Key Fact:** If $L$ and $\overline{L}$ are both recognizable, then $L$ is decidable
- **Proof:** Construct decider for $L$:
  - Run recognizer for $L$ and recognizer for $\overline{L}$ in parallel (alternating steps)
  - Since every string is in either $L$ or $\overline{L}$, one recognizer must eventually accept
  - If $L$'s recognizer accepts first, accept
  - If $\overline{L}$'s recognizer accepts first, reject
  - This always halts and correctly decides $L$

**Summary Table:**

| Language | Decidable? | Recognizable? |
|----------|------------|---------------|
| $A_{DFA}$ | ✓ Yes | ✓ Yes |
| $A_{NFA}$ | ✓ Yes | ✓ Yes |
| $A_{CFG}$ | ✓ Yes | ✓ Yes |
| $A_{TM}$ | ✗ No | ✓ Yes |
| $HALT_{TM}$ | ✗ No | ✓ Yes |
| $E_{TM}$ | ✗ No | ✗ No |
| $EQ_{TM}$ | ✗ No | ✗ No |
| $\overline{A_{TM}}$ | ✗ No | ✗ No |

---

## 6. Reducibility

### 6.1 Concept

**Reduction:** Problem $A$ reduces to problem $B$ ($A \leq_m B$) if:
- Solving $B$ would allow us to solve $A$
- We can convert instances of $A$ to instances of $B$

**Use:** To prove undecidability
- If $A$ is known to be undecidable
- And $A \leq_m B$
- Then $B$ is also undecidable

### 6.2 Mapping Reductions

**Definition:** $A \leq_m B$ if there exists computable function $f$ such that:
- $w \in A$ if and only if $f(w) \in B$

**Properties:**
- If $A \leq_m B$ and $B$ is decidable, then $A$ is decidable
- If $A \leq_m B$ and $A$ is undecidable, then $B$ is undecidable
- If $A \leq_m B$ and $B$ is recognizable, then $A$ is recognizable

### 6.3 Common Reductions

**$A_{TM} \leq_m HALT_{TM}$:**
- If we could decide halting, we could decide acceptance
- Reduction: Convert TM $M$ to $M'$ that halts on all inputs

**$A_{TM} \leq_m E_{TM}$:**
- If we could decide emptiness, we could decide acceptance
- Reduction: Construct TM that accepts $w$ if and only if given TM accepts $w$

**$A_{TM} \leq_m EQ_{TM}$:**
- If we could decide equivalence, we could decide acceptance
- Reduction: Compare given TM to a fixed TM

### 6.4 Rice's Theorem

**Statement:** Every nontrivial property of Turing-recognizable languages is undecidable.

**Nontrivial:** Property holds for some but not all TMs

**Examples:**
- "Does TM accept empty language?" → Undecidable
- "Does TM accept finite language?" → Undecidable
- "Does TM accept regular language?" → Undecidable

**Note:** Properties of the TM itself (not the language) may be decidable

---

## 7. Time Complexity

### 7.1 Big-O Notation

**Definition:** $f(n) = O(g(n))$ if there exist constants $c > 0$ and $n_0 > 0$ such that:
- $f(n) \leq c \cdot g(n)$ for all $n \geq n_0$

**Common Classes:**
- $O(1)$: Constant
- $O(\log n)$: Logarithmic
- $O(n)$: Linear
- $O(n \log n)$: Linearithmic
- $O(n^2)$: Quadratic
- $O(2^n)$: Exponential

### 7.2 Complexity Classes

#### P (Polynomial Time)
- Languages decidable by deterministic TM in polynomial time
- $P = \bigcup_{k \geq 0} TIME(n^k)$
- "Efficiently solvable" problems

#### NP (Nondeterministic Polynomial Time)
- Languages decidable by nondeterministic TM in polynomial time
- $NP = \bigcup_{k \geq 0} NTIME(n^k)$
- "Efficiently verifiable" problems

**Key Relationship:** $P \subseteq NP$ (open whether $P = NP$)

#### NP-Complete
- Problems in NP
- Every problem in NP reduces to them
- If any NP-complete problem is in P, then $P = NP$

**Examples:**
- SAT (Boolean satisfiability)
- 3SAT
- CLIQUE
- VERTEX-COVER
- HAMILTONIAN-PATH

### 7.3 Reductions in Complexity Theory

**Polynomial-Time Reductions:**
- $A \leq_p B$: $A$ reduces to $B$ in polynomial time
- If $B \in P$ and $A \leq_p B$, then $A \in P$
- If $A$ is NP-complete and $A \leq_p B$, then $B$ is NP-hard

**NP-Completeness Proof:**
1. Show problem is in NP
2. Show some known NP-complete problem reduces to it

### 7.4 Space Complexity

**PSPACE:** Languages decidable by TM using polynomial space

**Relationships:**
- $P \subseteq NP \subseteq PSPACE$
- $PSPACE = NPSPACE$ (Savitch's Theorem)

---

## 8. Key Theorems and Results

### Regular Languages
- **Theorem 1.16:** Regular languages closed under union
- **Theorem 1.19:** Regular languages closed under concatenation
- **Theorem 1.23:** Regular languages closed under star
- **Theorem 1.26:** Regular languages closed under intersection
- **Theorem 1.39:** Every NFA has equivalent DFA
- **Theorem 1.54:** Language is regular iff some regex describes it
- **Theorem 1.70:** Pumping Lemma for regular languages

### Context-Free Languages
- **Theorem 2.20:** Every CFL has grammar in CNF
- **Theorem 2.27:** CFG = Nondeterministic PDA
- **Theorem 2.34:** Pumping Lemma for CFLs
- Regular languages ⊆ Context-free languages

### Turing Machines
- **Theorem 3.13:** Multitape TM = Single-tape TM
- **Theorem 3.16:** Nondeterministic TM = Deterministic TM
- **Theorem 3.21:** Enumerator = Turing-recognizable languages
- **Church-Turing Thesis:** TMs capture all algorithms

### Decidability
- **Theorem 4.11:** $A_{TM}$ is undecidable
- **Theorem 4.17:** $HALT_{TM}$ is undecidable
- **Theorem 5.28:** Rice's Theorem

### Complexity
- **Cook-Levin Theorem:** SAT is NP-complete
- **Savitch's Theorem:** $PSPACE = NPSPACE$

---

## 9. Problem-Solving Strategies

### 9.1 Proving a Language is Regular

**Methods:**
1. Construct a DFA/NFA
2. Write a regular expression
3. Show it's built from regular languages using closure properties
4. Construct a regular grammar

### 9.2 Proving a Language is NOT Regular

**Method:** Pumping Lemma
1. Assume regular
2. Choose string $s$ (depends on $p$)
3. Show all splits $s = xyz$ lead to contradiction
4. Conclude not regular

**Alternative:** Myhill-Nerode (show infinitely many equivalence classes)

### 9.3 Proving a Language is Context-Free

**Methods:**
1. Construct a CFG
2. Construct a PDA
3. Show it's built from CFLs using closure properties

### 9.4 Proving a Language is NOT Context-Free

**Method:** Pumping Lemma for CFLs
1. Assume context-free
2. Choose string $w$ (depends on $p$)
3. Show all decompositions $w = uvxyz$ lead to contradiction
4. Conclude not context-free

### 9.5 Designing Turing Machines

**Strategy:**
1. Understand the language/algorithm
2. Break into phases (marking, scanning, verification)
3. Design states for each phase
4. Handle edge cases (empty string, boundaries)
5. Verify it always halts (if decider needed)

**Common Patterns:**
- Marking symbols (use special markers like $X$, $Y$)
- Counting (mark pairs)
- Comparison (copy and compare)
- Format verification (check structure first)

### 9.6 Proving Undecidability

**Methods:**
1. **Reduction:** Show $A_{TM} \leq_m B$ (or other known undecidable problem)
2. **Diagonalization:** Construct contradiction
3. **Rice's Theorem:** If nontrivial property of languages

### 9.7 Proving NP-Completeness

**Steps:**
1. Show problem is in NP (polynomial-time verifier)
2. Show known NP-complete problem reduces to it
3. Reduction must be polynomial-time

---

## 10. Quick Reference

### Language Hierarchy
```
Regular ⊂ Context-Free ⊂ Turing-Recognizable
```

### Closure Properties Summary

| Operation | Regular | Context-Free | Decidable | Recognizable |
|-----------|---------|--------------|-----------|--------------|
| Union | ✓ | ✓ | ✓ | ✓ |
| Concatenation | ✓ | ✓ | ✓ | ✓ |
| Star | ✓ | ✓ | ✓ | ✓ |
| Complement | ✓ | ✗ | ✓ | ✗ |
| Intersection | ✓ | ✗ | ✓ | ✓ |

### Pumping Lemmas

**Regular:** $s = xyz$ where $|y| > 0$, $|xy| \leq p$, $xy^iz \in L$ for all $i$

**CFL:** $w = uvxyz$ where $|vy| \geq 1$, $|vxy| \leq p$, $uv^ixy^iz \in L$ for all $i$

### Complexity Classes

- **P:** Polynomial time (deterministic)
- **NP:** Polynomial time (nondeterministic)
- **NP-Complete:** Hardest problems in NP
- **PSPACE:** Polynomial space

### Key Undecidable Problems

- $A_{TM}$: Acceptance problem
- $HALT_{TM}$: Halting problem
- $E_{TM}$: Emptiness problem
- $EQ_{TM}$: Equivalence problem

### Common Conversions

- **DFA → NFA:** Identity (DFA is NFA)
- **NFA → DFA:** Subset construction (exponential)
- **DFA → Regular Expression:** GNFA method
- **Regular Expression → NFA:** Structural induction
- **CFG → PDA:** Standard construction (3 states)
- **PDA → CFG:** State pair construction
- **DFA → Regular Grammar:** States → Nonterminals

### Study Tips

1. **Practice drawing automata** - essential skill
2. **Memorize pumping lemmas** - word-for-word
3. **Know closure properties** - which operations preserve which classes
4. **Understand reductions** - key technique for undecidability
5. **Work through examples** - theory makes sense when applied
6. **Test your constructions** - verify with sample strings
7. **Know the hierarchy** - understand relationships between classes

---

## Conclusion

This review covers the complete Theory of Computation course:

1. **Regular Languages** - Finite memory, DFAs/NFAs, regular expressions
2. **Context-Free Languages** - Stack memory, PDAs, CFGs
3. **Turing Machines** - Unlimited memory, most powerful model
4. **Decidability** - What can and cannot be computed
5. **Reducibility** - Techniques for proving undecidability
6. **Time Complexity** - Efficient algorithms, P vs NP

**Key Insight:** Each level adds computational power, but also introduces new limitations and undecidable problems.

**Good luck on your final exam!**

