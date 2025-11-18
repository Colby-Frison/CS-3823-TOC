# Additional Pumping Lemma Examples

## Example 1: L = {0^n 1^n | n ≥ 0}

**Language:** Equal number of 0's followed by equal number of 1's
- Examples: ε, "01", "0011", "000111"
- NOT in language: "001", "011", "00111"

**Proof that L is not regular:**

**1. Assume** L is regular

**2. Pumping Lemma** gives us some pumping length p

**3. Choose string:** s = 0^p 1^p
- Clearly s ∈ L (p 0's followed by p 1's)
- |s| = 2p ≥ p ✓

**4. Consider any split** s = xyz with |y| > 0 and |xy| ≤ p

**Analysis:**
- Since |xy| ≤ p and s starts with p 0's, both x and y consist only of 0's
- So: x = 0^a, y = 0^b, z = 0^c 1^p where a + b + c = p and b > 0

**5. Pump with i = 2:**
xy^2 z = 0^a 0^{2b} 0^c 1^p = 0^{a+2b+c} 1^p = 0^{p+b} 1^p

**6. Contradiction:**
- Original: p 0's, p 1's
- Pumped: (p+b) 0's, p 1's
- Since b > 0, we have more 0's than 1's
- Therefore xy^2 z ∉ L ✗

**Conclusion:** L is not regular. ∎

---

## Example 2: L = {ww | w ∈ Σ*} where Σ = {0, 1}

**Language:** Strings that are the concatenation of a string with itself
- Examples: ε, "00", "11", "0101", "101101"
- NOT in language: "01", "001", "1010"

**Proof that L is not regular:**

**1. Assume** L is regular

**2. Pumping Lemma** gives us some pumping length p

