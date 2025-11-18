Let's break this down.

We want a **regular grammar** for  
\[
L = \{ w \in \{0,1\}^* \mid w \text{ has at most two 0's} \}.
\]

---

## Step 1: Understanding the language
- Allowed strings: any string over {0,1} containing 0 zeros, 1 zero, or 2 zeros.
- Examples in $L$: `""`, `"1"`, `"0"`, `"101"`, `"1001"`, `"111"`, `"01010"` (has 2 zeros), etc.
- Not in $L$: `"000"`, `"10001"` (3 zeros), etc.

---

## Step 2: DFA idea (to derive grammar)
We can think in terms of states counting the number of 0's seen so far:

- State $S$: seen 0 zeros  
- State $A$: seen 1 zero  
- State $B$: seen 2 zeros  
- State $C$: seen 3 zeros (trap/reject state)

Transitions:  
- On `1`, stay in current state.  
- On `0`, go to next state (S→A, A→B, B→C).  
Accept states: S, A, B.

---

## Step 3: Convert to right-linear grammar
Right-linear grammar form:  
$ V \to tU $ or $ V \to t $ or $ V \to \varepsilon $, where $V,U$ are variables, $t$ is terminal.

Let’s assign:
- $S$ → start symbol (0 zeros so far)  
- $A$ → after 1 zero  
- $B$ → after 2 zeros  
- No variable for C (trap state) because we don't generate strings with ≥3 zeros.

---

**Rules**:

From $S$ (0 zeros):  
- Can generate `1` and stay in $S$: $ S \to 1S $  
- Can generate `0` and go to $A$: $ S \to 0A $  
- Can end with no zeros: $ S \to \varepsilon $

From $A$ (1 zero):  
- Can generate `1` and stay in $A$: $ A \to 1A $  
- Can generate `0` and go to $B$: $ A \to 0B $  
- Can end: $ A \to \varepsilon $

From $B$ (2 zeros):  
- Can generate `1` and stay in $B$: $ B \to 1B $  
- Cannot generate `0` (would go to trap, so no rule)  
- Can end: $ B \to \varepsilon $

---

## Step 4: Write the grammar


$S \to 1S \mid 0A \mid \varepsilon \\$
$A \to 1A \mid 0B \mid \varepsilon \\$
$B \to 1B \mid \varepsilon$



---

## Step 5: Verify with examples
- `"01010"`:  
  $S \to 0A \to 01A \to 010B \to 0101B \to 01010B \to 01010$ ✅ (2 zeros)  
- `"000"`:  
  $S \to 0A \to 00B$ — now to get third zero, no rule from B for `0`, so cannot generate. ✅

---

**Final regular grammar**:


$S \to 1S \mid 0A \mid \varepsilon \\$
$A \to 1A \mid 0B \mid \varepsilon \newline$
$B \to 1B \mid \varepsilon$
