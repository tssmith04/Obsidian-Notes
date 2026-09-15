Textbook: Achim Klemke
## Overview
Recall $\Omega$ is a sample space
Recall $\mathbb{P}$ is a probability measure telling you how likely something is to occur
Recall events are subsets of $\Omega$

Consider $\Omega=[0,1]$ and $\lambda$ = Lebesgue Measure and $\lambda(\Omega)=1$ in which case $\lambda$ is also a probability measure.
Question: Can we assign a meaningful probability (measure) to every subset of $\Omega$ ($2^{\Omega}$)?
No, there exists non-measurable sets.

So the probabilistic approach we take is to take a collection of measurable events $\mathcal{F}$.

Suppose $\Omega=\{0,1,2,3,\dots\}$ and we know $\mathbb{P}(\{ 1 \})$ and $\mathbb{P}(\{ 2 \})$ then we know $\mathbb{P}(\{ 1,2 \})$ and $\{ 1 \} \in \mathcal{F}$ along with $\{ 2 \}$ and $\{ 1,2 \}$. So $\mathcal{F}$ should have some structure.
If we want $\mathcal{F}$ to be "maximal" then do I need to assign probability to all events in $\mathcal{F}$?
So the question is how to efficiently define a measure?
I.e. What is a subcollection of $\mathcal{F}$ s.t. defining $\mathbb{P}$ on this subcollection uniquely determines the $\mathbb{P}$ on $\mathcal{F}$?

$(\Omega,\mathcal{F},\mathbb{P})$ is a probability space.

General roadmap:
- Basic measure theory
- Independence
- Properties of integrals (Expectation)
- Law of Large numbers
- CLT
	- Talking about convergence in a more in depth sense

Investigating $\mathcal{F}$ more we see $\mathcal{F}$ is a class of sets . So let $\Omega$ be a nonempty set and $2^{\Omega}$ be the power set of $\Omega$.

**Definition (field/algebra)**: A collection of sets $\mathcal{F}\subset2^{\Omega}$ is called a field (or an algebra) if
 a. $\Omega\in\mathcal{F}$
 b. Complement closed: If $A\in\mathcal{F}$ then $A^{c}\in\mathcal{F}$
 c. $\cup$-closed: $\mathcal{F}$ is closed under finite unions aka $\forall A_{i}\in \mathcal{F}\implies\bigcup_{i=1}^{n}A_{i}\in \mathcal{F}$
>Note: By being closed under complement we can apply DeMorgan's law to (c) to get the additional fact that a field is also $\cap$-closed (closed under finite intersections)

**Definition ($\sigma$-field/$\sigma$-algebra)**: A class $\mathcal{F}\subset2^{\Omega}$ is called a $\sigma$-field (or a $\sigma$-algebra) if
a. $\Omega\in\mathcal{F}$
b. $\mathcal{F}$ is complement closed
c. $\sigma$-$\cup$-closed: $\mathcal{F}$ is closed under **countable** union i.e. $\forall \{ A_{i} \}_{i\geq1}\subseteq\mathcal{F}\implies \bigcup_{i=1}^{\infty}A_{i}\in\mathcal{F}$
>Note: We upgrade from a field $\to$ $\sigma$-field here by upgrading from finite union to countable union. Following the same logic as above, (c) also implies $\sigma$-$\cap$-closed.

Example: $\mathcal{F}=\{ A\subset\Omega : \text{either } |A| \text{ is finite or } |A^{c}| \text{ is finite} \}$ (Recall $|\cdot|$ denotes cardinality here)
We claim that $\mathcal{F}$ is a field, so lets check the three conditions.
a. $\Omega^{c}=\emptyset\implies|\emptyset|=0\implies\Omega\in \mathcal{F}$
b. Somewhat trivially, $A\in F\implies A^{c}\in F$ (since $A\in\mathcal{F}$ implies that $|A|$ or $|A^{c}|$ are finite which implies $A^{c}\in \mathcal{F}$ )
c. Suppose $A_{1},\dots,A_{n}\in\mathcal{F}$ then if $A_{i}$ is finite $\forall i$ we have $\bigcup_{i=1}^{n}A_{i}\in \mathcal{F}$ because finite union of finite sets is finite. The other case to consider is if $\exists A_{i0}$ that is not finite (thus $A_{i0}^{c}$ is finite), then $\left( \bigcup_{i=1}^{n}A_{i} \right)^{c}=\bigcap_{i=1}^{n}A_{i}^{c}\subseteq A_{i0}^{c}$ (which is finite) thus, $\bigcap_{i=1}^{n}A_{i}^{c}$ is finite so $\bigcup_{i=1}^{n}A_{i}\in\mathcal{F}$
Question: Is $\mathcal{F}$ a $\sigma$-field? The answer is no. Why is left as homework and it deals only with property (c).
**Revisited outside class**: Consider the counter example $A_{i}=\{ 2i \}$ then note that every set $A_{i}$ is finite (only has one element) for $i\in \mathbb{N}$, however, $\bigcup_{n=1}^{\infty}A_{n}=\mathbb{N}^{\text{even}}\implies|\mathbb{N}^{\text{even}}|$ is not finite and note $(\mathbb{N}^{\text{even}})^{c}=\mathbb{N}^{\text{odd}}\implies|\mathbb{N}^{\text{odd}}|$ is not finite as well, thus $\bigcup_{n=1}^{\infty}A_{n}\not\in\mathcal{F}$.

