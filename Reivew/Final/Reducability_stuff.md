# Summary: Reducibility and the Undecidability Proof

## 1. What We're Trying to Prove

We want to prove that **$\text{HALT}_{\text{TM}}$** (the Halting Problem) is undecidable.

\[
\text{HALT}_{\text{TM}} = \left\{ \langle M, w \rangle \;\middle|\; M\ \text{halts on}\ w \right\}
\]

## 2. The Proof Strategy: Reduction

We use **reduction** — a technique where we show that *solving one problem would let us solve another problem that's already known to be unsolvable*.

### Key Principle

If problem A is already known to be undecidable, and we can show that:

> *If we could solve problem B, then we could use that solution to solve problem A*

then problem B must also be undecidable (otherwise we get a contradiction).

## 3. The Known Undecidable Problem: $A_{\text{TM}}$

From earlier in the course (pages 24–25):

- **$A_{\text{TM}} = \{\langle M, w \rangle \mid M \text{ accepts } w\}$** is undecidable.
- This was proven using **diagonalization** (the "D accepts ⟨D⟩" contradiction).

## 4. The Reduction Proof

### The Logical Flow

1. **Assume (for contradiction) that $\text{HALT}_{\text{TM}}$ is decidable.**
   - That is, there exists a Turing machine $R$ that decides $\text{HALT}_{\text{TM}}$.
   - $R$ always halts and says "yes" if $M$ halts on $w$, "no" if $M$ loops on $w".

2. **Build a Turing machine $S$ for $A_{\text{TM}}$ using $R$:**

   ```text
   S on input ⟨M, w⟩:
     1. Run R on ⟨M, w⟩.
     2. If R says "no" (M doesn't halt on w), 
        then S rejects (because if M doesn't halt, it can't accept).
     3. If R says "yes" (M does halt on w),
        then simulate M on w.
        If M accepts, S accepts; if M rejects, S rejects.
   ```

3. **Contradiction:**
   - We've now built $S$ that decides $A_{\text{TM}}$.
   - But we already know $A_{\text{TM}}$ is undecidable (Theorem 11).
   - Therefore, our initial assumption must be false.
   - **Therefore, $\text{HALT}_{\text{TM}}$ is undecidable.**

## 5. Notation Reference

- **$\langle M, w \rangle$**: a string encoding of both a TM $M$ and an input $w$.
- **$A_{\text{TM}} \leq \text{HALT}_{\text{TM}}$**: "$A_{\text{TM}}$ reduces to $\text{HALT}_{\text{TM}}$" (we use halting to solve acceptance).
- **$R$ is a decider**: $R$ always halts and gives a correct yes/no answer.

## 6. Why This Works

The reduction shows that $\text{HALT}_{\text{TM}}$ is **at least as hard as** $A_{\text{TM}}$:

- If you could solve $\text{HALT}_{\text{TM}}$, you could solve $A_{\text{TM}}$.
- Since $A_{\text{TM}}$ is impossible to solve, $\text{HALT}_{\text{TM}}$ must also be impossible.

## 7. Key Insights

1. **Reduction transfers undecidability** from one problem to another.
2. **$A_{\text{TM}}$ is the "seed" undecidable problem** — many others are proven undecidable by reducing $A_{\text{TM}}$ to them.
3. **The proof constructs a hypothetical machine** ($S$) that can't exist, showing the initial assumption (that $R$ exists) must be false.
4. **Both $A_{\text{TM}}$ and $\text{HALT}_{\text{TM}}$ are:**
   - Turing-recognizable (page 23: universal TM $U$ recognizes $A_{\text{TM}}$)
   - Undecidable
   - Not co-recognizable

## 8. Big Picture

This proof technique allows us to build a **hierarchy of undecidability**: once we prove a problem undecidable ($A_{\text{TM}}$ via diagonalization), we can prove many others undecidable by reduction—no need to redo the diagonalization argument every time.

> **Essence:**  
> If halting were decidable, acceptance would be decidable.  
> But acceptance isn't decidable, so halting can't be decidable either.
