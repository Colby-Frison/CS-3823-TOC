
# Q1

## (i) $L_1 = \text{\{w | w contains two consecutive 1s or w contains no 0s\}}$

Finite Automaton M = (Q, Σ, δ, q₀, F)

**Components:**
- $Q = \{q_0, q_1, q_2, q_3, q_4\}$ (set of states)
- $Σ = {0, 1}$ (alphabet)
- $q_0$ (initial state)
- $F = \{q_0, q_3, q_4\}$ (final states)

| Current State | Input | Next State |
| ------------- | ----- | ---------- |
| q₀            | 0     | q₁         |
| q₀            | 1     | q₄         |
| q₁            | 0     | q₁         |
| q₁            | 1     | q₂         |
| q₂            | 0     | q₁         |
| q₂            | 1     | q₃         |
| q₃            | 0     | q₃         |
| q₃            | 1     | q₃         |
| q₄            | 0     | q₁         |
| q₄            | 1     | q₃         |

![[Pasted image 20250925185039.png]]
## (ii) $L_1 = \{w | w = w_1w_2 ... w_n \text{ such that } w_{n-3} = 0 \text{ and } w_{n-2} = 1\}$

Finite Automaton M = (Q, Σ, δ, q₀, F)

Components:
- $Q = \{q_0, q_1, q_2, q_3, q_4, q_5, q_6, q_7\}$ (set of states)
- $Σ = \{0, 1\}$ (alphabet)
- $q_0$ (initial state)
- $F = \{q_6, q_7\}$ (accepting states)

### State tables
| Current State | Input 0 | Input 1 |
| ------------- | ------- | ------- |
| q₀            | q₁      | q₂      |
| q₁            | q₁      | q₃      |
| q₂            | q₁      | q₂      |
| q₃            | q₄      | q₅      |
| q₄            | q₇      | q₆      |
| q₅            | q₇      | q₇      |
| q₆            | q₅      | q₅      |
| q₇            | q₁      | q₁      |

| Current State | Input | Next States |
| ------------- | ----- | ----------- |
| q₀            | 0     | q₁          |
| q₀            | 1     | q₂          |
| q₁            | 0     | q₁          |
| q₁            | 1     | q₃          |
| q₂            | 0     | q₁          |
| q₂            | 1     | q₂          |
| q₃            | 0     | q₄          |
| q₃            | 1     | q₅          |
| q₄            | 0     | q₇          |
| q₄            | 1     | q₆          |
| q₅            | 0     | q₇          |
| q₅            | 1     | q₇          |
| q₆            | 0     | q₅          |
| q₆            | 1     | q₅          |
| q₇            | 0     | q₁          |
| q₇            | 1     | q₁          |
### Diagram
![[Pasted image 20250928215313.png]]
### save state for the automaton sim
{"type":"DFA","dfa":{"transitions":{"start":{"0":"s0","1":"s1"},"s0":{"0":"s0","1":"s2"},"s1":{"0":"s0","1":"s1"},"s2":{"0":"s3","1":"s4"},"s3":{"0":"s6","1":"s5"},"s4":{"0":"s6","1":"s6"},"s5":{"0":"s4","1":"s4"},"s6":{"0":"s0","1":"s0"}},"startState":"start","acceptStates":["s5","s6"]},"states":{"start":{},"s0":{"top":232.60000915527343,"left":174.59999389648436,"displayId":"q1"},"s1":{"top":366.3999969482422,"left":173.40001220703124,"displayId":"q2"},"s2":{"top":146.60000915527343,"left":411.6000244140625,"displayId":"q3"},"s3":{"top":294.0000030517578,"left":478.99998779296874,"displayId":"q4"},"s4":{"top":462.3999969482422,"left":379.40001220703124,"displayId":"q5"},"s6":{"isAccept":true,"top":318.79999084472655,"left":648.7999755859375,"displayId":"q7"},"s5":{"isAccept":true,"top":203.8000061035156,"left":643.7999755859375,"displayId":"q6"}},"transitions":[{"stateA":"start","label":"0","stateB":"s0"},{"stateA":"start","label":"1","stateB":"s1"},{"stateA":"s0","label":"0","stateB":"s0"},{"stateA":"s0","label":"1","stateB":"s2"},{"stateA":"s1","label":"0","stateB":"s0"},{"stateA":"s1","label":"1","stateB":"s1"},{"stateA":"s2","label":"0","stateB":"s3"},{"stateA":"s2","label":"1","stateB":"s4"},{"stateA":"s3","label":"0","stateB":"s6"},{"stateA":"s3","label":"1","stateB":"s5"},{"stateA":"s4","label":"0","stateB":"s6"},{"stateA":"s4","label":"1","stateB":"s6"},{"stateA":"s5","label":"0","stateB":"s4"},{"stateA":"s5","label":"1","stateB":"s4"},{"stateA":"s6","label":"0","stateB":"s0"},{"stateA":"s6","label":"1","stateB":"s0"}],"bulkTests":{"accept":"0111\n0100\n0101\n0110\n1110000111\n0001110100\n0101010101\n10101010110","reject":"1\n0\n11\n00\n01\n10\n111\n000\n101\n010\n110\n001\n1100\n0011\n1010"}}