#### Properties of a $\sigma$-field
Let $\mathcal{F}_{1},\mathcal{F}_{2}$ be two $\sigma$-fields in $\Omega$. Is $\mathcal{F}_{1}\cap\mathcal{F}_{2}$ a $\sigma$-field?
a. $\Omega\in\mathcal{F}_{1},\Omega\in\mathcal{F}_{2}\implies\Omega\in\mathcal{F}_{1}\cap\mathcal{F}_{2}$
b. $A\in \mathcal{F}_{1}\cap\mathcal{F}_{2}\implies A\in \mathcal{F}_{1},\mathcal{F}_{2}\implies A^{c}\in\mathcal{F}_{1},\mathcal{F}_{2}\implies A^{c}\in\mathcal{F}_{1}\cap\mathcal{F}_{2}$
c. $A_{i}\in \mathcal{F}_{1}\cap\mathcal{F}_{2}\;\forall i\geq1\implies A_{i}\in\mathcal{F}_{1},\mathcal{F}_{2}\implies \bigcup_{i=1}^{\infty}A_{i}\in\mathcal{F}_{1},\mathcal{F}_{2}\implies \bigcup_{i=1}^{\infty}A_{i}\in\mathcal{F}_{1}\cap\mathcal{F}_{2}$
So yes, $\mathcal{F}_{1}\cap\mathcal{F}_{2}$ is a $\sigma$-field.
>**Important Note (Useful fact)**: The intersection of two $\sigma$-fields on $\Omega$ is again a $\sigma$-field on $\Omega$. More generally, if $\{ \mathcal{F}_{\alpha} \}_{\alpha\in I}$ is a family of $\sigma$-fields on $\Omega$ (finite, countable, or uncountable) then $\bigcap_{\alpha\in I}\mathcal{F}_{\alpha}$ is a $\sigma$-field on $\Omega$.

Now the natural next consideration: $\mathcal{F}_{1}\cup\mathcal{F}_{2}$ a $\sigma$-field? No, with the following simple counterexample:
$\Omega=\{ 1,2,3,4 \}$ and $\mathcal{F}_{1}=\{ \emptyset,\Omega,\{ 1,2 \},\{ 3,4 \} \}$, $\mathcal{F}_{2}=\{ \emptyset,\Omega,\{ 1,3 \},\{ 2,4 \} \}$.
a. Works obviously
b. Also works trivially
c. Consider $A_{1}=\{ 1,2 \},A_{2}=\{ 2,4 \}\implies A_{1},A_{2}\in\mathcal{F}_{1}\cup\mathcal{F}_{2}$, but note that $A_{1}\cup A_{2}=\{ 1,2,4 \}\not\in\mathcal{F}_{1}\cup\mathcal{F}_{2}$. Thus, the $\sigma$-fields are not closed under finite union so definitely not under countable union.
>**Important Note (Useful fact)**: The union of two $\sigma$-fields on $\Omega$ need not be a $\sigma$-field. It can fail to even be a field, as it may not be closed under finite unions.

**Definition ($\sigma(\cdot)$)**: Let $A\subset2^{\Omega}$. The smallest $\sigma$-field containing $A$ denoted by $\sigma(A)$ is defined to be $$
\sigma(A)=\bigcap \{ \mathcal{F}:\mathcal{F}\text{ is a $\sigma$-field},A\subseteq\mathcal{F} \}
$$
>Note: $A$ does not need to have any structure

#### The Borel $\sigma$-field
Example: $\Omega=\mathbb{R}$ then $\mathcal{B}(\mathbb{R})$=Borel sets in $\mathbb{R}$=$\sigma (\{ A\subseteq \mathbb{R}:A \text{ is open} \})=\sigma(\{ (a,b):a,b\in \mathbb{R} \})$
**Definition (topological space)**: A topological space is a pair $(\Omega,S)$ where $\Omega$ is nonempty and $S$ is a collection of subsets of $\Omega$ such that
a. $\Omega,\emptyset\in S$
b. $S$ is closed under finite intersections ($\cap$-closed)
c. $S$ is closed under arbitrary union ($\sigma$-$\cup$-closed)
>Note: The members of $S$ are called the **open sets of the topology**.

Let $(\Omega,S)$ be a topological pair. Then we can now express the Borel $\sigma$-field as $\mathcal{B}(\Omega)=\sigma(\{ A\subseteq\Omega:A\text{ is an open set i.e. } A\in S \})$
In most cases we will look at metric spaces which have a notion of distance.

HW: Show that $\mathcal{B}(\mathbb{R}^{n})=\sigma(\epsilon)$ where $\epsilon=\{ B_{r}(x):x\in \mathbb{Q}^{n},r\in \mathbb{Q}^{+} \}$.
Proof (start): Since $B_{r}(x)$ is an open set (with respect to topological pair $(\Omega,S)=(\mathbb{R}^{n},S)$) it follows that $\epsilon \subseteq \{ A\subseteq \mathbb{R}^{n}:A \text{ is open} \}$. Thus, $\sigma(\epsilon)\subseteq\sigma(\{ A\subseteq \mathbb{R}^{n}:A \text{ is open} \})=\mathcal{B}(\mathbb{R}^{n})$.
Now we just need to show the reverse direction $\sigma(\epsilon)\supseteq\mathcal{B}(\mathbb{R}^{n})$.
Let $O$ be an open set in $\mathbb{R}^{n}$ (thus $O\in\sigma(\{ A\subseteq \mathbb{R}^{n}:A \text{ is an open set} \})=\mathcal{B}(\mathbb{R}^{n})$).Then $\forall y_{x}\in O\;\exists\text{ an open ball with }y_{x}\in \mathbb{Q},r_{x}\in \mathbb{Q}^{+}$ such that $B_{r_{x}}(y_{x})\subseteq O$. (Essentially for any point in $O$ you know there is an open ball (due to $O$ being open) with a rational $r_{x}$ (due to density of rationals) such that $B_{r_{x}}(y_{x})$ lies within $O$). Thus, $O=\bigcup_{x\in O}\{ x \}\subseteq \bigcup_{x\in O}B_{r_{x}}(y_{x})\subseteq O$. Since $O\subseteq \bigcup_{x\in O}B_{r_{x}}(y_{x})\implies O\in\sigma(\epsilon)\implies\sigma(\epsilon)\supseteq\mathcal{B}(\mathbb{R}^{n})$.

