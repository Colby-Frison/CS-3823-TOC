## **(i) Idea in Theorem 3.1 similar to one in our course**

The key idea in Theorem 3.1 is **state repetition** (or cycle detection) in finite automata.

**Proof strategy of Theorem 3.1:**
- P1 observes P2 (a DFA with $k$ states) for $3k$ rounds
- By the pigeonhole principle, P2 must enter a cycle
- Once in the cycle, P2's behavior becomes predictable and periodic
- P1 exploits this: plays $t$ when P2 is about to output $T$, or plays $h$ forever if the cycle only contains $H$

**Connection to our course:**

This is directly related to the **Pumping Lemma for Regular Languages**, which relies on the same fundamental property:

> *If a DFA has $k$ states and processes an input of length greater than $k$, then by the pigeonhole principle, it must visit some state twice. This creates a cycle that can be repeated ("pumped").*

Both Theorem 3.1 and the Pumping Lemma exploit the fact that:
- DFAs have **finite memory** (only $k$ states)
- After processing $k+1$ inputs, a state must repeat
- This repetition creates predictable, periodic behavior

The Pumping Lemma uses this to show certain languages are non-regular, while Theorem 3.1 uses it to show that a player can exploit a finite automaton's predictable behavior.

---

$$
\boxed{\text{The Pumping Lemma for Regular Languages (based on the pigeonhole principle and state repetition in DFAs)}}
$$

---

## **(ii) Why does this idea fail in Theorem 3.2?**

In Theorem 3.2, P1 does **not know the number of states $k$** of P2's DFA.

**The problem:**

The cycle detection method from Theorem 3.1 requires knowing $k$ to determine how long to observe (e.g., $3k$ rounds) to guarantee finding a cycle. Without knowing $k$, P1 faces a dilemma:

- **If P1 plays $t$ too early:** P2 might be designed to output $H$ at that specific round, giving P1 payoff 0
- **If P1 waits too long (or never plays $t$):** P2 could be designed to eventually output only $T$, but P1 never capitalizes on it, getting average payoff 0

**The adversarial construction:**

Since P1 is deterministic and doesn't know $k$, an adversary can construct a DFA with $k$ large enough that:
- The DFA outputs $H$ for longer than P1's observation period
- When P1 finally plays $t$ (at some predetermined round $n$), the DFA outputs $H$ at round $n$
- Or, if P1 never plays $t$, the DFA eventually outputs only $T$, but P1 misses all opportunities

**Conclusion:** Without knowing $k$, P1 cannot determine the observation length needed to guarantee seeing a complete cycle, so the DFA can always "hide" its periodic behavior beyond P1's detection threshold.

---

$$
\boxed{\text{Without knowing } k\text{, P1 cannot determine the observation length, so P2 can hide the cycle beyond P1's detection}}
$$
