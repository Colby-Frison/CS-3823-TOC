# Proof: Regular Languages are Closed Under Complement

## Statement
If L is a regular language over alphabet Σ, then L̅ (the complement of L) is also regular.

## Definition of Complement
For a language L ⊆ Σ*, the complement of L is:
**L̅ = Σ* - L** = {w ∈ Σ* | w ∉ L}

In other words, L̅ contains all strings over Σ that are NOT in L.

---

## Proof

### Step 1: Assume L is Regular
Since L is regular, there exists a DFA M = (Q, Σ, δ, q₀, F) that recognizes L.

### Step 2: Construct a DFA M' for L̅
We will construct a new DFA M' = (Q, Σ, δ, q₀, F') that recognizes L̅.

**Key insight:** To recognize the complement, we simply flip the accept states!

**Construction:**
- **States:** Same as M (Q)
- **Alphabet:** Same as M (Σ)  
- **Transition function:** Same as M (δ)
- **Start state:** Same as M (q₀)
- **Accept states:** F' = Q - F (the complement of F)

That is, a state is accepting in M' if and only if it is NOT accepting in M.

### Step 3: Prove M' Recognizes L̅

**Claim:** L(M') = L̅

**Proof of claim:**

**Part 1:** If w ∈ L̅, then w ∈ L(M')

- Since w ∈ L̅, we have w ∉ L = L(M)
- When M processes w, it ends in some state q ∈ Q
- Since w ∉ L(M), we have q ∉ F
- Therefore, q ∈ F' = Q - F
- When M' processes w, it follows the same transitions and ends in the same state q
- Since q ∈ F', we have w ∈ L(M') ✓

**Part 2:** If w ∈ L(M'), then w ∈ L̅

- Since w ∈ L(M'), when M' processes w, it ends in some state q ∈ F'
- By definition of F', we have q ∈ F' = Q - F, so q ∉ F
- Since M' has the same transitions as M, when M processes w, it also ends in state q
- Since q ∉ F, we have w ∉ L(M) = L
- Therefore, w ∈ L̅ ✓

### Step 4: Conclusion
Since we can construct a DFA M' that recognizes L̅, the language L̅ is regular.

---

## Key Insights

### Why This Works
1. **DFAs are "complete"**: Every state has a transition for every input symbol
2. **Every string leads to exactly one state**: No ambiguity about where the computation ends
3. **Complement = flip accept states**: Since every string ends somewhere, flipping the accept states gives us exactly the complement

### Important Notes
- **This proof only works for DFAs**, not NFAs
- **NFAs are not guaranteed to be complete**: An NFA might have missing transitions
- **If you have an NFA**, you must first convert it to a DFA using the subset construction, then flip the accept states

### Example
**Original DFA M for L = {strings ending in "01"}:**
```
    0,1
q₀ ──→ q₁ ──→ q₂
       ↑     ↓
       └─────┘
         0
```
- States: Q = {q₀, q₁, q₂}
- Accept states: F = {q₂}
- L(M) = {strings ending in "01"}

**Complement DFA M' for L̅:**
- Same structure, same transitions
- Accept states: F' = {q₀, q₁}
- L(M') = {strings NOT ending in "01"} = L̅

---

## Corollary: Regular Languages are Closed Under Union

**Bonus proof using complement and De Morgan's laws:**

We can also prove closure under union using complement and intersection:

**Theorem:** If L₁ and L₂ are regular, then L₁ ∪ L₂ is regular.

**Proof:**
1. L₁ is regular → L₁̅ is regular (by complement closure)
2. L₂ is regular → L₂̅ is regular (by complement closure)  
3. L₁̅ ∩ L₂̅ is regular (by intersection closure)
4. By De Morgan's law: (L₁̅ ∩ L₂̅)̅ = L₁ ∪ L₂
5. Since L₁̅ ∩ L₂̅ is regular, (L₁̅ ∩ L₂̅)̅ is regular (by complement closure)
6. Therefore, L₁ ∪ L₂ is regular ✓

This shows how closure properties can be used together to prove other closure properties!

---

## Summary

**Regular languages are closed under complement** because:
1. Any regular language L has a DFA M
2. We can construct a new DFA M' by flipping the accept states
3. M' recognizes exactly L̅
4. Therefore, L̅ is regular

This is one of the most elegant and intuitive closure properties!
