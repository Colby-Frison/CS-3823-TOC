**Proof that $A \setminus B$ is regular:**

Since $A$ and $B$ are regular languages, there exist deterministic finite automata (DFAs) that recognize them. Let:
- $M_A = (Q_A, \Sigma, \delta_A, q_{0A}, F_A)$ be a DFA for $A$,
- $M_B = (Q_B, \Sigma, \delta_B, q_{0B}, F_B)$ be a DFA for $B$.

We construct a new DFA $M = (Q, \Sigma, \delta, q_0, F)$ that recognizes $A \setminus B$ as follows:
## Constructing DFA
### State Set $Q$
To simulate both $M_A$ and $M_B$ simultaneously, we need to track the current state of each machine. Therefore, we define the state set of $M$ as the Cartesian product:
$$
Q = Q_A \times Q_B.
$$
Each state in $M$ is a pair $(p, q)$, where $p \in Q_A$ and $q \in Q_B$.

### Alphabet $\Sigma$
The alphabet remains the same as for $M_A$ and $M_B$.

### Transition Function $\delta$
For each state $(p, q) \in Q$ and each symbol $a \in \Sigma$, we define:
$$
\delta((p, q), a) = (\delta_A(p, a), \delta_B(q, a)).
$$
This means that when reading a symbol $a$, $M$ updates the state of $M_A$ from $p$ to $\delta_A(p, a)$ and the state of $M_B$ from $q$ to $\delta_B(q, a)$.

### Start State $q_0$
The start state of $M$ is the pair of start states of $M_A$ and $M_B$:
$$
q_0 = (q_{0A}, q_{0B}).
$$

### Accept States $F$
We want $M$ to accept a string $x$ if and only if $x \in A$ and $x \notin B$. This occurs when:
- $M_A$ ends in an accept state (i.e., $p \in F_A$), and
- $M_B$ ends in a non-accept state (i.e., $q \notin F_B$).

Therefore, we define the accept set of $M$ as:
$$
F = \{(p, q) \in Q \mid p \in F_A \text{ and } q \notin F_B\}.
$$

---

## Verification
Let $x \in \Sigma^*$. After processing $x$, the state of $M$ is:
$$
\delta^*(q_0, x) = (\delta_A^*(q_{0A}, x), \delta_B^*(q_{0B}, x)).
$$
Let $p = \delta_A^*(q_{0A}, x)$ and $q = \delta_B^*(q_{0B}, x)$. Then:
- $x \in A$ if and only if $p \in F_A$,
- $x \in B$ if and only if $q \in F_B$.

By the definition of $F$, $M$ accepts $x$ if and only if $p \in F_A$ and $q \notin F_B$, which is equivalent to $x \in A$ and $x \notin B$. Thus, $M$ accepts exactly $A \setminus B$.

### Why This Construction Avoids Closure Under Complement
This proof does not rely on the closure of regular languages under complement. Instead, it directly constructs a DFA for $A \setminus B$ by:
- Running $M_A$ and $M_B$ in parallel via the product construction,
- Defining acceptance based on the states of both machines: accept if $M_A$ accepts and $M_B$ rejects.

The condition $q \notin F_B$ is a simple check on the state of $M_B$ (since $F_B$ is a fixed finite set), and does not require constructing a DFA for the complement of $B$.

---

## Conclusion

Since we have constructed a DFA $M$ that recognizes $A \setminus B$, it follows that $A \setminus B$ is regular.


# Answer for document

**5 Closure \[4 points\]**

Let $A$ and $B$ be regular languages. Show that $A \setminus B$ is also regular.  
Recall that $A \setminus B = \{x \in A \mid x \notin B\}$. In other words, this operation removes from $A$ all the strings that are also in $B$.

---

**Proof:**  
Since $A$ and $B$ are regular, there exist deterministic finite automata (DFAs) $M_A = (Q_A, \Sigma, \delta_A, q_{0A}, F_A)$ and $M_B = (Q_B, \Sigma, \delta_B, q_{0B}, F_B)$ that recognize $A$ and $B$, respectively.

We construct a DFA $M = (Q, \Sigma, \delta, q_0, F)$ for $A \setminus B$ as follows:
- $Q = Q_A \times Q_B$ (the product states),
- $\delta((p, q), a) = (\delta_A(p, a), \delta_B(q, a))$ for all $(p, q) \in Q$ and $a \in \Sigma$,
- $q_0 = (q_{0A}, q_{0B})$,
- $F = \{(p, q) \in Q \mid p \in F_A \text{ and } q \notin F_B\}$.

**Correctness:**  
For any string $x \in \Sigma^*$, let $\delta^*(q_0, x) = (p, q)$, where $p = \delta_A^*(q_{0A}, x)$ and $q = \delta_B^*(q_{0B}, x)$. Then:
- $x \in A$ iff $p \in F_A$,
- $x \in B$ iff $q \in F_B$.

Thus, $x \in A \setminus B$ iff $p \in F_A$ and $q \notin F_B$, which is exactly when $M$ accepts $x$. Therefore, $M$ recognizes $A \setminus B$, proving it is regular.



