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
- **CFG → PDA:** Standard construction (simulate leftmost derivations)
- **PDA → CFG:** More complex (variables represent state pairs)

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

**Key Examples:**
- $A_{DFA}$ = $\{\langle M, w \rangle \mid M$ is a DFA that accepts $w\}$ ✓ Decidable
- $A_{NFA}$ = $\{\langle N, w \rangle \mid N$ is an NFA that accepts $w\}$ ✓ Decidable
- $A_{REX}$ = $\{\langle R, w \rangle \mid R$ is a regex that matches $w\}$ ✓ Decidable
- $A_{CFG}$ = $\{\langle G, w \rangle \mid G$ is a CFG that generates $w\}$ ✓ Decidable
- $E_{DFA}$ = $\{\langle M \rangle \mid M$ is a DFA and $L(M) = \emptyset\}$ ✓ Decidable
- $EQ_{DFA}$ = $\{\langle M_1, M_2 \rangle \mid M_1, M_2$ are DFAs and $L(M_1) = L(M_2)\}$ ✓ Decidable

**Techniques:**
- Simulate the automaton/grammar
- Use algorithms (e.g., reachability, minimization)

### 5.2 Undecidable Languages

**Key Examples:**
- $A_{TM}$ = $\{\langle M, w \rangle \mid M$ is a TM that accepts $w\}$ ✗ Undecidable
- $HALT_{TM}$ = $\{\langle M, w \rangle \mid M$ is a TM that halts on $w\}$ ✗ Undecidable
- $E_{TM}$ = $\{\langle M \rangle \mid M$ is a TM and $L(M) = \emptyset\}$ ✗ Undecidable
- $EQ_{TM}$ = $\{\langle M_1, M_2 \rangle \mid M_1, M_2$ are TMs and $L(M_1) = L(M_2)\}$ ✗ Undecidable

**Proof Technique:** Diagonalization and self-reference

**The Halting Problem:**
- Most famous undecidable problem
- No algorithm can determine if a TM halts on given input
- Proved by contradiction (assume decider exists, construct contradiction)

### 5.3 Recognizable but Not Decidable

**Examples:**
- $A_{TM}$ is recognizable but not decidable
- $E_{TM}$ is not recognizable (and not decidable)
- Complement of recognizable language may not be recognizable

**Key Fact:** If $L$ and $\overline{L}$ are both recognizable, then $L$ is decidable

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

