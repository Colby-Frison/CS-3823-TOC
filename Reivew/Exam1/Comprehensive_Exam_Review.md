# Theory of Computation - Comprehensive Exam 1 Review

**Coverage:** Slides 00-01, Homework 1-2
**Topics:** Introduction to Theory of Computation, Regular Languages, Finite Automata, Regular Expressions

---

## Table of Contents

1. [Mathematical Foundations](#1-mathematical-foundations)
   - 1.1 [Set Theory](#11-set-theory)
   - 1.2 [Mathematical Induction](#12-mathematical-induction)

2. [Finite Automata (FA)](#2-finite-automata-fa)
   - 2.1 [What is a Finite Automaton?](#21-what-is-a-finite-automaton)
   - 2.2 [State Diagrams](#22-state-diagrams)
   - 2.3 [Formal Description and Extended Transition Function](#23-formal-description-and-extended-transition-function)
   - 2.4 [Interpreting State Machines (HW1 Q4)](#24-interpreting-state-machines-hw1-q4)

3. [Nondeterministic Finite Automata (NFA)](#3-nondeterministic-finite-automata-nfa)
   - 3.1 [What is Nondeterminism?](#31-what-is-nondeterminism)
   - 3.2 [Designing NFAs (HW2 Q1)](#32-designing-nfas-hw2-q1)
   - 3.3 [NFAs and DFAs are Equivalent](#33-nfas-and-dfas-are-equivalent)
   - 3.4 [DFA vs NFA: Size Comparison (HW2 Q3)](#34-dfa-vs-nfa-size-comparison-hw2-q3)

4. [Regular Expressions](#4-regular-expressions)
   - 4.1 [What are Regular Expressions?](#41-what-are-regular-expressions)
   - 4.2 [Common Regular Expression Patterns](#42-common-regular-expression-patterns)
   - 4.3 [Writing Regular Expressions (HW2 Q4)](#43-writing-regular-expressions-hw2-q4)
   - 4.4 [Converting DFAs to Regular Expressions (GNFA)](#44-converting-dfas-to-regular-expressions-gnfa)
   - 4.5 [Regular Expressions ↔ Finite Automata](#45-regular-expressions--finite-automata)

5. [Non-Regular Languages](#5-non-regular-languages)
   - 5.1 [The Pumping Lemma](#51-the-pumping-lemma)
   - 5.2 [Example: L₁ = {www | w ∈ Σ*} (HW2 Q6-i)](#52-example-l_1--www-mid-w-in-sigma-hw2-q6-i)
   - 5.3 [Example: L₂ = {1^(2^n) | n ≥ 1} (HW2 Q6-ii)](#53-example-l_2--12n-mid-n-geq-1-hw2-q6-ii)
   - 5.4 [Tips for Using the Pumping Lemma](#54-tips-for-using-the-pumping-lemma)

6. [Closure Properties](#6-closure-properties)
   - 6.1 [What are Closure Properties?](#61-what-are-closure-properties)
   - 6.2 [Regular Languages are Closed Under Union](#62-regular-languages-are-closed-under-union)
   - 6.3 [Regular Languages are Closed Under Concatenation](#63-regular-languages-are-closed-under-concatenation)
   - 6.4 [Regular Languages are Closed Under Star](#64-regular-languages-are-closed-under-star)
   - 6.5 [Regular Languages are Closed Under Intersection](#65-regular-languages-are-closed-under-intersection)
   - 6.6 [Additional Closure Properties (Not from Slides)](#66-additional-closure-properties-not-from-slides)

7. [State Minimization and Complexity](#7-state-minimization-and-complexity)
   - 7.1 [Distinguishability](#71-distinguishability)
   - 7.2 [Myhill-Nerode Theorem](#72-myhill-nerode-theorem)
   - 7.3 [DFA Size Lower Bounds (Related to HW2 Q3)](#73-dfa-size-lower-bounds-related-to-hw2-q3)
   - 7.4 [State Minimization Algorithm (Optional/Advanced)](#74-state-minimization-algorithm-optionaladvanced)

8. [Important Algorithms and Techniques Summary](#8-important-algorithms-and-techniques-summary)
   - 8.1 [Converting Between Representations](#81-converting-between-representations)
   - 8.2 [Proving a Language is Regular](#82-proving-a-language-is-regular)
   - 8.3 [Proving a Language is Not Regular](#83-proving-a-language-is-not-regular)

9. [Key Theorems and Results](#9-key-theorems-and-results)
   - 9.1 [Regular Languages - Core Theorems](#regular-languages---core-theorems)

10. [Practice Problems and Strategies](#10-practice-problems-and-strategies)
    - 10.1 [Types of Problems You Might See](#types-of-problems-you-might-see)

11. [Common Mistakes to Avoid](#11-common-mistakes-to-avoid)
    - 11.1 [When Building DFAs/NFAs](#when-building-dfasnfas)
    - 11.2 [When Using Pumping Lemma](#when-using-pumping-lemma)
    - 11.3 [When Writing Regular Expressions](#when-writing-regular-expressions)
    - 11.4 [When Converting NFA to DFA](#when-converting-nfa-to-dfa)

12. [Quick Reference Formulas](#12-quick-reference-formulas)
    - 12.1 [Set Theory](#set-theory)
    - 12.2 [Automata](#automata)
    - 12.3 [Regular Expressions](#regular-expressions-1)
    - 12.4 [Pumping Lemma](#pumping-lemma)

13. [Study Tips](#13-study-tips)
    - 13.1 [For the Exam](#for-the-exam)
    - 13.2 [Key Things to Memorize](#key-things-to-memorize)
    - 13.3 [Understanding vs. Memorizing](#understanding-vs-memorizing)

14. [Additional Examples](#14-additional-examples)
    - 14.1 [Example: Binary numbers divisible by 3](#example-binary-numbers-divisible-by-3)
    - 14.2 [Example: Equal number of 0s and 1s](#example-equal-number-of-0s-and-1s)

15. [Conclusion](#conclusion)

---

## 1. Mathematical Foundations

### 1.1 Set Theory

#### What It Is
Set theory is the foundation of mathematics and computer science. A **set** is a collection of distinct objects called **elements** or **members**.

#### Key Concepts

**Basic Notation:**
- $A = \{1, 2, 3\}$ - a set containing elements 1, 2, 3
- $x \in A$ - element $x$ is a member of set $A$
- $x \notin A$ - element $x$ is not a member of set $A$
- $\emptyset$ or $\{\}$ - the empty set (contains no elements)

**Subset Relation:**
- $A \subseteq B$ means "A is a subset of B" - every element of A is also in B
- $A \subset B$ means "A is a proper subset of B" - A is a subset of B but $A \neq B$

**Set Operations:**

1. **Union** ($A \cup B$): All elements in A or B or both
   - $\{1,2,3\} \cup \{3,4,5\} = \{1,2,3,4,5\}$

2. **Intersection** ($A \cap B$): Elements in both A and B
   - $\{1,2,3\} \cap \{3,4,5\} = \{3\}$

3. **Set Difference** ($A \setminus B$): Elements in A but not in B
   - $\{1,2,3\} \setminus \{3,4,5\} = \{1,2\}$

4. **Complement** ($\bar{A}$ or $A^c$): All elements not in A (relative to some universe)

5. **Cartesian Product** ($A \times B$): Set of all ordered pairs $(a,b)$ where $a \in A$ and $b \in B$
   - $\{1,2\} \times \{a,b\} = \{(1,a), (1,b), (2,a), (2,b)\}$

**Power Set:**
- $\mathcal{P}(A)$ or $2^A$ - the set of all subsets of A
- If $A = \{1,2\}$, then $\mathcal{P}(A) = \{\emptyset, \{1\}, \{2\}, \{1,2\}\}$
- If $|A| = n$, then $|\mathcal{P}(A)| = 2^n$

#### Example Problem (HW1 Q1)
Let $A = \{x, y, z\}$ and $B = \{a, b, x\}$

1. **Is $A \subseteq B$?** 
   - No, because $y \in A$ but $y \notin B$

2. **What is $A \cap (B \setminus A)$?**
   - First find $B \setminus A = \{a, b\}$ (elements in B but not in A)
   - Then $A \cap \{a,b\} = \emptyset$ (no common elements)

3. **What is $A \times B$?**
   - $\{(x,a), (x,b), (x,x), (y,a), (y,b), (y,x), (z,a), (z,b), (z,x)\}$
   - Contains $|A| \times |B| = 3 \times 3 = 9$ elements

4. **What is the power set of $B$?**
   - $\mathcal{P}(B) = \{\emptyset, \{a\}, \{b\}, \{x\}, \{a,b\}, \{a,x\}, \{b,x\}, \{a,b,x\}\}$
   - Contains $2^3 = 8$ elements

#### Why It's Important
Set theory is used to define languages (sets of strings), state sets in automata, and closure properties of language classes.

---

### 1.2 Mathematical Induction

#### What It Is
Mathematical induction is a proof technique used to prove statements about all natural numbers (or any well-ordered set).

#### The Principle
To prove that a property $P(n)$ holds for all integers $n \geq n_0$:

1. **Base Case:** Prove $P(n_0)$ is true
2. **Inductive Hypothesis:** Assume $P(k)$ is true for some arbitrary $k \geq n_0$
3. **Inductive Step:** Prove that $P(k) \Rightarrow P(k+1)$

**Why it works:** Like dominoes falling - if the first falls and each one knocks down the next, all will fall.

#### Example Problem (HW1 Q2)
**Prove:** For all integers $k \geq 4$, we have $k! > 2^k$

**Proof:**

**Base Case** ($k = 4$):
- $4! = 24$
- $2^4 = 16$
- $24 > 16$ ✓

**Inductive Hypothesis:** Assume $k! > 2^k$ for some $k \geq 4$

**Inductive Step:** Prove $(k+1)! > 2^{k+1}$

Starting with the left side:
$$\begin{align}
(k+1)! &= (k+1) \cdot k! \\
       &> (k+1) \cdot 2^k \quad \text{(by inductive hypothesis)} \\
       &> 2 \cdot 2^k \quad \text{(since } k+1 > 2 \text{ for } k \geq 4\text{)} \\
       &= 2^{k+1}
\end{align}$$

Therefore, $(k+1)! > 2^{k+1}$, completing the proof. $\square$

#### Types of Induction

1. **Simple Induction:** Prove $P(k) \Rightarrow P(k+1)$
2. **Strong Induction:** Assume $P(n_0), P(n_0+1), \ldots, P(k)$ all true, then prove $P(k+1)$
3. **Structural Induction:** For recursively defined structures (like trees, strings)

#### When to Use It
- Proving properties of algorithms
- Proving correctness of recursive definitions
- Showing language properties
- Establishing bounds and inequalities

---

## 2. Finite Automata (FA)

### 2.1 What is a Finite Automaton?

#### Definition
A **Deterministic Finite Automaton (DFA)** is a mathematical model of computation consisting of:
- A finite set of **states**
- An **input alphabet**
- A **transition function** that determines the next state
- A **start state**
- A set of **accept (or final) states**

**Formal Definition:** A DFA is a 5-tuple $M = (Q, \Sigma, \delta, q_0, F)$ where:
- $Q$ is a finite set of states
- $\Sigma$ is a finite alphabet (input symbols)
- $\delta: Q \times \Sigma \rightarrow Q$ is the transition function
- $q_0 \in Q$ is the start state
- $F \subseteq Q$ is the set of accept states

#### How It Works
1. Start in state $q_0$
2. Read input string one symbol at a time from left to right
3. Follow transitions based on current state and input symbol
4. After reading entire input:
   - **Accept** if in an accept state (state in $F$)
   - **Reject** if in a non-accept state (state not in $F$)

#### Language of a DFA
The **language** of $M$, denoted $L(M)$, is the set of all strings that $M$ accepts:
$$L(M) = \{w \in \Sigma^* \mid \text{$M$ accepts $w$}\}$$

A language is **regular** if some DFA recognizes it.

---

### 2.2 State Diagrams

#### What They Are
State diagrams are visual representations of finite automata using:
- **Circles (nodes):** represent states
- **Arrows (edges):** represent transitions
- **Double circles:** represent accept states
- **Arrow from nowhere:** marks the start state
- **Labels on arrows:** show which input symbol causes that transition

#### Drawing State Diagrams (HW1 Q3)

**Example 1:** $L_1 = \{w \mid \text{length of $w$ is odd}\}$, $\Sigma = \{1\}$

**Strategy:** Use states to track whether we've seen an odd or even number of 1's
- State $q_0$ (accept): seen even number of 1's (including 0)
- State $q_1$ (reject): seen odd number of 1's

**Transitions:**
- From $q_0$ on input 1: go to $q_1$
- From $q_1$ on input 1: go to $q_0$

```
    ┌─→(q₀)←──┐
    │   ⇊     │
    │   1     1
    │   ⇊     │
    └───q₁────┘
```

**Example 2:** $L_2 = \{w \mid \text{$w$ has at most two occurrences of $b$}\}$, $\Sigma = \{a,b\}$

**Strategy:** Count the number of b's seen (0, 1, 2, or more than 2)
- State $q_0$ (accept): seen 0 b's
- State $q_1$ (accept): seen 1 b
- State $q_2$ (accept): seen 2 b's
- State $q_3$ (reject): seen 3+ b's

**Transitions:**
- From $q_i$ on input $a$: stay in $q_i$ (a's don't matter)
- From $q_i$ on input $b$: go to $q_{i+1}$ (count another b)
- From $q_3$ on any input: stay in $q_3$ (trap state)

**Example 3:** $L_3 = \{w \mid \text{$w$ starts with 1 or ends with 0}\}$, $\Sigma = \{0,1\}$

**Strategy:** This is a union of two conditions - track both possibilities
- If we see a 1 at the start, accept anything after
- Otherwise, accept only if the last symbol was 0

#### Design Tips

1. **Identify what to remember:** What information about the input so far affects future decisions?
2. **Use states to encode memory:** Each state represents a category of input histories
3. **Think incrementally:** How does each new input symbol change what we know?
4. **Minimize states:** Use only as many states as necessary
5. **Handle all cases:** Every state must have a transition for every input symbol

---

### 2.3 Formal Description and Extended Transition Function

#### Transition Function
$\delta: Q \times \Sigma \rightarrow Q$ tells us the next state
- $\delta(q, a)$ = the state reached from state $q$ on input symbol $a$

#### Extended Transition Function
$\delta^*: Q \times \Sigma^* \rightarrow Q$ handles strings (not just symbols)
- $\delta^*(q, \varepsilon) = q$ (reading empty string doesn't change state)
- $\delta^*(q, wa) = \delta(\delta^*(q, w), a)$ (process string $w$, then symbol $a$)

**Informal meaning:** $\delta^*(q, w)$ is the state reached from $q$ after reading string $w$

#### Acceptance
A DFA $M = (Q, \Sigma, \delta, q_0, F)$ **accepts** string $w$ if:
$$\delta^*(q_0, w) \in F$$

---

### 2.4 Interpreting State Machines (HW1 Q4)

#### Strategy for Understanding a DFA
1. **Trace small examples:** Try strings and see which are accepted/rejected
2. **Characterize states:** What does it mean to be in each state?
3. **Find patterns:** What property do accepted strings share?
4. **Formulate hypothesis:** State the language in English or set notation
5. **Verify:** Check edge cases and counterexamples

#### Example from HW1

Given a DFA with states $\{q_0, q_1, q_2, q_3\}$ and transitions (see homework for diagram)

**Analysis steps:**
1. **Test short strings:** $\varepsilon, 0, 1, 00, 01, 10, 11, \ldots$
2. **Notice patterns:** Which accepted strings have in common?
3. **State characterization:**
   - $q_0$: Haven't seen the pattern yet
   - $q_1$: Seen part of pattern
   - $q_2$: Seen complete pattern, in accepting zone
   - $q_3$: Trap state (will never accept)

**Writing Formal Description:**
For a DFA $M_1$ with the diagram shown, the 5-tuple is:
- $Q = \{q_0, q_1, q_2, q_3\}$
- $\Sigma = \{0, 1\}$
- $q_0$ is the start state
- $F = \{q_2\}$ (or whatever the accept states are)
- $\delta$ is given by the transition table:

| State | Input 0 | Input 1 |
|-------|---------|---------|
| $q_0$ | $q_1$   | $q_0$   |
| $q_1$ | $q_2$   | $q_3$   |
| $q_2$ | $q_2$   | $q_2$   |
| $q_3$ | $q_3$   | $q_3$   |

---

## 3. Nondeterministic Finite Automata (NFA)

### 3.1 What is Nondeterminism?

#### Key Idea
An NFA is like a DFA but with **superpowers**:
1. Can have **multiple transitions** from a state on the same input symbol
2. Can have **$\varepsilon$-transitions** (move without reading input)
3. Can have **no transition** for some state-symbol pairs

**Think of it as:** The machine can "guess" which path to take, and accepts if **any** possible path leads to acceptance.

#### Formal Definition
An NFA is a 5-tuple $N = (Q, \Sigma, \delta, q_0, F)$ where:
- $Q$ is a finite set of states
- $\Sigma$ is a finite alphabet
- $\delta: Q \times \Sigma_\varepsilon \rightarrow \mathcal{P}(Q)$ is the transition function
  - $\Sigma_\varepsilon = \Sigma \cup \{\varepsilon\}$ (alphabet plus empty string)
  - $\mathcal{P}(Q)$ is the power set of $Q$ (set of all subsets)
  - $\delta(q, a)$ is a **set of states** (possibly empty)
- $q_0 \in Q$ is the start state
- $F \subseteq Q$ is the set of accept states

#### Computation Model
An NFA accepts string $w$ if there exists **at least one** sequence of states:
$$q_0, q_1, q_2, \ldots, q_n$$
such that:
1. $q_0$ is the start state
2. $q_{i+1} \in \delta(q_i, w_i)$ for each $i$ (or $\varepsilon$-transitions)
3. $q_n \in F$ (ends in an accept state)
4. The input $w$ is fully consumed

**Important:** If **any** branch of computation accepts, the NFA accepts (think "parallel universes")

---

### 3.2 Designing NFAs (HW2 Q1)

NFAs are often **much easier** to design than DFAs because you can use nondeterminism.

#### Example 1: $L_1 = \{w \mid w \text{ contains two consecutive 1s OR } w \text{ contains no 0s}\}$

**Strategy:** This is a union - use nondeterminism to "guess" which part of the union!

**Design:**
- Start state has $\varepsilon$-transitions to two branches:
  - **Branch 1:** Recognize strings with "11"
  - **Branch 2:** Recognize strings with no 0s

**Branch 1 (two consecutive 1s):**
- Loop in start reading anything
- When you see a 1, guess it might be the first of "11"
- Read another 1, go to accept state
- Stay in accept state forever (once we have "11", we're good)

**Branch 2 (no 0s):**
- Accept only strings over $\{1\}$
- Loop on 1's in an accept state
- Any 0 goes to a trap state

#### Example 2: $L_2 = \{w \mid w = w_1w_2\ldots w_n \text{ such that } w_{n-3} = 0 \text{ and } w_{n-2} = 1\}$

**Strategy:** The 3rd and 2nd symbols from the end must be "01"

**Design using nondeterminism:**
- Loop in start state on all input (don't know where "01" is yet)
- When seeing a 0, **guess** it might be the 3rd symbol from end
- **Must** see a 1 next (2nd from end)
- Read any two more symbols (last two positions)
- Accept if we read exactly 2 more symbols

**Why NFAs are easier:** We don't need to track all possible positions of "01" - just guess the right one!

---

### 3.3 NFAs and DFAs are Equivalent

#### The Big Theorem (Theorem 1.39)
**Every NFA has an equivalent DFA.**

More precisely: If $N$ is an NFA recognizing language $A$, then there exists a DFA $M$ recognizing the same language $A$.

**What this means:**
- NFAs don't give us more **power** (can't recognize more languages)
- NFAs give us more **convenience** (can be exponentially smaller)
- Regular languages = languages recognized by DFAs = languages recognized by NFAs

#### The Subset Construction (Powerset Construction)

**Idea:** The DFA simulates the NFA by keeping track of **all possible states** the NFA could be in.

**Construction:** Given NFA $N = (Q_N, \Sigma, \delta_N, q_0, F_N)$, build DFA $M = (Q_M, \Sigma, \delta_M, q_{0M}, F_M)$:

1. **States:** $Q_M = \mathcal{P}(Q_N)$ (each DFA state is a subset of NFA states)
   - If NFA has $n$ states, DFA has up to $2^n$ states

2. **Start state:** $q_{0M} = E(\{q_0\})$ 
   - $E(S)$ = "$\varepsilon$-closure" of $S$ = all states reachable from states in $S$ using only $\varepsilon$-transitions

3. **Transition function:** For DFA state $R \subseteq Q_N$ and symbol $a$:
   $$\delta_M(R, a) = E\left(\bigcup_{q \in R} \delta_N(q, a)\right)$$
   - Follow all possible NFA transitions from all states in $R$
   - Then take $\varepsilon$-closure

4. **Accept states:** $F_M = \{R \subseteq Q_N \mid R \cap F_N \neq \emptyset\}$
   - DFA accepts if the set contains at least one NFA accept state

#### Example (HW2 Q2)

Given NFA $N = (\{q_1, q_2\}, \{0,1\}, \delta, q_1, \{q_1\})$ with:

| $\delta$ | 0 | 1 | $\varepsilon$ |
|----------|---|---|---------------|
| $q_1$ | $\{q_1, q_2\}$ | $\emptyset$ | $\emptyset$ |
| $q_2$ | $\emptyset$ | $\{q_1\}$ | $\{q_1\}$ |

**Building the DFA:**

1. **Start state:** $E(\{q_1\}) = \{q_1\}$ (no $\varepsilon$-transitions from $q_1$)

2. **From $\{q_1\}$:**
   - On 0: $\delta_N(q_1, 0) = \{q_1, q_2\}$, then $E(\{q_1,q_2\}) = \{q_1, q_2\}$
   - On 1: $\delta_N(q_1, 1) = \emptyset$

3. **From $\{q_1, q_2\}$:**
   - On 0: $\delta_N(q_1,0) \cup \delta_N(q_2,0) = \{q_1,q_2\} \cup \emptyset = \{q_1, q_2\}$
   - On 1: $\delta_N(q_1,1) \cup \delta_N(q_2,1) = \emptyset \cup \{q_1\} = \{q_1\}$

4. **Accept states:** Sets containing $q_1$: $\{q_1\}, \{q_1,q_2\}$

**Result:** DFA with states $\{\{q_1\}, \{q_1,q_2\}, \emptyset\}$ (often can remove unreachable $\emptyset$)

**Language recognized:** $L(N) = \{w \in \{0,1\}^* \mid \text{every 1 in $w$ is immediately preceded by a 0}\}$ = $(0 \cup 01)^*$

---

### 3.4 DFA vs NFA: Size Comparison (HW2 Q3)

#### Part (i): DFA implies NFA
**Claim:** If a language can be recognized by a DFA with $k$ states, it can be recognized by an NFA with $k$ states.

**Proof:** Every DFA **is** an NFA! 
- An NFA is a generalization of DFA
- A DFA is just an NFA where:
  - Each transition goes to exactly one state (set of size 1)
  - No $\varepsilon$-transitions
- No conversion needed - the DFA already satisfies NFA requirements

#### Parts (ii)-(iii): NFAs can be exponentially smaller

**Language:** $L_k = \Sigma^* 1 \Sigma^{k-1}$ (the $k$-th symbol from the end is a 1)

**NFA size (Part ii):** Can build an NFA with $k+1$ states
- Use nondeterminism to "guess" where the 1 that's $k$ from the end occurs
- One start state (loop on anything)
- Chain of $k$ states to count down $k-1$ symbols after seeing the 1

**DFA size (Part iii):** **Any** DFA needs at least $2^k$ states

**Proof (Myhill-Nerode / Pigeonhole argument):**
- There are $2^k$ different strings of length $k$ over $\{0,1\}$
- Any two different strings $x,y \in \{0,1\}^k$ are **distinguishable**:
  - They differ in some position $i$
  - Append a string that checks position $i$ (string of length $k-i$)
  - One will be accepted, the other rejected
- If DFA had fewer than $2^k$ states, two different strings would lead to same state (Pigeonhole)
- Then they wouldn't be distinguishable (contradiction!)

**Conclusion:** NFA has $k+1$ states, minimal DFA has $2^k$ states - exponential gap!

#### What This Tells Us (Parts iv-v)

**About Theorem 1.39:**
- The $2^n$ upper bound in subset construction is **tight**
- Exponential blowup can actually happen (not just worst-case theory)

**About DFAs vs NFAs:**
- **Expressiveness:** Equivalent (recognize exactly the regular languages)
- **Succinctness:** NFAs can be exponentially more compact
- **Tradeoff:** NFAs are smaller but harder to simulate; DFAs are larger but easier to implement

---

## 4. Regular Expressions

### 4.1 What are Regular Expressions?

#### Definition
Regular expressions are a **declarative** way to describe regular languages using a compact notation.

**The operations:**
1. **Literal symbols:** $a, b, 0, 1, \ldots$ match themselves
2. **Empty string:** $\varepsilon$ matches the empty string
3. **Empty set:** $\emptyset$ matches nothing
4. **Union:** $R_1 \cup R_2$ (also written $R_1 | R_2$ or $R_1 + R_2$) matches strings in either language
5. **Concatenation:** $R_1 R_2$ (or $R_1 \circ R_2$) matches strings formed by concatenating a string from $R_1$ with a string from $R_2$
6. **Kleene star:** $R^*$ matches zero or more concatenations of strings from $R$

#### Formal Definition (Recursive)
The set of regular expressions over alphabet $\Sigma$ is defined recursively:

**Base cases:**
- $\varepsilon$ is a regular expression
- $\emptyset$ is a regular expression  
- $a$ is a regular expression for each $a \in \Sigma$

**Recursive cases:** If $R_1$ and $R_2$ are regular expressions, so are:
- $(R_1 \cup R_2)$
- $(R_1 R_2)$
- $(R_1^*)$

#### Language of a Regular Expression
$L(R)$ denotes the language (set of strings) described by regular expression $R$:

- $L(\varepsilon) = \{\varepsilon\}$ (the set containing only the empty string)
- $L(\emptyset) = \emptyset$ (the empty set)
- $L(a) = \{a\}$ for $a \in \Sigma$
- $L(R_1 \cup R_2) = L(R_1) \cup L(R_2)$
- $L(R_1 R_2) = \{xy \mid x \in L(R_1) \text{ and } y \in L(R_2)\}$
- $L(R^*) = \{\varepsilon\} \cup L(R) \cup L(RR) \cup L(RRR) \cup \cdots$

#### Precedence Rules
To avoid excessive parentheses:
1. **Star** ($*$) has highest precedence
2. **Concatenation** has middle precedence
3. **Union** ($\cup$) has lowest precedence

Example: $ab^* \cup c$ means $((a(b^*)) \cup c)$, which is $\{a, ab, abb, abbb, \ldots\} \cup \{c\}$

---

### 4.2 Common Regular Expression Patterns

#### Basic Patterns

1. **Any string:** $\Sigma^*$ (or $(0 \cup 1)^*$ for binary)
   - Matches all possible strings

2. **At least one:** $R^+ = RR^*$
   - One or more occurrences
   - $(01)^+$ matches "01", "0101", "010101", ...

3. **Optional:** $R \cup \varepsilon$
   - Zero or one occurrence
   - $a(b \cup \varepsilon)$ matches "a" or "ab"

4. **Exactly $n$ occurrences:** $R^n = \underbrace{R R \cdots R}_{n \text{ times}}$
   - $0^3 1$ matches "0001"

5. **Between $m$ and $n$ occurrences:** $R^m \cup R^{m+1} \cup \cdots \cup R^n$

#### String Properties

**Starts with:** $\Sigma^*$ pattern at the end
- Starts with 01: $01\Sigma^*$ or $01(0 \cup 1)^*$

**Ends with:** Pattern at the end
- Ends with 01: $\Sigma^* 01$ or $(0 \cup 1)^* 01$

**Contains:** Pattern in the middle
- Contains 01: $\Sigma^* 01 \Sigma^*$ or $(0 \cup 1)^* 01 (0 \cup 1)^*$

**Does not contain:** More complex (need complementation or careful construction)

---

### 4.3 Writing Regular Expressions (HW2 Q4)

#### Example 1: $L_1 = \{w \mid \text{every even position of } w = w_1w_2\ldots w_n \text{ has a 0}\}$

**Understanding:**
- Positions numbered starting from 1
- Even positions (2, 4, 6, ...) must be 0
- Odd positions (1, 3, 5, ...) can be 0 or 1
- Empty string is included (no even positions to check)

**Pattern:** (odd position)(even position) repeats, plus maybe one final odd position

**Regular expression:**
$$((0 \cup 1)0)^*(\varepsilon \cup 0 \cup 1)$$

**Explanation:**
- $(0 \cup 1)0$ - any symbol followed by 0 (one odd-even pair)
- $((0 \cup 1)0)^*$ - zero or more such pairs
- $(\varepsilon \cup 0 \cup 1)$ - optionally one more odd-position symbol

**Verification:**
- $\varepsilon$ ✓ (no even positions)
- "0" ✓ (position 1 is odd)
- "00" ✓ (position 2 is 0)
- "01" ✗ (position 2 is 1)
- "1001" ✓ (positions 2 and 4 are both 0)

#### Example 2: $L_2 = \{w \mid w \text{ interpreted as a binary number is divisible by 2}\}$

**Understanding:**
- A number is divisible by 2 iff it's even
- In binary, a number is even iff its last bit is 0
- Empty string not included (not a valid number)

**Regular expression:**
$$(0 \cup 1)^* 0$$

**Explanation:**
- $(0 \cup 1)^*$ - any binary string
- $0$ - must end with 0

**Why it works:**
- $10_2 = 2_{10}$ (divisible by 2) ✓
- $100_2 = 4_{10}$ (divisible by 2) ✓
- $11_2 = 3_{10}$ (not divisible by 2) ✗
- Just like decimal: even numbers end in 0,2,4,6,8

---

### 4.4 Converting DFAs to Regular Expressions (GNFA)

#### The GNFA Method
**GNFA** = Generalized Nondeterministic Finite Automaton
- Like an NFA but transitions are labeled with **regular expressions** (not just symbols)
- Used as an intermediate step to convert DFA → Regular Expression

#### The Algorithm

**Step 0: Convert DFA to GNFA**
1. Add new start state with $\varepsilon$-transition to old start
2. Add new single accept state
3. Add $\varepsilon$-transitions from old accept states to new accept state
4. Label existing transitions with symbols (as 1-symbol regular expressions)
5. Add transitions with $\emptyset$ label between states with no transition

**Step 1-n: Remove states one by one**
When removing state $q_{rip}$:
- For each pair of states $q_i$ and $q_j$ (other than $q_{rip}$):
- Replace the path $q_i \to q_{rip} \to q_j$ with a direct edge
- New label: $R_{new}(q_i, q_j) = R(q_i, q_j) \cup R(q_i, q_{rip}) \cdot R(q_{rip}, q_{rip})^* \cdot R(q_{rip}, q_j)$

**Formula explanation:**
- $R(q_i, q_j)$ - existing direct path
- $R(q_i, q_{rip})$ - path to state being removed
- $R(q_{rip}, q_{rip})^*$ - loop on state being removed (zero or more times)
- $R(q_{rip}, q_j)$ - path from state being removed to destination
- Union all options

**Final step:** When only start and accept remain, the label on the edge from start to accept is the answer

#### Detailed Example (HW2 Q5)

**Original DFA:**
- States: $q_0$ (start, accept), $q_1$, $q_2$ (accept)
- Transitions:
  - $q_0 \xrightarrow{0} q_1$
  - $q_0 \xrightarrow{1} q_0$ (self-loop)
  - $q_1 \xrightarrow{0} q_1$ (self-loop)
  - $q_1 \xrightarrow{1} q_2$
  - $q_2 \xrightarrow{0} q_0$
  - $q_2 \xrightarrow{1} q_1$

**Step 0: Convert to GNFA**
Add $q_{start}$ and $q_{accept}$:
- $q_{start} \xrightarrow{\varepsilon} q_0$
- $q_0 \xrightarrow{\varepsilon} q_{accept}$ (since $q_0$ accepts)
- $q_2 \xrightarrow{\varepsilon} q_{accept}$ (since $q_2$ accepts)

**Step 1: Remove $q_1$**

Paths through $q_1$:
- $q_0 \to q_1 \to q_2$: $q_0 \xrightarrow{0} q_1 \xrightarrow{0^*} q_1 \xrightarrow{1} q_2$
  - New: $q_0 \xrightarrow{00^*1} q_2$
- $q_2 \to q_1 \to q_2$: $q_2 \xrightarrow{1} q_1 \xrightarrow{0^*} q_1 \xrightarrow{1} q_2$
  - New: $q_2 \xrightarrow{10^*1} q_2$ (self-loop)

After removing $q_1$:
- $q_0 \xrightarrow{1} q_0$ (self-loop)
- $q_0 \xrightarrow{00^*1} q_2$
- $q_2 \xrightarrow{0} q_0$
- $q_2 \xrightarrow{10^*1} q_2$ (self-loop)

**Step 2: Remove $q_2$**

Paths through $q_2$:
- $q_0 \to q_2 \to q_0$: $q_0 \xrightarrow{00^*1} q_2 \xrightarrow{(10^*1)^*} q_2 \xrightarrow{0} q_0$
  - Combines with existing $q_0 \xrightarrow{1} q_0$
  - New: $q_0 \xrightarrow{1 \cup 00^*1(10^*1)^*0} q_0$
- $q_0 \to q_2 \to q_{accept}$: $q_0 \xrightarrow{00^*1} q_2 \xrightarrow{(10^*1)^*} q_2 \xrightarrow{\varepsilon} q_{accept}$
  - Combines with existing $q_0 \xrightarrow{\varepsilon} q_{accept}$
  - New: $q_0 \xrightarrow{\varepsilon \cup 00^*1(10^*1)^*} q_{accept}$

**Step 3: Remove $q_0$**

Path $q_{start} \to q_0 \to q_{accept}$:
$$\varepsilon \cdot (1 \cup 00^*1(10^*1)^*0)^* \cdot (\varepsilon \cup 00^*1(10^*1)^*)$$

Since $\varepsilon \cdot R = R$:
$$(1 \cup 00^*1(10^*1)^*0)^* (\varepsilon \cup 00^*1(10^*1)^*)$$

**Final Answer:**
$$(1 \cup 00^*1(10^*1)^*0)^*(\varepsilon \cup 00^*1(10^*1)^*)$$

---

### 4.5 Regular Expressions ↔ Finite Automata

#### Equivalence Theorem (Theorem 1.54)
A language is **regular** if and only if some regular expression describes it.

**Proof outline:**
1. **Regular expression → NFA:** Structural induction on regex
   - Base cases: $\varepsilon$, $\emptyset$, $a$ → simple NFAs
   - Union: Use $\varepsilon$-transitions to branch
   - Concatenation: Connect end to start
   - Star: Add loops with $\varepsilon$-transitions

2. **DFA → Regular expression:** GNFA method (described above)

3. **NFA → DFA:** Subset construction (Theorem 1.39)

**Result:** Regular expressions, DFAs, and NFAs all describe exactly the same class of languages: **regular languages**

---

## 5. Non-Regular Languages

### 5.1 The Pumping Lemma

#### What It Is
The **Pumping Lemma** is a property that **all** regular languages must satisfy. 

**Main use:** Prove a language is **not regular** by showing it violates the Pumping Lemma.

#### The Theorem (Pumping Lemma for Regular Languages)

If $L$ is a regular language, then there exists a number $p$ (the "pumping length") such that:

For **any** string $s \in L$ with $|s| \geq p$, we can split $s$ into three parts, $s = xyz$, satisfying:
1. $|y| > 0$ (the middle part is non-empty)
2. $|xy| \leq p$ (the first two parts together are at most length $p$)
3. For all $i \geq 0$, the string $xy^iz \in L$ (we can "pump" $y$ any number of times)

**Intuition:** 
- A DFA with $p$ states must repeat a state when reading a string of length $\geq p$ (Pigeonhole Principle)
- The part of the string between the first and second visit to a repeated state can be "pumped"
- Pumping means: repeat that part 0, 1, 2, 3, ... times and stay in the language

#### How to Use It (Proof by Contradiction)

**Goal:** Prove language $L$ is not regular

**Steps:**
1. **Assume** $L$ is regular
2. The Pumping Lemma guarantees some pumping length $p$ exists
3. **Choose** a specific string $s \in L$ with $|s| \geq p$ (choose cleverly!)
4. **Show** that for **all** possible ways to split $s = xyz$ (following conditions 1-2), there exists some $i$ where $xy^iz \notin L$
5. **Contradiction** with condition 3 of Pumping Lemma
6. **Conclude** $L$ is not regular

**Key insight:** We choose the string $s$, but the adversary chooses how to split it into $xyz$. We must handle all possible splits.

---

### 5.2 Example: $L_1 = \{www \mid w \in \Sigma^*\}$ (HW2 Q6-i)

**Language:** Strings that are three identical copies concatenated
- Examples: $\varepsilon$, "000000" (="00"+"00"+"00"), "010101010101" (="0101"+"0101"+"0101")

**Proof that $L_1$ is not regular:**

**1. Assume** $L_1$ is regular

**2. Pumping Lemma** gives us some pumping length $p$

**3. Choose string:** Let $w = 0^p$ (a string of $p$ zeros), and $s = www = 0^{3p}$
- Clearly $s \in L_1$ (three copies of $0^p$)
- $|s| = 3p \geq p$ ✓

**4. Consider any split** $s = xyz$ with $|y| > 0$ and $|xy| \leq p$

**Analysis:**
- Since $|xy| \leq p$ and $s = 0^{3p}$, both $x$ and $y$ consist only of 0's from the first $p$ symbols
- This means $x$ and $y$ are entirely within the **first copy** of $w$
- We can write: $x = 0^a$, $y = 0^b$, $z = 0^c$ where $a + b \leq p$, $b > 0$, and $a + b + c = 3p$

**5. Pump with** $i = 2$ (add one more copy of $y$):
$$xy^2z = 0^a 0^{2b} 0^c = 0^{a+2b+c} = 0^{3p+b}$$

**Is $0^{3p+b} \in L_1$?**
- For $0^{3p+b}$ to be in $L_1$, we need $0^{3p+b} = www$ for some $w$
- This requires $(3p+b)$ to be divisible by 3
- But $3p$ is divisible by 3, and $0 < b < p$
- So $3p + b$ is NOT divisible by 3 (adding a non-multiple-of-3 to a multiple-of-3)
- Therefore, we cannot write $0^{3p+b}$ as three equal parts
- Thus $xy^2z \notin L_1$ ✗

**6. Contradiction!** The Pumping Lemma says $xy^2z$ must be in $L_1$, but we showed it's not.

**Conclusion:** $L_1$ is not regular. $\square$

---

### 5.3 Example: $L_2 = \{1^{2^n} \mid n \geq 1\}$ (HW2 Q6-ii)

**Language:** Strings of 1's where the length is a power of 2
- Examples: "11" ($2^1$), "1111" ($2^2$), "11111111" ($2^3$), ...
- NOT in language: "111" (length 3), "11111" (length 5)

**Proof that $L_2$ is not regular:**

**1. Assume** $L_2$ is regular

**2. Pumping Lemma** gives us some pumping length $p$

**3. Choose string:** $s = 1^{2^p}$
- Clearly $s \in L_2$ (length is $2^p$, which is a power of 2)
- $|s| = 2^p \geq p$ ✓ (for $p \geq 1$)

**4. Consider any split** $s = xyz$ with $|y| > 0$ and $|xy| \leq p$

**Analysis:**
- From conditions: $0 < |y| \leq |xy| \leq p$
- So $1 \leq |y| \leq p$

**5. Pump with** $i = 2$:
$$|xy^2z| = |xyz| + |y| = 2^p + |y|$$

**Find bounds:**
- Lower bound: $|xy^2z| = 2^p + |y| > 2^p$ (since $|y| > 0$)
- Upper bound: $|xy^2z| = 2^p + |y| \leq 2^p + p$

**Key inequality:** For $p \geq 1$, we have $p < 2^p$ (exponential grows faster than linear)

Therefore:
$$2^p + p < 2^p + 2^p = 2 \cdot 2^p = 2^{p+1}$$

Combining:
$$2^p < |xy^2z| \leq 2^p + p < 2^{p+1}$$

**6. Contradiction:**
- For $xy^2z \in L_2$, its length must be a power of 2
- But $|xy^2z|$ is strictly between $2^p$ and $2^{p+1}$
- There are **no powers of 2** between consecutive powers of 2!
- Therefore $xy^2z \notin L_2$ ✗

**Conclusion:** $L_2$ is not regular. $\square$

---

### 5.4 Tips for Using the Pumping Lemma

#### Choosing the String
1. **Choose a string that depends on $p$** (the pumping length)
   - Common: $0^p 1^p$, $0^{p!}$, $1^{2^p}$
2. **Choose a string that's "on the edge"** of the language's property
3. **Make it simple** so you can analyze what pumping does

#### Handling All Possible Splits
- You don't choose $x$, $y$, $z$ - the adversary does
- Use the constraints to limit possibilities:
  - $|xy| \leq p$ tells you where $y$ can be
  - $|y| > 0$ tells you $y$ is not empty
- Show that **no matter** how they split it (within constraints), pumping fails

#### Common Proof Strategies

1. **Imbalance counting:** Show pumping creates mismatch in counts
   - Example: $\{0^n 1^n\}$ - pumping in 0's makes counts unequal

2. **Gap in sequence:** Show pumped length falls between valid lengths
   - Example: $\{1^{n^2}\}$ - pumped length between consecutive squares

3. **Pattern destruction:** Show pumping breaks required pattern
   - Example: $\{ww\}$ - pumping makes two halves different

---

## 6. Closure Properties

### 6.1 What are Closure Properties?

#### Definition
A class of languages is **closed** under an operation if applying that operation to languages in the class always produces another language in the class.

**Example:** Regular languages are closed under union means:
- If $L_1$ and $L_2$ are regular
- Then $L_1 \cup L_2$ is also regular

#### Why They Matter
1. **Build complex languages:** Combine simple regular languages using operations
2. **Prove regularity:** Show a language is regular without building a DFA/NFA
3. **Prove non-regularity:** If a language can be built from regular languages using closed operations, it's regular; otherwise, explore non-regularity

---

### 6.2 Regular Languages are Closed Under Union

#### Theorem
If $L_1$ and $L_2$ are regular languages, then $L_1 \cup L_2$ is regular.

#### Proof (Using NFAs)
**Given:** DFAs $M_1$ and $M_2$ recognizing $L_1$ and $L_2$

**Construct NFA $N$:**
- New start state with $\varepsilon$-transitions to both $M_1$ and $M_2$ start states
- Nondeterministically "guess" which machine should accept
- Accept if either $M_1$ or $M_2$ accepts

**Formal construction:**
- $Q = Q_1 \cup Q_2 \cup \{q_0\}$ (combine states, add new start)
- $F = F_1 \cup F_2$ (accept if either accepts)
- $\delta(q_0, \varepsilon) = \{q_{01}, q_{02}\}$ (start both machines)
- Other transitions from $M_1$ and $M_2$ unchanged

**Result:** $L(N) = L(M_1) \cup L(M_2) = L_1 \cup L_2$, which is regular. $\square$

---

### 6.3 Regular Languages are Closed Under Concatenation

#### Theorem
If $L_1$ and $L_2$ are regular languages, then $L_1 \circ L_2 = \{xy \mid x \in L_1, y \in L_2\}$ is regular.

#### Proof (Using NFAs)
**Construct NFA:**
- Start with $M_1$
- Add $\varepsilon$-transitions from accept states of $M_1$ to start state of $M_2$
- Accept states are only those from $M_2$
- Nondeterministically "guess" where to split input between $L_1$ and $L_2$

**Result:** Accepts $xy$ iff $x \in L_1$ and $y \in L_2$. $\square$

---

### 6.4 Regular Languages are Closed Under Star

#### Theorem
If $L$ is a regular language, then $L^* = \{\varepsilon\} \cup L \cup LL \cup LLL \cup \cdots$ is regular.

#### Proof (Using NFAs)
**Construct NFA:**
- New start state (which is also an accept state, for $\varepsilon$)
- $\varepsilon$-transition from new start to old start
- $\varepsilon$-transitions from old accept states back to old start (for repetition)
- Accept if we've completed 0 or more cycles through $M$

**Result:** Accepts strings in $L^*$, which is regular. $\square$

---

### 6.5 Regular Languages are Closed Under Intersection

#### Theorem
If $L_1$ and $L_2$ are regular languages, then $L_1 \cap L_2$ is regular.

#### Proof (Product Construction)
**Given:** DFAs $M_1 = (Q_1, \Sigma, \delta_1, q_{01}, F_1)$ and $M_2 = (Q_2, \Sigma, \delta_2, q_{02}, F_2)$

**Construct DFA $M$:**
- $Q = Q_1 \times Q_2$ (pairs of states - simulate both machines in parallel)
- $\delta((q_1, q_2), a) = (\delta_1(q_1, a), \delta_2(q_2, a))$
- $q_0 = (q_{01}, q_{02})$
- $F = F_1 \times F_2$ (accept only if both machines accept)

**How it works:**
- The DFA $M$ runs both $M_1$ and $M_2$ simultaneously
- It tracks the current state of each machine as an ordered pair $(q_1, q_2)$
- It accepts only if both machines would accept
- Therefore, $L(M) = L(M_1) \cap L(M_2) = L_1 \cap L_2$

**Result:** $M$ accepts iff both $M_1$ and $M_2$ accept. $\square$

---

### 6.6 Additional Closure Properties (Not from Slides)

**Note:** The following closure properties were NOT covered in the lecture slides, but are important to know. Set Difference was covered in HW1 Q5.

#### Complement

**Theorem:** If $L$ is a regular language over alphabet $\Sigma$, then $\overline{L} = \Sigma^* \setminus L$ is regular.

**Proof (Using DFAs):**
- Given: DFA $M = (Q, \Sigma, \delta, q_0, F)$ recognizing $L$
- Construct DFA $M' = (Q, \Sigma, \delta, q_0, Q \setminus F)$
- Same as $M$ but swap accept and non-accept states
- $M'$ accepts exactly when $M$ rejects
- Therefore $L(M') = \overline{L}$ $\square$

**Important:** This requires a DFA with complete transition function.

#### Set Difference (HW1 Q5)

**Theorem:** If $L_1$ and $L_2$ are regular languages, then $L_1 \setminus L_2 = \{w \in L_1 \mid w \notin L_2\}$ is regular.

**Proof (Direct Product Construction):**
- Given: DFAs $M_1 = (Q_1, \Sigma, \delta_1, q_{01}, F_1)$ and $M_2 = (Q_2, \Sigma, \delta_2, q_{02}, F_2)$
- Construct DFA $M$:
  - $Q = Q_1 \times Q_2$ (simulate both in parallel)
  - $\delta((q_1, q_2), a) = (\delta_1(q_1, a), \delta_2(q_2, a))$
  - $q_0 = (q_{01}, q_{02})$
  - $F = \{(q_1, q_2) \mid q_1 \in F_1 \text{ and } q_2 \notin F_2\}$
- Accept when $M_1$ accepts AND $M_2$ rejects
- This directly captures $L_1 \setminus L_2$ $\square$

**Alternative proof:** $L_1 \setminus L_2 = L_1 \cap \overline{L_2}$ (using complement and intersection)

---

### 6.7 Summary of Closure Properties

#### From Lecture Slides (Theorems 1.16, 1.19, 1.23, 1.26)

| Operation | Regular? | Proof Technique | Theorem |
|-----------|----------|----------------|---------|
| **Union** | ✓ Yes | NFA with $\varepsilon$-transitions | Theorem 1.16 |
| **Concatenation** | ✓ Yes | NFA with $\varepsilon$-transitions | Theorem 1.19 |
| **Star** | ✓ Yes | NFA with $\varepsilon$-loops | Theorem 1.23 |
| **Intersection** | ✓ Yes | Product construction | Theorem 1.26 |

#### Additional (Not from Slides)

| Operation | Regular? | Proof Technique |
|-----------|----------|----------------|
| Complement | ✓ Yes | Swap accept/reject states (DFA) |
| Set Difference | ✓ Yes | Product construction (HW1 Q5) |
| Reversal | ✓ Yes | Reverse all transitions, swap start/accept |
| Homomorphism | ✓ Yes | Replace each symbol with its image |

**Application:** These properties let us build complex regular languages from simpler ones.

---

## 7. State Minimization and Complexity

### 7.1 Distinguishability

#### Definition
Two states $p$ and $q$ in a DFA are **distinguishable** if there exists a string $w$ such that:
- Starting from $p$ and reading $w$ leads to an accept state, but
- Starting from $q$ and reading $w$ leads to a reject state (or vice versa)

Formally: $\delta^*(p, w) \in F$ and $\delta^*(q, w) \notin F$ (or opposite)

If no such string $w$ exists, $p$ and $q$ are **indistinguishable** (or **equivalent**).

#### Why It Matters
- Indistinguishable states can be merged without changing the language
- Minimization algorithms merge indistinguishable states to create smallest equivalent DFA
- Used in proving lower bounds on DFA size

---

### 7.2 Myhill-Nerode Theorem

#### Theorem
The following are equivalent for a language $L$:
1. $L$ is regular
2. $L$ is the union of equivalence classes of a right-invariant equivalence relation of finite index
3. The number of equivalence classes of the relation $\equiv_L$ is finite

**Relation $\equiv_L$:** For strings $x, y \in \Sigma^*$, define $x \equiv_L y$ if:
$$\forall z \in \Sigma^*: (xz \in L \Leftrightarrow yz \in L)$$

That is, $x$ and $y$ are equivalent if they can be extended in the same ways to strings in $L$.

#### Consequences
1. **Minimization:** Every regular language has a unique minimal DFA (up to state renaming)
2. **Lower bounds:** To show a DFA for $L$ needs at least $n$ states, find $n$ pairwise distinguishable strings
3. **Non-regularity:** If $L$ has infinitely many equivalence classes, $L$ is not regular

---

### 7.3 DFA Size Lower Bounds (Related to HW2 Q3)

#### Example: $L_k = \Sigma^* 1 \Sigma^{k-1}$

**Claim:** Any DFA for $L_k$ needs at least $2^k$ states.

**Proof:**
Consider all strings of length $k$: there are $2^k$ such strings.

**Show they are pairwise distinguishable:**
- Take two different strings $x, y \in \{0,1\}^k$ with $x \neq y$
- They differ in some position $i$ (say $x_i \neq y_i$)
- WLOG, assume $x_i = 1$ and $y_i = 0$
- Let $z$ be any string of length $k - i$

**Distinguish them:**
- $xz$: the $k$-th symbol from the end is $x_i = 1$, so $xz \in L_k$
- $yz$: the $k$-th symbol from the end is $y_i = 0$, so $yz \notin L_k$
- Therefore $x$ and $y$ are distinguishable

**Conclusion:**
- We have $2^k$ pairwise distinguishable strings
- A DFA must have at least one state for each equivalence class
- Therefore, any DFA for $L_k$ needs at least $2^k$ states $\square$

**Contrast with NFA:** An NFA for $L_k$ needs only $k+1$ states (use nondeterminism to guess where the target 1 is).

---

### 7.4 State Minimization Algorithm (Optional/Advanced)

#### Table-Filling Algorithm
**Goal:** Find all pairs of distinguishable states

**Algorithm:**
1. **Initialize:** Mark all pairs $(p, q)$ where exactly one of $p, q$ is in $F$ (base case: distinguishable by $\varepsilon$)
2. **Iterate:** For each unmarked pair $(p, q)$ and each symbol $a$:
   - If $(\delta(p, a), \delta(q, a))$ is marked, mark $(p, q)$
3. **Repeat** step 2 until no new marks
4. **Merge:** All unmarked pairs are indistinguishable - merge them

**Result:** Minimal DFA equivalent to original DFA

#### Complexity
- $O(n^2)$ space (table of pairs)
- $O(n^2 \cdot |\Sigma|)$ time
- Where $n = |Q|$ is number of states

---

## 8. Important Algorithms and Techniques Summary

### 8.1 Converting Between Representations

| From | To | Method | Complexity |
|------|----|----|---|
| DFA | NFA | Identity (DFA is an NFA) | $O(1)$ |
| NFA | DFA | Subset construction | $O(2^n)$ states |
| DFA | Regular Expression | GNFA method | Exponential in states |
| Regular Expression | NFA | Structural induction | Linear in regex size |
| NFA | Regular Expression | Convert to DFA, then GNFA | Doubly exponential |

### 8.2 Proving a Language is Regular

**Methods:**
1. **Build a DFA/NFA** that recognizes it
2. **Build a regular expression** that describes it
3. **Show it's built from regular languages** using closure properties

### 8.3 Proving a Language is Not Regular

**Method:** Use the Pumping Lemma
1. Assume language is regular
2. Choose a string $s$ (depending on pumping length $p$)
3. Show that for all splits $s = xyz$ (satisfying conditions), some $xy^iz$ is not in the language
4. Contradiction with Pumping Lemma
5. Conclude language is not regular

**Alternative:** Use Myhill-Nerode (show infinitely many equivalence classes)

---

## 9. Key Theorems and Results

### Regular Languages - Core Theorems

**From Lecture Slides:**
1. **Theorem 1.16:** The class of regular languages is closed under union
2. **Theorem 1.19:** The class of regular languages is closed under concatenation
3. **Theorem 1.23:** The class of regular languages is closed under star
4. **Theorem 1.26:** The class of regular languages is closed under intersection
5. **Theorem 1.39:** Every NFA has an equivalent DFA
6. **Theorem 1.54:** A language is regular iff some regular expression describes it
7. **Pumping Lemma (Theorem 1.70):** All regular languages satisfy the pumping property

**Additional (Not explicitly in slides):**
- **Theorem 1.25:** The class of regular languages is closed under complement
- **Myhill-Nerode Theorem:** Minimality and uniqueness of DFAs

---

## 10. Practice Problems and Strategies

### Types of Problems You Might See

1. **Drawing DFAs/NFAs**
   - Understand what property to track
   - Use states to encode relevant history
   - Verify with test strings

2. **Interpreting state machines**
   - Trace execution on small inputs
   - Characterize what each state represents
   - Generalize to describe the language

3. **Converting between representations**
   - DFA ↔ NFA ↔ Regular Expression
   - Follow systematic algorithms
   - Check your work with test strings

4. **Closure proofs**
   - Know standard constructions (product, union via $\varepsilon$-transitions)
   - Argue why construction is correct

5. **Pumping Lemma proofs**
   - Choose string cleverly (depends on $p$)
   - Handle all possible splits
   - Show pumping breaks language property

6. **Set theory and proofs**
   - Basic set operations
   - Induction proofs
   - Formal notation and definitions

---

## 11. Common Mistakes to Avoid

### When Building DFAs/NFAs
- ❌ Forgetting to handle all symbols from all states (DFA must be complete)
- ❌ Not marking start state or accept states correctly
- ❌ Confusing "or" with "and" in language descriptions

### When Using Pumping Lemma
- ❌ Trying to choose how to split the string (you can't - adversary does)
- ❌ Only showing one split fails (must show ALL splits fail)
- ❌ Choosing a string not in the language
- ❌ Choosing a string too short ($|s| < p$)

### When Writing Regular Expressions
- ❌ Forgetting precedence rules (star > concatenation > union)
- ❌ Confusing $\varepsilon$ (empty string) with $\emptyset$ (empty set)
- ❌ Not handling edge cases (empty string, single symbols)

### When Converting NFA to DFA
- ❌ Forgetting $\varepsilon$-closures
- ❌ Not considering all reachable subset states
- ❌ Incorrect accept state marking (need at least one NFA accept state in subset)

---

## 12. Quick Reference Formulas

### Set Theory
- **Cartesian product:** $|A \times B| = |A| \cdot |B|$
- **Power set:** $|\mathcal{P}(A)| = 2^{|A|}$
- **DeMorgan's Laws:** $\overline{A \cup B} = \overline{A} \cap \overline{B}$ and $\overline{A \cap B} = \overline{A} \cup \overline{B}$

### Automata
- **DFA states in subset construction:** Up to $2^n$ where $n = |Q_{NFA}|$
- **String length over binary alphabet:** $|\Sigma^n| = 2^n$ for $\Sigma = \{0,1\}$

### Regular Expressions
- **Common patterns:**
  - At least one: $R^+ = RR^*$
  - Optional: $R \cup \varepsilon$
  - Exactly $n$: $R^n$

### Pumping Lemma
- Must have: $|y| > 0$ and $|xy| \leq p$
- For all $i \geq 0$: $xy^iz \in L$

---

## 13. Study Tips

### For the Exam

1. **Practice drawing automata** - this is a skill that improves with repetition
2. **Memorize the Pumping Lemma** - know it word-for-word
3. **Understand closure proofs** - know the constructions, not just the statements
4. **Work through examples** - theory makes sense when you see it applied
5. **Check your work** - test your DFAs/NFAs with strings
6. **Write clearly** - especially for proofs, show all steps

### Key Things to Memorize

- Formal definition of DFA (5-tuple)
- Formal definition of NFA (5-tuple with power set)
- Pumping Lemma statement
- Which operations regular languages are closed under
- Regular expression operations and precedence

### Understanding vs. Memorizing

**Understand:**
- Why subset construction works
- Why pumping lemma proves non-regularity
- How closure properties help build languages

**Memorize:**
- Formal definitions
- Pumping lemma statement
- Common language patterns and their automata

---

## 14. Additional Examples

### Example: Binary numbers divisible by 3

**Language:** $L = \{w \in \{0,1\}^* \mid w \text{ interpreted as binary number is divisible by 3}\}$

**DFA approach:**
- States represent remainder when divided by 3: $\{q_0, q_1, q_2\}$
- $q_0$ is start and accept (remainder 0)
- Transitions: Reading bit $b$ in state $q_i$, go to state $q_j$ where $j = (2i + b) \mod 3$

**Why it works:** Reading a new bit doubles the number and adds the bit (in binary), which we can track mod 3

### Example: Equal number of 0s and 1s

**Language:** $L = \{w \in \{0,1\}^* \mid \#_0(w) = \#_1(w)\}$

**Claim:** This language is NOT regular

**Proof:** Use Pumping Lemma
- Choose $s = 0^p 1^p$ (clearly in $L$)
- Any split with $|xy| \leq p$ means $y = 0^k$ for some $k > 0$
- $xy^2z = 0^{p+k} 1^p$ has more 0s than 1s
- So $xy^2z \notin L$ ✗
- Contradiction! $\square$

---

## Conclusion

This review covers all the major topics from the introduction to Theory of Computation and Regular Languages:
- Mathematical foundations (sets, induction)
- Finite Automata (DFA, NFA)
- Regular Expressions
- Non-Regular Languages (Pumping Lemma)
- Closure Properties
- Algorithms and Complexity

**Remember:** Theory of Computation is about understanding computational limits and capabilities. Regular languages are the simplest class - limited memory (finite states), but still powerful enough for many applications (lexical analysis, pattern matching, etc.).

**Good luck on your exam!** 🎓