8/20
$\pi$-system
**Definition**: A class $C$ of subsets of $\Omega$ is a $\pi$-system if it is closed under finite intersections. I.e. if $A,B\in C\implies A\cap B\in C$.
**Definition**: A class $L$ of subsets is a $\lambda$-system if
1. $\Omega\in L$
2. Complement closed: $A\in L\implies A^{c}\in L$
3. Any (finite or countable) union of disjoint sets in $L$ belongs to $L$.
We can see that a $\sigma$-field is automatically a $\lambda$-system.

Exercise: Show that a class $L$ is a $\lambda$-system iff it satisfies:
1. $\Omega\in L$
2. Closed under proper differences: $A,B\in L,\;A\subset B\implies B\backslash A\in L$
3. Closed under increasing unions: $\forall A_{n}\in L,A_{n}\subset A_{n+1}\implies\bigcup_{n=1}A_{n}\in L$

Exercise: An arbitrary (index set $\Lambda$) intersection of $\lambda$-systems is a $\lambda$-system.
We can talk about the smallest $\lambda$-system: $\lambda(l):=\bigcap_{L :\text{L is a }\lambda\text{-system},l \subset L} L$. So $\lambda(l)$ is the $\lambda$-system generated by class $l$

A $\sigma$-field is a $\lambda$-system. Is a $\lambda$-system necessarily a $\sigma$-field? (Answer should be no since one more condition)
Exercise: If $\mathcal{F}$ is a field and a $\lambda$-system, show that it is a $\sigma$-field. **Useful fact used in next proof**

**Theorem ($\pi-\lambda$ theorem)**
If a class $l$ is a $\pi$-system then $\lambda(l)=\sigma(l)$.
Proof: Simple side: Since $\sigma(l)$ is a $\lambda$-system containing $l$ $\implies\lambda(l)\subseteq \sigma(l)$.
It remains to show $\sigma(l)\subseteq\lambda(l)$. It suffices to show $\lambda(l)$ is a $\sigma$-field. It suffices to show $\lambda(l)$ is a field (from exercise above). So to check it is a field:
1. $\Omega\in\lambda(l)$
2. Closed under complement
3. Closed under finite union (but will use intersections because closed under complement from 2)
Note 1 and 2 come from definition of $\lambda$-system anyway.
Let $\lambda_{1}(l)=\{ A\in \lambda(l):A\cap B\in\lambda(l)\;\forall B\in l \}$
The goal is to say $\forall A,B\in \lambda(l)\implies A\cap B\in\lambda(l)$.
Starting point: $A,B\in l\implies A\cap B\in l$.
Construct $\lambda_{2}(l)=\{ B\in \lambda(l):A\cap B\in\lambda(l)\;\forall A\in l \}$.
Now if we can show that the whole system $\lambda(l)=\lambda_{1}(l)=\lambda_{2}(l)$ we are done.
Step 1: Since $l$ is a $\pi$-system $l\subseteq\lambda_{1}(l)$. We can verify that $\lambda_{1}(l)$ is a $\lambda$-system.  I.e. If $\lambda_{1}(l)$ is a $\lambda$-system containing $l$ then $\lambda(l)\subseteq\lambda_{1}(l)$. Note also by definition that $\lambda_{1}(l)\subseteq\lambda(l)$. Therefore, $\lambda_{1}(l)=\lambda(l)$.
It remains to show $\lambda_{2}(l)=\lambda(l)$. By definition of $\lambda_{2}(l)$, $\lambda_{2}(l)\subseteq\lambda(l)$. To show other inclusion, $\lambda(l)\subseteq\lambda_{2}(l)$ it suffices to show $\lambda_{2}(l)$ is a $\lambda$-system. Follow same logic as above.
Therefore, we have shown $\lambda_{2}(l)=\lambda(l)$. Thus, $\lambda(l)$ is closed under intersection from definitions of $\lambda_{1}(l),\lambda_{2}(l)$ which shows $\lambda(l)$ is a field which shows $\lambda(l)$ is a $\sigma$-field.

### Measures
Let $\Omega$ be a nonempty set. A set function is an extended real-valued function defined on a subcollection of $2^{\Omega}$.
**Definition (measure)**: Let $\mathcal{F}$ be a $\sigma$-field on $\Omega$. A set function $\mu$ on $\mathcal{F}$ is called a measure if:
1. $\mu(A)\in[0,\infty)$ for all $A\in\mathcal{F}$
2. $\mu(\emptyset)=0$
3. Countable additivity: Let $A_{1},A_{2},\dots$ be disjoint events in $\mathcal{F}$. Then $\mu\left( \bigcup_{i=1}^{\infty}A_{i} \right)=\sum_{i=1}^{\infty}\mu(A_{i})$. The measure $\mu$ is said to be finite if $\mu(\Omega)<\infty$. (Example: $\mu(\Omega)=1$ probability measure). If $\mu(\Omega)=\infty$ then $\mu$ is infinite.

**Definition ($\sigma$-finiteness)**: A measure $\mu$ on a measurable space $(\Omega,\mathcal{F})$ is said to be $\sigma$-finite if $\exists$ a countable collection of sets $\{ A_{i} \}\subseteq \mathcal{F}$ such that $\bigcup_{i=1}^{\infty}A_{i}=\Omega$ and $\mu(A_{i})<\infty$ for all $i\geq1$.
The benefit of this is now we can approximate the entire space through a series of increasing events with finite probability: $B_{n}\subset B_{n+1}$ where $B_{n}=\bigcup_{i=1}^{n}A_{i}\implies \mu(B_{n})<\infty$ for each $n$ and $\lim_{ n \to \infty }B_{n}=\bigcup_{n}B_{n}=\Omega$.
Example: Let $\Omega=\mathbb{R}$ and $\mu(A)=|A|$ (counting measure). In this example, $\mu$ is not $\sigma$-finite since $\mathbb{R}$ is uncountable.
Example: Let $\Omega=\mathbb{Z}$ and $\mu(A)=|A|$. Now $\mu$ is $\sigma$-finite (since integers are countable).

