# Turing Machines and the Church-Turing Thesis

## Table of Contents
- [Introduction to Turing Machines](#introduction-to-turing-machines)
- [Formal Definition](#formal-definition)
- [How Turing Machines Compute](#how-turing-machines-compute)
- [Configuration Notation](#configuration-notation)
- [Turing-Recognizable vs Turing-Decidable](#turing-recognizable-vs-turing-decidable)
- [Example Turing Machines](#example-turing-machines)
- [Variants of Turing Machines](#variants-of-turing-machines)
- [The Church-Turing Thesis](#the-church-turing-thesis)

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
$M = (Q, Σ, Γ, δ, q₀, q_{accept}, q_{reject})$

Where:
- **Q**: Finite set of states
- **Σ**: Input alphabet (does not contain the blank symbol $\sqcup$)
- **Γ**: Tape alphabet (where $\sqcup$ ∈ Γ and Σ ⊆ Γ)
- **δ**: Transition function $Q × Γ → Q × Γ × {L, R}$
- **q₀**: Start state ($q₀ ∈ Q$)
- **$q_{accept}$**: Accept state
- **$q_{reject}$**: Reject state ($q_{reject} ≠ q_{accept}$)

---

## How Turing Machines Compute

**Transition Function:**
$δ(q, a) = (r, b, D)$ means:
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

**Example:** $1011q₇01111$ means:
- Tape: $101101111$
- Current state: $q₇$
- Head position: On the second $0$ (the first symbol of $01111$)

**Yielding:** Configuration $C₁$ yields $C₂$ if TM can go from $C₁$ to $C₂$ in one step

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

## Example Turing Machines

### Example 1: $\{0²ⁿ | n ≥ 0\}$ (Powers of 2)
**TM M₂ Algorithm:**
```
1. Sweep left to right, crossing off every other 0
2. If single 0 remains, accept
3. If odd number of 0s (>1), reject
4. Return head to left end
5. Go to step 1
```

**Formal Description:**
- States: $\{q₁, q₂, q₃, q₄, q₅, q_accept, q_reject\}$
- Tape alphabet: $\{0, x, \sqcup\}$
- Uses state diagram with transitions like $0→x, R$

### Example 2: $\{aⁱbʲcᵏ | i × j = k and i, j, k ≥ 1\}$
**TM M₃ Algorithm:**
```
1. Verify input is of form a⁺b⁺c⁺
2. For each a:
   - Cross off one a
   - For each b: cross off one b and one c
   - Restore b's and repeat
3. If all c's are crossed off when all a's are gone, accept
```

---

## Variants of Turing Machines

### Multitape Turing Machines
- **k tapes**, each with independent read/write heads
- Transition function: $δ: Q × Γᵏ → Q × Γᵏ × {L, R, S}ᵏ$
- **Theorem:** Every multitape TM has an equivalent single-tape TM
- **Simulation:** Use single tape with separators ($\#$) and marked symbols to track head positions

### Nondeterministic Turing Machines
- Transition function: $δ: Q × Γ → P(Q × Γ × {L, R})$
- Accepts input if **any** computation path leads to accept
- **Theorem:** Every nondeterministic TM has an equivalent deterministic TM
- **Simulation:** Use BFS on computation tree using address strings to track paths.

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
- The set $D = \{p | p is a polynomial with an integral root\}$ is:
  - **Turing-recognizable** (we can systematically search for roots)
  - **Not Turing-decidable** (no algorithm always halts with correct answer)
- For **single-variable** polynomials, the problem **is** decidable
- The Church-Turing thesis establishes Turing machines as the formal equivalent of our intuitive concept of computation
