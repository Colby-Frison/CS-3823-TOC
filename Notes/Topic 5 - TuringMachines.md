# Turing Machines and the Church-Turing Thesis

## Table of Contents
- [Introduction to Turing Machines](#introduction-to-turing-machines)
- [Formal Definition](#formal-definition)
- [How Turing Machines Compute](#how-turing-machines-compute)
- [Configuration Notation](#configuration-notation)
- [Turing-Recognizable vs Turing-Decidable](#turing-recognizable-vs-turing-decidable)
- [Variants of Turing Machines](#variants-of-turing-machines)
- [The Church-Turing Thesis](#the-church-turing-thesis)
- [Examples](#examples)

---

## Introduction to Turing Machines

Turing Machines (TMs) are theoretical computing devices that extend the capabilities of finite automata by adding:
- **Unlimited memory** in the form of an infinite tape
- **Read/write capability** that can move in both directions
- **Accept and reject states** that immediately halt computation

**Key Differences from Finite Automata:**
1. Can **write** on the tape (not just read)
2. Read/write head can move **both left and right**
3. Tape is **infinite** (extends indefinitely)
4. Special **accept/reject states** take effect immediately

**Basic Operation:**
- Input string written on leftmost squares of tape
- Rest of tape filled with blank symbols ($\sqcup$)
- Head starts at leftmost position
- Computation continues until accept/reject state reached

---

## Formal Definition

A Turing Machine is a 7-tuple:
$$M = (Q, \Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject})$$

Where:
- **Q**: Finite set of states
- **Σ**: Input alphabet (does not contain the blank symbol $\sqcup$)
- **Γ**: Tape alphabet (where $\sqcup \in \Gamma$ and $\Sigma \subseteq \Gamma$)
- **δ**: Transition function $Q \times \Gamma \to Q \times \Gamma \times \{L, R\}$
- **$q_0$**: Start state ($q_0 \in Q$)
- **$q_{accept}$**: Accept state
- **$q_{reject}$**: Reject state ($q_{reject} \neq q_{accept}$)

---

## How Turing Machines Compute

**Transition Function:**
$\delta(q, a) = (r, b, D)$ means:
- In state $q$, reading symbol $a$
- Go to state $r$, write symbol $b$, move direction $D$ (Left/Right)

**Special Cases:**
- Moving left at leftmost position leaves head in place
- Computation halts immediately upon entering $q_{accept}$ or $q_{reject}$

---

## Configuration Notation

A configuration represents the complete state of a TM at any point:

**Format:** $u q v$
- $u$: Tape content to the left of head
- $q$: Current state
- $v$: Tape content at and to the right of head (head on first symbol of $v$)

**Example:** $1011q_701111$ means:
- Tape: $101101111$
- Current state: $q_7$
- Head position: On the second $0$ (the first symbol of $01111$)

**Yielding:** Configuration $C_1$ yields $C_2$ if TM can go from $C_1$ to $C_2$ in one step

---

## Turing-Recognizable vs Turing-Decidable

### Turing-Recognizable (Recursively Enumerable)
- A language $L$ is Turing-recognizable if some TM $M$ accepts all strings in $L$
- $M$ may loop forever on strings not in $L$
- TM **recognizes** the language

### Turing-Decidable (Recursive)
- A language $L$ is Turing-decidable if some TM $M$:
  - Accepts all strings in $L$
  - Rejects all strings not in $L$
- $M$ always halts on every input
- TM **decides** the language

**Relationship:** All decidable languages are recognizable, but not vice versa.

---

## Variants of Turing Machines

### Multitape Turing Machines
- **k tapes**, each with independent read/write heads
- Transition function: $\delta: Q \times \Gamma^k \to Q \times \Gamma^k \times \{L, R, S\}^k$
- **Theorem:** Every multitape TM has an equivalent single-tape TM
- **Simulation:** Use single tape with separators ($\#$) and marked symbols to track head positions

### Nondeterministic Turing Machines
- Transition function: $\delta: Q \times \Gamma \to \mathcal{P}(Q \times \Gamma \times \{L, R\})$
- Accepts input if **any** computation path leads to accept
- **Theorem:** Every nondeterministic TM has an equivalent deterministic TM
- **Simulation:** Use BFS on computation tree using address strings to track paths

### Enumerators
- TM with attached printer
- Prints out all strings in the language (in any order, with possible repetition)
- **Theorem:** A language is Turing-recognizable iff some enumerator enumerates it

**Equivalence:** All these variants recognize the same class of languages.

---

## The Church-Turing Thesis

### Historical Context
- **1900:** Hilbert's 23 problems, including the 10th problem:
  *"Is there an algorithm to determine if a polynomial has an integral root?"*
- **1936:** Church (λ-calculus) and Turing (Turing machines) independently formalize the notion of algorithm
- **1970:** Matijasevic proves no such algorithm exists for Hilbert's 10th problem

### The Thesis
**"The intuitive notion of algorithms equals Turing machine algorithms"**

### Key Implications
- The set $D = \{p \mid p \text{ is a polynomial with an integral root}\}$ is:
  - **Turing-recognizable** (we can systematically search for roots)
  - **Not Turing-decidable** (no algorithm always halts with correct answer)
- For **single-variable** polynomials, the problem **is** decidable
- The Church-Turing thesis establishes Turing machines as the formal equivalent of our intuitive concept of computation

---

## Examples

### Example 1: Turing Machine for $\{0^n1^n \mid n \geq 1\}$

**Problem:** Design a deterministic Turing Machine $M_1$ that recognizes the language $L_3 = \{0^n1^n \mid n \geq 1\}$ over $\Sigma = \{0,1\}$.

**Algorithm:**
1. Mark the leftmost unmarked $0$ with a special symbol (e.g., $Y$)
2. Move right to find the leftmost unmarked $1$
3. Mark that $1$ with $Y$
4. Move back left to find the next unmarked $0$
5. Repeat until all $0$'s are marked
6. Verify that only $Y$'s remain (no unmarked $1$'s)
7. Accept if verification passes; reject otherwise

**State Description:**
- $q_0$: Start state, look for first $0$ to mark
- $q_1$: Moving right to find first unmarked $1$
- $q_2$: Moving left to return to $0$'s section
- $q_3$: Verification state, checking that only $Y$'s remain
- $q_{accept}$: Accept state
- $q_{reject}$: Reject state

**Key Transitions:**
- $q_0$: On $0$, write $Y$, move right, go to $q_1$
- $q_0$: On $1$ or $\sqcup$, reject (wrong format)
- $q_1$: On $0$ or $Y$, move right, stay in $q_1$
- $q_1$: On $1$, write $Y$, move left, go to $q_2$
- $q_1$: On $\sqcup$, reject (ran out of $1$'s)
- $q_2$: On $0$ or $Y$, move left, stay in $q_2$
- $q_2$: On $\sqcup$, move right, go to $q_0$ (start next iteration)
- $q_2$: On $1$, reject (found $1$ in $0$'s section)
- $q_0$: On $Y$, move right, go to $q_3$ (all $0$'s marked)
- $q_3$: On $Y$, move right, stay in $q_3$
- $q_3$: On $\sqcup$, accept
- $q_3$: On $0$ or $1$, reject (unmarked symbols remain)

**Is $M_1$ a decider?**

**Yes**, $M_1$ is a decider.

**Proof that $M_1$ Always Halts:**

A Turing machine is a decider if it:
1. Accepts all strings in the language
2. Rejects all strings not in the language  
3. Always halts (never loops infinitely) on every input

**Termination Analysis:**

For any input string $w$:
- Each complete iteration ($q_0 \to q_1 \to q_2 \to q_0$) marks exactly one $0$ and one $1$
- Maximum possible iterations = $\min(\text{count}(0), \text{count}(1)) \leq |w|/2$
- Each iteration performs bounded work:
  - $q_0$: Scans through at most $|w|$ symbols
  - $q_1$: Scans through at most $|w|$ symbols  
  - $q_2$: Scans through at most $|w|$ symbols
- Total operations $\leq |w|^3$ (polynomial bound)

**Case Analysis:**

1. **$w \in L_3 = \{0^n1^n \mid n \geq 1\}$:**
   - Exactly $n$ iterations, each marking one $(0,1)$ pair
   - Ends in $q_3$, verifies only $Y$'s remain, accepts
   - **Halts in accept state**

2. **$w \notin L_3$:**
   - **Wrong count ($0^n1^m$, $n \neq m$):** Either runs out of $1$'s in $q_1$ ($n>m$) or finds unmarked $1$'s in $q_3$ ($n<m$)
   - **Wrong order:** Rejects immediately in $q_0$ ($1$ before $0$) or $q_2$ ($1$ in $0$'s region)
   - **Mixed pattern:** Rejects in $q_3$ when finding $0/1$ during verification
   - **Empty string:** Rejects immediately in $q_0$
   - **Always halts in reject state**

**No Infinite Loops Possible:**
- The number of unmarked symbols strictly decreases each iteration
- Machine progresses monotonically through the input
- All transitions are well-defined for all symbols
- No cycles exist except the productive marking cycle

**Conclusion:**
Since $M_1$:
- **Accepts** all strings in $L_3$
- **Rejects** all strings not in $L_3$  
- **Halts on every input** in finite time

**$M_1$ is a decider** and therefore **$L_3$ is Turing-decidable**.

---

### Example 2: Powers of 2

**Problem:** Design a TM that recognizes $\{0^{2^n} \mid n \geq 0\}$ (strings with length equal to a power of 2).

**TM $M_2$ Algorithm:**
```
1. Sweep left to right, crossing off every other 0
2. If single 0 remains, accept
3. If odd number of 0s (>1), reject
4. Return head to left end
5. Go to step 1
```

**Formal Description:**
- States: $\{q_1, q_2, q_3, q_4, q_5, q_{accept}, q_{reject}\}$
- Tape alphabet: $\{0, x, \sqcup\}$
- Uses state diagram with transitions like $0 \to x, R$

**How it works:**
- Each iteration halves the number of $0$'s
- If we can repeatedly halve until we get exactly one $0$, the original length was a power of 2
- If we get an odd number (>1) at any point, reject
- Accept when exactly one $0$ remains

**Example trace for $0000$ (length 4 = $2^2$):**
1. First pass: Cross off every other $0$ → $x0x0$
2. Second pass: Cross off every other remaining $0$ → $x0xx$ (one $0$ remains)
3. Accept

**Example trace for $00000$ (length 5, not a power of 2):**
1. First pass: Cross off every other $0$ → $x0x0x$ (odd number remains)
2. Reject

