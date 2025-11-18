Let's go step-by-step.

---

## **Grammar $ G_2 $**
$ S \to 0X $
$ X \to 0X \mid 1X \mid 1 $

---

### **(i) Language recognized**

Start with $ S \Rightarrow 0X $.  
From $ X $, we can derive any string of 0's and 1's **ending with 1**, because the only way to terminate is via $ X \to 1 $, and before that we can have $ X \to 0X $ or $ X \to 1X $ any number of times.

So $ X $ generates $ \{0,1\}^*1 $.

Thus:
$ S \Rightarrow 0X \Rightarrow 0\,(\{0,1\}^*1) $
So:
$ L(G_2) = \{ 0w \mid w \in \{0,1\}^*,\ w \text{ ends with } 1 \} $.
Equivalently: all binary strings starting with 0 and ending with 1.

$ \boxed{0u1 \mid u \in \{0,1\}^*} $

---

### **(ii) Is $L(G_2)$ regular?**

**Yes**, $L(G_2)$ is regular.

**Proof using Regular Grammar Definition:**

Recall that a **regular grammar** is one that is either right-linear or left-linear:
- **Right-linear:** All productions have the form $A \to xB$ or $A \to x$, where $A, B \in V$ (nonterminals) and $x \in T^*$ (string of terminals)
- **Left-linear:** All productions have the form $A \to Bx$ or $A \to x$

Let's examine the productions of $G_2$:

$$
\begin{aligned}
S &\to 0X && \text{(form: } A \to xB \text{, where } x=0, B=X \text{)} \\
X &\to 0X && \text{(form: } A \to xB \text{, where } x=0, B=X \text{)} \\
X &\to 1X && \text{(form: } A \to xB \text{, where } x=1, B=X \text{)} \\
X &\to 1 && \text{(form: } A \to x \text{, where } x=1 \text{)}
\end{aligned}
$$

Every production is of the form $A \to xB$ or $A \to x$, so $G_2$ is a **right-linear grammar**.

Since $G_2$ is a regular grammar, it generates a regular language. Therefore, $L(G_2)$ is regular.

**Additional Evidence:**

We can also describe $L(G_2)$ with the regular expression $0(0 \cup 1)^*1$, which further confirms it is regular.

Furthermore, a DFA can be constructed for this language:
- Start state $q_0$: no input yet
- State $q_1$: have seen `0` but not yet a final `1`
- State $q_2$: have seen `0` and last char was `1` (accepting)
- Dead state: for strings starting with `1`

Transitions:
- From $q_0$: on `0` go to $q_1$, on `1` go to dead state
- From $q_1$: on `0` stay in $q_1$, on `1` go to $q_2$ (accept)
- From $q_2$: on `0` go to $q_1$, on `1` stay in $q_2$

$\boxed{\text{Yes, } L(G_2) \text{ is regular because } G_2 \text{ is a right-linear (regular) grammar}}$


---

### **(iii) CNF for $L(G_2)$**

**Goal:** Convert the grammar to Chomsky Normal Form (CNF), where every production is either:
- $A \to BC$ (two nonterminals), or
- $A \to a$ (single terminal)

**Step 1: Start with the original grammar**

$$
\begin{aligned}
S &\to 0X \\
X &\to 0X \mid 1X \mid 1
\end{aligned}
$$

**Step 2: Identify problematic productions**

Let's check each production against CNF rules:
- $S \to 0X$: **Problem!** This has a terminal (`0`) mixed with a nonterminal ($X$). CNF requires either two nonterminals or one terminal, not a mix.
- $X \to 0X$: **Problem!** Same issue - terminal mixed with nonterminal.
- $X \to 1X$: **Problem!** Same issue - terminal mixed with nonterminal.
- $X \to 1$: **Good!** This is already in CNF form ($A \to a$).

**Step 3: Introduce new nonterminals for terminals**

To fix the problematic productions, we introduce new nonterminals that generate each terminal:
- Let $T_0$ be a nonterminal that generates `0`: $T_0 \to 0$
- Let $T_1$ be a nonterminal that generates `1`: $T_1 \to 1$

**Step 4: Replace terminals in mixed productions**

Now replace the terminals in the problematic productions with their corresponding nonterminals:
- $S \to 0X$ becomes $S \to T_0 X$ (now has two nonterminals)
- $X \to 0X$ becomes $X \to T_0 X$ (now has two nonterminals)
- $X \to 1X$ becomes $X \to T_1 X$ (now has two nonterminals)
- $X \to 1$ stays as $X \to 1$ (already in CNF form)

**Step 5: Verify CNF requirements**

Let's verify each production:
- $S \to T_0 X$: Two nonterminals ✓
- $X \to T_0 X$: Two nonterminals ✓
- $X \to T_1 X$: Two nonterminals ✓
- $X \to 1$: Single terminal ✓
- $T_0 \to 0$: Single terminal ✓
- $T_1 \to 1$: Single terminal ✓

All productions are now in CNF!

**Final Answer:**
$$
\boxed{
\begin{aligned}
S &\to T_0 X \\
X &\to T_0 X \mid T_1 X \mid 1 \\
T_0 &\to 0 \\
T_1 &\to 1
\end{aligned}
}
$$

**Why this works:** The grammar still generates the same language $L(G_2) = \{0u1 \mid u \in \{0,1\}^*\}$ because:
- We start with $S \Rightarrow T_0 X \Rightarrow 0X$
- Then for each symbol in $u$, we use $X \Rightarrow T_i X \Rightarrow iX$ (where $i$ is either 0 or 1)
- Finally, we end with $X \Rightarrow 1$
- This produces the same strings as the original grammar, just with additional intermediate steps


---

### **(iv) Is this CFG ambiguous?**

**No**, the grammar is **unambiguous**.

**Proof using the Definition of Ambiguity:**

Recall that a grammar $G$ is **ambiguous** if it generates some string $w$ ambiguously, meaning that string has two or more different leftmost derivations.

Conversely, a grammar is **unambiguous** if every string in $L(G)$ has exactly one leftmost derivation.

For our grammar $G_2$, consider any string $w \in L(G_2)$. We know $w$ has the form $w = 0u1$ where $u \in \{0,1\}^*$.

The leftmost derivation of $w$ must proceed as follows:

1. **Start:** $S \Rightarrow 0X$ (this is the only production from $S$, so no choice here)
2. **Middle:** For each symbol $s_i$ in $u = s_1s_2\ldots s_k$:
   - If $s_i = 0$: we must apply $X \Rightarrow 0X$ (uniquely determined by the symbol we need)
   - If $s_i = 1$: we must apply $X \Rightarrow 1X$ (uniquely determined by the symbol we need)
3. **End:** $X \Rightarrow 1$ (this is the only way to terminate and produce the final 1)

Since each derivation step is uniquely determined by the target string, every string in $L(G_2)$ has **exactly one leftmost derivation**.

Therefore, by definition, the grammar $G_2$ is **unambiguous**.

$\boxed{\text{No, the grammar is unambiguous because every string has exactly one leftmost derivation.}}$
