# Additional Practice Problems - Homework Variations

## Table of Contents
- [Overview](#overview)
- [Problem 1: Regular Grammar with Different Constraint](#problem-1-regular-grammar-with-different-constraint)
- [Problem 2: CFG Analysis with Different Language](#problem-2-cfg-analysis-with-different-language)
- [Problem 3: PDA Design for Different Pattern](#problem-3-pda-design-for-different-pattern)
- [Problem 4: CFG to PDA with Different Structure](#problem-4-cfg-to-pda-with-different-structure)
- [Problem 5: Pumping Lemma with Different Language](#problem-5-pumping-lemma-with-different-language)
- [Problem 6: Turing Machine for Different Pattern](#problem-6-turing-machine-for-different-pattern)
- [Problem 7: Combined Regular Grammar and CFG](#problem-7-combined-regular-grammar-and-cfg)
- [Problem 8: PDA to CFG with Different Structure](#problem-8-pda-to-cfg-with-different-structure)
- [Problem 9: CNF Conversion with Different Grammar](#problem-9-cnf-conversion-with-different-grammar)
- [Problem 10: Integrated Problem - Multiple Topics](#problem-10-integrated-problem---multiple-topics)

---

## Overview

This document contains additional practice problems that are variations of homework problems. Each problem:
- Tests similar concepts but with different languages or values
- May combine multiple topics
- Provides step-by-step solutions
- Helps prepare for exams by practicing similar problem types

---

## Problem 1: Regular Grammar with Different Constraint

**Problem:** Let $\Sigma = \{0, 1\}$. Find a regular grammar that generates the language:
$$L = \{w \in \Sigma^* \mid w \text{ has exactly three } 0\text{'s}\}$$

**Solution:**

We construct a right-linear grammar by tracking how many 0's we've seen:
- State $S$: 0 zeros seen (start symbol)
- State $A$: 1 zero seen
- State $B$: 2 zeros seen
- State $C$: 3 zeros seen

**The regular grammar is:**
$$
\begin{array}{rcl}
S & \to & 1S \mid 0A \\
A & \to & 1A \mid 0B \\
B & \to & 1B \mid 0C \\
C & \to & 1C \mid \varepsilon
\end{array}
$$

**How it works:**
- From $S$: Read 1's and stay in $S$, or read a 0 and move to $A$
- From $A$: Read 1's and stay in $A$, or read a 0 and move to $B$
- From $B$: Read 1's and stay in $B$, or read a 0 and move to $C$
- From $C$: Read 1's and stay in $C$, or terminate with $\varepsilon$

**Examples:**
- "01010": $S \Rightarrow 0A \Rightarrow 01A \Rightarrow 010B \Rightarrow 0101B \Rightarrow 01010B \Rightarrow 01010$ (3 zeros, valid)
- "000": $S \Rightarrow 0A \Rightarrow 00B \Rightarrow 000C \Rightarrow 000$ (3 zeros, valid)
- "0000": $S \Rightarrow 0A \Rightarrow 00B \Rightarrow 000C$, but $C$ has no rule for producing another 0, so the derivation cannot continue (reject)

---

## Problem 2: CFG Analysis with Different Language

**Problem:** Consider the context-free grammar $G_3$:
$$
\begin{array}{rcl}
S & \to & 1X \\
X & \to & 0X \mid 1X \mid 0
\end{array}
$$

**(a)** What language does $G_3$ recognize?

**(b)** Is $L(G_3)$ regular? Why or why not?

**(c)** Give a CFG in Chomsky Normal Form generating $L(G_3)$.

**(d)** Is this CFG ambiguous?

**Solution:**

**(a) Language recognized by $G_3$:**

Starting with $S \Rightarrow 1X$, we observe that $X$ generates any string of 0's and 1's that **ends with 0**, since:
- The only way to terminate is via $X \to 0$
- Before terminating, we can use $X \to 0X$ or $X \to 1X$ any number of times

Therefore:
$$L(G_3) = \{ 1w \mid w \in \{0,1\}^*, \text{ and } w \text{ ends with } 0 \}$$

Equivalently: $L(G_3) = \{ 1u0 \mid u \in \{0,1\}^* \}$ (all binary strings starting with 1 and ending with 0).

**(b) Is $L(G_3)$ regular?**

**Yes**, $L(G_3)$ is regular.

**Proof:** Let's examine the productions:
$$
\begin{array}{rcll}
S & \to & 1X & \text{(form: } A \to xB \text{)} \\
X & \to & 0X & \text{(form: } A \to xB \text{)} \\
X & \to & 1X & \text{(form: } A \to xB \text{)} \\
X & \to & 0 & \text{(form: } A \to x \text{)}
\end{array}
$$

Every production is of the form $A \to xB$ or $A \to x$, so $G_3$ is a **right-linear grammar**. Since $G_3$ is a regular grammar, it generates a regular language.

**(c) CFG in Chomsky Normal Form:**

**Step 1:** Add new start variable (not needed)

**Step 2:** Eliminate $\lambda$-rules (none exist)

**Step 3:** Eliminate unit rules (none exist)

**Step 4:** Patch up (not needed)

**Step 5:** Convert to CNF

Introduce terminal nonterminals:
- $T_0 \to 0$
- $T_1 \to 1$

**Final CNF Grammar:**
$$
\begin{array}{rcl}
S & \to & T_1 X \\
X & \to & T_0 X \mid T_1 X \mid 0 \\
T_0 & \to & 0 \\
T_1 & \to & 1
\end{array}
$$

**(d) Is this CFG ambiguous?**

**No**, the grammar is **not ambiguous**.

For any string $w \in L(G_3)$, we know $w = 1u0$ where $u \in \{0,1\}^*$. The leftmost derivation must proceed as:
1. $S \Rightarrow 1X$ (only production from $S$)
2. For each symbol in $u$: apply $X \Rightarrow 0X$ or $X \Rightarrow 1X$ (uniquely determined)
3. $X \Rightarrow 0$ (only way to terminate)

Since each step is uniquely determined, every string has exactly one leftmost derivation. Therefore, the grammar is **unambiguous**.

---

## Problem 3: PDA Design for Different Pattern

**Problem:** Design a PDA $P_4$ that recognizes the language:
$$L(P_4) = \{ 0w \mid w \in \{0,1\}^* \text{ and } w \text{ has exactly two more } 1\text{'s than } 0\text{'s}  \} \cup \{ 1w \mid w \in \{0,1\}^* \text{ and } w \text{ has exactly two more } 0\text{'s than } 1\text{'s} \}$$

**Solution:**

**Formal Description:**

$P_4 = (Q, \Sigma, \Gamma, \delta, q_0, F)$ where:
- $Q = \{q_0, q_1, q_2\}$
- $\Sigma = \{0, 1\}$
- $\Gamma = \{0, 1, \$\}$
- $q_0 \in Q$ is the start state
- $F = \{q_0\} \subseteq Q$

**Transition Function:**
$\delta: Q \times \Sigma_\varepsilon \times \Gamma_\varepsilon \to \mathcal{P}(Q \times \Gamma_\varepsilon)$

**Transition Table:**

| State | Input | Pop | New State | Push |
|-------|-------|-----|-----------|------|
| $q_0$ | $0$ | $\varepsilon$ | $q_1$ | $\$$ |
| $q_0$ | $1$ | $\varepsilon$ | $q_2$ | $\$$ |
| $q_1$ | $0$ | $\varepsilon$ | $q_1$ | $0$ |
| $q_1$ | $1$ | $0$ | $q_1$ | $\varepsilon$ |
| $q_1$ | $1$ | $\$$ | $q_1$ | $1$ |
| $q_1$ | $1$ | $1$ | $q_1$ | $11$ |
| $q_1$ | $\varepsilon$ | $11$ | $q_0$ | $\$$ |
| $q_2$ | $1$ | $\varepsilon$ | $q_2$ | $1$ |
| $q_2$ | $0$ | $1$ | $q_2$ | $\varepsilon$ |
| $q_2$ | $0$ | $\$$ | $q_2$ | $0$ |
| $q_2$ | $0$ | $0$ | $q_2$ | $00$ |
| $q_2$ | $\varepsilon$ | $00$ | $q_0$ | $\$$ |

**How it works:**

**Case 1: Strings starting with 0**
- When the first symbol is 0, the PDA enters state $q_1$
- In $q_1$: Reading a 0 pushes it onto the stack; reading a 1 pops a 0 from the stack
- When we run out of 0's to pop, we push 1's onto the stack (two extra 1's)
- The PDA accepts when we have exactly two 1's on the stack (after popping all 0's) and return to $q_0$

**Case 2: Strings starting with 1**
- When the first symbol is 1, the PDA enters state $q_2$
- In $q_2$: Reading a 1 pushes it onto the stack; reading a 0 pops a 1 from the stack
- When we run out of 1's to pop, we push 0's onto the stack (two extra 0's)
- The PDA accepts when we have exactly two 0's on the stack (after popping all 1's) and return to $q_0$

**Note:** This PDA uses **final state acceptance** (accepts in state $q_0 \in F$).

---

## Problem 4: CFG to PDA with Different Structure

**Problem:** Given the context-free grammar $G = (V, \Sigma, R, S)$ with:
- $V = \{S, A\}$
- $\Sigma = \{a,b\}$
- Productions:
  - $S \to aSb \mid A$
  - $A \to aAb \mid \varepsilon$

**(a)** Describe the language $L(G)$ in words and set notation.

**(b)** Construct a PDA $M$ that accepts $L(G)$ using the standard CFG → PDA construction.

**Solution:**

**(a) Language Description:**

The grammar generates strings with balanced $a$'s and $b$'s. The rule $S \to aSb$ adds one $a$ and one $b$ to the outside, while $A \to aAb$ adds one $a$ and one $b$ to the inside. Both can terminate with $\varepsilon$.

**Formal notation:**
$$L(G) = \{ a^n b^n \mid n \geq 0 \}$$

**How it works:**
- $S \Rightarrow A \Rightarrow \varepsilon$ gives the empty string ($n=0$)
- $S \Rightarrow aSb \Rightarrow aAb \Rightarrow a\varepsilon b = ab$ gives "ab" ($n=1$)
- $S \Rightarrow aSb \Rightarrow aaSbb \Rightarrow aaAbb \Rightarrow aabb$ gives "aabb" ($n=2$)
- Or: $S \Rightarrow aSb \Rightarrow aAb \Rightarrow aaAbb \Rightarrow aabb$ (using $A$ rules)

**(b) PDA Construction:**

The PDA uses the stack to simulate leftmost derivations:

**Key transitions:**
- $\varepsilon, \varepsilon \to \$$: Initialize stack
- $\varepsilon, \varepsilon \to S$: Push start symbol
- $\varepsilon, S \to bSa$: Apply production $S \to aSb$ (push in reverse: $b$, then $S$, then $a$)
- $\varepsilon, S \to A$: Apply production $S \to A$
- $\varepsilon, A \to bAa$: Apply production $A \to aAb$ (push in reverse)
- $\varepsilon, A \to \varepsilon$: Apply production $A \to \varepsilon$
- $a, a \to \varepsilon$: Match terminal $a$
- $b, b \to \varepsilon$: Match terminal $b$
- $\varepsilon, \$ \to \varepsilon$: Accept when stack is empty

**Note:** This construction uses **empty stack acceptance**.

**Verification:**
- For string "aabb": The PDA pushes $S$, applies $S \to aSb$ (pushes $bSa$), matches $a$, applies $S \to aSb$ again, matches $a$, applies $S \to A$, applies $A \to aAb$, matches $b$, matches $b$, accepts.

---

## Problem 5: Pumping Lemma with Different Language

**Problem:** Let $\Sigma = \{a, b, c, d\}$. Is the language 
$$L_2 = \{w \in \Sigma^* \mid \text{in } w, \text{ the number of } a\text{'s equals the number of } b\text{'s, and the number of } c\text{'s equals the number of } d\text{'s}\}$$
context-free? Show your answer is correct.

**Solution:**

The language
$$L_2 = \{ w \in \{a,b,c,d\}^* \mid \#_a(w) = \#_b(w) \text{ and } \#_c(w) = \#_d(w) \}$$
is **not** context-free. We prove this by contradiction using the pumping lemma for context-free languages.

**Assumption:** Assume, for contradiction, that $L_2$ is context-free. Then by the pumping lemma, there exists a pumping length $p > 0$ such that any string $w \in L_2$ with $|w| \geq p$ can be decomposed as $w = uvxyz$ where:
1. $|vxy| \leq p$
2. $|vy| \geq 1$
3. For all $i \geq 0$, the string $uv^ixy^iz \in L_2$

**Choose the string:** Consider $w = a^p c^p b^p d^p$ which clearly lies in $L_2$ since it has exactly $p$ of each symbol.

**Analysis:** By the pumping lemma, we can write $w = uvxyz$ with $|vxy| \leq p$ and $|vy| \geq 1$.

Since $|vxy| \leq p$, the substring $vxy$ must be contained entirely within one of the four uniform blocks $a^p, c^p, b^p, d^p$, or it must straddle exactly one adjacent boundary.

**Case analysis:**

**Case 1:** $vxy$ is contained within a single block (say $a^p$)
- Pumping up ($i = 2$) increases the number of $a$'s without changing $b$'s, $c$'s, or $d$'s
- This breaks the requirement $\#_a = \#_b$
- Contradiction

**Case 2:** $vxy$ straddles the $a/c$ boundary
- Pumping changes $a$'s and/or $c$'s but not $b$'s or $d$'s
- This breaks at least one of the requirements
- Contradiction

**Case 3:** $vxy$ straddles the $c/b$ boundary
- Similar to Case 2, pumping breaks the balance
- Contradiction

**Case 4:** $vxy$ straddles the $b/d$ boundary
- Similar to Case 2, pumping breaks the balance
- Contradiction

**Conclusion:** In all cases, pumping leads to a string not in $L_2$, contradicting the pumping lemma. Therefore, $L_2$ is **not** context-free.

---

## Problem 6: Turing Machine for Different Pattern

**Problem:** Design a Turing machine that recognizes the language:
$$L = \{0^n 1^m 0^n \mid n, m \geq 1\}$$

**Solution:**

**Algorithm:**
1. Mark the leftmost unmarked $0$ with $X$
2. Move right past all $1$'s to find the first unmarked $0$ in the third block
3. Mark that $0$ with $X$
4. Move back left past all $1$'s to find the next unmarked $0$ in the first block
5. Repeat until all $0$'s in the first block are marked
6. Verify that only marked $0$'s ($X$'s) and $1$'s remain in the middle and end
7. Accept if verification passes

**State description:**
- $q_0$: Start, mark first $0$ in first block
- $q_1$: Moving right through $1$'s to find first $0$ in third block
- $q_2$: Mark $0$ in third block, moving left to return
- $q_3$: Moving left through $1$'s to return to first block
- $q_4$: Verification state
- $q_{accept}$: Accept state
- $q_{reject}$: Reject state

**Key transitions:**
- $q_0$: On $0$, write $X$, move right, go to $q_1$
- $q_0$: On $1$ or $\sqcup$, reject (wrong format)
- $q_1$: On $1$, move right, stay in $q_1$
- $q_1$: On $0$, move right, go to $q_2$ (found first $0$ in third block)
- $q_1$: On $X$ or $\sqcup$, reject (no matching $0$)
- $q_2$: On $0$, write $X$, move left, go to $q_3$
- $q_3$: On $1$, move left, stay in $q_3$
- $q_3$: On $X$, move right, go to $q_0$ (start next iteration)
- $q_0$: On $1$, move right, go to $q_4$ (all first block $0$'s marked)
- $q_4$: On $1$ or $X$, move right, stay in $q_4$
- $q_4$: On $\sqcup$, accept
- $q_4$: On $0$, reject (unmarked $0$ remains)

**Is this a decider?**

**Yes**, the machine is a decider. Each iteration marks exactly one $0$ from the first block and one from the third block. The number of iterations is bounded by the length of the input, and each iteration performs bounded work. The machine always halts.

---

## Problem 7: Combined Regular Grammar and CFG

**Problem:** Consider the language:
$$L = \{w \in \{0,1\}^* \mid w \text{ starts with } 0 \text{ and has an even number of } 1\text{'s}\}$$

**(a)** Give a regular grammar for $L$.

**(b)** Give a context-free grammar for $L$ (that is not necessarily regular).

**(c)** Is your CFG from part (b) a regular grammar? Explain.

**Solution:**

**(a) Regular Grammar:**

We need to track:
- Whether we've seen the initial $0$ (start symbol handles this)
- Whether we've seen an even or odd number of $1$'s

**Right-linear grammar:**
$$
\begin{array}{rcl}
S & \to & 0A \\
A & \to & 0A \mid 1B \mid \varepsilon \\
B & \to & 0B \mid 1A \mid \varepsilon
\end{array}
$$

**Explanation:**
- $S$: Start, must produce $0$ first
- $A$: Even number of $1$'s seen so far
- $B$: Odd number of $1$'s seen so far
- From $A$: Read $0$ and stay in $A$, read $1$ and go to $B$, or terminate
- From $B$: Read $0$ and stay in $B$, read $1$ and go to $A$, or terminate

**(b) Context-Free Grammar:**

Since $L$ is regular, we can use the same grammar as in (a). However, here's an alternative CFG (which happens to also be regular):
$$
\begin{array}{rcl}
S & \to & 0T \\
T & \to & 0T \mid 1T1T \mid \varepsilon
\end{array}
$$

**Explanation:**
- $S$: Start, must produce $0$ first
- $T$: Generates strings with even number of $1$'s
- $T \to 1T1T$: Adds two $1$'s (one on each side of a recursive $T$), maintaining even count

**(c) Is the CFG from (b) regular?**

**Yes**, the CFG from (b) is a regular grammar. All productions are of the form:
- $S \to 0T$ (form: $A \to xB$)
- $T \to 0T$ (form: $A \to xB$)
- $T \to 1T1T$ (form: $A \to xBC$ - wait, this has two nonterminals!)

Actually, $T \to 1T1T$ is **not** in right-linear or left-linear form because it has two nonterminals. So this grammar is **not** regular.

However, since $L$ is regular, there exists a regular grammar for it (the one in part (a)).

---

## Problem 8: PDA to CFG with Different Structure

**Problem:** Consider a PDA $P_5$ that recognizes the language:
$$L(P_5) = \{ 0^n 1^m 0^n \mid n \geq 0, m \geq 1 \}$$

Give a context-free grammar that generates $L(P_5)$.

**Solution:**

We construct a CFG by considering the structure:
- $n$ zeros, followed by $m$ ones (where $m \geq 1$), followed by $n$ zeros

**Grammar:**
$$
\begin{array}{rcl}
S & \to & 0S0 \mid A \\
A & \to & 1A \mid 1
\end{array}
$$

**Explanation:**
- $S \to 0S0$: Adds one $0$ to the front and one to the back (maintains $n$ zeros on each side)
- $S \to A$: Passes control to generate the middle $1$'s
- $A \to 1A \mid 1$: Generates one or more $1$'s (ensures $m \geq 1$)

**Examples:**
- $S \Rightarrow A \Rightarrow 1$ gives "1" ($n=0, m=1$)
- $S \Rightarrow 0S0 \Rightarrow 0A0 \Rightarrow 010$ gives "010" ($n=1, m=1$)
- $S \Rightarrow 0S0 \Rightarrow 00S00 \Rightarrow 00A00 \Rightarrow 00100$ gives "00100" ($n=2, m=1$)
- $S \Rightarrow 0S0 \Rightarrow 0A0 \Rightarrow 01A0 \Rightarrow 0110$ gives "0110" ($n=1, m=2$)

**Verification:**
The grammar correctly generates all strings of the form $0^n 1^m 0^n$ where $n \geq 0$ and $m \geq 1$.

---

## Problem 9: CNF Conversion Utilizing All Steps

**Problem:** Convert the following grammar to Chomsky Normal Form:
$$
\begin{array}{rcl}
S & \to & aSb \mid SS \mid A \mid \varepsilon \\
A & \to & B \\
B & \to & bB \mid C \\
C & \to & cC \mid \varepsilon
\end{array}
$$

**Solution:**

This grammar requires **all five steps** of the CNF conversion process.

### Step 1: Add a new start variable

Since $S$ appears on the right-hand side of the production $S \to SS$, we need to add a new start variable $S_0$:

$$
\begin{array}{rcl}
S_0 & \to & S \\
S & \to & aSb \mid SS \mid A \mid \varepsilon \\
A & \to & B \\
B & \to & bB \mid C \\
C & \to & cC \mid \varepsilon
\end{array}
$$

### Step 2: Eliminate all $\lambda$-rules ($A \to \varepsilon$)

We have two $\lambda$-rules: $S \to \varepsilon$ and $C \to \varepsilon$.

**Eliminating $S \to \varepsilon$:**

For each production where $S$ appears on the right-hand side, we add new productions with $S$ removed:
- From $S_0 \to S$: Add $S_0 \to \varepsilon$
- From $S \to SS$: Add $S \to S$ (unit rule, we'll handle later) and $S \to \varepsilon$ (already exists)
- From $S \to aSb$: Add $S \to ab$

**Eliminating $C \to \varepsilon$:**

For each production where $C$ appears on the right-hand side, we add new productions with $C$ removed:
- From $B \to C$: Add $B \to \varepsilon$
- From $C \to cC$: Add $C \to c$

**Eliminating $B \to \varepsilon$ (newly added):**

For each production where $B$ appears on the right-hand side:
- From $A \to B$: Add $A \to \varepsilon$
- From $B \to bB$: Add $B \to b$ (when the $B$ on the right becomes $\varepsilon$)

**Eliminating $A \to \varepsilon$ (newly added):**

For each production where $A$ appears on the right-hand side:
- From $S \to A$: Add $S \to \varepsilon$ (already exists, so no change)

**Eliminating $S \to \varepsilon$:**

For each production where $S$ appears on the right-hand side:
- From $S_0 \to S$: Add $S_0 \to \varepsilon$
- From $S \to SS$: Add $S \to S$ (unit rule, we'll handle in Step 3) and $S \to \varepsilon$ (already exists)
- From $S \to aSb$: Add $S \to ab$

**Now remove all ε-rules** (except $S_0 \to \varepsilon$ since the language contains $\varepsilon$):

After Step 2 (all ε-rules eliminated except $S_0 \to \varepsilon$):
$$
\begin{array}{rcl}
S_0 & \to & S \mid \varepsilon \\
S & \to & aSb \mid SS \mid A \mid ab \\
A & \to & B \\
B & \to & bB \mid C \mid b \\
C & \to & cC \mid c
\end{array}
$$

**Note:** We keep $S_0 \to \varepsilon$ because the original language contains the empty string. All other ε-rules ($S \to \varepsilon$, $A \to \varepsilon$, $B \to \varepsilon$, $C \to \varepsilon$) have been removed, and their effects are captured by the new productions we added.

### Step 3: Eliminate all unit rules ($A \to B$)

We have the following unit rules:
- $S_0 \to S$
- $S \to A$
- $A \to B$
- $B \to C$

**Eliminating $B \to C$:**
- Remove $B \to C$
- Add $B \to cC \mid c$ (all $C$ productions)

**Eliminating $A \to B$:**
- Remove $A \to B$
- Add $A \to bB \mid cC \mid c \mid b$ (all $B$ productions; no $\varepsilon$ since we removed it in Step 2)

**Eliminating $S \to A$:**
- Remove $S \to A$
- Add $S \to bB \mid cC \mid c \mid b$ (all $A$ productions; no $\varepsilon$ since we removed it in Step 2)

**Eliminating $S_0 \to S$:**
- Remove $S_0 \to S$
- Add all $S$ productions to $S_0$: $S_0 \to aSb \mid SS \mid bB \mid cC \mid c \mid b \mid ab \mid \varepsilon$

After Step 3:
$$
\begin{array}{rcl}
S_0 & \to & aSb \mid SS \mid bB \mid cC \mid c \mid b \mid ab \mid \varepsilon \\
S & \to & aSb \mid SS \mid bB \mid cC \mid c \mid b \mid ab \\
A & \to & bB \mid cC \mid c \mid b \\
B & \to & bB \mid cC \mid c \mid b \\
C & \to & cC \mid c
\end{array}
$$

**Note:** Only $S_0 \to \varepsilon$ remains (since the language contains $\varepsilon$). All other ε-rules were removed in Step 2.

### Step 4: Patch up the grammar

We need to verify the grammar still generates the same language. The original grammar generates:
- Strings with balanced $a$'s and $b$'s (from $S \to aSb$)
- Concatenations of such strings (from $S \to SS$)
- Strings of $b$'s and $c$'s (from the $A \to B \to C$ chain)
- The empty string

The patched grammar should generate the same. We can remove variables that are no longer reachable or useful, but let's keep them for now.

### Step 5: Convert remaining rules to CNF form

CNF requires all productions to be either:
- $A \to BC$ (two nonterminals), or
- $A \to a$ (single terminal)

**Introduce terminal nonterminals:**
- $T_a \to a$
- $T_b \to b$
- $T_c \to c$

**Convert each rule:**

**For $S_0$ and $S$:**
- $S_0 \to \varepsilon$: Keep (we'll handle $\varepsilon$ separately if needed, but typically CNF doesn't allow $\varepsilon$ except for start symbol)
- $S_0 \to a$: Wait, we have $S_0 \to c \mid b$ but not $S_0 \to a$. Let's check: we have $S_0 \to ab$, which needs conversion.
- $S_0 \to ab$: Becomes $S_0 \to T_a T_b$
- $S_0 \to aSb$: Becomes $S_0 \to T_a B_1$ where $B_1 \to S T_b$
- $S_0 \to SS$: Already in CNF form (two nonterminals)
- $S_0 \to bB$: Becomes $S_0 \to T_b B$
- $S_0 \to cC$: Becomes $S_0 \to T_c C$
- $S_0 \to c$: Becomes $S_0 \to T_c$
- $S_0 \to b$: Becomes $S_0 \to T_b$

**For $A$:**
- $A \to \varepsilon$: Keep (if $A$ can be removed, but typically we don't allow $\varepsilon$ in CNF except start)
- $A \to bB$: Becomes $A \to T_b B$
- $A \to cC$: Becomes $A \to T_c C$
- $A \to c$: Becomes $A \to T_c$
- $A \to b$: Becomes $A \to T_b$

**For $B$:**
- $B \to bB$: Becomes $B \to T_b B$
- $B \to cC$: Becomes $B \to T_c C$
- $B \to c$: Becomes $B \to T_c$
- $B \to b$: Becomes $B \to T_b$

**For $C$:**
- $C \to cC$: Becomes $C \to T_c C$
- $C \to c$: Becomes $C \to T_c$

**Final CNF Grammar:**

$$
\begin{array}{rcl}
S_0 & \to & T_a T_b \mid SS \mid T_b B \mid T_c C \mid T_c \mid T_b \mid T_a B_1 \mid \varepsilon \\
S & \to & T_a T_b \mid SS \mid T_b B \mid T_c C \mid T_c \mid T_b \mid T_a B_1 \\
A & \to & T_b B \mid T_c C \mid T_c \mid T_b \\
B & \to & T_b B \mid T_c C \mid T_c \mid T_b \\
C & \to & T_c C \mid T_c \\
B_1 & \to & S T_b \\
T_a & \to & a \\
T_b & \to & b \\
T_c & \to & c
\end{array}
$$

**Note:** Only $S_0 \to \varepsilon$ remains, which is correct for CNF. In Chomsky Normal Form, if the language contains $\varepsilon$, only the start symbol can have an $\varepsilon$-production. All other ε-rules were properly eliminated in Step 2.

**Verification:**

The CNF grammar generates the same language as the original:
- Original: $S \Rightarrow aSb \Rightarrow ab$ generates "ab"
- CNF: $S_0 \Rightarrow T_a T_b \Rightarrow ab$ generates "ab"
- Original: $S \Rightarrow SS \Rightarrow aSb \cdot ab \Rightarrow ab \cdot ab$ generates "abab"
- CNF: $S_0 \Rightarrow SS \Rightarrow T_a B_1 \cdot T_a T_b \Rightarrow a S b \cdot ab \Rightarrow ab \cdot ab$ generates "abab"

---

## Problem 10: Integrated Problem - Multiple Topics

**Problem:** Consider the language:
$$L = \{a^i b^j c^k \mid i, j, k \geq 0 \text{ and } i = j + k\}$$

**(a)** Is $L$ regular? Prove your answer.

**(b)** Is $L$ context-free? If yes, give a CFG. If no, prove it.

**(c)** If $L$ is context-free, convert your CFG to Chomsky Normal Form.

**(d)** Design a PDA that recognizes $L$.

**(e)** Is your PDA a decider? Explain.

**Solution:**

**(a) Is $L$ regular?**

**No**, $L$ is not regular.

**Proof using pumping lemma for regular languages:**

Assume $L$ is regular. Then there exists pumping length $p$. Consider $w = a^p b^0 c^0 = a^p \in L$ (since $p = 0 + 0$).

By pumping lemma, $w = xyz$ where $|xy| \leq p$, $|y| \geq 1$, and $xy^iz \in L$ for all $i \geq 0$.

Since $|xy| \leq p$, both $x$ and $y$ contain only $a$'s.

Pump up: $xy^2z = a^{p+|y|} \in L$. For this to be in $L$, we need $p+|y| = 0 + 0 = 0$, which means $p+|y| = 0$, a contradiction since $p > 0$ and $|y| \geq 1$.

Therefore, $L$ is not regular.

**(b) Is $L$ context-free?**

**Yes**, $L$ is context-free.

**CFG:**
$$
\begin{array}{rcl}
S & \to & aSc \mid T \\
T & \to & aTb \mid \varepsilon
\end{array}
$$

**Explanation:**
- $T$ generates $a^j b^j$ (equal numbers of $a$'s and $b$'s)
- $S \to aSc$ adds one $a$ and one $c$ to the outside
- $S \to T$ passes control to generate the $a$'s and $b$'s
- This generates $a^{j+k} b^j c^k$ where $i = j + k$

**Verification:**
- For $a^3 b^1 c^2$ ($i=3, j=1, k=2$, and $3 = 1+2$):
  - $S \Rightarrow aSc \Rightarrow aaScc \Rightarrow aaTcc \Rightarrow aaaTbcc \Rightarrow aaabcc$

**(c) Chomsky Normal Form:**

**Step 1:** Add new start (not needed)

**Step 2:** Eliminate $\lambda$-rules:
- Remove $T \to \varepsilon$, add $S \to \varepsilon$ (since $S \to T$)

**Step 3:** Eliminate unit rules:
- Remove $S \to T$, add $S \to aTb \mid \varepsilon$

**Step 4:** Patch up (done)

**Step 5:** Convert to CNF

Introduce $T_a \to a$, $T_b \to b$, $T_c \to c$

**Final CNF:**
$$
\begin{array}{rcl}
S & \to & T_a S_1 \mid T_a T_2 \mid \varepsilon \\
S_1 & \to & S T_c \\
T_2 & \to & T T_b \\
T & \to & T_a T_3 \\
T_3 & \to & T T_b \\
T_a & \to & a \\
T_b & \to & b \\
T_c & \to & c
\end{array}
$$

**(d) PDA Design:**

**Algorithm:**
1. Push $a$'s onto the stack as they are read
2. When $b$'s start, pop one $a$ for each $b$
3. When $c$'s start, pop one $a$ for each $c$
4. Accept if stack is empty when all input is consumed

**States:**
- $q_0$: Reading $a$'s, pushing onto stack
- $q_1$: Reading $b$'s, popping $a$'s
- $q_2$: Reading $c$'s, popping $a$'s
- $q_{accept}$: Accept state

**Key transitions:**
- $q_0$: On $a$, push $a$, stay in $q_0$
- $q_0$: On $b$, pop $a$, go to $q_1$
- $q_0$: On $c$, pop $a$, go to $q_2$
- $q_1$: On $b$, pop $a$, stay in $q_1$
- $q_1$: On $c$, pop $a$, go to $q_2$
- $q_2$: On $c$, pop $a$, stay in $q_2$
- $q_2$: On $\sqcup$ with empty stack, accept

**(e) Is the PDA a decider?**

**Yes**, the PDA is a decider (when converted to a Turing machine or when we consider it as a computational model that always halts).

**Termination analysis:**
- Each symbol read performs bounded work
- The number of stack operations is bounded by the input length
- The PDA will always halt: either accept when stack empties, or reject if it tries to pop from empty stack or has symbols remaining on stack

Since the PDA always halts and correctly accepts/rejects, it is a decider.

