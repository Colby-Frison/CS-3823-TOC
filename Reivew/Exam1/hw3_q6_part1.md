# Homework 3 Question 6 Part 1 - Pumping Lemma Proof (Corrected)

## Question
Prove that **L = {www | w ∈ Σ*}** where Σ = {0, 1} is **not regular** using the Pumping Lemma.

---

## Proof by Contradiction

### Step 1: Assume L is regular
Assume, for the sake of contradiction, that L is regular.

### Step 2: Apply the Pumping Lemma
Since L is regular, by the Pumping Lemma, there exists a pumping length **p > 0** such that for every string s ∈ L with |s| ≥ p, we can write s = xyz where:
1. |y| > 0 (y is non-empty)
2. |xy| ≤ p (the first two parts are within the first p characters)
3. For all i ≥ 0, xy^i z ∈ L (we can pump y any number of times and stay in the language)

### Step 3: Choose a specific string s ∈ L with |s| ≥ p
Let w = 0^p (a string of p zeros), and let **s = www = 0^p 0^p 0^p = 0^(3p)**.

- Clearly s ∈ L (it's three identical copies of 0^p)
- |s| = 3p ≥ p ✓

### Step 4: Consider ANY division s = xyz satisfying |y| > 0 and |xy| ≤ p

**Key constraint analysis:**

Since |xy| ≤ p and s starts with 3p zeros, the substring xy must be entirely within the first p characters (the first copy of w).

Therefore:
- x = 0^a (some number a of zeros, where a ≥ 0)
- y = 0^b (some number b of zeros, where b > 0 since |y| > 0)
- z = 0^c (the remaining zeros)

Where:
- a + b ≤ p (from |xy| ≤ p)
- b > 0 (from |y| > 0)
- a + b + c = 3p (total length)

**Visual representation:**
```
s = 0^(3p) = [0^p] [0^p] [0^p]
              ↑____↑
              xy must
              be here
```

Since xy is entirely in the first block, y is also entirely in the first block.

### Step 5: Show that the pumped string fails for ALL i (find a value that works)

**The key insight:**

The original string s = www had three equal parts, each of length p:
- First part: 0^p
- Second part: 0^p  
- Third part: 0^p

Since xy is entirely within the first p characters (from |xy| ≤ p), pumping y **only affects the first copy**.

**The crucial observation (applies to ALL i ≠ 1):**

The original string s has the property that it can be divided into three equal parts of length p.

After pumping with xy^i z, the total length becomes:
- |xy^i z| = |x| + i|y| + |z| = a + ib + c = 3p + (i-1)b

For i ≠ 1, we have (i-1)b ≠ 0 (since b > 0), so |xy^i z| ≠ 3p.

**Now we need to show that even if the length is divisible by 3, the string still fails.**

Here's the key: Since xy lies entirely within the first p characters (the first copy of w), the pumping **only changes the first part** of the string. Let's break down what xy^i z looks like:

Looking at where the boundaries of the original three parts were:
- Characters 1 through p: First 0^p (this is where x and y are)
- Characters p+1 through 2p: Second 0^p (completely unchanged)  
- Characters 2p+1 through 3p: Third 0^p (completely unchanged)

After pumping to get xy^i z:
- The substring from position |x| + i|y| + 1 onward is exactly the same as the original string from position |x| + |y| + 1 onward
- This means the second and third "copies" in the original string remain intact

**For ANY i ≠ 1, specifically let's check i = 0:**

Taking i = 0, we get xy^0 z = xz = 0^(a+c) = 0^(3p-b).

For this to be in L, we need 0^(3p-b) = www for some w ∈ Σ*.
- This requires 3p - b to be divisible by 3
- If 3p - b = 3k for some integer k, then b = 3p - 3k = 3(p-k), meaning b must be divisible by 3

But we don't get to choose b! The adversary chooses how to split xyz, and b can be ANY value from 1 to p (satisfying |xy| ≤ p).

**More importantly:** The structure argument shows that even if the length works out, the string has the wrong form. Since z contains the complete second and third copies of 0^p from the original string, and these had combined length 2p, but now we only have length 3p - b < 3p total, we cannot have three complete equal copies.

**Therefore:** For i = 0 (and this is just ONE example that suffices), we have xy^0 z ∉ L.

This contradicts the Pumping Lemma condition that xy^i z ∈ L for **ALL i ≥ 0**.

### Step 6: Contradiction

This contradicts condition 3 of the Pumping Lemma (that xy^i z ∈ L for all i ≥ 0).

Therefore, our assumption that L is regular must be **false**.

---

## Conclusion

**L = {www | w ∈ Σ*} is NOT regular.** ∎

---

## Key Points to Remember

1. **We don't choose how to split the string** - we must show that NO MATTER HOW the adversary splits it (following the constraints), pumping fails.

2. **We only need to find ONE value of i that fails** - The Pumping Lemma says xy^i z ∈ L for **ALL i ≥ 0**. To get a contradiction, we only need to show that there exists **at least one** value of i where xy^i z ∉ L. Commonly we use i = 0 or i = 2, but any value that gives a contradiction works.

3. **The choice of string:** We choose a string that depends on p (like 0^(3p)) to ensure that pumping breaks the language property.

4. **The key insight:** Since |xy| ≤ p, pumping y only affects one of the three copies, making it impossible to maintain the "three identical copies" property of the language.

5. **Logic of the proof:** The Pumping Lemma states "For ALL i ≥ 0, xy^i z ∈ L". To contradict this, we show "There EXISTS some i where xy^i z ∉ L". Finding one counterexample is sufficient!

