# Comprehensive Examples and Test Preparation

## Table of Contents
- [Overview](#overview)
- [Problem 1: CFG to PDA Conversion](#problem-1-cfg-to-pda-conversion)
- [Problem 2: PDA to CFG Conversion](#problem-2-pda-to-cfg-conversion)
- [Problem 3: Regular Grammar Construction](#problem-3-regular-grammar-construction)
- [Problem 4: Chomsky Normal Form Conversion](#problem-4-chomsky-normal-form-conversion)
- [Problem 5: Ambiguity Analysis](#problem-5-ambiguity-analysis)
- [Problem 6: Pumping Lemma for CFLs](#problem-6-pumping-lemma-for-cfls)
- [Problem 7: Turing Machine Design](#problem-7-turing-machine-design)
- [Problem 8: Decider Proof](#problem-8-decider-proof)
- [Problem 9: Language Classification](#problem-9-language-classification)
- [Problem 10: Integrated Problem](#problem-10-integrated-problem)

---

## Overview

This document provides comprehensive examples that integrate multiple topics from the course, demonstrating how different concepts work together. These problems are designed for test preparation and cover:

- Regular grammars
- Context-free grammars
- Pushdown automata
- Chomsky Normal Form
- Ambiguity
- Pumping lemmas
- Turing machines
- Language classification

---

## Problem 1: CFG to PDA Conversion

**Problem:** Given the context-free grammar $G = (V, \Sigma, R, S)$ with:
- $V = \{S, T\}$
- $\Sigma = \{a,b,c\}$
- Productions:
  - $S \to aSc \mid T$
  - $T \to bTc \mid \varepsilon$

**(a)** Describe the language $L(G)$ in words and set notation.

**(b)** Construct a PDA $M$ that accepts $L(G)$ using the standard CFG → PDA construction.

**Solution:**

**(a) Language Description:**

The grammar generates strings that have some number of leading $a$'s, followed by some number of $b$'s, and then as many trailing $c$'s as the combined count of $a$'s and $b$'s.

**Formal notation:**
$$L(G) = \{ a^i b^j c^{i+j} \mid i, j \geq 0 \}$$

**How it works:**
- The rule $S \to aSc$ adds one $a$ to the front and one $c$ to the back each time it's used
- The rule $S \to T$ passes control to $T$ when we're done adding $a$'s and $c$'s
- The nonterminal $T$ generates $b^j c^j$ by repeatedly using $T \to bTc$ and eventually $T \to \varepsilon$
- This also allows for the empty string when both $i = 0$ and $j = 0$

**Examples:**
- $\varepsilon$ (when $i=0, j=0$)
- $bc$ (when $i=0, j=1$)
- $ac$ (when $i=1, j=0$)
- $aabbcccc$ (when $i=2, j=2$: 2 $a$'s, 2 $b$'s, 4 $c$'s)

**(b) PDA Construction:**

The PDA uses the stack to simulate leftmost derivations. Here's the construction:

**States:**
- $q_{start}$: Start state
- $q_{loop}$: Main processing state
- $q_{accept}$: Accept state

**Transitions:**
1. **Initialize:** $\varepsilon, \varepsilon \to \$$ (push bottom marker)
2. **Push start symbol:** $\varepsilon, \varepsilon \to S$ (push $S$ onto stack)
3. **Production $S \to aSc$:** $\varepsilon, S \to cSa$ (push in reverse: $c$, then $S$, then $a$)
4. **Production $S \to T$:** $\varepsilon, S \to T$
5. **Production $T \to bTc$:** $\varepsilon, T \to cTb$ (push in reverse)
6. **Production $T \to \varepsilon$:** $\varepsilon, T \to \varepsilon$ (pop $T$)
7. **Match terminal $a$:** $a, a \to \varepsilon$
8. **Match terminal $b$:** $b, b \to \varepsilon$
9. **Match terminal $c$:** $c, c \to \varepsilon$
10. **Accept:** $\varepsilon, \$ \to \varepsilon$ (when stack is empty)

**How it works:**
- The PDA nondeterministically chooses which production to apply when a nonterminal is on the stack
- When a terminal matches the input, it's popped from the stack
- The PDA accepts when the stack is empty (only $\$$ remains) and all input is consumed

---

## Problem 2: PDA to CFG Conversion

**Problem:** Consider the PDA $P_3$ from the homework that recognizes:
$$L(P_3) = \{ 0w \mid w \in \{0,1\}^* \text{ and } w \text{ has exactly one more 1 than 0}  \} \cup \{ 1w \mid w \in \{0,1\}^* \text{ and } w \text{ has exactly one more 0 than 1} \}$$

Give a context-free grammar that generates $L(P_3)$.

**Solution:**

We construct a CFG by considering the two cases separately:

**Grammar:**
$$
\begin{array}{rcl}
S & \to & 0E1 \mid 1E0 \\
E & \to & 0E1E \mid 1E0E \mid \varepsilon
\end{array}
$$

**Explanation:**

The nonterminal $E$ generates all strings with equal numbers of 0's and 1's (a balanced string):
- $E \to 0E1E$ adds a 0, recursively generates a balanced string, adds a 1, then recursively generates another balanced string
- $E \to 1E0E$ does the same but with 1 first, then 0
- $E \to \varepsilon$ allows termination

The start symbol $S$ uses $E$ to create strings with the desired imbalance:
- $S \to 0E1$: Start with 0, insert a balanced string (equal 0's and 1's), end with 1. This gives one more 1 than 0 overall.
- $S \to 1E0$: Start with 1, insert a balanced string (equal 0's and 1's), end with 0. This gives one more 0 than 1 overall.

**Examples:**
- $S \Rightarrow 0E1 \Rightarrow 01$ gives string "01" (one 0, two 1's)
- $S \Rightarrow 0E1 \Rightarrow 0(0E1E)1 \Rightarrow 0011$ gives string "0011" (two 0's, three 1's)
- $S \Rightarrow 1E0 \Rightarrow 10$ gives string "10" (two 0's, one 1)

---

## Problem 3: Regular Grammar Construction

**Problem:** Let $\Sigma = \{0, 1\}$. Construct a regular grammar for the language:
$$L = \{w \in \Sigma^* \mid w \text{ contains exactly two } 1\text{'s}\}$$

**Solution:**

We construct a right-linear grammar by tracking how many 1's we've seen:
- State $S$: 0 ones seen (start symbol)
- State $A$: 1 one seen
- State $B$: 2 ones seen

**The regular grammar is:**
$$
\begin{array}{rcl}
S & \to & 0S \mid 1A \\
A & \to & 0A \mid 1B \\
B & \to & 0B \mid \varepsilon
\end{array}
$$

**How it works:**
- From $S$: Read 0's and stay in $S$, or read a 1 and move to $A$
- From $A$: Read 0's and stay in $A$, or read a 1 and move to $B$
- From $B$: Read 0's and stay in $B$, or terminate with $\varepsilon$

**Examples:**
- "110": $S \Rightarrow 1A \Rightarrow 11B \Rightarrow 110B \Rightarrow 110$
- "01010": $S \Rightarrow 0S \Rightarrow 01A \Rightarrow 010A \Rightarrow 0101B \Rightarrow 01010B \Rightarrow 01010$

---

## Problem 4: Chomsky Normal Form Conversion

**Problem:** Convert the following grammar to Chomsky Normal Form:
$$
\begin{array}{rcl}
S & \to & aSb \mid ab \mid SS
\end{array}
$$

**Solution:**

**Step 1: Add new start variable**
Not needed (S doesn't appear on right-hand side).

**Step 2: Eliminate $\lambda$-rules**
No $\lambda$-rules exist.

**Step 3: Eliminate unit rules**
No unit rules exist.

**Step 4: Patch up**
No patching needed.

**Step 5: Convert to CNF**

Introduce terminal nonterminals:
- $T_a \to a$
- $T_b \to b$

Original rules:
- $S \to aSb$ becomes $S \to T_a S T_b$
- $S \to ab$ becomes $S \to T_a T_b$
- $S \to SS$ is already in CNF (two nonterminals)

Now handle $S \to T_a S T_b$ (three symbols):
- Introduce $A \to T_a S$
- Then $S \to A T_b$

**Final CNF Grammar:**
$$
\begin{array}{rcl}
S & \to & A T_b \mid T_a T_b \mid SS \\
A & \to & T_a S \\
T_a & \to & a \\
T_b & \to & b
\end{array}
$$

**Verification:**
- Original: $S \Rightarrow aSb \Rightarrow aabb$ generates "aabb"
- CNF: $S \Rightarrow A T_b \Rightarrow T_a S T_b \Rightarrow a S b \Rightarrow a T_a T_b b \Rightarrow aabb$ generates "aabb"

---

## Problem 5: Ambiguity Analysis

**Problem:** Consider the grammar:
$$
\begin{array}{rcl}
E & \to & E + E \mid E \times E \mid (E) \mid a
\end{array}
$$

Is this grammar ambiguous? If so, show two different parse trees for the string $a + a \times a$.

**Solution:**

**Yes**, this grammar is ambiguous.

The string $a + a \times a$ has two different parse trees:

**Parse Tree 1 (addition first):**
```
        E
      / | \
     E  +  E
     |    /|\
     a   E × E
         |   |
         a   a
```
This corresponds to $(a + a) \times a = 2a$.

**Parse Tree 2 (multiplication first):**
```
        E
      / | \
     E  ×  E
    /|\    |
   E + E   a
   |   |
   a   a
```
This corresponds to $a + (a \times a) = a + a^2$.

Since the string $a + a \times a$ has two different parse trees (and thus two different leftmost derivations), the grammar is **ambiguous**.

**Note:** This ambiguity is problematic for programming languages because it leads to different interpretations of expressions. Real programming languages use operator precedence and associativity rules to resolve this.

---

## Problem 6: Pumping Lemma for CFLs

**Problem:** Prove that the language $L = \{a^n b^n c^n \mid n \geq 0\}$ is not context-free.

**Solution:**

**Proof by contradiction:**

Assume, for contradiction, that $L$ is context-free. Then by the pumping lemma for context-free languages, there exists a pumping length $p > 0$ such that any string $w \in L$ with $|w| \geq p$ can be decomposed as $w = uvxyz$ where:
1. $|vxy| \leq p$
2. $|vy| \geq 1$
3. For all $i \geq 0$, the string $uv^ixy^iz \in L$

**Choose the string:** $w = a^p b^p c^p$ which clearly lies in $L$.

**Analysis:** By the pumping lemma, we can write $w = uvxyz$ with $|vxy| \leq p$ and $|vy| \geq 1$.

Since $|vxy| \leq p$, the substring $vxy$ cannot contain all three symbols $a$, $b$, and $c$ simultaneously (they're separated by $p$ symbols each).

**Case analysis:**

**Case 1:** $vxy$ contains only $a$'s (or only $b$'s, or only $c$'s)
- Pumping up ($i = 2$) increases the count of one symbol without changing the others
- This breaks the balance: $uv^2xy^2z$ has unequal counts
- Contradiction

**Case 2:** $vxy$ contains $a$'s and $b$'s (but no $c$'s)
- Pumping up increases $a$'s and/or $b$'s but not $c$'s
- This breaks the balance
- Contradiction

**Case 3:** $vxy$ contains $b$'s and $c$'s (but no $a$'s)
- Pumping up increases $b$'s and/or $c$'s but not $a$'s
- This breaks the balance
- Contradiction

**Case 4:** $vxy$ straddles boundaries (e.g., contains some $a$'s and some $b$'s)
- Similar to Case 2, pumping breaks the balance
- Contradiction

**Conclusion:** In all cases, pumping leads to a string not in $L$, contradicting the pumping lemma. Therefore, $L$ is **not** context-free.

---

## Problem 7: Turing Machine Design

**Problem:** Design a Turing machine that recognizes the language:
$$L = \{w \# w \mid w \in \{0,1\}^*\}$$

This is the language of strings that consist of a binary string, followed by $\#$, followed by the same binary string.

**Solution:**

**Algorithm:**
1. Mark the leftmost unmarked symbol of the first copy
2. Move right past the $\#$ to find the corresponding symbol in the second copy
3. If they match, mark it and return left
4. Repeat until all symbols before $\#$ are marked
5. Verify that only marked symbols and $\#$ remain
6. Accept if verification passes

**State description:**
- $q_0$: Start, look for first unmarked symbol before $\#$
- $q_1$: Moving right to find $\#$
- $q_2$: Moving right to find corresponding symbol in second copy
- $q_3$: Moving left to return to first copy
- $q_4$: Verification state
- $q_{accept}$: Accept state
- $q_{reject}$: Reject state

**Key transitions:**
- $q_0$: On $0$ or $1$, mark it as $X$ or $Y$, move right, go to $q_1$
- $q_1$: On $0$ or $1$, move right, stay in $q_1$
- $q_1$: On $\#$, move right, go to $q_2$
- $q_2$: On matching symbol (e.g., $0$ if we marked $0$), mark it, move left, go to $q_3$
- $q_2$: On non-matching symbol, reject
- $q_3$: Move left until finding $\#$, then move left again, go to $q_0$
- $q_0$: On $\#$, move right, go to $q_4$ (all symbols before $\#$ are marked)
- $q_4$: On marked symbols, move right, stay in $q_4$
- $q_4$: On $\sqcup$, accept

---

## Problem 8: Decider Proof

**Problem:** Prove that the Turing machine from Problem 7 is a decider.

**Solution:**

A Turing machine is a decider if it:
1. Accepts all strings in the language
2. Rejects all strings not in the language
3. Always halts on every input

**Termination analysis:**

For any input string $w$:
- Each iteration marks exactly one symbol from the first copy and one corresponding symbol from the second copy
- Maximum iterations = length of string before $\#$
- Each iteration performs bounded work:
  - Scan to $\#$: at most $|w|$ steps
  - Find matching symbol: at most $|w|$ steps
  - Return: at most $|w|$ steps
- Total operations: $O(|w|^2)$ (polynomial bound)

**Case analysis:**

1. **$w \in L$ (string has form $u\#u$):**
   - All symbols match
   - Machine marks all symbols and accepts
   - **Halts in accept state**

2. **$w \notin L$:**
   - **Wrong format (no $\#$):** Rejects when $\#$ expected
   - **Symbols don't match:** Rejects when finding mismatch in $q_2$
   - **Different lengths:** Rejects when running out of symbols
   - **Always halts in reject state**

**No infinite loops:**
- Number of unmarked symbols strictly decreases
- Machine progresses monotonically
- All transitions well-defined

**Conclusion:** The machine is a **decider**, so $L$ is **Turing-decidable**.

---

## Problem 9: Language Classification

**Problem:** Classify each of the following languages as regular, context-free but not regular, or neither. Justify your answers.

**(a)** $L_1 = \{0^n 1^n \mid n \geq 0\}$

**(b)** $L_2 = \{0^n 1^m \mid n, m \geq 0\}$

**(c)** $L_3 = \{0^n 1^n 0^n \mid n \geq 0\}$

**(d)** $L_4 = \{w \in \{0,1\}^* \mid w = w^R\}$ (palindromes)

**Solution:**

**(a) $L_1 = \{0^n 1^n \mid n \geq 0\}$**

**Context-free but not regular.**

- **Not regular:** Requires counting, which finite automata cannot do. Use pumping lemma for regular languages.
- **Context-free:** Can be generated by CFG:
  $$
  S \to 0S1 \mid \varepsilon
  $$
  Or recognized by a PDA that pushes 0's and pops them for 1's.

**(b) $L_2 = \{0^n 1^m \mid n, m \geq 0\}$**

**Regular.**

- Can be recognized by DFA: accept any string of 0's followed by any string of 1's
- Regular expression: $0^*1^*$
- Regular grammar:
  $$
  S \to 0S \mid 1A \mid \varepsilon \\
  A \to 1A \mid \varepsilon
  $$

**(c) $L_3 = \{0^n 1^n 0^n \mid n \geq 0\}$**

**Neither regular nor context-free.**

- **Not context-free:** Use pumping lemma for CFLs. The string $0^p 1^p 0^p$ cannot be pumped while maintaining the structure.
- **Not regular:** Obviously not regular (requires more power than CFLs).

**(d) $L_4 = \{w \in \{0,1\}^* \mid w = w^R\}$ (palindromes)**

**Context-free but not regular.**

- **Not regular:** Requires comparing symbols at symmetric positions, which finite automata cannot do.
- **Context-free:** Can be generated by CFG:
  $$
  S \to 0S0 \mid 1S1 \mid 0 \mid 1 \mid \varepsilon
  $$
  Or recognized by a PDA that nondeterministically guesses the midpoint and compares.

---

## Problem 10: Integrated Problem

**Problem:** Consider the language:
$$L = \{a^i b^j c^k \mid i, j, k \geq 0 \text{ and } i + j = k\}$$

**(a)** Is $L$ regular? Prove your answer.

**(b)** Is $L$ context-free? If yes, give a CFG. If no, prove it.

**(c)** If $L$ is context-free, convert your CFG to Chomsky Normal Form.

**(d)** Design a PDA that recognizes $L$.

**Solution:**

**(a) Is $L$ regular?**

**No**, $L$ is not regular.

**Proof using pumping lemma for regular languages:**

Assume $L$ is regular. Then there exists pumping length $p$. Consider $w = a^p b^0 c^p = a^p c^p \in L$ (since $p + 0 = p$).

By pumping lemma, $w = xyz$ where $|xy| \leq p$, $|y| \geq 1$, and $xy^iz \in L$ for all $i \geq 0$.

Since $|xy| \leq p$, both $x$ and $y$ contain only $a$'s.

Pump up: $xy^2z = a^{p+|y|} c^p$. For this to be in $L$, we need $(p+|y|) + 0 = p$, which means $|y| = 0$, a contradiction.

Therefore, $L$ is not regular.

**(b) Is $L$ context-free?**

**Yes**, $L$ is context-free.

**CFG:**
$$
\begin{array}{rcl}
S & \to & Sc \mid T \\
T & \to & aTc \mid bTc \mid \varepsilon
\end{array}
$$

**Explanation:**
- $T$ generates strings with equal numbers of $(a+b)$'s and $c$'s
- $S$ can add extra $c$'s at the end
- This generates all strings where $i + j = k$

**Verification:**
- For $a^2 b^1 c^3$: $S \Rightarrow Sc \Rightarrow Scc \Rightarrow Tcc \Rightarrow aTccc \Rightarrow abTccc \Rightarrow abccc$

**(c) Chomsky Normal Form:**

**Step 1:** Add new start variable (not needed)

**Step 2:** Eliminate $\lambda$-rules:
- $T \to \varepsilon$: Remove and add $S \to \varepsilon$ (since $S \to T$)

**Step 3:** Eliminate unit rules:
- $S \to T$: Remove and add $S \to aTc \mid bTc \mid \varepsilon$

**Step 4:** Patch up (already done)

**Step 5:** Convert to CNF:
- Introduce $T_a \to a$, $T_b \to b$, $T_c \to c$
- $S \to Sc$ becomes $S \to ST_c$
- $S \to aTc$ becomes $S \to T_a T_1$ where $T_1 \to T T_c$
- $S \to bTc$ becomes $S \to T_b T_1$
- $T \to aTc$ becomes $T \to T_a T_1$
- $T \to bTc$ becomes $T \to T_b T_1$

**Final CNF:**
$$
\begin{array}{rcl}
S & \to & ST_c \mid T_a T_1 \mid T_b T_1 \mid \varepsilon \\
T & \to & T_a T_1 \mid T_b T_1 \\
T_1 & \to & T T_c \\
T_a & \to & a \\
T_b & \to & b \\
T_c & \to & c
\end{array}
$$

**(d) PDA Design:**

**Algorithm:**
1. Push $a$'s and $b$'s onto the stack as they are read
2. When $c$'s start, pop one symbol from the stack for each $c$
3. Accept if stack is empty when all input is consumed

**States:**
- $q_0$: Start state, reading $a$'s and $b$'s
- $q_1$: Reading $c$'s, popping from stack
- $q_{accept}$: Accept state

**Transitions:**
- $q_0$: On $a$, push $a$, stay in $q_0$
- $q_0$: On $b$, push $b$, stay in $q_0$
- $q_0$: On $c$, pop symbol, go to $q_1$
- $q_1$: On $c$, pop symbol, stay in $q_1$
- $q_1$: On $\sqcup$ with empty stack, accept

**Note:** Use $\$$ as bottom-of-stack marker for proper initialization and acceptance checking.