Proposition: Let $(\Omega,\mathcal{F})$ and $\mu$ be a measure on $\mathcal{F}$ then $\mu$ satisfies:
1. (Finite additivity) $A_{i}\in \mathcal{F}$ for $i\leq n$ where $A_{i}$'s are disjoint it follows $\mu\left( \bigcup_{i=1}^{n}A_{i} \right)=\sum_{i=1}^{n}\mu(A_{i})$.
2. (Monotonicity) If $A,B\in \mathcal{F}$ and $A\subseteq B$ then $\mu(A)\leq \mu(B)$ (follows from non-negativity and additivity)
3. (Monotone Continuity from below) Take collection $\{ A_{i}\in \mathcal{F}:A_{i}\subset A_{i+1}\;\forall i \}$ then $\lim_{ n \to \infty }A_{n}=\bigcup_{i=1}^{\infty}A_{i}\implies \mu(\lim_{ n \to \infty }A_{n})=\lim_{ n \to \infty }\mu(A_{n})$
4. (Monotone continuity from above) Take collection $\{ A_{n} \}\subseteq \mathcal{F},A_{n+1}\subset A$ and $\mu(A_{k})<\infty$ for some $k$ then $\mu(\lim_{ n \to \infty }A_{n})=\mu\left( \bigcap_{n=1}^{\infty}A_{n} \right)=\lim_{ n \to \infty }\mu(A_{n})$.
5. (Countable subadditivity) For $\{ A_{i} \}\subset \mathcal{F}$ we have $\mu\left( \bigcup_{i=1}^{\infty}A_{i} \right)\leq \sum_{i=1}^{\infty}\mu(A_{i})$.
Proof of 2: $B=(B\backslash A)\cup A$
Proof of 3: $B_{n}=A_{n}\backslash A_{n-1}$ and we have $\mu\left( \lim_{ n \to \infty }A_{n} \right) =\mu\left( \bigcup_{i=1}^{\infty}A_{i} \right)=\mu\left( \bigcup_{n=1}^{\infty}B_{n} \right)=\sum_{n=1}^{\infty}\mu(B_{n})=\lim_{ N \to \infty }\sum_{n=1}^{N}\mu(B_{n})=\lim_{ N \to \infty }\mu(A_{N})$Proof of 4: WLOG say $\mu(A_{1})<\infty$ and $B_{n}=A_{1}\backslash A_{n}$

Proof of 5: Exercise: $(\Omega,\mathcal{F})$ and $\mu$ is a set function on $\mathcal{F}$ such that
1. $\mu$ takes values in $[0,\infty)$
2. $\mu(\emptyset)=0$
3. $\mu$ satisfies finite additivity and monotone continuity from below

Examples (Lebesgue-Stieljes measure): A Lebesgue-Stieljes measure on $\mathbb{R}$ is generated by a non-decreasing right continuous function.
Let $(\Omega,\mathcal{F})=(\mathbb{R},\mathcal{B}(\mathbb{R}))$.  (Note $\mathcal{B}$ here denotes a Borel field). Let $F(\cdot)$ be such a function (non-decreasing right continuous). Naturally, we can define a set function $\mu_{F}((a,b))=F(b)-F(a)$ and $\mu_{F}((a,\infty))=\lim_{ b \to \infty }F(b)-F(a)$
Note that $\mu_{F}$ is defined on the collection $C=\{ (a,b),(a,\infty) :a,b\in \mathbb{R},-\infty\leq a<b<\infty\}$.
Question: Is it sufficient to determine the measure $\mu_{F}$ on the entire Borel $\sigma$-field $\mathcal{B}(\mathbb{R})$?
We can translate this into a uniqueness question: If two measures $\mu$ and $\nu$ agree on a subcollection $C\subseteq \mathcal{F}$ ($\mu(A)=\nu(A)$ for all $A\in C$), then are they the same on $\mathcal{F}$?

8/24
Recall from last time the $\pi-\lambda$ theorem: If $\mathcal{C}$ is a $\pi$-system then $\lambda(\mathcal{C})=\sigma(\mathcal{C})$.
**Corollary**: If $\mathcal{C}$ is a $\pi$-system and $\mathcal{L}$ is a $\lambda$-system containing $\mathcal{C}$ then $\sigma(\mathcal{C})\subseteq \mathcal{L}$.
Proof: $\sigma(\mathcal{C})=\lambda(\mathcal{C})\subseteq \mathcal{L}$

Motivating question from last time: Let $\mathcal{C}\subseteq2^{\Omega}$. What property does $\mathcal{C}$ need in order to uniquely determine the measure on $\sigma(\mathcal{C})$?
**Theorem (Uniqueness)**: Suppose  $\mu_{1},\mu_{2}$ are two measures on a measurable space $(\Omega,\mathcal{F})$. Let $\mathcal{C}\subseteq\mathcal{F}$ be a $\pi$-system such that $\sigma(\mathcal{C})=\mathcal{F}$. Suppose $\mu_{1}(c)=\mu_{2}(c)\;\forall c\in\mathcal{C}$, then $\mu_{1}(A)=\mu_{2}(A)\;\forall A\in\mathcal{F}$ in the following cases:
1. $\mu_{1}$ and $\mu_{2}$ are finite measures and $\mu_{1}(\Omega)=\mu_{2}(\Omega)$
2. $\mu_{1}$ and $\mu_{2}$ are $\sigma$-finite and there exists a sequence $c_{n}\in\mathcal{C}$ such that $c_{n}\subseteq c_{n+1}$ and $\bigcup_{n=1}^{\infty}c_{n}=\Omega$ and $\mu_{1}(c_{n})<\infty$ for every $n$