# Q2

# Q3: Representation [10 points]

**Context:** Let $\Sigma = \{0, 1\}$. Let $\Sigma^n = \underbrace{\Sigma\Sigma\cdots\Sigma}_{n \text{ times}}$. Consider the regular language $L_k = \Sigma^*1\Sigma^{k-1}$ for some positive integer $k$.

This language consists of all strings where the $k$-th character from the end is a $1$.

## (i) [1 point] Argue that if a language can be recognized by a DFA with $k$ states, then it can be recognized by an NFA with $k$ states.

**Answer:**

Every DFA is, by definition, also an NFA. This is because an NFA (Nondeterministic Finite Automaton) is a generalization of a DFA (Deterministic Finite Automaton).

A DFA is simply a special case of an NFA where:
1. For each state and each input symbol, there is exactly one transition (no nondeterminism)
2. There are no $\varepsilon$-transitions (empty string transitions)

Therefore, any DFA with $k$ states can be viewed directly as an NFA with $k$ states that happens to be deterministic. The transition function, start state, and accepting states remain the same. No conversion is needed - the DFA already satisfies all the requirements of being an NFA.

## (ii) [2 points] Show that $L_k$ can be recognized by an NFA with $k + 1$ states.

**Answer:**

We can construct an NFA with $k + 1$ states as follows:

**States:** $Q = \{q_0, q_1, q_2, \ldots, q_k\}$

