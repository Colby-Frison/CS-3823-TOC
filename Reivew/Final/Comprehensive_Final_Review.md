# Theory of Computation - Comprehensive Final Review

**Course Coverage:** All topics from Introduction through Time Complexity  
**Reference Materials:** Sipser textbook sections 0.1-0.4, 1.1-1.4, 2.1-2.3, 3.1-3.3, 4.1-4.2, 5.1-5.2, 7.1-7.3  
**Exam Format:** Exercises, True/False, Multiple Choice

---

## Table of Contents

1. [Mathematical Preliminaries (0.1-0.4)](#1-mathematical-preliminaries)
2. [Regular Languages (1.1-1.4)](#2-regular-languages)
3. [Context-Free Languages (2.1-2.3)](#3-context-free-languages)
4. [Turing Machines (3.1-3.3)](#4-turing-machines)
5. [Decidability (4.1-4.2)](#5-decidability)
6. [Reducibility (5.1-5.2)](#6-reducibility)
7. [Time Complexity (7.1-7.3)](#7-time-complexity)
8. [Key Theorems and Results](#8-key-theorems-and-results)
9. [Problem-Solving Strategies](#9-problem-solving-strategies)
10. [Quick Reference](#10-quick-reference)

---

## 1. Mathematical Preliminaries (0.1-0.4)

### 1.1 Sets and Sequences

**Sets:**
- **Definition:** A collection of distinct objects (elements)
- **Notation:** $\{a, b, c\}$, $\{x \mid P(x)\}$ (set builder notation)
- **Empty set:** $\emptyset$ or $\{\}$
- **Cardinality:** $|A|$ = number of elements in set $A$
- **Subset:** $A \subseteq B$ if every element of $A$ is in $B$
- **Proper subset:** $A \subset B$ if $A \subseteq B$ and $A \neq B$
- **Power set:** $\mathcal{P}(A) = \{B \mid B \subseteq A\}$ (set of all subsets)
  - Example: If $A = \{1, 2\}$, then $\mathcal{P}(A) = \{\emptyset, \{1\}, \{2\}, \{1,2\}\}$
  - **Cardinality:** $|\mathcal{P}(A)| = 2^{|A|}$

**Set Operations:**
- **Union:** $A \cup B = \{x \mid x \in A \text{ or } x \in B\}$
- **Intersection:** $A \cap B = \{x \mid x \in A \text{ and } x \in B\}$
- **Difference:** $A - B = \{x \mid x \in A \text{ and } x \notin B\}$
- **Complement:** $\overline{A} = \{x \mid x \notin A\}$ (relative to universe)
- **Cartesian Product:** $A \times B = \{(a,b) \mid a \in A, b \in B\}$
  - Example: $\{1,2\} \times \{a,b\} = \{(1,a), (1,b), (2,a), (2,b)\}$

**Sequences and Tuples:**
- **Sequence:** Ordered list of elements: $(a_1, a_2, \ldots, a_n)$
- **Tuple:** Finite sequence (ordered pair, triple, etc.)
- **String:** Sequence of symbols from an alphabet
- **Length:** $|w|$ = number of symbols in string $w$
- **Empty string:** $\varepsilon$ or $\lambda$ (length 0)

**Example:** Let $A = \{0, 1\}$ and $B = \{a, b\}$
- $A \cup B = \{0, 1, a, b\}$
- $A \cap B = \emptyset$
- $A \times B = \{(0,a), (0,b), (1,a), (1,b)\}$
- Strings over $A$: $\varepsilon, 0, 1, 00, 01, 10, 11, 000, \ldots$

### 1.2 Functions and Relations

**Functions:**
- **Definition:** $f: A \to B$ assigns exactly one element of $B$ to each element of $A$
- **Domain:** Set $A$ (inputs)
- **Codomain:** Set $B$ (possible outputs)
- **Range:** $\{f(a) \mid a \in A\}$ (actual outputs)
- **One-to-one (injective):** $f(a_1) = f(a_2)$ implies $a_1 = a_2$
- **Onto (surjective):** For every $b \in B$, there exists $a \in A$ with $f(a) = b$
- **Bijective:** Both one-to-one and onto

**Example:** $f: \{1,2,3\} \to \{a,b\}$ defined by $f(1) = a$, $f(2) = b$, $f(3) = a$
- Domain: $\{1,2,3\}$, Codomain: $\{a,b\}$, Range: $\{a,b\}$
- Not one-to-one (since $f(1) = f(3) = a$)
- Onto (both $a$ and $b$ are in range)

**Relations:**
- **Binary relation:** Subset of $A \times B$
- **Equivalence relation:** Reflexive, symmetric, transitive
- **Partial order:** Reflexive, antisymmetric, transitive

### 1.3 Graphs

**Graphs:**
- **Definition:** $G = (V, E)$ where $V$ is set of vertices, $E$ is set of edges
- **Directed graph:** Edges have direction (ordered pairs)
- **Undirected graph:** Edges have no direction (unordered pairs)
- **Path:** Sequence of vertices connected by edges
- **Cycle:** Path that starts and ends at same vertex
- **Tree:** Connected graph with no cycles
- **Degree:** Number of edges incident to a vertex

**Example:** Graph with $V = \{1,2,3,4\}$ and $E = \{(1,2), (2,3), (3,4), (4,1)\}$
- This is a cycle of length 4
- Each vertex has degree 2

### 1.4 Strings and Languages

**Alphabet:**
- **Definition:** Finite, nonempty set of symbols (denoted $\Sigma$)
- **Examples:** $\Sigma = \{0, 1\}$ (binary), $\Sigma = \{a, b, c\}$ (letters)

**Strings:**
- **Definition:** Finite sequence of symbols from alphabet
- **Length:** $|w|$ = number of symbols
- **Empty string:** $\varepsilon$ (length 0)
- **Concatenation:** If $w = w_1w_2\ldots w_n$ and $v = v_1v_2\ldots v_m$, then $wv = w_1w_2\ldots w_nv_1v_2\ldots v_m$
- **Powers:** $w^0 = \varepsilon$, $w^1 = w$, $w^2 = ww$, $w^n = ww^{n-1}$
- **Reversal:** $w^R$ = string written backwards
  - Example: If $w = abc$, then $w^R = cba$

**Languages:**
- **Definition:** Set of strings over an alphabet
- **Example:** $L = \{0^n1^n \mid n \geq 0\} = \{\varepsilon, 01, 0011, 000111, \ldots\}$
- **Operations:**
  - **Union:** $L_1 \cup L_2 = \{w \mid w \in L_1 \text{ or } w \in L_2\}$
  - **Concatenation:** $L_1L_2 = \{w_1w_2 \mid w_1 \in L_1, w_2 \in L_2\}$
  - **Kleene Star:** $L^* = \{w_1w_2\ldots w_k \mid k \geq 0, w_i \in L\}$
    - $L^0 = \{\varepsilon\}$, $L^1 = L$, $L^2 = LL$, etc.
    - $L^* = L^0 \cup L^1 \cup L^2 \cup \ldots$

**Example:** Let $\Sigma = \{a, b\}$ and $L = \{a, ab\}$
- $L^0 = \{\varepsilon\}$
- $L^1 = \{a, ab\}$
- $L^2 = \{aa, aab, aba, abab\}$
- $L^* = \{\varepsilon, a, ab, aa, aab, aba, abab, aaa, \ldots\}$ (all strings that can be formed by concatenating elements of $L$)

### 1.5 Proof Techniques

**Proof by Construction:**
- Show existence by explicitly constructing the object
- Example: "There exists a DFA that recognizes language $L$" - construct the DFA

**Proof by Contradiction:**
- Assume the opposite, derive a contradiction
- Example: Pumping lemma proofs assume language is regular, show contradiction

**Proof by Induction:**
- **Base case:** Show statement holds for $n = 0$ (or smallest case)
- **Inductive step:** Assume true for $n = k$, prove for $n = k+1$
- Example: Prove $1 + 2 + \ldots + n = \frac{n(n+1)}{2}$

---

## 2. Regular Languages (1.1-1.4)

### 2.1 Finite Automata

#### Deterministic Finite Automaton (DFA)

**Formal Definition:** $M = (Q, \Sigma, \delta, q_0, F)$
- $Q$: Finite set of states
- $\Sigma$: Input alphabet
- $\delta: Q \times \Sigma \rightarrow Q$: Transition function
- $q_0 \in Q$: Start state
- $F \subseteq Q$: Accept states

**Extended Transition Function:** $\delta^*: Q \times \Sigma^* \rightarrow Q$
- $\delta^*(q, \varepsilon) = q$
- $\delta^*(q, wa) = \delta(\delta^*(q, w), a)$ for $w \in \Sigma^*$, $a \in \Sigma$

**Acceptance:** String $w$ is accepted if $\delta^*(q_0, w) \in F$
- **Language recognized:** $L(M) = \{w \mid \delta^*(q_0, w) \in F\}$

**Example DFA:** Recognize language $\{w \mid w$ contains substring $01\}$ over $\Sigma = \{0, 1\}$

States: $Q = \{q_0, q_1, q_2\}$
- $q_0$: Haven't seen 0 yet
- $q_1$: Just saw 0, waiting for 1
- $q_2$: Already saw 01 (accept state)

Transitions:
- $\delta(q_0, 0) = q_1$, $\delta(q_0, 1) = q_0$
- $\delta(q_1, 0) = q_1$, $\delta(q_1, 1) = q_2$
- $\delta(q_2, 0) = q_2$, $\delta(q_2, 1) = q_2$

Accept states: $F = \{q_2\}$

**Trace:** Input $w = 001$
- Start: $q_0$
- Read 0: $\delta(q_0, 0) = q_1$
- Read 0: $\delta(q_1, 0) = q_1$
- Read 1: $\delta(q_1, 1) = q_2 \in F$ → **Accept**

#### Nondeterministic Finite Automaton (NFA)

**Formal Definition:** $N = (Q, \Sigma, \delta, q_0, F)$
- $\delta: Q \times \Sigma_\varepsilon \rightarrow \mathcal{P}(Q)$: Transition function (returns set of states)
- Can have multiple transitions, $\varepsilon$-transitions, or no transition

**Extended Transition Function:** $\delta^*: Q \times \Sigma^* \rightarrow \mathcal{P}(Q)$
- $\delta^*(q, \varepsilon) = \{q\} \cup \{\text{all states reachable via } \varepsilon\text{-transitions}\}$
- $\delta^*(q, wa) = \bigcup_{r \in \delta^*(q, w)} \delta(r, a)$

**Acceptance:** String $w$ is accepted if $\delta^*(q_0, w) \cap F \neq \emptyset$
- **Key:** At least one computation path leads to accept state

**Example NFA:** Recognize language $\{w \mid w$ ends with $01\}$ over $\Sigma = \{0, 1\}$

States: $Q = \{q_0, q_1, q_2\}$
Transitions:
- $\delta(q_0, 0) = \{q_0, q_1\}$, $\delta(q_0, 1) = \{q_0\}$
- $\delta(q_1, 1) = \{q_2\}$
- $\delta(q_2, 0) = \emptyset$, $\delta(q_2, 1) = \emptyset$

Accept states: $F = \{q_2\}$

**Trace:** Input $w = 001$
- Start: $\{q_0\}$
- Read 0: $\delta(q_0, 0) = \{q_0, q_1\}$
- Read 0: $\delta(q_0, 0) \cup \delta(q_1, 0) = \{q_0, q_1\} \cup \emptyset = \{q_0, q_1\}$
- Read 1: $\delta(q_0, 1) \cup \delta(q_1, 1) = \{q_0\} \cup \{q_2\} = \{q_0, q_2\}$
- Since $q_2 \in F$ and $q_2 \in \{q_0, q_2\}$ → **Accept**

#### Equivalence: DFA = NFA

**Theorem 1.39:** Every NFA has an equivalent DFA.

**Subset Construction Algorithm:**
1. DFA states = all subsets of NFA states
2. DFA start state = $\{q_0\} \cup \{\text{all states reachable via } \varepsilon\text{-transitions}\}$
3. DFA transition: $\delta_{DFA}(R, a) = \bigcup_{r \in R} \delta_{NFA}(r, a)$ (then add $\varepsilon$-closure)
4. DFA accept states = all subsets containing at least one NFA accept state

**Example:** Convert NFA above to DFA

NFA states: $\{q_0, q_1, q_2\}$
DFA states: $\{\emptyset, \{q_0\}, \{q_1\}, \{q_2\}, \{q_0,q_1\}, \{q_0,q_2\}, \{q_1,q_2\}, \{q_0,q_1,q_2\}\}$

Key transitions:
- $\delta_{DFA}(\{q_0\}, 0) = \{q_0, q_1\}$
- $\delta_{DFA}(\{q_0\}, 1) = \{q_0\}$
- $\delta_{DFA}(\{q_0,q_1\}, 0) = \{q_0, q_1\}$
- $\delta_{DFA}(\{q_0,q_1\}, 1) = \{q_0, q_2\}$

Accept states: All subsets containing $q_2$

**Complexity:** If NFA has $n$ states, DFA can have up to $2^n$ states (exponential blowup)

### 2.2 Regular Expressions

**Operations:**
- **Union:** $R_1 \cup R_2$ (or $R_1 | R_2$) - matches strings in $R_1$ or $R_2$
- **Concatenation:** $R_1 R_2$ - matches $w_1w_2$ where $w_1 \in R_1$, $w_2 \in R_2$
- **Kleene Star:** $R^*$ - matches zero or more concatenations of strings from $R$

**Precedence:** Star > Concatenation > Union
- Example: $ab^*|c$ means $(a(b^*))|c$, not $(ab)^*|c$

**Equivalence:** Regular Expressions = DFAs = NFAs = Regular Grammars

**Examples:**
- $(0|1)^*$: All binary strings
- $(0|1)^*0(0|1)^*$: Binary strings containing at least one 0
- $0^*1^*$: Strings with zero or more 0s followed by zero or more 1s
- $(00)^*$: Even-length strings of 0s
- $(0|1)(0|1)$: All binary strings of length exactly 2

**Converting DFA → Regular Expression: GNFA Method**
1. Convert DFA to GNFA (add new start state with $\varepsilon$ to old start, add new accept state with $\varepsilon$ from old accepts)
2. Remove states one by one (except start and accept)
3. When removing state $q$:
   - For each pair $(q_i, q_j)$ where $q_i \neq q \neq q_j$:
     - Update edge: $R_{ij} = R_{ij} | R_{iq}(R_{qq})^*R_{qj}$
4. Final edge label is the regular expression

**Example:** Convert DFA recognizing $\{w \mid w$ contains $01\}$ to regex
- After GNFA conversion and state removal: $(0|1)^*01(0|1)^*$

### 2.3 Regular Grammars

**Right-Linear Form:**
- Productions: $A \to xB$ or $A \to x$ where $x \in \Sigma^*$, $A, B \in V$
- Example: $S \to 0S \mid 1A$, $A \to 0A \mid 1S \mid \varepsilon$

**Left-Linear Form:**
- Productions: $A \to Bx$ or $A \to x$ where $x \in \Sigma^*$, $A, B \in V$

**Conversion DFA → Regular Grammar:**
- Each state becomes a nonterminal
- Each transition $\delta(q, a) = r$ becomes production $q \to ar$
- Each accept state $q$ gets production $q \to \varepsilon$

**Example:** DFA with states $\{q_0, q_1\}$, $\delta(q_0, 0) = q_1$, $\delta(q_1, 1) = q_0$, $F = \{q_1\}$
- Grammar: $q_0 \to 0q_1 \mid 1q_0$, $q_1 \to 0q_1 \mid 1q_0 \mid \varepsilon$

### 2.4 Pumping Lemma for Regular Languages

**Statement:** If $L$ is regular, then there exists pumping length $p$ such that for any string $s \in L$ with $|s| \geq p$, we can write $s = xyz$ where:
1. $|y| > 0$
2. $|xy| \leq p$
3. For all $i \geq 0$, $xy^iz \in L$

**Intuition:** In any string long enough, there's a "pumpable" substring that can be repeated

**Use:** Prove languages are **NOT regular** by contradiction

**Proof Strategy:**
1. Assume $L$ is regular (so pumping length $p$ exists)
2. Choose string $s \in L$ with $|s| \geq p$ (cleverly!)
3. Show for **all** splits $s = xyz$ (satisfying conditions 1-2), some $xy^iz \notin L$
4. Contradiction → $L$ is not regular

**Example:** Prove $L = \{0^n1^n \mid n \geq 0\}$ is not regular

**Proof:**
1. Assume $L$ is regular with pumping length $p$
2. Choose $s = 0^p1^p$ (clearly $|s| = 2p \geq p$ and $s \in L$)
3. For any split $s = xyz$ with $|xy| \leq p$ and $|y| > 0$:
   - Since $|xy| \leq p$ and $s$ starts with $p$ zeros, $y$ consists only of 0s
   - Let $y = 0^k$ where $1 \leq k \leq p$
   - Consider $xy^0z = xz = 0^{p-k}1^p$
   - This has fewer 0s than 1s, so $xz \notin L$
4. Contradiction! Therefore $L$ is not regular.

**Common String Choices:**
- $0^p1^p$: For languages requiring equal counts
- $0^{p!}$: For languages with factorial constraints
- $1^{2^p}$: For languages with exponential constraints

### 2.5 Closure Properties

**Regular languages are closed under:**
- **Union:** Given DFAs $M_1, M_2$, construct NFA with $\varepsilon$-transitions from new start to both old starts
- **Concatenation:** Connect accept states of $M_1$ to start state of $M_2$ via $\varepsilon$
- **Star:** Add $\varepsilon$-transitions from accept states back to start, make start accepting
- **Complement:** Swap accept and reject states in DFA
- **Intersection:** Product construction: $Q = Q_1 \times Q_2$, $\delta((q_1,q_2), a) = (\delta_1(q_1,a), \delta_2(q_2,a))$, $F = F_1 \times F_2$
- **Set Difference:** $L_1 - L_2 = L_1 \cap \overline{L_2}$ (use intersection and complement)

**Example:** Show $L = \{w \mid w$ has even number of 0s and odd number of 1s$\}$ is regular
- $L_1 = \{w \mid w$ has even number of 0s$\}$ is regular
- $L_2 = \{w \mid w$ has odd number of 1s$\}$ is regular
- $L = L_1 \cap L_2$ is regular (by closure under intersection)

---

## 3. Context-Free Languages (2.1-2.3)

### 3.1 Context-Free Grammars (CFG)

**Formal Definition:** $G = (V, \Sigma, R, S)$
- $V$: Nonterminals (variables)
- $\Sigma$: Terminals
- $R$: Production rules of form $A \to w$ where $A \in V$, $w \in (V \cup \Sigma)^*$
- $S$: Start symbol

**Language:** $L(G) = \{w \in \Sigma^* \mid S \Rightarrow^* w\}$

**Derivations:**
- **Leftmost:** Always expand leftmost nonterminal
- **Rightmost:** Always expand rightmost nonterminal
- **Parse tree:** Tree representation showing how string is derived

**Example:** Grammar $G$ with productions:
- $S \to aSb \mid ab$

**Leftmost derivation for "aabb":**
$S \Rightarrow aSb \Rightarrow aabb$
- Step 1: Apply $S \to aSb$ (leftmost $S$ expanded)
- Step 2: Apply $S \to ab$ to the middle $S$ (leftmost $S$ expanded)

**Rightmost derivation for "aabb":**
$S \Rightarrow aSb \Rightarrow aabb$
- (Same for this grammar since only one nonterminal at each step)

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

**Key Point:** For each step, strictly expand the leftmost (or rightmost) nonterminal until it's replaced by terminals before moving to the next nonterminal.

**Chomsky Normal Form (CNF):**
- All productions: $A \to BC$ or $A \to a$ where $A, B, C \in V$, $a \in \Sigma$
- Every CFL has a grammar in CNF

**Conversion to CNF (5 steps):**
1. Add new start variable $S_0$ if $S$ appears on RHS
2. Eliminate $\varepsilon$-rules ($A \to \varepsilon$) except possibly $S_0 \to \varepsilon$
3. Eliminate unit rules ($A \to B$)
4. Patch up grammar (handle any issues from steps 2-3)
5. Convert to CNF form:
   - Replace terminals in long productions: $A \to aB$ becomes $A \to A_aB$ where $A_a \to a$
   - Break long sequences: $A \to BCD$ becomes $A \to BE$, $E \to CD$

**Example:** Convert grammar $S \to aSb \mid ab$ to CNF
- Step 1: No need (S doesn't appear on RHS)
- Step 2: No $\varepsilon$-rules
- Step 3: No unit rules
- Step 4: N/A
- Step 5:
  - $S \to aSb$: Introduce $A \to a$, $B \to b$, then $S \to ASB$, then $S \to AC$, $C \to SB$
  - $S \to ab$: $S \to AB$
- Final CNF: $S \to AC \mid AB$, $C \to SB$, $A \to a$, $B \to b$

**Ambiguity:**
- Grammar is ambiguous if some string has multiple leftmost derivations (equivalently, multiple parse trees)
- Some languages are inherently ambiguous (every grammar is ambiguous)

**Example of Ambiguous Grammar:** 
- $E \to E + E \mid E * E \mid id$

String "id + id * id" has two different leftmost derivations:

**Derivation 1** (addition before multiplication):
$E \Rightarrow E + E \Rightarrow id + E \Rightarrow id + E * E \Rightarrow id + id * E \Rightarrow id + id * id$
- Parse tree: $(id + id) * id$

**Derivation 2** (multiplication before addition):
$E \Rightarrow E * E \Rightarrow E + E * E \Rightarrow id + E * E \Rightarrow id + id * E \Rightarrow id + id * id$
- Parse tree: $id + (id * id)$

**To remove ambiguity:** Use grammar with precedence:
- $E \to E + T \mid T$ (addition at outer level)
- $T \to T * F \mid F$ (multiplication at inner level)
- $F \to (E) \mid id$ (parentheses and identifiers)

This forces multiplication to bind tighter than addition.

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

**Example PDA:** Recognize $\{0^n1^n \mid n \geq 0\}$

States: $Q = \{q_0, q_1, q_2\}$
Stack alphabet: $\Gamma = \{0, \$\}$ (use $\$$ as bottom marker)

Transitions:
- $\delta(q_0, \varepsilon, \varepsilon) = \{(q_1, \$)\}$: Push $\$$ to mark bottom
- $\delta(q_1, 0, \varepsilon) = \{(q_1, 0)\}$: Read 0, push 0
- $\delta(q_1, 1, 0) = \{(q_2, \varepsilon)\}$: Read 1, pop 0
- $\delta(q_2, 1, 0) = \{(q_2, \varepsilon)\}$: Read 1, pop 0
- $\delta(q_2, \varepsilon, \$) = \{(q_2, \varepsilon)\}$: Pop $\$$, accept

**Trace:** Input $w = 0011$
- Start: $q_0$, stack: $\varepsilon$
- $\varepsilon$-transition: $q_1$, stack: $\$$
- Read 0: $q_1$, stack: $0\$$
- Read 0: $q_1$, stack: $00\$$
- Read 1: $q_2$, stack: $0\$$ (popped one 0)
- Read 1: $q_2$, stack: $\$$ (popped one 0)
- $\varepsilon$-transition: $q_2$, stack: $\varepsilon$ → **Accept** (empty stack)

**Equivalence:** CFG = Nondeterministic PDA

**CFG → PDA (Standard Construction):**
1. Push start symbol $S$ onto stack
2. For each production $A \to w$: Add transition $\varepsilon, A \to w^R$ (push $w$ in reverse)
3. For each terminal $a$: Add transition $a, a \to \varepsilon$ (match terminal)
4. Accept by empty stack

**Example:** Grammar $S \to aSb \mid ab$ → PDA:
- $\varepsilon, S \to bSa$ (for $S \to aSb$, reversed: $bSa$)
- $\varepsilon, S \to ba$ (for $S \to ab$, reversed: $ba$)
- $a, a \to \varepsilon$ and $b, b \to \varepsilon$ (match terminals)

**PDA → CFG (State Pair Construction):**
- Variables $A_{pq}$ represent "path from state $p$ to state $q$ that empties stack"
- For transition $\delta(p, a, A) \ni (q, B_1B_2\ldots B_k)$:
  - Add productions: $A_{pq} \to a B_{1,r_1} B_{2,r_2} \ldots B_{k,r_k}$ for all state sequences
- For transition $\delta(p, a, A) \ni (q, \varepsilon)$:
  - Add production: $A_{pq} \to a$
- Start variable: $S = A_{q_0,q_{accept}}$

**Deterministic PDAs:** Recognize proper subset of CFLs (deterministic CFLs)

### 3.3 Pumping Lemma for Context-Free Languages

**Statement:** If $L$ is context-free, then there exists pumping length $p$ such that for any string $w \in L$ with $|w| \geq p$, we can write $w = uvxyz$ where:
1. $|vxy| \leq p$
2. $|vy| \geq 1$
3. For all $i \geq 0$, $uv^ixy^iz \in L$

**Key Difference from Regular:** 5 parts instead of 3 (due to branching in parse trees)

**Use:** Prove languages are **NOT context-free**

**Proof Strategy:**
1. Assume $L$ is context-free (so pumping length $p$ exists)
2. Choose string $w \in L$ with $|w| \geq p$ (cleverly!)
3. Show for **all** decompositions $w = uvxyz$ (satisfying conditions 1-2), some $uv^ixy^iz \notin L$
4. Contradiction → $L$ is not context-free

**Example:** Prove $L = \{a^nb^nc^n \mid n \geq 0\}$ is not context-free

**Proof:**
1. Assume $L$ is context-free with pumping length $p$
2. Choose $w = a^pb^pc^p$ (clearly $|w| = 3p \geq p$ and $w \in L$)
3. For any decomposition $w = uvxyz$ with $|vxy| \leq p$ and $|vy| \geq 1$:
   - Since $|vxy| \leq p$, $vxy$ cannot contain all three symbols $a, b, c$
   - **Case 1:** $vxy$ contains only $a$s and $b$s (or only $b$s and $c$s)
     - Then $uv^2xy^2z$ has more $a$s and $b$s than $c$s (or vice versa)
     - So $uv^2xy^2z \notin L$
   - **Case 2:** $vxy$ contains only one type of symbol
     - Then $uv^2xy^2z$ has unequal counts, so $\notin L$
4. Contradiction! Therefore $L$ is not context-free.

**Common String Choices:**
- $a^pb^pc^p$: For languages requiring equal counts of different symbols
- $a^pc^pb^pd^p$: For languages with multiple symbol types

**Case Analysis:** Since $|vxy| \leq p$, consider:
- $vxy$ contained in one block (e.g., all in $a^p$ section)
- $vxy$ straddles boundaries (e.g., part in $a^p$, part in $b^p$)

### 3.4 Closure Properties

**Context-free languages are closed under:**
- **Union:** $S \to S_1 \mid S_2$ where $S_1, S_2$ are start symbols of grammars for $L_1, L_2$
- **Concatenation:** $S \to S_1 S_2$
- **Star:** $S \to S_1 S \mid \varepsilon$

**Context-free languages are NOT closed under:**
- **Complement:** If CFLs were closed under complement, they'd be closed under intersection (since $L_1 \cap L_2 = \overline{\overline{L_1} \cup \overline{L_2}}$), but they're not
- **Intersection:** Counterexample: $\{a^nb^nc^n\}$ is intersection of $\{a^nb^mc^n\}$ and $\{a^mb^nc^n\}$, both CFLs, but result is not CFL

**Regular ⊆ Context-Free:**
- Every DFA is a PDA (ignore stack)
- Every regular language is context-free

---

## 4. Turing Machines (3.1-3.3)

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

**Configuration:** $uqv$ where:
- $u$: Tape content to left of head
- $q$: Current state
- $v$: Tape content at and to right of head
- Head is reading first symbol of $v$

**Example:** Configuration $01q_21$ means:
- Tape: $\ldots \sqcup 0 1 1 \sqcup \ldots$
- State: $q_2$
- Head: reading the rightmost 1

**Computation:** Sequence of configurations
- Start: $q_0w$ (input $w$ on tape, head at leftmost symbol)
- Step: $uqv \vdash u'rq'v'$ if transition applies
- Accept: Configuration with $q_{accept}$
- Reject: Configuration with $q_{reject}$
- Loop: Infinite sequence (never halts)

**Example TM:** Decide language $\{w \mid w$ contains substring $01\}$ over $\{0,1\}$

States: $Q = \{q_0, q_1, q_{accept}, q_{reject}\}$
- $q_0$: Haven't seen 0 yet
- $q_1$: Just saw 0, looking for 1

Transitions:
- $\delta(q_0, 0) = (q_1, 0, R)$: See 0, move to $q_1$, stay on tape
- $\delta(q_0, 1) = (q_0, 1, R)$: See 1, stay in $q_0$, move right
- $\delta(q_1, 0) = (q_1, 0, R)$: See 0, stay in $q_1$, move right
- $\delta(q_1, 1) = (q_{accept}, 1, R)$: See 1, accept
- $\delta(q_0, \sqcup) = (q_{reject}, \sqcup, R)$: End of input in $q_0$, reject
- $\delta(q_1, \sqcup) = (q_{reject}, \sqcup, R)$: End of input in $q_1$, reject

**Trace:** Input $w = 001$
- Start: $q_0 001$
- $\delta(q_0, 0) = (q_1, 0, R)$: $0q_1 01$
- $\delta(q_1, 0) = (q_1, 0, R)$: $00q_1 1$
- $\delta(q_1, 1) = (q_{accept}, 1, R)$: $001q_{accept} \sqcup$ → **Accept**

### 4.2 Language Classes

#### Turing-Recognizable (Recursively Enumerable)
- Language $L$ is recognizable if some TM accepts all strings in $L$
- TM may loop forever on strings not in $L$
- **Example:** $A_{TM} = \{\langle M, w \rangle \mid M$ accepts $w\}$ is recognizable (universal TM simulates $M$ on $w$)

#### Turing-Decidable (Recursive)
- Language $L$ is decidable if some TM:
  - Accepts all strings in $L$
  - Rejects all strings not in $L$
- TM **always halts** on every input
- **Example:** $A_{DFA} = \{\langle M, w \rangle \mid M$ is DFA that accepts $w\}$ is decidable (simulate DFA, always halts)

**Relationship:** Decidable ⊆ Recognizable
- Every decider is also a recognizer
- But not every recognizer is a decider

### 4.3 Variants of Turing Machines

**All variants are equivalent:**
- **Multitape TM = Single-tape TM:** Use separators and marked symbols to simulate multiple tapes
- **Nondeterministic TM = Deterministic TM:** BFS on computation tree
- **Enumerator = Turing-recognizable languages:** Enumerator lists all strings in language

**Simulation Techniques:**
- **Multitape:** Use tape symbols like $\#a\#b\#$ to represent multiple tapes, use markers to track head positions
- **Nondeterministic:** Systematically explore all computation paths using breadth-first search

### 4.4 The Church-Turing Thesis

**Statement:** "The intuitive notion of algorithms equals Turing machine algorithms"

**Implications:**
- TMs capture all computable functions
- If no TM can solve a problem, no algorithm can
- Establishes TMs as formal model of computation

---

## 5. Decidability (4.1-4.2)

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
  - Process each symbol of $w$ exactly once
  - Each transition lookup is constant time
  - Total: $|w|$ operations = $O(|w|)$

**$A_{NFA}$ = $\{\langle N, w \rangle \mid N$ is an NFA that accepts $w\}$** ✓ Decidable
- **Decider:** Convert NFA to equivalent DFA (subset construction), then simulate
- Or: Simulate NFA by tracking all possible states simultaneously
- **Time complexity:** $O(2^{|Q|} \cdot |w|)$ where $Q$ is set of states
  - Subset construction creates at most $2^{|Q|}$ states
  - Simulation on $|w|$ symbols: $O(2^{|Q|} \cdot |w|)$

**$A_{REX}$ = $\{\langle R, w \rangle \mid R$ is a regex that matches $w\}$** ✓ Decidable
- **Decider:** Convert regex to equivalent NFA, then use $A_{NFA}$ decider
- **Time complexity:** Exponential in worst case (due to NFA to DFA conversion)

**$A_{CFG}$ = $\{\langle G, w \rangle \mid G$ is a CFG that generates $w\}$** ✓ Decidable
- **Decider:** Use CYK algorithm or convert to CNF and check all derivations
- **Time complexity:** $O(|w|^3 \cdot |G|)$ for CYK algorithm
  - Fill $|w|^2$ table cells
  - Each cell: check $O(|w|)$ splits, $O(|G|)$ productions
  - Total: $O(|w|^3 \cdot |G|)$

**$E_{DFA}$ = $\{\langle M \rangle \mid M$ is a DFA and $L(M) = \emptyset\}$** ✓ Decidable
- **Decider:** Check if any accept state is reachable from start state
- Use graph reachability (BFS/DFS) on DFA's state diagram
- Accept if no accept state reachable, reject otherwise
- **Time complexity:** $O(|Q| + |\delta|)$ where $Q$ is states, $\delta$ is transitions
  - Graph traversal visits each state and transition once

**$EQ_{DFA}$ = $\{\langle M_1, M_2 \rangle \mid M_1, M_2$ are DFAs and $L(M_1) = L(M_2)\}$** ✓ Decidable

**Method 1: Symmetric Difference (Standard Method)**
- **Key Idea:** $L(M_1) = L(M_2)$ if and only if their symmetric difference is empty
- **Symmetric difference:** $L(M_1) \triangle L(M_2) = (L(M_1) \cap \overline{L(M_2)}) \cup (\overline{L(M_1)} \cap L(M_2))$
- **Algorithm:**
  1. Construct DFA $C$ for symmetric difference using closure properties
  2. Use $E_{DFA}$ decider on $C$
  3. If $L(C) = \emptyset$, then $L(M_1) = L(M_2)$ (accept)
  4. Otherwise, $L(M_1) \neq L(M_2)$ (reject)
- **Time complexity:** Polynomial $O((nm)^2 \cdot |\Sigma|)$ where $n, m$ are number of states

**Method 2: Testing All Strings Up to a Certain Size**
- **Bound:** Test all strings up to length $n \cdot m - 1$ where $n, m$ are number of states
- **Reasoning:** If languages differ, shortest distinguishing string has length $< n \cdot m$
- **Time complexity:** Exponential $O(|\Sigma|^{nm} \cdot nm)$
- **Note:** Less efficient but demonstrates the bound

### 5.2 Undecidable Languages

**Definition:** A language $L$ is **undecidable** if no Turing machine can decide it.

**Key Examples:**

**$A_{TM}$ = $\{\langle M, w \rangle \mid M$ is a TM that accepts $w\}$** ✗ Undecidable
- **Why undecidable:** TMs can loop forever. We cannot determine if a TM will accept without running it, but running it might never halt.
- **Proof (Diagonalization):**
  1. Assume $A_{TM}$ is decidable by decider $H$
  2. Construct TM $D$ that: On input $\langle M \rangle$, runs $H$ on $\langle M, \langle M \rangle \rangle$
  3. $D$ accepts if $H$ rejects, $D$ rejects if $H$ accepts
  4. Consider $D$ on input $\langle D \rangle$:
     - If $D$ accepts $\langle D \rangle$, then $H$ rejects $\langle D, \langle D \rangle \rangle$, so $D$ doesn't accept $\langle D \rangle$ → Contradiction!
     - If $D$ rejects $\langle D \rangle$, then $H$ accepts $\langle D, \langle D \rangle \rangle$, so $D$ accepts $\langle D \rangle$ → Contradiction!
  5. Therefore, $H$ cannot exist

**$HALT_{TM}$ = $\{\langle M, w \rangle \mid M$ is a TM that halts on $w\}$** ✗ Undecidable
- **Proof:** Reduction from $A_{TM}$
  - Assume $HALT_{TM}$ is decidable by decider $H$
  - To decide $A_{TM}$ on $\langle M, w \rangle$:
    1. Run $H$ on $\langle M, w \rangle$ (check if $M$ halts on $w$)
    2. If no, reject (doesn't accept)
    3. If yes, simulate $M$ on $w$ until it halts, then check if it accepted
  - This would decide $A_{TM}$, contradiction!

**$E_{TM}$ = $\{\langle M \rangle \mid M$ is a TM and $L(M) = \emptyset\}$** ✗ Undecidable
- **Proof:** Reduction from $A_{TM}$
  - Given $\langle M, w \rangle$, construct $M'$ that: ignores input, simulates $M$ on $w$, accepts if $M$ accepts $w$
  - $L(M') = \Sigma^*$ if $M$ accepts $w$, else $L(M') = \emptyset$
  - If $E_{TM}$ were decidable, we could decide $A_{TM}$: check if $L(M') = \emptyset$

**$EQ_{TM}$ = $\{\langle M_1, M_2 \rangle \mid M_1, M_2$ are TMs and $L(M_1) = L(M_2)\}$** ✗ Undecidable
- **Proof:** Reduction from $E_{TM}$
  - Given $\langle M \rangle$, check if $L(M) = L(M_\emptyset)$ where $M_\emptyset$ rejects everything
  - If $EQ_{TM}$ were decidable, $E_{TM}$ would be decidable, contradiction

### 5.3 Recognizable but Not Decidable

**Definition:** A language $L$ is **Turing-recognizable** if there exists a TM $M$ that:
- Accepts all strings in $L$
- May loop forever on strings not in $L$

**Key Relationship:** Decidable ⊆ Recognizable

**Examples:**
- **$A_{TM}$ is recognizable but not decidable:**
  - Universal TM $U$ simulates $M$ on $w$
  - If $M$ accepts $w$, $U$ accepts
  - If $M$ rejects or loops, $U$ loops
- **$E_{TM}$ is not recognizable:**
  - To recognize $E_{TM}$, need to verify TM accepts nothing
  - But checking all inputs is impossible (infinite)
  - If we find one accepting input, language is non-empty
  - But if we never find one, can't tell if empty or haven't checked enough

**Key Fact:** If $L$ and $\overline{L}$ are both recognizable, then $L$ is decidable
- **Proof:** Run recognizers for $L$ and $\overline{L}$ in parallel (alternating steps)
- One must eventually accept, then decide accordingly

---

## 6. Reducibility (5.1-5.2)

### 6.1 Notation and Basic Concepts

**Notation:**
- **$\langle M, w \rangle$:** A string encoding of both a Turing machine $M$ and an input string $w$
- **$A \leq_m B$:** Problem $A$ reduces to problem $B$ (read as "$A$ reduces to $B$" or "$B$ is at least as hard as $A$")
- **Mapping reduction:** A computable function that converts instances of problem $A$ to instances of problem $B$

**Key Principle:**
If problem $A$ is already known to be undecidable, and we can show that:
> *If we could solve problem $B$, then we could use that solution to solve problem $A$*

then problem $B$ must also be undecidable (otherwise we get a contradiction).

**Intuition:** If we could solve $B$, we could solve $A$. Since $A$ is unsolvable, $B$ must be unsolvable too.

### 6.2 The Foundation: $A_{TM}$ (The Acceptance Problem)

**Definition:** $A_{TM} = \{\langle M, w \rangle \mid M$ is a TM that accepts $w\}$

**Why $A_{TM}$ is Important:**
- **$A_{TM}$ is the "seed" undecidable problem** — proven undecidable using diagonalization (Theorem 4.11)
- Many other problems are proven undecidable by reducing $A_{TM}$ to them
- Once we have one undecidable problem, we can prove others undecidable via reduction

**Key Facts about $A_{TM}$:**
- **Undecidable:** No TM can decide $A_{TM}$ (proven by diagonalization)
- **Turing-recognizable:** Universal TM $U$ recognizes $A_{TM}$ (simulates $M$ on $w$; accepts if $M$ accepts)
- **Not co-recognizable:** $\overline{A_{TM}}$ is not recognizable

**The Diagonalization Proof (Summary):**
1. Assume $A_{TM}$ is decidable by decider $H$
2. Construct TM $D$ that: On input $\langle M \rangle$, runs $H$ on $\langle M, \langle M \rangle \rangle$
3. $D$ accepts if $H$ rejects, $D$ rejects if $H$ accepts
4. Consider $D$ on input $\langle D \rangle$: Contradiction!
5. Therefore, $H$ cannot exist

### 6.3 Mapping Reductions: Formal Definition

**Definition:** $A \leq_m B$ if there exists computable function $f$ such that:
- $w \in A$ if and only if $f(w) \in B$

**Properties of Mapping Reductions:**
- If $A \leq_m B$ and $B$ is decidable, then $A$ is decidable
- If $A \leq_m B$ and $A$ is undecidable, then $B$ is undecidable
- If $A \leq_m B$ and $B$ is recognizable, then $A$ is recognizable

**How Reductions Work:**
1. Given an instance $w$ of problem $A$
2. Transform it into instance $f(w)$ of problem $B$ using computable function $f$
3. Solve problem $B$ on $f(w)$
4. The answer for $B$ gives us the answer for $A$

**Use:** To prove undecidability
- If $A$ is known to be undecidable
- And $A \leq_m B$
- Then $B$ is also undecidable

### 6.4 First Reduction: $A_{TM} \leq_m HALT_{TM}$ (The Halting Problem)

**Goal:** Prove that $HALT_{TM} = \{\langle M, w \rangle \mid M$ halts on $w\}$ is undecidable.

**Why This Matters:**
- The Halting Problem is one of the most famous undecidable problems
- It's the foundation for understanding that we cannot write perfect program analyzers
- Demonstrates the reduction technique clearly

**Proof Strategy:** Use reduction from $A_{TM}$ (which we know is undecidable from diagonalization).

**The Reduction Function:**
Given $\langle M, w \rangle$, construct $\langle M', w \rangle$ where $M'$ is a TM that:
- Simulates $M$ on $w$
- If $M$ accepts, $M'$ accepts
- If $M$ rejects, $M'$ enters infinite loop

**Claim:** $\langle M, w \rangle \in A_{TM}$ if and only if $\langle M', w \rangle \in HALT_{TM}$

**Verification:**
- If $M$ accepts $w$: Then $M'$ halts (accepts) → $\langle M', w \rangle \in HALT_{TM}$ ✓
- If $M$ rejects $w$: Then $M'$ loops → $\langle M', w \rangle \notin HALT_{TM}$ ✓
- If $M$ loops on $w$: Then $M'$ loops → $\langle M', w \rangle \notin HALT_{TM}$ ✓

**The Complete Proof by Contradiction:**

1. **Assume (for contradiction) that $HALT_{TM}$ is decidable.**
   - That is, there exists a Turing machine $R$ that decides $HALT_{TM}$.
   - $R$ always halts and:
     - Accepts if $M$ halts on $w$
     - Rejects if $M$ loops (doesn't halt) on $w$

2. **Build a Turing machine $S$ for $A_{TM}$ using $R$:**
   
   **Algorithm for $S$ on input $\langle M, w \rangle$:**
   ```
   1. Run R on ⟨M, w⟩.
   2. If R rejects (M doesn't halt on w), 
      then S rejects (because if M doesn't halt, it can't accept).
   3. If R accepts (M does halt on w),
      then simulate M on w until it halts.
      - If M accepts, S accepts.
      - If M rejects, S rejects.
   ```

3. **Analysis of $S$:**
   - **$S$ always halts:** Since $R$ always halts, and if $R$ says $M$ halts, we can simulate $M$ until it halts (which it will, by $R$'s guarantee).
   - **$S$ correctly decides $A_{TM}$:**
     - If $\langle M, w \rangle \in A_{TM}$ (i.e., $M$ accepts $w$):
       - Then $M$ halts on $w$, so $R$ accepts
       - $S$ simulates $M$ on $w$ and sees it accepts
       - $S$ accepts ✓
     - If $\langle M, w \rangle \notin A_{TM}$ (i.e., $M$ rejects or loops on $w$):
       - If $M$ loops: $R$ rejects, so $S$ rejects ✓
       - If $M$ rejects: $R$ accepts (since $M$ halts), $S$ simulates and sees rejection, so $S$ rejects ✓

4. **Contradiction:**
   - We've constructed $S$ that decides $A_{TM}$.
   - But we know from Theorem 4.11 that $A_{TM}$ is undecidable (proven by diagonalization).
   - Therefore, our initial assumption must be false.
   - **Conclusion: $HALT_{TM}$ is undecidable.**

**Key Insights:**
- **Reduction transfers undecidability:** If solving $HALT_{TM}$ would let us solve $A_{TM}$, and $A_{TM}$ is unsolvable, then $HALT_{TM}$ must also be unsolvable.
- **The proof constructs a hypothetical machine ($S$) that can't exist**, showing the initial assumption (that $R$ exists) must be false.
- **Both $A_{TM}$ and $HALT_{TM}$ are:**
  - Turing-recognizable (universal TM recognizes $A_{TM}$; similar construction for $HALT_{TM}$)
  - Undecidable
  - Not co-recognizable (their complements are not recognizable)

**Essence:** If halting were decidable, acceptance would be decidable. But acceptance isn't decidable, so halting can't be decidable either.

### 6.4 More Reductions: Building the Hierarchy

**Big Picture:**
This proof technique allows us to build a **hierarchy of undecidability**: once we prove a problem undecidable ($A_{TM}$ via diagonalization), we can prove many others undecidable by reduction—no need to redo the diagonalization argument every time.

**$A_{TM} \leq_m E_{TM}$: The Emptiness Problem**

**Definition:** $E_{TM} = \{\langle M \rangle \mid M$ is a TM and $L(M) = \emptyset\}$

**Goal:** Prove $E_{TM}$ is undecidable.

**Reduction Strategy:** If we could decide emptiness, we could decide acceptance.

**The Reduction:**
Given $\langle M, w \rangle$, construct $M'$ that:
- Ignores input $x$
- Simulates $M$ on $w$
- If $M$ accepts $w$, $M'$ accepts $x$
- If $M$ rejects or loops on $w$, $M'$ rejects $x$

**Claim:** $\langle M, w \rangle \in A_{TM}$ if and only if $\langle M' \rangle \notin E_{TM}$

**Verification:**
- If $M$ accepts $w$: Then $L(M') = \Sigma^* \neq \emptyset$ → $\langle M' \rangle \notin E_{TM}$ ✓
- If $M$ doesn't accept $w$: Then $L(M') = \emptyset$ → $\langle M' \rangle \in E_{TM}$ ✓

**Conclusion:** If $E_{TM}$ were decidable, we could decide $A_{TM}$ (contradiction). Therefore, $E_{TM}$ is undecidable.

**$A_{TM} \leq_m EQ_{TM}$: The Equivalence Problem**

**Definition:** $EQ_{TM} = \{\langle M_1, M_2 \rangle \mid M_1, M_2$ are TMs and $L(M_1) = L(M_2)\}$

**Goal:** Prove $EQ_{TM}$ is undecidable.

**Reduction Strategy:** Use the $E_{TM}$ reduction as a building block.

**The Reduction:**
Given $\langle M, w \rangle$, construct:
- $M_1 = M'$ (from $E_{TM}$ reduction above)
- $M_2$ = TM that rejects everything (so $L(M_2) = \emptyset$)

**Claim:** $\langle M, w \rangle \in A_{TM}$ if and only if $\langle M_1, M_2 \rangle \notin EQ_{TM}$

**Verification:**
- If $M$ accepts $w$: Then $L(M_1) = \Sigma^* \neq \emptyset = L(M_2)$ → not equivalent → $\langle M_1, M_2 \rangle \notin EQ_{TM}$ ✓
- If $M$ doesn't accept $w$: Then $L(M_1) = \emptyset = L(M_2)$ → equivalent → $\langle M_1, M_2 \rangle \in EQ_{TM}$ ✓

**Conclusion:** If $EQ_{TM}$ were decidable, we could decide $A_{TM}$ (contradiction). Therefore, $EQ_{TM}$ is undecidable.

**Note:** We can also reduce $E_{TM}$ to $EQ_{TM}$ directly: Given $\langle M \rangle$, check if $L(M) = L(M_\emptyset)$ where $M_\emptyset$ rejects everything.

### 6.5 Post Correspondence Problem (PCP)

**Definition:** Given a collection of dominoes, each with a top string and bottom string, determine if there exists a sequence of dominoes (with repetition allowed) such that the concatenation of top strings equals the concatenation of bottom strings.

**Example:** Dominoes:
- Domino 1: $\frac{a}{ab}$ (top: $a$, bottom: $ab$)
- Domino 2: $\frac{b}{a}$ (top: $b$, bottom: $a$)
- Domino 3: $\frac{ab}{b}$ (top: $ab$, bottom: $b$)

**Solution:** Use dominoes 1, 2, 3, 2:
- Top: $a \cdot b \cdot ab \cdot b = ababb$
- Bottom: $ab \cdot a \cdot b \cdot a = ababa$
- Not equal, so this is not a solution.

**Actual solution:** Use domino 1 twice, then domino 2:
- Top: $a \cdot a = aa$
- Bottom: $ab \cdot ab = abab$
- Not equal either.

**Key Fact:** The Post Correspondence Problem is **undecidable**.
- This means there is no algorithm that can determine, for an arbitrary set of dominoes, whether a solution exists.
- Used as a tool to prove other problems undecidable via reduction.

---

## 7. Time Complexity (7.1-7.3)

### 7.1 Asymptotic Notation

**Big-O Notation ($O$):**
- **Definition:** $f(n) = O(g(n))$ if there exist constants $c > 0$ and $n_0 > 0$ such that:
  - $f(n) \leq c \cdot g(n)$ for all $n \geq n_0$
- **Intuition:** $f$ grows no faster than $g$ (upper bound)
- **Example:** $2n + 3 = O(n)$
  - Proof: $2n + 3 \leq 2n + 3n = 5n$ for $n \geq 1$, so $c = 5$, $n_0 = 1$

**Big-Omega Notation ($\Omega$):**
- **Definition:** $f(n) = \Omega(g(n))$ if there exist constants $c > 0$ and $n_0 > 0$ such that:
  - $f(n) \geq c \cdot g(n)$ for all $n \geq n_0$
- **Intuition:** $f$ grows at least as fast as $g$ (lower bound)
- **Example:** $n^2 = \Omega(n)$
  - Proof: $n^2 \geq 1 \cdot n$ for $n \geq 1$, so $c = 1$, $n_0 = 1$

**Theta Notation ($\Theta$):**
- **Definition:** $f(n) = \Theta(g(n))$ if $f(n) = O(g(n))$ and $f(n) = \Omega(g(n))$
- **Intuition:** $f$ grows at the same rate as $g$ (tight bound)
- **Example:** $3n^2 + 2n + 1 = \Theta(n^2)$
  - $3n^2 + 2n + 1 = O(n^2)$: $3n^2 + 2n + 1 \leq 3n^2 + 2n^2 + n^2 = 6n^2$ for $n \geq 1$
  - $3n^2 + 2n + 1 = \Omega(n^2)$: $3n^2 + 2n + 1 \geq 3n^2$ for $n \geq 1$

**Little-o Notation ($o$):**
- **Definition:** $f(n) = o(g(n))$ if $\lim_{n \to \infty} \frac{f(n)}{g(n)} = 0$
- **Intuition:** $f$ grows strictly slower than $g$
- **Example:** $n = o(n^2)$
  - Proof: $\lim_{n \to \infty} \frac{n}{n^2} = \lim_{n \to \infty} \frac{1}{n} = 0$

**Little-omega Notation ($\omega$):**
- **Definition:** $f(n) = \omega(g(n))$ if $\lim_{n \to \infty} \frac{f(n)}{g(n)} = \infty$
- **Intuition:** $f$ grows strictly faster than $g$
- **Example:** $n^2 = \omega(n)$
  - Proof: $\lim_{n \to \infty} \frac{n^2}{n} = \lim_{n \to \infty} n = \infty$

**Common Complexity Classes:**
- $O(1)$: Constant time
- $O(\log n)$: Logarithmic
- $O(n)$: Linear
- $O(n \log n)$: Linearithmic
- $O(n^2)$: Quadratic
- $O(n^3)$: Cubic
- $O(2^n)$: Exponential
- $O(n!)$: Factorial

**Examples:**
- $2n = O(n)$: Yes, $2n \leq 3n$ for $n \geq 1$
- $3^n = 2^{O(n)}$: Yes, $3^n = 2^{n \log_2 3} = 2^{O(n)}$
- $n = o(2n)$: No, $\lim_{n \to \infty} \frac{n}{2n} = \frac{1}{2} \neq 0$
- $2^n = o(3^n)$: Yes, $\lim_{n \to \infty} \frac{2^n}{3^n} = \lim_{n \to \infty} (\frac{2}{3})^n = 0$

### 7.2 Complexity Classes P and NP

**Definition 7.12 (TIME):** For function $t: \mathbb{N} \to \mathbb{R}^+$, define:
- $TIME(t(n)) = \{L \mid L$ is decided by $O(t(n))$-time deterministic TM$\}$

**Definition 7.18 (P):** $P = \bigcup_{k \geq 0} TIME(n^k)$
- Languages decidable by deterministic TM in polynomial time
- "Efficiently solvable" problems
- Examples: Sorting, graph connectivity, shortest path

**Definition 7.19 (NTIME):** For function $t: \mathbb{N} \to \mathbb{R}^+$, define:
- $NTIME(t(n)) = \{L \mid L$ is decided by $O(t(n))$-time nondeterministic TM$\}$

**NP (Nondeterministic Polynomial Time):**
- $NP = \bigcup_{k \geq 0} NTIME(n^k)$
- Languages decidable by nondeterministic TM in polynomial time
- Equivalently: Languages with polynomial-time verifiers
- "Efficiently verifiable" problems

**Polynomial-Time Verifier:**
- Language $L$ has verifier $V$ if:
  - $w \in L$ if and only if there exists certificate $c$ such that $V$ accepts $\langle w, c \rangle$
  - $V$ runs in polynomial time
- **Example:** SAT has verifier: given assignment (certificate), check if it satisfies formula in polynomial time

**Key Relationship:** $P \subseteq NP$
- Every problem in P is also in NP (deterministic TM is special case of nondeterministic TM)
- **Open question:** Is $P = NP$?
  - Most experts believe $P \neq NP$
  - If $P = NP$, many "hard" problems would become efficiently solvable
  - One of the most important open problems in computer science

**Examples of Problems in P:**
- Sorting: $O(n \log n)$
- Graph connectivity: $O(|V| + |E|)$
- Shortest path: $O(|V|^2)$ or $O(|E| + |V| \log |V|)$
- Matrix multiplication: $O(n^3)$

**Examples of Problems in NP:**
- **SAT (Boolean Satisfiability):** Given Boolean formula, is there assignment making it true?
  - Certificate: Assignment of truth values
  - Verifier: Check if assignment satisfies formula (polynomial time)
- **3SAT:** SAT where each clause has exactly 3 literals
- **CLIQUE:** Given graph and $k$, does graph contain clique of size $k$?
  - Certificate: Set of $k$ vertices
  - Verifier: Check if all pairs connected (polynomial time)
- **VERTEX-COVER:** Given graph and $k$, does graph have vertex cover of size $k$?
- **HAMILTONIAN-PATH:** Given graph, does it contain path visiting each vertex exactly once?

### 7.3 NP-Completeness

**NP-Complete:**
- Problems in NP
- Every problem in NP reduces to them (in polynomial time)
- If any NP-complete problem is in P, then $P = NP$

**NP-Hard:**
- Every problem in NP reduces to it (may not be in NP itself)

**Cook-Levin Theorem:** SAT is NP-complete
- First problem proven NP-complete
- Shows that SAT captures the difficulty of all problems in NP

**NP-Completeness Proof Strategy:**
1. Show problem is in NP (polynomial-time verifier exists)
2. Show some known NP-complete problem reduces to it (polynomial-time reduction)
3. Reduction must be polynomial-time computable

**Polynomial-Time Reductions:**
- $A \leq_p B$: $A$ reduces to $B$ in polynomial time
- If $B \in P$ and $A \leq_p B$, then $A \in P$
- If $A$ is NP-complete and $A \leq_p B$, then $B$ is NP-hard
- If additionally $B \in NP$, then $B$ is NP-complete

**Common NP-Complete Problems:**
- **SAT:** Boolean satisfiability
- **3SAT:** SAT with 3 literals per clause
- **CLIQUE:** Largest complete subgraph
- **VERTEX-COVER:** Smallest set covering all edges
- **HAMILTONIAN-PATH:** Path visiting all vertices
- **TSP (Traveling Salesman Problem):** Shortest tour visiting all cities

**Example Reduction:** 3SAT $\leq_p$ CLIQUE
- Given 3SAT formula $\phi$ with $k$ clauses, construct graph:
  - Create 3 vertices for each clause (one per literal)
  - Connect vertices from different clauses if literals are compatible (not negations of each other)
  - Graph has $k$-clique if and only if $\phi$ is satisfiable
- Reduction is polynomial-time

**P vs NP Question:**
- **If $P = NP$:** Many currently intractable problems become efficiently solvable
  - Cryptography would need new foundations
  - Optimization problems become easy
  - AI and machine learning could be revolutionized
- **If $P \neq NP$ (widely believed):** Confirms that some problems are inherently difficult
  - Current cryptographic systems remain secure
  - Some problems will always require exponential time (unless quantum computers help)

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

### Complexity
- **Cook-Levin Theorem:** SAT is NP-complete

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
3. **Rice's Theorem:** If nontrivial property of languages (not covered in exam)

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

### Asymptotic Notation

- **Big-O:** $f(n) = O(g(n))$ if $f(n) \leq c \cdot g(n)$ for large $n$ (upper bound)
- **Big-Omega:** $f(n) = \Omega(g(n))$ if $f(n) \geq c \cdot g(n)$ for large $n$ (lower bound)
- **Theta:** $f(n) = \Theta(g(n))$ if both $O$ and $\Omega$ (tight bound)
- **Little-o:** $f(n) = o(g(n))$ if $\lim_{n \to \infty} \frac{f(n)}{g(n)} = 0$ (strictly slower)
- **Little-omega:** $f(n) = \omega(g(n))$ if $\lim_{n \to \infty} \frac{f(n)}{g(n)} = \infty$ (strictly faster)

### Complexity Classes

- **P:** Polynomial time (deterministic) - efficiently solvable
- **NP:** Polynomial time (nondeterministic) - efficiently verifiable
- **NP-Complete:** Hardest problems in NP
- **NP-Hard:** At least as hard as NP-complete (may not be in NP)

### Key Undecidable Problems

- $A_{TM}$: Acceptance problem
- $HALT_{TM}$: Halting problem
- $E_{TM}$: Emptiness problem
- $EQ_{TM}$: Equivalence problem
- **Post Correspondence Problem:** Undecidable

### Common Conversions

- **DFA → NFA:** Identity (DFA is NFA)
- **NFA → DFA:** Subset construction (exponential)
- **DFA → Regular Expression:** GNFA method
- **Regular Expression → NFA:** Structural induction
- **CFG → PDA:** Standard construction
- **PDA → CFG:** State pair construction
- **DFA → Regular Grammar:** States → Nonterminals

### Important Definitions

- **Configuration of TM:** $uqv$ (tape content, state, head position)
- **Decidable:** TM always halts and correctly accepts/rejects
- **Recognizable:** TM accepts strings in language (may loop on others)
- **Mapping Reduction:** $A \leq_m B$ if computable $f$ such that $w \in A \iff f(w) \in B$
- **Polynomial-Time Reduction:** $A \leq_p B$ if reduction is polynomial-time computable

---

## Conclusion

This comprehensive review covers all material for the Theory of Computation final exam:

1. **Mathematical Preliminaries** - Sets, functions, graphs, strings, languages, proof techniques
2. **Regular Languages** - DFAs, NFAs, regular expressions, pumping lemma, closure properties
3. **Context-Free Languages** - CFGs, PDAs, CNF, ambiguity, pumping lemma
4. **Turing Machines** - Formal definition, variants, Church-Turing thesis
5. **Decidability** - Decidable and undecidable problems, recognizability
6. **Reducibility** - Mapping reductions, common reductions, Post Correspondence Problem
7. **Time Complexity** - Asymptotic notation, P and NP, NP-completeness

**Key Insights:**
- Each computational model adds power but introduces new limitations
- Some problems are fundamentally unsolvable (undecidable)
- Some problems are solvable but intractable (NP-complete)
- The P vs NP question remains one of the most important open problems

**Good luck on your final exam!**