Proof of (1):
Let $\mathcal{L}=\{ A\in\mathcal{F}:\mu_{1}(A)=\mu_{2}(A) \}$. By assumption we have $\mathcal{C}\subseteq \mathcal{L}$. So now if we can additionally show $\mathcal{L}$ is a $\lambda$-system then since $\mathcal{C}$ is a $\pi$-system we will have the entire $\sigma$-field $\mathcal{F}=\sigma(\mathcal{C})\subseteq \mathcal{L}$. Now we check that $\mathcal{L}$ is a $\lambda$-system:
	1. $\Omega\in \mathcal{L}$ since $\mu_{1}(\Omega)=\mu_{2}(\Omega)$
	2. If $A\in \mathcal{L}$ then $\mu_{1}(A)=\mu_{2}(A)$. Note that $\mu_{1}(A^{c})=\mu_{1}(\Omega)-\mu_{1}(A)=\mu_{2}(\Omega)-\mu_{2}(A)=\mu_{2}(A^{c})\implies A^{c}\in \mathcal{L}$
	3. If $A_{i}$ are disjoint in $\mathcal{L}$ then $\mu_{1}\left( \bigcup_{i=1}^{\infty}A_{i} \right)=\sum_{i=1}^{\infty}\mu_{1}(A_{i})=\sum_{i=1}^{\infty}\mu_{2}(A_{i})=\mu_{2}\left( \bigcup_{i=1}^{\infty}A_{i} \right)$

Proof of (2):
In this case say $\mu_{1}(\Omega)=\mu_{2}(\Omega)=\infty$. Define $\mu_{i}^{n}(\cdot)=\mu_{i}\left( \cdot \bigcap c_{n} \right)$ for $i=1,2$. Then both $\mu_{1}^{n},\mu_{2}^{n}$} are finite measures. We have $\mu_{1}(A\cap c_{n})=\mu_{1}^{n}(A)=\mu_{2}^{n}(A)=\mu_{2}(A\cap c_{n})$ for every $A\in\mathcal{F}$ by part (1) (note for each $A\in\mathcal{C}$ we have $\mu_{1}^{n}(A)=\mu_{1}(A\cap c_{n})=\mu_{2}(A\cap c_{n})=\mu_{2}^{n}(A)\implies \mu_{1}^{n}(\Omega)=\mu_{2}^{n}(\Omega)$ because note that $A\cap c_{n}\in\mathcal{C}$ still in the $\pi$-system). For $A\in\mathcal{F}$ to recover the measure $\mu_{1}(A)=\lim_{ n \to \infty }\mu_{1}(A\cap c_{n})=\lim_{ n \to \infty }\mu_{2}(A\cap c_{n})=\mu_{2}(A)$.

Let $\mathcal{C}\subseteq2^{\Omega}$ be a $\pi$-system then knowing the measure $\mu$ on $\mathcal{C}$ plus some additional mild assumptions **determines** $\mu$ on entire $\sigma$-field $\sigma(\mathcal{C})$. We've now established uniqueness, but now need to establish existence.

**Definition (semi-algebra)**: A class of sets $\mathcal{C}$ in $2^{\Omega}$ is a semi-algebra if:
1. $\Omega\in\mathcal{C}$
2. For any two sets $A,B\in\mathcal{C}$ we have $B\backslash A$ is a finite union of disjoint sets in $\mathcal{C}$
3. $\mathcal{C}$ is a $\pi$-system (recall closed under finite intersections)

Exercise: Show that $\mathcal{C}$ is a semialgebra if 
1. $\Omega\in\mathcal{C}$
2. $\forall A\in\mathcal{C},A^{c}$ is a finite union of disjoint sets in $\mathcal{C}$
3. $\mathcal{C}$ is a $\pi$-system

Exercise: (Also homework problem) For a semialgebra $\mathcal{C}$, let $\mathcal{A}(\mathcal{C})$ be the smallest field containing $\mathcal{C}$. $\mathcal{A(C)}=\left\{  A\subset\Omega:\text{for some }k\in \mathbb{N}\text{ and disjoint } B_{1},\dots,B_{k}\in\mathcal{C},A=\bigcup_{i=1}^{k}B_{i}  \right\}$

**Definition (premeasure)**: A set function $\mu$ on a semialgebra $\mathcal{C}$ taking values in $[0,\infty]$ is called a premeasure if:
1. $\mu(\emptyset)=0$
2. For any sequence of disjoint $\{ A_{n} \}\subseteq\mathcal{C}$ with $\bigcup_{n}A_{n}\in\mathcal{C}$ we have countable additivity $\mu\left( \bigcup_{n=1}^{\infty}A_{n} \right)=\sum_{n=1}^{\infty}\mu(A_{n})$. 
>Note: It is called $\sigma$-finite if there exists $C_{n}\in\mathcal{C}$ such that $\mu(C_{n})<\infty$ for every $n$ and $\bigcup_{n=1}^{\infty}C_{n}=\Omega$

**Theorem (Caratheodory Extension)**: Let $\mu$ be a $\sigma$-finite premeasure on a semialgebra $\mathcal{C}$ in $\Omega$. Then $\mu$ has a unique extension to a measure $\tilde{\mu}$ on $\sigma(\mathcal{C})$. That is there exists a unique measure $\tilde{\mu}$ on $\sigma(\mathcal{C})$ such that $\tilde{\mu}(A)=\mu(A)$ for every $A\in\mathcal{C}$.

In real analysis we would have $\mu([a,b])=b-a$ and class $\mathcal{C}=\{ (a,b] : -\infty\leq a\leq b<\infty \}\cup \{ \emptyset \}$.
Exercise: check that $\mathcal{C}$ is a semialgebra. Basically verifying that the measure $\mu$ is enough information and $\mathcal{C}$ has enough structure. Thus, $\sigma(\mathcal{C})=\mathcal{B}(\mathbb{R})$. In real analysis the outer measure is $A\subseteq \bigcup_{i=1}^{\infty}I_{i}$ where $I_{i}$ are intervals.
Proof (of above theorem):
Outline: Uniqueness follows from the fact that $\mathcal{C}$ is a $\pi$-system. Existence is by construction.