**Construction:**
- $q_0$ is the start state
- $q_k$ is the only accepting state
- From $q_0$: 
  - On input $0$ or $1$: stay in $q_0$ (loop)
  - On input $1$: *nondeterministically* transition to $q_1$ (this is the "guess" that we've seen the $1$ that is $k$ positions from the end)
- From $q_i$ (for $i = 1, 2, \ldots, k-1$):
  - On input $0$ or $1$: transition to $q_{i+1}$
- $q_k$ is the accepting state (reached after reading exactly $k-1$ more symbols after the crucial $1$)

**How it works:**
The NFA uses nondeterminism to "guess" when it sees the $1$ that is exactly $k$ positions from the end. It stays in $q_0$ reading arbitrary input until it nondeterministically decides to move to $q_1$ upon seeing a $1$. Then it must read exactly $k-1$ more characters (states $q_1 \to q_2 \to \cdots \to q_k$). If the string ends exactly when reaching $q_k$, it accepts.

**State count:** This NFA has exactly $k + 1$ states $(q_0, q_1, \ldots, q_k)$.

## (iii) [4 points] Prove that any DFA recognizing $L_k$ must have at least $2^k$ states.

**Answer:**

**Proof by contradiction:**

Assume, for the sake of contradiction, that there exists a DFA $M$ that recognizes $L_k$ and has fewer than $2^k$ states.

Consider all possible strings of length $k$ over $\Sigma = \{0, 1\}$. There are exactly $2^k$ such strings. Let's call this set $S = \Sigma^k = \{x_1, x_2, \ldots, x_{2^k}\}$.

Since $M$ has fewer than $2^k$ states, and we are reading $2^k$ different strings, by the **Pigeonhole Principle**, at least two distinct strings from $S$ must lead to the same state in $M$.

Let's call these two strings $x$ and $y$ where $x \neq y$, and both are in $\Sigma^k$. Write:
- $x = x_1x_2\cdots x_k$
- $y = y_1y_2\cdots y_k$

Since $x \neq y$, there must exist some position $i$ where $1 \leq i \leq k$ and $x_i \neq y_i$.

Without loss of generality, assume $x_i = 1$ and $y_i = 0$.

Now consider the string $z$ consisting of any $(k-i)$ symbols from $\Sigma$. In other words, $z \in \Sigma^{k-i}$.

Observe:
- In $xz = x_1x_2\cdots x_kz$, the $k$-th character from the end is $x_i = 1$, so $xz \in L_k$
- In $yz = y_1y_2\cdots y_kz$, the $k$-th character from the end is $y_i = 0$, so $yz \notin L_k$

Since $x$ and $y$ lead to the same state in $M$, and $M$ is deterministic, reading the same suffix $z$ from that state must lead to the same final state. Therefore:
- Either both $xz$ and $yz$ are accepted by $M$
- Or both $xz$ and $yz$ are rejected by $M$

But we just showed that $xz \in L_k$ (should be accepted) and $yz \notin L_k$ (should be rejected).

This is a **contradiction!** The DFA $M$ cannot correctly recognize $L_k$ if it accepts both or rejects both.

Therefore, our assumption must be false, and any DFA recognizing $L_k$ must have **at least $2^k$ states**. $\square$

## (iv) [2 points] What does part (iii) of this question tell you about Theorem 1.39 from the book?

**Answer:**

Theorem 1.39 (the NFA to DFA conversion theorem) states that for every NFA, there exists an equivalent DFA. The standard subset construction algorithm can convert an NFA with $n$ states to a DFA with at most $2^n$ states.

Part (iii) demonstrates that this exponential blow-up is not just a theoretical upper bound, but can actually occur in practice:

- The NFA for $L_k$ has $k + 1$ states (from part ii)
- The minimum DFA for $L_k$ has $2^k$ states (from part iii)

This shows that:
1. The conversion from NFA to DFA can indeed require exponentially many states
2. The $2^n$ upper bound in the subset construction is tight - there exist languages where the exponential blow-up actually happens
3. While every NFA can be converted to a DFA (proving NFA and DFA have the same expressive power), the size cost can be exponential

## (v) [1 point] What do parts (i), (ii), and (iii) of this question tell you about DFAs as compared to NFAs?

**Answer:**

Combining parts (i), (ii), and (iii):

**Expressive power:** DFAs and NFAs are equivalent in terms of the languages they can recognize (both recognize exactly the regular languages).

**Succinctness:** NFAs can be *exponentially more succinct* than DFAs. For the language $L_k$:
- NFA requires only $k + 1$ states
- DFA requires $2^k$ states

This is an exponential gap $(2^k$ vs. $k+1)$.

**Key insight:** While NFAs and DFAs recognize the same class of languages, NFAs can represent some languages much more efficiently. Nondeterminism allows for more compact representations at the cost of more complex acceptance semantics (multiple possible computation paths). This makes NFAs particularly useful for:
- Theoretical analysis
- Regular expression matching
- Initial design before converting to DFA for implementation

The tradeoff is: NFAs are smaller but require tracking multiple states simultaneously (or backtracking), while DFAs are potentially much larger but have simpler, deterministic execution.

# Q4: Regular Expressions [4 points; 2 points each]

Let $\Sigma = \{0, 1\}$. Give regular expressions for the following languages.

Note that $\varepsilon \in L_1$, whereas $\varepsilon \notin L_2$.

## (i) $L_1 = \{w \mid \text{every even position of } w = w_1w_2\ldots w_n \text{ has a 0}\}$

**Answer:**

**Understanding the problem:**
- Positions are numbered starting from 1: $w_1, w_2, w_3, w_4, \ldots$
- Even positions are: 2, 4, 6, 8, ...
- Each even position MUST be 0
- Odd positions (1, 3, 5, 7, ...) can be either 0 or 1

**Pattern analysis:**
- Position 1 (odd): can be 0 or 1 → $(0 \cup 1)$
- Position 2 (even): must be 0 → $0$
- Position 3 (odd): can be 0 or 1 → $(0 \cup 1)$
- Position 4 (even): must be 0 → $0$
- Pattern repeats: $(0 \cup 1)0$

The pattern $(0 \cup 1)0$ repeats zero or more times, and we may have **one final odd-positioned character (or none for the empty string).**

**Regular expression:** 

$$((0 \cup 1)0)^*(\varepsilon \cup 0 \cup 1)$$

**Verification:**
- $\varepsilon$: accepted (no even positions to check) $\checkmark$
- $0$: accepted (only position 1, which is odd) $\checkmark$
- $1$: accepted (only position 1, which is odd) $\checkmark$
- $00$: accepted (position 2 is 0) $\checkmark$
- $10$: accepted (position 2 is 0) $\checkmark$
- $01$: rejected (position 2 is 1) $\times$
- $11$: rejected (position 2 is 1) $\times$
- $000$: accepted (position 2 is 0) $\checkmark$
- $100$: accepted (position 2 is 0) $\checkmark$
- $1001$: accepted (positions 2 and 4 are both 0) $\checkmark$
- $1011$: rejected (position 4 is 1) $\times$

## (ii) $L_2 = \{w \mid w \text{ interpreted as a binary number is divisible by 2 (or 10 in binary)}\}$

**Answer:**

**Understanding the problem:**
- We interpret strings as binary numbers
- A number is divisible by 2 if it's even
- In binary, a number is even if and only if it ends in 0 (just like in decimal, a number is divisible by 10 iff it ends in 0)
- $\varepsilon$ should NOT be accepted (per the problem statement)

**Examples:**
- $10_2 = 2_{10}$: divisible by 2 ✓
- $100_2 = 4_{10}$: divisible by 2 ✓
- $110_2 = 6_{10}$: divisible by 2 ✓
- $1000_2 = 8_{10}$: divisible by 2 ✓
- $1_2 = 1_{10}$: not divisible by 2 ✗
- $11_2 = 3_{10}$: not divisible by 2 ✗
- $101_2 = 5_{10}$: not divisible by 2 ✗

**Key insight:** A binary number is divisible by 2 if and only if its last bit is 0.

**Regular expression:**

$$(0 \cup 1)^*0$$

**Verification:**
- $0$: $0_{10}$ divisible by 2 ✓
- $10$: $2_{10}$ divisible by 2 ✓
- $100$: $4_{10}$ divisible by 2 ✓
- $110$: $6_{10}$ divisible by 2 ✓
- $1000$: $8_{10}$ divisible by 2 ✓
- $1010$: $10_{10}$ divisible by 2 ✓
- $1$: $1_{10}$ not divisible by 2 ✗
- $11$: $3_{10}$ not divisible by 2 ✗
- $101$: $5_{10}$ not divisible by 2 ✗
- $\varepsilon$: not accepted ✓

# Q5: DFAs to Regular Expressions [6 points]

Convert the DFA to a regular expression by starting from the equivalent GNFA, then remove state $q_1$, then state $q_2$, and finally state $q_0$.

## DFA Structure

**States:** $q_0$ (start, accepting), $q_1$ (not accepting), $q_2$ (accepting)

**Transitions:**
- $\delta(q_0, 0) = q_1$
- $\delta(q_0, 1) = q_0$ (self-loop)
- $\delta(q_1, 0) = q_1$ (self-loop)
- $\delta(q_1, 1) = q_2$
- $\delta(q_2, 0) = q_0$
- $\delta(q_2, 1) = q_1$

**Accepting states:** $\{q_0, q_2\}$

## Solution: GNFA Conversion

### Step 0: Convert DFA to GNFA

Add new start state $q_{start}$ and new accept state $q_{accept}$:
- $q_{start} \xrightarrow{\varepsilon} q_0$
- $q_0 \xrightarrow{\varepsilon} q_{accept}$ (since $q_0$ is accepting)
- $q_2 \xrightarrow{\varepsilon} q_{accept}$ (since $q_2$ is accepting)

All other transitions remain with their labels.

### Step 1: Remove $q_1$

**Formula:** When removing a state $q$, for each pair of states $p$ and $r$ (where $p \neq q$ and $r \neq q$), replace the path $p \to q \to r$ with a direct edge:

$$R_{new}(p,r) = R(p,r) \cup R(p,q) \cdot R(q,q)^* \cdot R(q,r)$$

**Paths through $q_1$:**

1. **$q_0$ to $q_2$ through $q_1$:**
   - $q_0 \xrightarrow{0} q_1 \xrightarrow{0^*} q_1 \xrightarrow{1} q_2$
   - New edge: $q_0 \xrightarrow{00^*1} q_2$

2. **$q_2$ to $q_2$ through $q_1$:**
   - $q_2 \xrightarrow{1} q_1 \xrightarrow{0^*} q_1 \xrightarrow{1} q_2$
   - New edge: $q_2 \xrightarrow{10^*1} q_2$ (self-loop)

**After removing $q_1$:**
- $q_{start} \xrightarrow{\varepsilon} q_0$
- $q_0 \xrightarrow{1} q_0$ (self-loop)
- $q_0 \xrightarrow{00^*1} q_2$
- $q_0 \xrightarrow{\varepsilon} q_{accept}$
- $q_2 \xrightarrow{0} q_0$
- $q_2 \xrightarrow{10^*1} q_2$ (self-loop)
- $q_2 \xrightarrow{\varepsilon} q_{accept}$

### Step 2: Remove $q_2$

**Paths through $q_2$:**

1. **$q_0$ to $q_0$ through $q_2$:**
   - $q_0 \xrightarrow{00^*1} q_2 \xrightarrow{(10^*1)^*} q_2 \xrightarrow{0} q_0$
   - New edge: $q_0 \xrightarrow{00^*1(10^*1)^*0} q_0$

2. **$q_0$ to $q_{accept}$ through $q_2$:**
   - $q_0 \xrightarrow{00^*1} q_2 \xrightarrow{(10^*1)^*} q_2 \xrightarrow{\varepsilon} q_{accept}$
   - New edge: $q_0 \xrightarrow{00^*1(10^*1)^*} q_{accept}$

**After removing $q_2$:**
- $q_{start} \xrightarrow{\varepsilon} q_0$
- $q_0 \xrightarrow{1 \cup 00^*1(10^*1)^*0} q_0$ (combined self-loops)
- $q_0 \xrightarrow{\varepsilon \cup 00^*1(10^*1)^*} q_{accept}$

### Step 3: Remove $q_0$

**Path from $q_{start}$ to $q_{accept}$ through $q_0$:**

Apply the formula:
$$R(q_{start}, q_{accept}) = R(q_{start}, q_0) \cdot R(q_0, q_0)^* \cdot R(q_0, q_{accept})$$

Substituting:
$$= \varepsilon \cdot (1 \cup 00^*1(10^*1)^*0)^* \cdot (\varepsilon \cup 00^*1(10^*1)^*)$$

Since $\varepsilon$ is the identity for concatenation ($\varepsilon \cdot R = R$):
$$= (1 \cup 00^*1(10^*1)^*0)^* \cdot (\varepsilon \cup 00^*1(10^*1)^*)$$

**Final Regular Expression:**

$$(1 \cup 00^*1(10^*1)^*0)^*(\varepsilon \cup 00^*1(10^*1)^*)$$

# Q6: Non Regular Languages [8 points]

Use the Pumping Lemma to prove that the following languages are not regular.

## The Pumping Lemma - Quick Explanation

**What it says:** If a language $L$ is regular, then there exists a "pumping length" $p$ such that any string $s \in L$ with $|s| \geq p$ can be split into three parts $s = xyz$ where:

1. $|y| > 0$ (the middle part is non-empty)
2. $|xy| \leq p$ (the first two parts together are at most length $p$)
3. For all $i \geq 0$, the string $xy^iz \in L$ (we can "pump" $y$ any number of times and stay in the language)

**How we use it:** We prove a language is NOT regular by contradiction:
1. Assume the language IS regular
2. The Pumping Lemma says there must be some pumping length $p$
3. We choose a specific string $s \in L$ with $|s| \geq p$
4. We show that NO MATTER HOW you split $s = xyz$ (following the rules), you can find some $i$ where $xy^iz \notin L$
5. This contradicts the Pumping Lemma, so the language must NOT be regular

## (i) $L_1 = \{www \mid w \in \Sigma^*\}$ where $\Sigma = \{0, 1\}$

This language consists of strings that are three identical copies concatenated together (like "000000" = "00" + "00" + "00").

**Proof by contradiction:**

Assume $L_1$ is regular. Then by the Pumping Lemma, there exists a pumping length $p$.

**Choose a string:** Let $w \in \Sigma^*$ be any string with $|w| = p$. Consider $s = www$.

Then $s \in L_1$ and $|s| = 3p \geq p$.

By the Pumping Lemma, we can write $s = xyz$ where:
- $|y| > 0$
- $|xy| \leq p$
- For all $i \geq 0$, $xy^iz \in L_1$

**Analysis of the split:**

Since $s = www$ with $|w| = p$, we can view the string as three consecutive copies of $w$:
$$s = \underbrace{w}_{\text{1st copy}} \underbrace{w}_{\text{2nd copy}} \underbrace{w}_{\text{3rd copy}}$$

The constraint $|xy| \leq p$ means that $xy$ is entirely contained within the first copy of $w$ (since the first $w$ has length $p$).

Since $xy$ lies within the first $w$:
- $x$ corresponds to some prefix of $w$ (possibly empty)
- $y$ corresponds to the next part of $w$ (non-empty, since $|y| > 0$)
- $z$ consists of the remainder of the first $w$ (if $|xy| < p$) plus the entire second and third copies of $w$, OR just the second and third copies of $w$ (if $|xy| = p$)

**Pumping to get a contradiction:**

Consider $i = 2$ (pump once). Then:
$$xy^2z = xyyz$$

Since $xy$ lies entirely within the first copy of $w$, pumping $y$ adds extra characters only to the first copy. The second and third copies of $w$ remain completely unchanged.

For $xy^2z$ to be in $L_1$, it must equal $w'w'w'$ for some string $w' \in \Sigma^*$ (three identical copies).

However:
- The first part of $xy^2z$ has been lengthened by $|y|$ characters (since we added an extra copy of $y$)
- The second and third parts remain as the original $w$

Since $|y| > 0$, the first part is now different from the second and third parts. Therefore, $xy^2z$ cannot be written as three identical copies.

Therefore, $xy^2z \notin L_1$.

This is a **contradiction!** Therefore, $L_1$ is not regular. $\square$

## (ii) $L_2 = \{1^{2^n} \mid n \geq 1\}$ where $\Sigma = \{1\}$

This language consists of strings of 1s where the length is a power of 2 (at least 2).

**Proof by contradiction:**

Assume $L_2$ is regular. Then by the Pumping Lemma, there exists a pumping length $p$.

**Choose a string:** Let $s = 1^{2^p}$.

Then $s \in L_2$ and $|s| = 2^p \geq p$.

By the Pumping Lemma, we can write $s = xyz$ where:
- $|y| > 0$
- $|xy| \leq p$
- For all $i \geq 0$, $xy^iz \in L_2$

**Analysis of the constraints:**

From the Pumping Lemma conditions:
- Since $|xy| \leq p$, we have $|y| \leq p$
- Since $|y| > 0$, we know $y$ is non-empty

**Pumping to get a contradiction:**

Consider $i = 2$ (pump once). Compare the original string $xyz$ with the pumped string $xy^2z$.

The original string has length: $|xyz| = 2^p$

The pumped string has length: $|xy^2z| = |xyz| + |y| = 2^p + |y|$

Since $0 < |y| \leq p$, we can establish bounds on the pumped length:
- **Lower bound:** $|xy^2z| = 2^p + |y| > 2^p$ (since $|y| > 0$)
- **Upper bound:** $|xy^2z| = 2^p + |y| \leq 2^p + p$

Now, for $p \geq 1$, we have $p < 2^p$ (exponential growth), which means:
$$2^p + p < 2^p + 2^p = 2 \cdot 2^p = 2^{p+1}$$

Combining these inequalities:
$$2^p < |xy^2z| \leq 2^p + p < 2^{p+1}$$

**The contradiction:**

For $xy^2z$ to be in $L_2$, its length must be a power of 2. However, we've shown that:
$$2^p < |xy^2z| < 2^{p+1}$$

This means the length of $xy^2z$ is strictly between two consecutive powers of 2. Since there are no powers of 2 between $2^p$ and $2^{p+1}$, we have $xy^2z \notin L_2$.

This contradicts the Pumping Lemma, which states that $xy^2z$ must be in $L_2$.

Therefore, our assumption is false, and $L_2$ is not regular. $\square$