**3. Choose string:** s = 0^p 1 0^p 1
- Clearly s ∈ L (it's "0^p 1" concatenated with itself)
- |s| = 2p + 2 ≥ p ✓

**4. Consider any split** s = xyz with |y| > 0 and |xy| ≤ p

**Analysis:**
- Since |xy| ≤ p and s starts with 0^p, both x and y consist only of 0's
- So: x = 0^a, y = 0^b, z = 0^c 1 0^p 1 where a + b + c = p and b > 0

**5. Pump with i = 0:**
xy^0 z = xz = 0^a 0^c 1 0^p 1 = 0^{a+c} 1 0^p 1 = 0^{p-b} 1 0^p 1

**6. Contradiction:**
- For this to be in L, it must be ww for some w
- First half: 0^{p-b} 1 (length = p-b+1)
- Second half: 0^p 1 (length = p+1)
- Since b > 0, the two halves have different lengths
- Therefore xy^0 z ∉ L ✗

**Conclusion:** L is not regular. ∎

---

## Example 3: L = {0^n 1^m | n > m ≥ 0}

**Language:** More 0's than 1's
- Examples: "0", "00", "001", "0001", "00011"
- NOT in language: ε, "1", "01", "011"

**Proof that L is not regular:**

**1. Assume** L is regular

**2. Pumping Lemma** gives us some pumping length p

**3. Choose string:** s = 0^{p+1} 1^p
- Clearly s ∈ L (p+1 0's, p 1's, so more 0's than 1's)
- |s| = 2p+1 ≥ p ✓

**4. Consider any split** s = xyz with |y| > 0 and |xy| ≤ p

**Analysis:**
- Since |xy| ≤ p and s starts with 0^{p+1}, both x and y consist only of 0's
- So: x = 0^a, y = 0^b, z = 0^c 1^p where a + b + c = p+1 and b > 0

**5. Pump with i = 0:**
xy^0 z = xz = 0^a 0^c 1^p = 0^{a+c} 1^p = 0^{p+1-b} 1^p

**6. Contradiction:**
- Original: (p+1) 0's, p 1's → more 0's ✓
- Pumped: (p+1-b) 0's, p 1's
- Since b > 0, we have (p+1-b) ≤ p 0's
- So we have p or fewer 0's, but p 1's
- This means we don't have more 0's than 1's
- Therefore xy^0 z ∉ L ✗

**Conclusion:** L is not regular. ∎

---

## Example 4: L = {0^i 1^j | i ≠ j}

**Language:** Different number of 0's and 1's
- Examples: "01", "001", "011", "0001", "0011"
- NOT in language: ε, "0", "1", "0011", "000111"

**Proof that L is not regular:**

**1. Assume** L is regular

**2. Pumping Lemma** gives us some pumping length p

**3. Choose string:** s = 0^p 1^{p+1}
- Clearly s ∈ L (p 0's, p+1 1's, so different counts)
- |s| = 2p+1 ≥ p ✓

**4. Consider any split** s = xyz with |y| > 0 and |xy| ≤ p

**Analysis:**
- Since |xy| ≤ p and s starts with 0^p, both x and y consist only of 0's
- So: x = 0^a, y = 0^b, z = 0^c 1^{p+1} where a + b + c = p and b > 0

**5. Pump with i = 2:**
xy^2 z = 0^a 0^{2b} 0^c 1^{p+1} = 0^{a+2b+c} 1^{p+1} = 0^{p+b} 1^{p+1}

**6. Contradiction:**
- Original: p 0's, (p+1) 1's → different counts ✓
- Pumped: (p+b) 0's, (p+1) 1's
- Since b > 0, we have (p+b) > p 0's
- But we still have (p+1) 1's
- If b = 1, then we have (p+1) 0's and (p+1) 1's → equal counts!
- Therefore xy^2 z ∉ L ✗

**Conclusion:** L is not regular. ∎

---

## Example 5: L = {0^n 1^{2n} | n ≥ 0}

**Language:** n 0's followed by 2n 1's
- Examples: ε, "011", "001111", "000111111"
- NOT in language: "01", "0011", "0011111"

**Proof that L is not regular:**

**1. Assume** L is regular

**2. Pumping Lemma** gives us some pumping length p

**3. Choose string:** s = 0^p 1^{2p}
- Clearly s ∈ L (p 0's, 2p 1's)
- |s| = 3p ≥ p ✓

**4. Consider any split** s = xyz with |y| > 0 and |xy| ≤ p

**Analysis:**
- Since |xy| ≤ p and s starts with 0^p, both x and y consist only of 0's
- So: x = 0^a, y = 0^b, z = 0^c 1^{2p} where a + b + c = p and b > 0

**5. Pump with i = 2:**
xy^2 z = 0^a 0^{2b} 0^c 1^{2p} = 0^{a+2b+c} 1^{2p} = 0^{p+b} 1^{2p}

**6. Contradiction:**
- Original: p 0's, 2p 1's → ratio is 1:2 ✓
- Pumped: (p+b) 0's, 2p 1's
- For this to be in L, we need 2(p+b) 1's, but we only have 2p 1's
- Since b > 0, we need 2p + 2b 1's but only have 2p 1's
- Therefore xy^2 z ∉ L ✗

**Conclusion:** L is not regular. ∎

---

## Common Patterns in Pumping Lemma Proofs

### 1. **Imbalance Counting**
- Languages that require specific counts or ratios
- Examples: {0^n 1^n}, {0^n 1^{2n}}, {0^i 1^j | i ≠ j}
- Strategy: Pump to break the required count/ratio

### 2. **Pattern Matching**
- Languages that require specific patterns
- Examples: {ww}, {www}, {w^R w} (palindromes)
- Strategy: Pump to break the required pattern

### 3. **Gap in Sequence**
- Languages where valid lengths have gaps
- Examples: {1^{2^n}}, {1^{n^2}}
- Strategy: Show pumped length falls in a gap

### 4. **Structural Requirements**
- Languages with complex structural constraints
- Examples: {0^n 1^m | n > m}, {balanced parentheses}
- Strategy: Pump to violate structural requirements

---

## Tips for Choosing the Right i Value

- **i = 0 (remove y)**: Good when removing characters breaks a pattern
- **i = 2 (pump once)**: Good when adding characters breaks counts/ratios
- **i = k (pump k-1 times)**: Use when you need a specific multiple

The key is to choose i so that the pumped string clearly violates the language's defining property!