**Definition (outer measure)**: Given a premeasure $\mu$ on the semialgebra $\mathcal{C}$. The outer measure $\mu^{*}$ induced by $\mu$ on $2^{\Omega}$ is defined as $\mu^{*}(A)=inf\left\{ \sum_{n=1}^{\infty}\mu(A_{n}) :\left\{  A_{n}\subset\mathcal{C},A\subseteq \bigcup_{n=1}^{\infty}A_{n}  \right\}  \right\}$ where $A\subset\Omega$. In words we are essentially trying to find the optimal/minimal cover.
>Remark: We can check that $\mu^{*}(A)=\mu(A)\;\forall A\in\mathcal{C}$.
>Additionally the outer measure $\mu^{*}$ is monotone, that is if $A\subseteq B\implies \mu^{*}(A)\leq \mu^{*}(B)$.
>$\mu^{*}(\emptyset)=0$

Note that $\mu^{*}$ is defined on the entire collection of subsets $2^{\Omega}$.
Does it satisfy countable additivity on the whole $2^{\Omega}$? The answer should be no. Consider real analysis example. 

So the next step is what is a $\sigma$-field where $\mu^{*}$ is a measure?

Proposition: The outer measure $\mu^{*}$ is $\sigma$-subadditive, that is let $A_{n}\subseteq\Omega$ for all $n\geq1$ then $\mu^{*}\left( \bigcup_{n=1}^{\infty}A_{n} \right)\leq \sum_{n=1}^{\infty}\mu^{*}(A_{n})$
Proof (By covering): WLOG assume $\mu^{*}$ is finite for every set $A_{n}$ i.e. $\mu^{*}(A_{n})<\infty$ for all $n\geq1$.
Now let $\epsilon>0$ be fixed. By definition of the outer measure $\mu^{*}$ we can find a covering of $\{ A_{n} \}_{n\geq1}\subseteq\mathcal{C}$ of $A_{n}$ such that $\sum_{i=1}^{\infty}\mu^{*}(A_{n,i})\leq \mu^{*}(A_{n})+\epsilon*2^{-n}$. Note that $\{ A_{n,i} \}_{n,i}$ is a covering of $A=\bigcup_{n=1}^{\infty}A_{n}\implies A\subseteq \bigcup_{n=1}^{\infty}\bigcup_{i=1}^{\infty}A_{n,i}$ (since its a cover of $A$, $A$ must be a subset) and thus $\mu^{*}(A)\leq \sum_{n=1}^{\infty}\sum_{i=1}^{\infty}\mu^{*}(A_{n,i})\leq \sum_{n=1}^{\infty}(\mu^{*}(A_{n})+\epsilon*2^{-n})\leq \sum_{n=1}^{\infty}\mu^{*}(A_{n})+\epsilon$. Lastly observe that $\epsilon$ is arbitrary thus taking $\epsilon$ to 0 we complete the proof.

**Definition ($\mu^{*}$-measurable)**: A set $A\subseteq\Omega$ is called $\mu^{*}$-measurable if $\mu^{*}(E)=\mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})$ for every $E\subset\Omega$. I.e. you can split the sets cleanly. This is analog of Lebesgue measurable sets.

**Lemma**: Let $\mu(\mu^{*})=\{ A\subseteq\Omega:A \text{ is } \mu^{*}\text{-measurable} \}$.  $A\in \mu(\mu^{*})$ (A is $\mu^{*}$-measurable) $\iff$ $\mu^{*}(E)\geq \mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})$ for all $E\subset\Omega$.
Proof of $\impliedby$ direction: $\mu^{*}(E)\leq \mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})$ follows from $\sigma$-subadditivity of $\mu^{*}$ and combining these two gives equality which is the definition. Note the forward direction is trivial because we are given equality for free which implies the inequality.

Proposition: If $\mu^{*}$ is an outer measure, then $\mu(\mu^{*})$ is a $\sigma$-field and $\mu^{*}$ is a measure on $\mu(\mu^{*})$.
Proof: It suffices to show that $\mu(\mu^{*})$ is both a $\pi$-system and a $\lambda$-system.
To show $\mu(\mu^{*})$ is a $\pi$-system it suffices to check $A,B\in \mu(\mu^{*})$, we have $A\cap B\in \mu(\mu^{*})\iff \forall E\in\Omega,\mu^{*}(E)\geq \mu^{*}(A\cap B\cap E)+\mu^{*}((A\cap B)^{c}\cap E)$ (from lemma above)
We can express the right side of the inequality differently as $\mu^{*}(A\cap B\cap E)+\mu^{*}((A\cap B)^{c}\cap E)=\mu^{*}(A\cap B\cap E)+\mu^{*}(((A^{c}\cap B)\cup B^{c})\cap E)$
$\leq\mu^{*}(A\cap B\cap E)+\mu^{*}(A^{c}\cap B\cap E)+\mu^{*}(B^{c}\cap E)$ (by subadditivity)
$\leq \mu^{*}(B\cap E)+\mu^{*}(B^{c}\cap E)\leq \mu^{*}(E)$
Thus, $A\cap B\in \mu(\mu^{*})$.

8/27
Recall from last time we have the Caratheodory extension: if we have a premeasure $\mu$ on a semialgebra $\mathcal{C}$ then can we uniquely extend it to $\sigma(\mathcal{C})$? How?
By construction with an outer measure $\mu^{*}$
	Recall $\mu(\mu^{*})=\{ A \subset\Omega : A \text{ is } \mu^{*}\text{-measurable} \}$ and $A\in \mu(\mu^{*})\iff \mu^{*}(E)\geq\mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})$ for all $E\subset\Omega$.
