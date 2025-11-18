Most is on ipad side annotations

starting at side 38

# DFA vs NFA

## DFA

## NFA

## Difference

## Conversion
![[Pasted image 20250909122240.png]]
In the above image we have an NFA that has 3 states and 2 characters, below is the same language represented in a DFA
![[Pasted image 20250909122231.png]]
==make sure this is correct==:
I think its like the tree thing, where with an NFA there are multiple choice for transitions so its like a tree, but a DFA is a path. Each layer of the tree created by going through the NFA is a union making something like {1,2}. The transitions to these are then broken down
### Question and explanation from reddit
![[Pasted image 20250909123151.png]]
The states of the DFA are sets of states of the NFA.

The start sate of the NFA is 1, but you can take an epsilon transition to 2 right away, so the start state of the DFA is {1,2}.

- From {1,2} a can take you to 2 and nowhere else, so the state from {1,2} along a is {2}.
- From {1,2} b can take you to 3 or 5, which is an accept state, so {3,5} accepting.

Keep going from the states you have so far until everything is reached.

- From {2} an a leads to {}, a failure state, or you can just leave it off in some definitions of the diagrams.
- From {2} b leads to {5} accepting.
- From {3,5} a leads to {2,5}.
- From {3,5} b leads to {4,5}
- From {4,5} a leads to {2,5}
- From {4,5} b leads to {5}
-  From {2,5} a leads to {5}
- From {2,5} b leads to {5}

I think that's all of them that can be reached.

### Equivalence of NFAs and DFAs

# Closure under regular Operations
## Union

>**Theorem 14:**
>	The class of regular languages is closed under the union operation

**Proof idea:**
	Create an NFA N from N1 and N2 that recognize the languages A1 and A2 respectively.

![[Pasted image 20250909124221.png]]
If both $N_1$ and $N_2$ are regular than their union is also regular

#### Proof
![[Pasted image 20250909124722.png]]

## Concatenation

>**Theorem 15:**
>	The class of regular languages is closed under concatenation.

**Proof idea:**
	Nondeterministically guess where to make the split.

![[Pasted image 20250909124842.png]]

#### Proof
![[Pasted image 20250909124909.png]]

## Star

>**Theorem 16:**
>	The class of regular languages is closed under the star operation.

If a is regular, then A* is regular

**Proof idea:**
	Construct an NFA N that accepts its input whenever it can be broken into several pieces and N1 accepts each such piece.

![[Pasted image 20250909124945.png]]

#### Proof
![[Pasted image 20250909125139.png]]

# Regular Expressions

## Computation of a GNFA
![[Pasted image 20250909130836.png]]

## Regular Languages
![[Pasted image 20250909130911.png]]

>![[Pasted image 20250909130923.png]]![[Pasted image 20250909130933.png]]

