# Pushdown Automata (PDAs)

## Table of Contents
- [Introduction to PDAs](#introduction-to-pdas)
- [Formal Definition of PDA](#formal-definition-of-pda)
- [How PDAs Compute](#how-pdas-compute)
- [PDA Notation and State Diagrams](#pda-notation-and-state-diagrams)
- [Equivalence with Context-Free Grammars](#equivalence-with-context-free-grammars)
- [Relationship with Regular Languages](#relationship-with-regular-languages)
- [Key Properties of PDAs](#key-properties-of-pdas)
- [Examples](#examples)

---

## Introduction to PDAs

Pushdown Automata (PDAs) are computational models that extend the capabilities of finite automata by adding a **stack** (last-in, first-out memory). This additional memory allows PDAs to recognize languages that cannot be recognized by finite automata alone, particularly **context-free languages**.

**Key motivations for PDAs:**
- Finite automata cannot recognize languages like $\{0^n1^n \mid n \geq 0\}$
- Context-free grammars (CFGs) describe programming language syntax
- PDAs provide an automata-based approach to recognizing context-free languages

**Power of PDAs:**
- Nondeterministic PDAs are equivalent in power to context-free grammars
- Deterministic PDAs are less powerful than nondeterministic ones
- PDAs can recognize all context-free languages

---

## Formal Definition of PDA

A pushdown automaton is formally defined as a 6-tuple:

$M = (Q, \Sigma, \Gamma, \delta, q_0, F)$

Where:
- **Q**: Finite set of states
- **Σ**: Input alphabet
- **Γ**: Stack alphabet
- **δ**: Transition function $Q \times \Sigma_\varepsilon \times \Gamma_\varepsilon \to \mathcal{P}(Q \times \Gamma_\varepsilon)$
- **$q_0$**: Start state ($q_0 \in Q$)
- **F**: Set of accept states ($F \subseteq Q$)

**Notation:**
- $\Sigma_\varepsilon = \Sigma \cup \{\varepsilon\}$ (input alphabet including empty string)
- $\Gamma_\varepsilon = \Gamma \cup \{\varepsilon\}$ (stack alphabet including empty string)
- $\mathcal{P}(Q \times \Gamma_\varepsilon)$ denotes the power set of $Q \times \Gamma_\varepsilon$

---

## How PDAs Compute

A PDA **accepts** an input string $w$ if there exists some computation path where:

1. **Initialization**: Starts in state $q_0$ with an empty stack
2. **Transitions**: Moves according to $\delta$, reading input and modifying stack
3. **Acceptance**: There are two equivalent ways a PDA can accept:

### Acceptance by Final State

The PDA accepts if:
- All input has been read
- The PDA ends in an accept state (a state in $F$)
- The stack contents don't matter (can be empty or non-empty)

This is the method used in the formal definition above, where $F$ is the set of accept states.

### Acceptance by Empty Stack

The PDA accepts if:
- All input has been read
- The stack is completely empty
- The current state doesn't matter (can be any state)

**Note:** In this model, we don't need a set of accept states $F$ since acceptance is determined solely by the empty stack condition.

### Equivalence of Acceptance Methods

**Theorem:** A language is accepted by a PDA using final state acceptance **if and only if** it is accepted by a PDA using empty stack acceptance.

**Key insight:** We can convert between the two methods:
- **Final state → Empty stack:** Add transitions that empty the stack when entering accept states
- **Empty stack → Final state:** Add a new accept state that is reached when the stack becomes empty

**In practice:** The formal definition uses final state acceptance (with set $F$), but many constructions (especially CFG → PDA conversions) use empty stack acceptance for simplicity. Both methods are equally powerful.

**Transition interpretation:**
$\delta(q, a, b) = \{(r, c), ...\}$ means:
- In state $q$, reading input $a$ (or $\varepsilon$), with $b$ on stack top
- Move to state $r$, replace $b$ with $c$ on stack

**Special cases:**
- $a = \varepsilon$: Transition without reading input
- $b = \varepsilon$: Transition without checking stack (push only)
- $c = \varepsilon$: Pop operation (remove stack top)

---

## PDA Notation and State Diagrams

In state diagrams, transitions are labeled as:

$a, b \to c$

Where:
- $a$: Input symbol to read ($\varepsilon$ for no read)
- $b$: Stack symbol to pop ($\varepsilon$ for no pop)
- $c$: Stack symbol to push ($\varepsilon$ for no push)

**Common conventions:**
- `$` is often used as a bottom-of-stack marker
- The stack starts empty ($\varepsilon$)
- Acceptance can be by final state or empty stack

---

## Equivalence with Context-Free Grammars

### Theorem
A language is context-free **if and only if** it is recognized by some PDA.

### Proof Directions:

**CFG → PDA Construction:**
- PDA simulates leftmost derivations
- Use stack to store intermediate strings
- Nondeterministically choose production rules
- Match terminals with input

**PDA → CFG Construction:**
- More complex construction
- Variables represent pairs of PDA states: $A_{pq}$
- $A_{pq}$ generates all strings taking PDA from state $p$ to $q$ with empty stack
- Rules based on PDA transitions and state pairs

---

## Relationship with Regular Languages

**Corollary**: Every regular language is context-free.

**Proof**: 
- Every finite automaton is a PDA that ignores its stack
- Regular languages $\subseteq$ Context-free languages
- The containment is proper (e.g., $\{0^n1^n\}$ is CF but not regular)

**Hierarchy:**
```
Regular Languages ⊂ Context-Free Languages ⊂ Context-Sensitive Languages
```

---

## Key Properties of PDAs

**Nondeterminism:**
- Essential for PDAs to recognize all CFLs
- Deterministic PDAs recognize a proper subset of CFLs
- Some CFLs are inherently nondeterministic

**Limitations:**
- PDAs cannot recognize languages like $\{a^nb^nc^n \mid n \geq 0\}$
- This requires more power (context-sensitive grammars)

**Applications:**
- Parsing programming languages
- Syntax analysis in compilers
- Natural language processing
- XML/HTML parsing

---

## Examples

### Example 1: PDA Recognizing Strings with Imbalanced 0's and 1's

**Problem:** Design a PDA $P_3$ that recognizes the language:
$$L(P_3) = \{ 0w \mid w \in \{0,1\}^* \text{ and } w \text{ has exactly one more 1 than 0}  \} \cup \{ 1w \mid w \in \{0,1\}^* \text{ and } w \text{ has exactly one more 0 than 1} \}$$

**Formal Description:**

$P_3 = (Q, \Sigma, \Gamma, \delta, q_0, F)$ where:
- $Q = \{q_0, q_1, q_2\}$
- $\Sigma = \{0, 1\}$
- $\Gamma = \{0, 1, \$\}$
- $q_0 \in Q$ is the start state
- $F = \{q_0\} \subseteq Q$

**Transition Function:**
$\delta: Q \times \Sigma_\varepsilon \times \Gamma_\varepsilon \to \mathcal{P}(Q \times \Gamma_\varepsilon)$

where $\Sigma_\varepsilon = \Sigma \cup \{\varepsilon\}$ and $\Gamma_\varepsilon = \Gamma \cup \{\varepsilon\}$.

**Transition Table:**

| State | Input | Pop | New State | Push |
|-------|-------|-----|-----------|------|
| $q_0$ | $0$ | $\varepsilon$ | $q_1$ | $\$$ |
| $q_0$ | $1$ | $\varepsilon$ | $q_2$ | $\$$ |
| $q_1$ | $0$ | $\varepsilon$ | $q_1$ | $0$ |
| $q_1$ | $1$ | $0$ | $q_1$ | $\varepsilon$ |
| $q_1$ | $1$ | $\$$ | $q_0$ | $\varepsilon$ |
| $q_2$ | $0$ | $1$ | $q_2$ | $\varepsilon$ |
| $q_2$ | $1$ | $\varepsilon$ | $q_2$ | $1$ |
| $q_2$ | $0$ | $\$$ | $q_0$ | $\varepsilon$ |

**How it works:**

**Case 1: Strings starting with 0**
- When the first symbol is 0, the PDA enters state $q_1$
- In $q_1$: Reading a 0 pushes it onto the stack; reading a 1 pops a 0 from the stack
- The PDA accepts when the stack becomes empty (reaching $\$$) after reading a 1, and returns to accept state $q_0$
- This happens when the string has exactly one more 1 than 0
- **Note:** This PDA uses **final state acceptance** (accepts in state $q_0 \in F$)

**Case 2: Strings starting with 1**
- When the first symbol is 1, the PDA enters state $q_2$
- In $q_2$: Reading a 1 pushes it onto the stack; reading a 0 pops a 1 from the stack
- The PDA accepts when the stack becomes empty (reaching $\$$) after reading a 0, and returns to accept state $q_0$
- This happens when the string has exactly one more 0 than 1
- **Note:** This PDA uses **final state acceptance** (accepts in state $q_0 \in F$)

**Is $L(P_3)$ regular?**

**No**, $L(P_3)$ is **not regular**. The language requires counting the number of 0's and 1's to ensure they differ by exactly one. This counting property cannot be achieved with a finite automaton, which has only finite memory. More formally, we can prove this using the pumping lemma for regular languages: consider strings of the form $0^n1^{n+1}$ for large $n$. Any attempt to pump a substring will destroy the precise balance between 0's and 1's required by the language.

---

### Example 2: Converting CFG to PDA

**Problem:** Given the context-free grammar $G = (V, \Sigma, R, S)$ with:
- $V = \{S, T\}$
- $\Sigma = \{a,b,c\}$
- Productions:
  - $S \to aSc \mid T$
  - $T \to bTc \mid \varepsilon$

Construct a PDA $M$ that accepts $L(G)$.

**Language Description:**
The grammar generates strings that have some number of leading $a$'s, followed by some number of $b$'s, and then as many trailing $c$'s as the combined count of $a$'s and $b$'s. In formal notation:

$$L(G) = \{ a^i b^j c^{i+j} \mid i, j \geq 0 \}$$

**PDA Construction (Standard CFG → PDA Algorithm):**

The PDA uses the stack to simulate leftmost derivations:

1. **Start**: Push $\$$ onto stack, then push $S$ (start symbol)
2. **For each production rule**: When a nonterminal is on top of the stack, nondeterministically choose a production and replace the nonterminal with the right-hand side (in reverse order for stack)
3. **For terminals**: When a terminal matches the input, pop it from the stack and advance input
4. **Accept**: When stack is empty (only $\$$ remains) and all input is read
   - **Note:** This construction uses **empty stack acceptance** (the standard CFG → PDA conversion uses this method)

**Key transitions:**
- $\varepsilon, \varepsilon \to \$$: Initialize stack
- $\varepsilon, \varepsilon \to S$: Push start symbol
- $\varepsilon, S \to aSc$: Apply production $S \to aSc$ (push $cSa$ in reverse)
- $\varepsilon, S \to T$: Apply production $S \to T$
- $\varepsilon, T \to bTc$: Apply production $T \to bTc$ (push $cTb$ in reverse)
- $\varepsilon, T \to \varepsilon$: Apply production $T \to \varepsilon$
- $a, a \to \varepsilon$: Match terminal $a$
- $b, b \to \varepsilon$: Match terminal $b$
- $c, c \to \varepsilon$: Match terminal $c$
- $\varepsilon, \$ \to \varepsilon$: Accept when stack is empty

**Verification:**
- For string $aabbcc$: $S \Rightarrow aSc \Rightarrow aTc \Rightarrow abTcc \Rightarrow abcc$ (with $i=1, j=1$)
- The PDA accepts by matching $a$, then $b$, then two $c$'s, verifying the count relationship