Proposition: If $\mu^{*}$ is an outer measure then $\mu(\mu^{*})$ is a $\sigma$-field. In particular, $\mu^{*}$ is a measure on $\mu(\mu^{*})$.
Proof: Last time we proved that $\mu(\mu^{*})$ is a $\pi$-system by checking $A\cap B\in \mu(\mu^{*})$ whenever $A,B\in \mu(\mu^{*})$. $\mu^{*}(A\cap B\cap E)+\mu^{*}((A\cap B)^{c}\cap E)\leq \mu^{*}(E)$ for all $E\subset\Omega$.
Next we show that $\mu(\mu^{*})$ is a $\lambda$-system:
1. $\Omega\in \mu(\mu^{*})$: $\mu^{*}(E)\geq \mu^{*}(E\cap \Omega)+\mu^{*}(E\cap \emptyset)$ for all $E\subset\Omega$
2. If $A\in \mu(\mu^{*)})\implies \mu^{*}(E)\geq\mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})$ for all $E\subset\Omega$, but observe that this is the same criterion for $A^{c}\implies A^{c}\in \mu(\mu^{*})$
3. If $A_{1},A_{2},\dots$ are disjoint and in $\mu(\mu^{*})$ we want their union to still be $\mu^{*}$-measurable. We want to show $A=\bigcup_{i=1}^{\infty}A_{i}\in \mu(\mu^{*})$ i.e. we want to show that $\mu^{*}(E)\geq\mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})$ for all $E\subset\Omega$ which means we want to show $\mu^{*}(E)\geq\mu^{*}\left( \bigcup_{i=1}^{\infty}(E\cap A_{i}) \right)+\mu^{*}\left( \bigcap_{i=1}^{\infty}(E\cap A^{c}_{i}) \right)$. So now, let $S_{n}=\bigcup_{i=1}^{n}A_{i}$. Note that since $\mu(\mu^{*})$ is closed under finite intersections ($\pi$-system) and under complement (as shown in (2)) this means it should also be closed under finite union (combining these two properties). Hence, $\mu(\mu^{*})$ is closed under finite union $\implies S_{n}\in \mu(\mu^{*})$. Moreover, since $S_{n}\in \mu(\mu^{*})$ for any $n\geq1$ we can even try to understand what should be the measure of $S_{n}$. Observe that $\mu^{*}(E\cap S_{n+1})=\mu^{*}(E\cap S_{n})+\mu^{*}(E\cap A_{n+1})=\sum_{i=1}^{n+1}\mu^{*}(E\cap A_{i})$ where the last equality comes inductively. For all $E\subset\Omega$ we have the following equality since $S_{n}$ is measurable: $\mu^{*}(E)=\mu^{*}(E\cap S_{n})+\mu^{*}(E\cap S_{n}^{c})\geq \mu^{*}(E\cap S_{n})+\mu^{*}(E\cap A^{c})$ since $S_{n}\subseteq A\implies A^{c}\subseteq S_{n}^{c}$. Continuing the inequality from above we have $=\sum_{i=1}^{n}\mu^{*}(E\cap A_{i})+\mu^{*}(E\cap A^{c})\implies \mu^{*}(E)\geq \sum_{i=1}^{\infty}\mu^{*}(E\cap A_{i})+\mu^{*}(E\cap A^{c})\geq \mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})$. Therefore, $A\in \mu(\mu^{*})$. Thus, $\mu(\mu^{*})$ is a $\lambda$-system which makes $\mu(\mu^{*})$ is a $\sigma$-field.

Lastly, we show that $\mu^{*}$ is a measure on $\mu(\mu^{*})$. We verify countable additivity i.e. for disjoint $A_{1},A_{2},\dots\in \mu(\mu^{*})$ we are trying to understand whether we can have equality of $\mu^{*}\left( \bigcup_{n=1}^{\infty} A_{n} \right)\geq \mu^{*}\left( \bigcup_{i=1}^{n}A_{i} \right)=\mu^{*}(S_{n})=\sum_{i=1}^{n}\mu^{*}(A_{i})$. So taking $n\to \infty$ we prove one side of the countable additivity: $\mu^{*}\left( \bigcup_{i=1}^{\infty}A_{i} \right)\geq \sum_{i=1}^{\infty}\mu^{*}(A_{i})$. The other side follows by $\sigma$-subadditivity: $\mu^{*}\left( \bigcup_{i=1}^{\infty}A_{i} \right)\leq \sum_{i=1}^{\infty}\mu^{*}(A_{i})$. Indeed, $\mu^{*}$ is a measure on $\mu(\mu^{*})$.

We still need to argue that this gives us the extension that we want on $\mathcal{C}$ (Proof of Caratheodory extension). We need to find an extension on $\sigma(\mathcal{C})$.
We consider the restriction of the outer measure $\mu^{*}$ to $\sigma(\mathcal{C})$ denote it by $\tilde{\mu}$. 
We want to check that $\mu^{*}$ is indeed an extension i.e. that $\tilde{\mu}$ agrees with $\mu$ on $\mathcal{C}$. This is somewhat trivial because for any $A\in\mathcal{C}$ we have $\tilde{\mu}(A)=\mu^{*}(A)=\mu(A)$. 
We also need to check that $\mu^{*}$ is an extension to the entire $\sigma$-field $\sigma(\mathcal{C})\subseteq \mu(\mu^{*})$. Since $\mu(\mu^{*})$ is a $\sigma$-field it suffices to show that $\mathcal{C}\subseteq \mu(\mu^{*})$. That is to say for any $A\in\mathcal{C}$ we know $A$ is measurable ($A\in \mu(\mu^{*})$) i.e. $\mu^{*}(E)\geq\mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})$ for all $E\subset\Omega$. If $\mu^{*}(E)=\infty$ then nothing to prove. WLOG, assume $\mu^{*}(E)<\infty$. For any $E$, by the definition of outer measure there exists a collection of things in $\mathcal{C}$: $\exists E_{1},E_{2},\dots\in\mathcal{C}$ such that $E\subset \bigcup_{i=1}^{\infty}E_{i}$ and $\sum_{i=1}^{\infty}\mu(E_{i})\leq \mu^{*}(E)+\epsilon$. In words we are trying to find a good cover for $E$ of elements in $\mathcal{C}$. Let $B_{n}=E_{n}\cap A$. Note that $E\cap A_{n}\subseteq (\cup E_{i})\cap A=\cup(E_{i}\cap A)$. As $E_{n}\in\mathcal{C},A\in\mathcal{C}\implies B_{n}=E_{n}\cap A\in\mathcal{C}$. Thus, $\mu^{*}(B_{n})=\mu(B_{n})$. Note that $E\cap A^{c}\subseteq \bigcup_{i=1}^{\infty}(E_{n}\cap A^{c})$. Let $C_{n}=E_{n}\cap A^{c}=E_{n}\backslash A$. Because $\mathcal{C}$ is a semialgebra we know $\exists$ finite collection of disjoint elements $\{ C_{n} \}_{n\geq1}\subseteq\mathcal{C}$ such that $E_{n}\backslash A=\bigcup_{i=1}^{m_{n}}C_{n,i}$ . Also $\mu^{*}(C_{n})=\sum_{i=1}^{m_{n}}\mu^{*}(C_{n,i})$. Then $\mu^{*}(E\cap A)+\mu^{*}(E\cap A^{c})\leq \mu^{*}\left( \bigcup_{n=1}^{\infty} (A\cap E_{n}) \right)+\mu^{*}\left( \bigcup_{n=1}^{\infty}(A^{c}\cap E_{n}) \right)\leq \sum_{n=1}^{\infty}\mu^{*}(B_{n})+\sum_{n=1}^{\infty}\mu^{*}(C_{n})$ $=\sum_{n=1}^{\infty}\mu(B_{n})+\sum_{n=1}^{\infty}\sum_{i=1}^{m_{n}}\mu(C_{n,i})=\sum_{n=1}^{\infty}\left( \mu(B_{n})+\sum_{i=1}^{m_{n}}\mu(C_{n,i}) \right)$. Note that $B_{n},\{ C_{n,i} \}$ are all disjoint in $\mathcal{C}$ and $\mu$ is a premeasure on $\mathcal{C}$. Then continuing the equality we have $=\sum_{n=1}^{\infty}\mu(E_{n})\leq \mu^{*}(E)+\epsilon$. Taking $\epsilon$ arbitrarily small completes the proof of showing $A\in \mu(\mu^{*})$ ($A$ is measurable) which implies that $\sigma(\mathcal{C})\subseteq \mu(\mu^{*})$.

Example: Lebesgue-Stieljes measure
$\mu_{F}((a,b])=F(b)-F(a)$ where $F$ is non-decreasing and right continuous. 
$\mathcal{C}=\{ (a,b],(a,\infty): -\infty\leq a<b<\infty \}\cup \{ \emptyset \}$.
Check that $\mathcal{C}$ is a semialgebra. Also check that $\mu_{F}$ is a premeasure on $\mathcal{C}$. By Caratheodory extension, we know how to assign the measure (extend $\mu_{F}$ to $\sigma(\mathcal{C})=\mathcal{B}(\mathbb{R})$ from homework on sets of intervals). We also know that $\mathcal{B}(\mathbb{R})\neq$ the collection of Lebesgue measurable sets denoted $\lambda(\mathbb{R})$. So our natural question: Is $\sigma(\mathcal{C})=\mu(\mu^{*})$? In general no. What does $\mu(\mu^{*})$ have in extra? 
Go back to $\mathcal{B}(\mathbb{R})$, then $\lambda(\mathbb{R})$ has all sets of zero measure which is what it has in addition to $\mathcal{B}(\mathbb{R})$.
Lets clarify this understanding formally.

**Definition (Null sets/sets of zero measure)**: Let $(\Omega,\mathcal{F},\mu)$ be a measure space and $B\subset\Omega$ is a null set if $\exists A\in\mathcal{F}$ such that $B\subseteq A$ and $\mu(A)=0$.

**Definition (complete)**: A measure space $(\Omega,\mathcal{F},\mu)$ is complete if $\mathcal{N}_{\mu}\subseteq\mathcal{F}$. In other words a measure space is complete if every zero-measure (under outer measure) set is measurable.
>Remark: $(\mathbb{R},\mathcal{B}(\mathbb{R}),\lambda)$ is not complete ($\lambda$ is Lebesgue measure)

Continuing, $\mu(\lambda)=\sigma(\mathcal{N}_{\mu}\cup\mathcal{B}(\mathbb{R}))$.
Completion of measure space means $\exists$ a unique smallest $\sigma$-field. $(\Omega,\mathcal{F},\mu)\to(\Omega,\bar{\mathcal{F}},\bar{\mu})$ there exists a unique $(\Omega,\bar{\mathcal{F}},\bar{\mu})$ and the extension from $\mu$ to $\bar{\mu}$ such that this bigger space $(\Omega,\bar{\mathcal{F}},\bar{\mu})$ is complete.
>Note: Completeness will not be on any exams, not that important in the scope of our course.

Next week: 
- Random Variables
	- Measurable maps ($(\Omega,\mathcal{F},\mu)\to(\Omega',\mathcal{F}',\mu')$)
- Afterwards we will look at objects of interest:
	- $\frac{X_{1}+X_{2}+\dots+X_{n}}{n}$
	- $S_{n}=\sum_{i=1}^{k}X_{i}$
	- $\lim_{ n \to \infty }S_{n}$
	- $X+Y$
	- $XY$
	- $lim\inf S_{n}$
