8/18
Data is
- numbers/information typically on a computer
- information on how it was collected (and what it represents)
From data we then generate/formulate a model. A model is a collection of probability distributions represented as $\{ P_{\theta} \}_{\theta \in \Theta}$.
The way to think about it is that these distributions could be somehow used to generate the data.
For example, take a random sample of US voters and ask them if they like cats or dogs more; the data generating process/randomness in distributions here is through the sample.
In modeling we view how the data generating process produces data. Drawn on board as $$
data\;generating\;process \to^{P_{\theta}}data
$$
Statistical inference works as an inverse where you are given the data and want to find the probability distributions that explain the data generating process. Drawn on board as $$
data\to^{statistica\;inference}data\;generating\;process
$$
Where statistical inference is defined as find $\theta$ that is most in agreement with the data.
This class is not about selecting the data generating process/model or how to communicate findings. Mathematical statistics is about statistical inference, so studying the inverse problem of finding the best fitting probability distribution and proving that its good.

Will be learning about:
- Point estimation is about finding one parameter
- Confidence intervals is about finding a set (for uncertainty quantification).
- Hypothesis testing
- Prediction

Notation
- $\mathcal{X}=(X_{1},\dots,X_{n})$ for data
- $\{ f(x|\theta) \}_{\theta \in\Theta}$ for model
- $\mathbb{E}_{\theta}X=\int xf(x|\theta)dx$

Probability theory will be the main tool used

Whereas ML is about prediction, statistics is really about uncertainty quantification which is done using probabilistic language.

Schools of statistics
- Frequentist - relative frequency and repeated experiments (a lot of what we do in this class; think repeated experiments e.g. flipping a coin a bunch and seeing it converges to 1/2 then claiming the coin has probability 1/2 of heads/tails)
	- Confidence Interval
	- Hypothesis Testing (typically)
- Bayesian - subjective beliefs tested on behavior (trying to make sense of the probability e.g. "I believe this will happen with probability 3/4"; a little more "subjective"; One way to think about it though is that if I believe something will happen with probability p, then I should be willing to take bets at that probability payout.)
	- Posterior
	- Credible set
- Fisherian - engineering (understanding the inner working)
	- inner properties of experiment
		- symmetries

8/20
## Basic language of Mathematical Statistics
**Data**: $\mathcal{X}=(X_{1},\dots,X_{n})$ which is a collection of random variables
**Model**: $\{ P_{\theta} \}=\{ f(\mathcal{X}|\theta) \}$ is a collection of probabilities distributions (densities) where $\theta\in\Theta$ and $\Theta$ indexes the model
**Statistic**: $T(\mathcal{X})$ is a function of the data (does not depend on unknown parameters)
- Example: $X_{1},\dots,X_{n}$ iid $N(\mu,\sigma^{2})$ with $\mu\in \mathbb{R},\sigma^{2}>0$. $\bar{X_{n}}=\frac{1}{n}\sum_{i=1}^{n}X_{i}$ is a statistic. On the other hand, $\frac{\bar{X}_{n}-\mu}{\sigma}$ is not a statistic since it depends on unknowns ($\mu$ and $\sigma$). However, when we get to hypothesis testing like $H_{0}: \mu=\mu_{0},H_{1}:\mu\neq \mu_{0}$ and test $Z=\frac{\bar{X}-\mu_{0}}{\frac{S}{\sqrt{ n }}}$ is a statistic because we choose $\mu_{0}$ and $n$ is known and $S$ is given by a formula.
**Identifiability**: The model is identifiable if $\theta_{1}\neq\theta_{2}\implies P_{\theta_{1}}\neq P_{\theta_{2}}$ (essentially with two different parameters we have two different distributions)
- Example: Suppose $\mathcal{X}\sim N(\mu,\Sigma)$ which is definitely identifiable, but $\mathcal{X}=\mu+A\mathbb{Z}$ where $\mathbb{Z}\sim N(0,I)$ then $\mathcal{X}$ is not identifiable because $\Sigma=AA^{T}$ and there are multiple matrix $A$'s which could make the same $\Sigma$ covariance matrix.

Now and next few classes will be on detour to learn tools useful later in the class.

## Transformations
### CDF Method
Suppose normal distribution $X\sim N(\mu,\sigma^{2})$.
For example, what is the distribution of $X^{2}$?
- **CDF method/Direct calculation** is often useful for one variable transformations
So in this example, $$\mathbb{P}(X^{2}<s)=\begin{cases}
0 & s<0 \\
\mathbb{P}(-\sqrt{ s }\leq X\leq \sqrt{ s })=F_{X}(\sqrt{ s })-F_{X}(-\sqrt{ s }) & s\geq0
\end{cases}$$
Then the density of $X^{2}$ can be computed directly from the CDF.
Note indicator function is expressed in this class as $$I_{A}^{(s)}=\begin{cases}
1 & s\in A \\
0 & s\notin A
\end{cases}$$
### Jacobian Method
$\mathcal{X}=(X_{1},\dots,X_{n})\sim f(x)$ (random vector following $f(x)$) where $f(x)$ is a density (with respect to $\lambda$-Lebesgue measure)
The goal is to find $G:\mathcal{X}\to Y$ that is find the distribution of $Y=G(\mathcal{X})$.
Assumptions:
- $A=\{ x:f(x)>0 \}$ is the support of $\mathcal{X}$
- $A$ is partitioned into $A_{0}\cup A_{1}\cup\dots \cup A_{k}$ where $\mathbb{P}(\mathcal{X}\in A_{0})=0$ and for $l=1,\dots,k$ the map $G$ is 1-1 between $A_{l}$ and $B_{l}$ where $B_{l}$ is the range of $G(A_{l})$. Note that it is just 1-1 for each partition, so in the $X^{2}$ example above, even though it isn't 1-1 across the whole $\mathbb{R}$ it is when you partition it into $(-\infty,0)\cup \{ 0 \}\cup(0,\infty)$.
- Let the $l$th inverse be $H_{l}:B_{l}\to A_{l}$
- Jacobian: $J_{l}(y)=\det\left( \frac{\partial \mathcal{X}}{\partial Y} \right)=\det\left[ \frac{\partial(H_{l})_{i}(y)}{\partial y_{j}} \right]_{i,j=1}^{n}$ (look at pic on phone), basically taking partial of $i$th entry of vector $H_{l}(\cdot)$ with respect to $j$th entry of variable of $Y$
Assuming $J_{l}\neq0$ on $B$ for all $l$ then $$
f_{Y}(y)=\sum_{l=1}^{k} f_{\mathcal{X}}(H_{l}(y))|J_{l}(y)|I_{B}
$$
Example: (Polar coordinates)
Suppose vector $(X,Y)\sim f(x,y)$. Now to map to $(R,\theta)$ polar coordinates.
For simplicity, assume support of $X,Y$ is $\mathbb{R}$. Thus, if $A=\mathbb{R}^{2}$ then note the edge cases are difficult such as origin because $R=0$ but any $\theta$ works and also on x-axis we have $\theta=0$ and $\theta=2\pi$ both being the same. To handle this we partition $A$ into $A_{0}=\{ (X,0):x\geq0 \}$, $A_{1}=A\backslash A_{0}$ and we have $B=(0,\infty)\times(0,2\pi)$. Now to find the joint density of $(R,\theta)^{T}$
$\mathbb{P}((X,i)\in A_{0})=0$ (assuming $i\neq0$) and the function $H(r,\theta)=(r\cos\theta,r\sin\theta)$
So we have Jacobian $J=$ $\cos\theta\;,\sin\theta\;,-r\sin\theta\;,r\cos\theta$ as a matrix reading from top left to bottom right.
If $(X,Y)\sim N(0,I)$ ($X,Y$ are iid $N(0,1)$) then we have standard joint density of multiplying two normal's together.
In the case of join density of $(R,\theta)$ we have $$
f_{R,\theta}=\frac{1}{\sqrt{ 2\pi }}e^{-((r\cos\theta)^{2}+(-r\sin\theta)^{2})/2}rI_{(0,\sigma)}(r)I_{(0,2\pi)}(\theta)=e^{-r^{2}/2}rI_{(0,\sigma)}(r) \frac{1}{2\pi}I_{(0,2\pi)}(\theta)
$$
Looking at the factorized example on the last equality we see that $\theta$ follows a uniform distribution.

8/25
### Probability Inverse Transformation
Let $X$ be a random variable: $\{ X(\Omega,\mathcal{F},\mathbb{P})\to(\mathbb{R},\mathcal{B}) \}$ (map from probability space to measurable real line)
The **Cumulative Distribution Function (CDF)** is given by $F_{X}(s)=\mathbb{P}(X\leq s)$.
Recall some properties of the CDF:
1. Uniquely characterizes the distribution of $X$
2. Is right continuous
3. Non-decreasing
4. $F(-\infty)=0,F(\infty)=1$
The "inverse" (quotations because it isn't actually an inverse, but almost is) is given by $$
F^{-}(u)=inf_{s}\{ F(s)\geq u \}
$$
Consider a $u$ such that there exists a $s$ where $F(s)=u$ then this acts like a true inverse. Consider a $u$ that lies within a gap/jump, then the $s$ that satisfies this is the $s$ that makes this jump. The most interesting is picking a $u$ that lies on a flat piece (the function doesn't change in y value), in which case $F^{-}(u)$ gives the left most point $s$ of this flat portion.

Observations from this:
1. $x<F^{-}(u)\implies F(x)<F(F^{-}(u))$
2. $F^{-}(u)\leq x \iff u\leq F(x)$ (note that this is true because of (1) and the fact that CDF is right continuous).

**Lemma**: Let $F$ be a CDF, then the random variable $X=F^{-}(U)$ where $U\sim U(0,1)$ has $F$ as its CDF.
Proof: $\mathbb{P}(X\leq s)=\mathbb{P}(F^{-}(U)\leq s)=\mathbb{P}(U\leq F(s))=F(s)$. Note the second equality comes from (2) above.

**Lemma**: If $X$ has a CDF $F$ with strictly increasing continuous CDF then $F(X)\sim U(0,1)$ ($F(\cdot)$ is 1-1 since strictly increasing so its inverse is an actual inverse). 
Proof: $F(X)=F(F^{-}(U))=U$
>Note: $F$ does **not** have to be strictly increasing for this to hold, it is just convenient for a short proof. The following statement is also true: If $X$ has CDF $F$ that is continuous then $F(X)\sim U(0,1)$ i.e. $F(F^{-}(U))=U$ iff $F$ is continuous.

In a HW we will prove that $\mathbb{P}(F(X)\leq\alpha)\leq\alpha$ for $\alpha\in(0,1)$

**Lemma (from homework)**: $F(F^{-}(u))\geq u$
Think about this as dealing with jumps of $F(\cdot)$ since $F^{-}(u)$ gives us the smallest $x$ such that $F(x) \geq u$, if $u$ is in a jump then the smallest $x$ attains a higher probability than the given probability $u$, thus, $F(F^{-}(u))\geq u$.

**Lemma (from homework)**: $F^{-}(F(x))\leq x$
Think about this as dealing with flat bits of $F(\cdot)$ since we get a probability from $F(x)$ then $F^{-}(\cdot)$ spits back out the minimum $x$ that achieves this probability.

## Inequalities
### Jensen's Inequality
Function $g$ is convex if:
1. $\forall x,y\in \mathcal{D(g)}$, $\lambda\in(0,1)$ it is true that $\lambda x+(1-\lambda)y\in \mathcal{D}(g)$ where $\mathcal{D(g)}$ is the domain of $g$
2. $g(\lambda x+(1-\lambda)y)\leq\lambda g(x)+(1-\lambda)g(y)$
Recall some properties of convex are also that the first derivative is non-decreasing and the second derivative is positive. I.e. $f$ with open and convex domain $\mathcal{D}(f)$ is convex iff:
3. $f(y)\geq f(x)+\nabla f(x)^{T}(y-x),\;\forall x,y\in \mathcal{D(f)}$ (assuming $f$ differentiable)
	1. In $\mathbb{R}$ this is just $f'\text{ non-decreasing}\iff f\text{ convex}$
	2. Thus, $f'\text{ strictly increasing} \iff f\text{ strictly convex}$
4. $\nabla^{2} f(x) \succeq0,\;\forall x\in \mathcal{D}(f)$ (i.e. Hessian PSD assuming $f$ twice differentiable)
	1. In $\mathbb{R}$ this is just $f''\geq0\iff f\text{ convex}$ (Note $f$ convex on some interval $I$ if $f''\geq0$ on interval $I$ even if $f''\not\geq0$ on whole domain)

Function $f$ is concave if:
1. $\forall x,y\in \mathcal{D(f)}$, $\lambda\in(0,1)$ it is true that $\lambda x+(1-\lambda)y\in \mathcal{D}(f)$ where $\mathcal{D(f)}$ is the domain of $f$
2. $f(\lambda x+(1-\lambda)y)\geq\lambda f(x)+(1-\lambda)f(y)$
AKA $f$ is concave if $-f$ is convex

Examples: 
- $aX+b$ is convex and concave
- $g(x)=x^{2}$ is convex
- $g(x)=\sqrt{ x }$ is concave on $(0,\infty)$
- $e^{x}$ is convex
- $|x|$ is convex

**Fact (supporting hyperplane)**: If $g$ is convex on $\mathcal{D}$ then 
1. $g$ is continuous on $\mathcal{D}$
2. $\forall u\in \mathcal{D}\;\exists l(s)$ a linear function s.t. $l(s)\leq g(s)\;\forall s$ and $l(u)=g(u)$ (equal at at least one point)

#### Jensen's Inequality
Let $g$ be a convex function on domain $\mathcal{D}$ and let $X$ be such that $\mathbb{P}(X\in \mathcal{D})=1$. Then $$
g(\mathbb{E}X)\leq \mathbb{E}g(X)
$$provided $\mathbb{E}X$ exists.
Proof: Take a linear function $l(x)$ so that $l(\mathbb{E}X)=g(\mathbb{E}X)$ and $l(s)\leq g(s)\;\forall s\in \mathcal{D}$. Then $g(\mathbb{E}X)=l(\mathbb{E}X)=\mathbb{E}l(X)$ (linearity of expectation) $\leq \mathbb{E}g(X)$ (from fact that $l(s)\leq g(s)$).

>Note: If $g$ is strictly convex, then $g(\mathbb{E}X)<\mathbb{E}g(X)$ iff $\mathbb{P}(X=\mathbb{E}X)<1$ (i.e. random variable is actually random).

Immediate consequences of Jensen's Inequality:
1. $\mathbb{E}X^{2}\geq (\mathbb{E}X)^{2}$ (variance is nonnegative)
2. $\mathbb{E}|X|\geq|\mathbb{E}X|$
3. $\mathbb{E}e^{X}\geq e^{\mathbb{E}X}$
4. $\mathbb{E}\log X\leq \log\mathbb{E}X$
5. $\mathbb{E}\sqrt{ X }\leq \sqrt{ \mathbb{E}X }$

Example: Suppose we have a sequence of positive numbers $a_{1},\dots,a_{n}>0$. Then $\frac{1}{n}\sum_{i=1}^{n}a_{i}=AM$ (arithmetic mean) and $^{n}\sqrt{ \prod_{i=1}^{n} a_{i} }=GM$ (geometric mean). We will prove $AM\geq GM$ using Jensen's.
Let $X$ be a random variable such that $\mathbb{P}(X=a_{i})=\frac{1}{n}$. 
Note $\log(GM)=\log^{n}\sqrt{ \prod_{i=1}^{n} a_{i}}=\frac{1}{n}\sum_{i=1}^{n}\log(a_{i})=\mathbb{E}\log X\leq \log \mathbb{E}X=\log \frac{1}{n}\sum_{i=1}^{n}a_{i}=\log AM$

#### Likelihood ratio and (KL divergence)
Let $X$ be a random variable with density $f$ (with respect to some measure $\mu$). Take some other density $g$ (with respect to the same $\mu$). Lets look at the log likelihood ratio: $$
\log \frac{f(X)}{g(X)}
$$
We have the fact that $$
\mathbb{E}\left( \log \frac{f(X)}{g(X)} \right)\geq0\tag{KL(f||g)>=0}
$$
Proof: $\mathbb{E}\left( -\log \frac{f(X)}{g(X)} \right)=\mathbb{E}\log \frac{g(X)}{f(X)}\leq \log \mathbb{E}\frac{g(X)}{f(X)}=\log \int \frac{g(x)}{f(x)}f(x)dx=\log \int g(x)I_{f(x)>0}dx\leq \log1=0$


**Lemma**: Let $a,b>0$ and $1<p,q<\infty$ such that $\frac{1}{p}+\frac{1}{q}=1$. Then note that $\frac{1}{p}a^{p}+\frac{1}{q}b^{q}\geq ab$ with equality iff $a^{p}=b^{q}$.
Proof: $ab=\exp(\log a+\log b)=\exp\left( \frac{1}{p}\log a^{p}+\frac{1}{q}\log b^{q} \right)\leq \frac{1}{p}\exp(\log a^{p})+\frac{1}{q}\exp(\log b^{q})=\frac{1}{p}a^{p}+\frac{1}{q}b^{q}$Note that the inequality comes from Jensen's with random variable $$
X=\begin{cases}
a^{p} & w.p. \frac{1}{p} \\
b^{q} & w.p. \frac{1}{q}
\end{cases}
$$
8/25
Recall that if $g$ is convex and $\mathbb{P}(X\in \mathcal{D(g)})=1$ then $g(\mathbb{E}X)\leq \mathbb{E}g(X)$ provided that $\mathbb{E}X$ exists.
Also recall Lemma above: $a,b>0$ and $0<p,q<\infty, \frac{1}{p}+\frac{1}{q}=1$ then $\frac{1}{p}a^{p}+\frac{1}{q}b^{q}\geq ab$ with equality iff $a^{p}=b^{q}$.

**Definition**: For $X$ and $p\geq1$ we define $$
||X||_{p}=\;\sqrt[p]{\mathbb{E}|X|^{p}}
$$

**Theorem (Holder's Inequality)**: Let $1<p,q$ such that $\frac{1}{p}+\frac{1}{q}=1$ and let $X,Y$ be random variables so that $\mathbb{E}|X|^{p}<\infty,\mathbb{E}|Y|^{q}<\infty$. Then $$
|\mathbb{E}XY|\leq \mathbb{E}|XY|\leq||X||_{p}||Y||_{q}
$$
>Note: This inequality holds for $p,q\geq1$ as well, but the proof is slightly different. Just need other p/q that isn't 1 to be infinity norm.

Proof: Let $a=\frac{|X|}{||X||_{p}}$ and $b=\frac{|Y|}{||Y||_{q}}$. Our inequality from Lemma above states that $$
\frac{1}{p} \frac{|X|^{p}}{||X||_{p}^{p}}+\frac{1}{q} \frac{|Y|^{q}}{||Y||_{q}^{q}}\geq \frac{|X|}{||X||_{p}} \frac{|Y|}{||Y||_{q}}
$$
Then taking expectation gives $$
\frac{1}{p} \frac{\mathbb{E}|X|^{p}}{||X||_{p}^{p}}+\frac{1}{q} \frac{\mathbb{E}|Y|^{q}}{||Y||_{q}^{q}}\geq \frac{\mathbb{E}|XY|}{||X||_{p}|Y||_{q}} 
$$
Note that the fractions on left side cancel thus giving $$
1=\frac{1}{q}+\frac{1}{p}\geq \frac{\mathbb{E}|XY|}{||X||_{p}||Y||_{q}}\implies \mathbb{E}|XY|\leq||X||_{p}||Y||_{q}
$$
>Comment: We have equality iff $\frac{|X|^{p}}{||X||_{p}^{p}}=\frac{|Y|^{q}}{||Y||_{q}^{q}}$ as $|X|^{p}=c|Y|^{q}$ a.s. for some $c\neq0$ (namely $c=\frac{||X||_{p}^{p}}{||Y||_{q}^{q}}$)

An important case is $p=q=2$ which says $|\mathbb{E}XY|\leq \sqrt{ \mathbb{E}X^{2}\mathbb{E}Y^{2} }$ which is called Cauchy-Schwartz inequality.

>Note for next inequality that the inequality itself isn't that important, but the trick used in proving it is used all the time.

Recall that $f$ is nondecreasing if $x\leq y\implies f(x)\leq f(y)$ and nonincreasing is $x\leq y\implies f(x)\geq f(y)$.
**Theorem**: Let $X$ be a random variable and $f,g$ be the functions such that $\mathbb{E}|f(X)|,\mathbb{E}|g(X)|,\mathbb{E}|f(X)g(X)|<\infty$. Then if $f,g$ are both nondecreasing/nonincreasing then $$\mathbb{E}f(X)\mathbb{E}g(X)\leq \mathbb{E}f(X)g(X)$$
Proof: Take random variable $X$ and let $Y$ be an independent copy i.e. $X\overset{d}{=}Y$ and $X\perp\!\!\!\perp Y$. Then we have $\mathbb{E}f(X)=\mathbb{E}f(Y)$ comes from equal in distribution and $\mathbb{E}f(X)g(Y)=\mathbb{E}f(X)\mathbb{E}g(Y)$ comes from independence. **This is the important step/method to take note of.**
We have $(f(X)-f(Y))(g(X)-g(Y))\geq0$ due to $g,f$ both being nonincreasing/nondecreasing. Now we take expectation and have $0\leq \mathbb{E}[(f(X)-f(Y))(g(X)-g(Y))]=\mathbb{E}f(X)g(X)-\mathbb{E}f(X)g(Y)-\mathbb{E}f(Y)g(X)+\mathbb{E}f(Y)g(Y)$
We know that the first and fourth term are equal (similarly 2,3 terms) due to equal in distribution. Thus, we have $2\mathbb{E}f(X)g(Y)\leq2\mathbb{E}f(X)g(X)\implies \mathbb{E}f(X)\mathbb{E}g(Y)\leq \mathbb{E}f(X)g(X)\implies \mathbb{E}f(X)\mathbb{E}g(X)\leq \mathbb{E}f(X)g(X)$. The key to the inequality here is that the $\mathbb{E}f(\cdot)g(\cdot)$ cannot be separated where $\cdot=X\text{ or } Y$, but the term where we have $X$ and $Y$ we can separate due to independence.
>Note: If $f$ is nondecreasing/nonincreasing and $g$ is nonincreasing/nonincreasing respectively (flipped instead of matching) then the inequality just flips.

### Markov Inequality
For non-negative r.v. $X$ and some constant $t>0$, we have
$$
\mathbb{P}(X\geq t) \leq \frac{\mathbb{E}X}{t}
$$
Proof: $\mathbb{P}(X\geq s)=\mathbb{E}\mathbb{I}_{\{ X\geq s \}}(X)\leq \mathbb{E} \frac{X}{s} \mathbb{I}_{\{ X\geq s \}}\leq \mathbb{E} \frac{X}{s}=\frac{\mathbb{E}X}{s}$
	Note the first inequality above comes from the fact that $\frac{X}{s}\geq1$ which was the value of indicator when $X\geq s$ on left hand side.
>Note: (From doing homework) Markov Inequality holds with equality iff $X\in \{ 0,t \}\;\text{a.s.}$ The probabilities on $\{ 0,t \}$ are unconstrained i.e. $\mathbb{P}(X=t)=p$ for any $p\in[0,1]$ since $\frac{\mathbb{E}X}{t}=\frac{pt}{t}=p=\mathbb{P}(X\geq t)$.
### Chernoff's Inequality
Let $X$ be a random variable and $t>0$. Then $$
\mathbb{P}(X\geq t)\leq \inf_{s>0} \frac{\mathbb{E}e^{sX}}{e^{st}}
$$
Proof: $\mathbb{P}(X\geq t)=\mathbb{P}(sX\geq st)=\mathbb{P}(e^{sX}\geq e^{st})\leq \frac{\mathbb{E}e^{sX}}{e^{st}}$. Since this holds for every $s>0$ we can just take an infimum.

### Moment Generating Function
$$
M_{X}(s)=\mathbb{E}e^{sX},\;s\in \mathbb{R}
$$
No matter what $M_{X}(0)=1$. We say the moment generating function exists if $\exists\epsilon>0$ such that  $M_{X}(s)<\infty$ for all $|s|\leq\epsilon$. (i.e. MGF is finite for some neighborhood of 0)

Recall that $e^{sX}=\sum_{k=0}^{\infty} \frac{(sX)^{k}}{k!}$. Thus, $\mathbb{E}e^{sX}=M_{X}(s)=\mathbb{E}\sum_{k=0}^{\infty} \frac{(sX)^{k}}{k!}=\sum_{k=0}^{\infty} \frac{s^{k}\mathbb{E}X^{k}}{k!}$ Note that the last equality here comes from Fubini's Theorem and the fact that $|s|<\epsilon\implies \mathbb{E}e^{s|X|}\leq \mathbb{E}(e^{sX}+e^{-sX})<\infty$ (which powers Fubini).
**Fact from analysis**: $M_{X}(s)$ is determined by knowing $\mathbb{E}X^{k}$ for all $k$.

We also know that $M_{X}'(s)=\frac{d}{ds}\sum_{k=0}^{\infty} \frac{s^{k}\mathbb{E}X^{k}}{k!}=\sum_{k=1}^{\infty} \frac{ks^{k-1}\mathbb{E}X^{k}}{k!}=\mathbb{E}\sum_{k=1}^{\infty} \frac{s^{k-1}X^{k}}{(k-1)!}=\mathbb{E}X\sum_{k=1}^{\infty} \frac{s^{k-1}X^{k-1}}{(k-1)!}=\mathbb{E}Xe^{sX}$. 
Now if $s=0$ then all terms for $k>1$ will disappear. Thus, $M_{X}'(0)=\mathbb{E}X$. This generalizes to $$M_{X}^{(k)}(0)=\mathbb{E}X^{k}$$
**Fact**: If $X,Y$ both have the same MGF $M(s)$ (assuming it exists) then $X\overset{d}{=}Y$.

9/1
**MGFs continued**
Recall that $\mathbb{E}e^{sX}=M_{X}(s)=\mathbb{E}\sum_{k=0}^{\infty} \frac{(sX)^{k}}{k!}=\sum_{k=0}^{\infty} \frac{s^{k}\mathbb{E}X^{k}}{k!}$
Consequently $$\frac{d^{k}}{ds^{k}}M_{X}(s)=\mathbb{E}X^{k}e^{sX}$$
Notice that
1. $\mathbb{E}X^{k}=M_{X}^{(k)}(0)$
2. $M_{X}^{(2)}(s)=\mathbb{E}X^{2}e^{sX}\geq0\implies M_{X}(s)$ convex. If $X$ is not zero almost surely, then $M_{X}(s)$ is strictly convex.

Example
$X\sim Pois(\lambda)$ then $M_{X}(s)=e^{\lambda(e^{s}-1)}$ for all $s\in \mathbb{R}$
Proof: $\mathbb{E}e^{sX}=\sum_{x=0}^{\infty}e^{sx} \frac{\lambda^{x}e^{-\lambda}}{x!}=e^{-\lambda} \sum_{x=0}^{\infty} \frac{(\lambda e^{s})^{x}}{x!}=e^{-\lambda}e^{\lambda e^{s}}$

Example
$X\sim Exp(\lambda)$ then $M_{X}(s)=\frac{\lambda}{\lambda-s}$ for $s<\lambda$
Proof: $\mathbb{E}e^{sX}=\int_{0}^{\infty}e^{sx}\lambda e^{-\lambda x}dx=\lambda\int_{0}^{\infty} e^{(s-\lambda)x}dx$. So if $s<\lambda$ then $e^{(s-\lambda)x}\to0$, but if $s\geq\lambda$ then the integral $\to \infty$ and remember MGFs must be finite to "exist".

Example (**MGF Linear Transformation**)
Suppose $Y=aX+b$ then $$M_{Y}(s)=\mathbb{E}e^{(aX+b)s}=e^{bs}\mathbb{E}e^{asX}=M_{X}(as)e^{bs}$$

Example
Suppose $Z\sim N(0,1)$ then $M_{Z}(s)=e^{s^{2}/2}$. Consequently, if $X\sim N(\mu,\sigma^{2})$ then $M_{X}(s)=e^{\mu s+(\sigma^{2}s^{2}/2)}$
Proof: $X=\mu + \sigma Z$ then using linear transformation above we just need $M_{Z}(s)$.
$M_{Z}(s)=\mathbb{E}e^{sZ}=\int_{-\infty}^{\infty}e^{sz} \frac{1}{\sqrt{ 2\pi }}e^{-z^{2}/2} dz= \frac{1}{\sqrt{ 2\pi }}\int_{-\infty}^{\infty}e^{-z^{2}/2+sz}dz=\frac{1}{\sqrt{ 2\pi }}\int_{-\infty}^{\infty}e^{-(z-s)^{2}/2}e^{s^{2}/2}dz$ (complete the square) $=e^{s^{2/2}}\int_{-\infty}^{\infty} \frac{e^{-(z-s)^{2}/2}}{\sqrt{ 2\pi }}dz$ and recognize that this integral is the density of a $N(s,1)$ variable so we know it evaluates to 1, thus, $M_{Z}(s)=e^{s^{2}/2}$. 

>**Important Fact**: If $X,Y$ have the same MGF ($M_{X}(s)=M_{Y}(s)\;\forall|s|<\epsilon$) then $X\overset{d}{=}Y$.

#### Sum of i.i.d. RVs MGF
**Proposition**: Let $Y_{1},\dots,Y_{n}$ be independent with MGF $M_{Y_{i}}(s)$ then $$
S=\sum_{i=1}^{n} Y_{i}
$$ has MGF $M_{S}(s)=\prod_{i=1}^{n}M_{Y_{i}}(s)$.
Proof: $M_{S}(s)=\mathbb{E}e^{s(Y_{1}+\dots+Y_{n})}=\mathbb{E}(e^{sY_{1}}e^{sY_{2}}\dots e^{sY_{n}})=\mathbb{E}e^{sY_{1}}\mathbb{E}e^{sY_{2}}\dots \mathbb{E}e^{sY_{n}}$.

#### (Back to) Chernoff's Bound
Recall Chernoff's Bound: If $X$ has a MGF then $\mathbb{P}(X\geq t)\leq\inf\limits_{s>0}e^{st}M_{X}(s)$ with $t>0$
Examples
If $X\sim Exp(\lambda)$. We know $\mathbb{P}(X>t)=\int_{t}^{\infty}\lambda e^{-\lambda x}dx=e^{-\lambda t}$. Lets see how close Chernoff's bound comes: $\inf\limits_{s>0} e^{-st} \frac{\lambda}{\lambda-s}$ for $s<\lambda$. Note $\frac{d}{ds} \left( e^{-st} \frac{\lambda}{\lambda-s} \right)=-te^{-st} \frac{\lambda}{\lambda-s}+e^{-st} \frac{\lambda}{(\lambda-s)^{2}}=\left( e^{-st} \frac{\lambda}{\lambda-s} \right)\left( \frac{1}{\lambda-s} -  t \right)=0\implies s=\lambda-\frac{1}{t}$ we need $t > \frac{1}{\lambda}$ (since $s>0$).
Thus, $\inf\limits_{s>0} e^{-t(\lambda-1/t)} \frac{\lambda}{\lambda-\left( \lambda-\frac{1}{t} \right)}=e^{-\lambda t}(et\lambda)$ if $t > \frac{1}{\lambda}$. So we can see that the additional "price we pay" above the actual value ($e^{-\lambda t}$ is $et\lambda$).

Example
Suppose $Z\sim N(0,1)$. Fact (will prove in homework):$$
\mathbb{P}(Z>t)\leq\frac{1}{\sqrt{ 2\pi t^{2} }} e^{-t^{2}/2},\;t>0
$$
For Chernoff's bound: $\mathbb{P}(Z>t)\leq \inf\limits_{s>0} e^{-st}M_{Z}(s)=\inf\limits_{s>0} e^{-st+s^{2}/2}=e^{-t^{2}/2}$ for $t>0$. We can see that the minimum is attained at $s=t$.
These bounds are typically used for large $t$ i.e. in the tails (note for $0<t<1$ Chernoff's is better, but we don't really care because we care about the tails).

Some cousins of MGF that are useful:
#### Cumulant Generating Functions (CGF)
$$
K_{X}(s)=\log M_{X}(s)
$$
The derivatives of CGF are called cumulants: $\mathcal{K}_{k}=\frac{d^{k}}{ds^{k}}K_{X}(s)|_{s=0}$.
Check for yourself that the first cumulant $\mathcal{K}_{1}=\mathbb{E}X$ and $\mathcal{K}_{2}=\mathrm{Var}(X)=\sigma^{2}$ and $\mathcal{K}_{3}=$ skewness.

#### Characteristic Function
$$
\phi_{X}(s)=\mathbb{E}e^{isX}=M_{X}(is),\;i=\sqrt{ -1 }
$$
This is useful because if $sx$ is real then we have $e^{isx}=\cos(sx)+i\sin(sx)\implies|e^{isx}|=1$. Characteristic functions are nice because they don't explode, but MGFs can explode.

## Concentration Inequalities
Recall (one) CLT for $X_{1},X_{2},\dots$ iid with $\mathbb{E}X=\mu$ and $\mathrm{Var}(X)=\sigma^{2}<\infty$. Then we have $\frac{\bar{X}_{n}-\mu}{\frac{\sigma}{\sqrt{ n }}} \to Z\sim N(0,1)\implies \mathbb{P}(\frac{\bar{X}_{n}-\mu}{\frac{\sigma}{\sqrt{ n }}}>t)\to \mathbb{P}(Z>t)$. We see that we have a bound on how far the sample mean is from the deviation around the mean: $\mathbb{P}\left( \frac{\bar{X}_{n}-\mu}{\frac{\sigma}{\sqrt{ n }}}>t \right)=\mathbb{P}\left( \bar{X}_{n}>\mu + \frac{t\sigma}{\sqrt{ n }} \right)$

Often people are interested in large deviations. set $\mu=0,\sigma=1$ then we have $\mathbb{P}(\bar{X}_{n}>t)=\mathbb{P}\left( \frac{\bar{X}_{n}-0}{\frac{1}{\sqrt{ n }}} >t\sqrt{ n } \right) \not\to \mathbb{P}(Z>t\sqrt{ n })$. Note the **not** converges to because we can't just plug in $n$ because it goes to infinity and the CLT works by pointwise comparison and only letting $n$ go to infinity on the left side of $\mathbb{P}(\sqrt{ n }\bar{X}_{n}>x)\to \mathbb{P}(Z>x)$ (where convergence is true).

# Take Notes from homework like MGF of $X^{2}$

9/3
### Hoeffding's Inequality
Recall Chernoff's: $\mathbb{P}(X\geq t)\leq \inf\limits_{s>0} e^{-st}M_{X}(s)$
**Lemma**: $X$ random variable s.t. $\mathbb{E}X=0$ and has support $a\leq X\leq b$. Then $\mathbb{E}e^{sX}\leq e^{\frac{s^{2}(b-a)^{2}}8}$.
>Note: Hoeffding's isn't tighter than Chernoff's (since we are bounding MGF above), but it is easier to use than Chernoff's because it comes "out of the box" ready.

Proof: By convexity we know $e^{sX}\leq \frac{b}{b-a}e^{sa}-\frac{a}{b-a}e^{sb}$.
Call $-\frac{a}{b-a}=p$. Then the above becomes $e^{sX}\leq((1-p)+pe^{s(b-a)})e^{sa}=((1-p)+pe^{s(b-a)})e^{-p(b-a)s}$
Now call $u=s(b-a)$ and rename above as $e^{\phi(u)}$ where $\phi(u)=-pu+\log(1-p+pe^{u})$.
Notice $\phi(0)=0$ and $\phi'(0)=-p+\frac{pe^{u}}{(1-p)+pe^{u}}|_{u=0}=0$ and $\phi''(u)=\frac{pe^{u}}{(1-p)+pe^{u}}-\frac{(pe^{u})^{2}}{[(1-p)+pe^{u}]^{2}}=\gamma(1-\gamma)$ with $\gamma\in[0,1]$ which means $\phi''(u)\leq \frac{1}{4}$ since at worst case $\gamma=\frac{1}{2}$.
Note $\phi(u)=\phi(0)+u\phi'(0)+\frac{u^{2}\phi''(s)}{2}$ where $s\in[0,u]$ which implies $\phi(u)\leq \frac{u^{2}}{8}$.
Thus, $e^{sX}\leq \frac{e^{s^{2}(b-a)^{2}}}{8}$

Now to actually proof Hoeffding's.
Let $X_{1},X_{2},\dots$ be independent such that $a_{i}\leq X_{i}\leq b_{i}$ (w.p. 1)
Then for all positive $t$ we have $$
\mathbb{P}(S_{n}-\mathbb{E}S_{n}\geq t)\leq \exp\left( -\frac{2t^{2}}{\sum_{i=1}^{n} (b_{i}-a_{i})^{2}} \right)
$$
Where $S_{n}=\sum_{i=1}^{n}X_{i}$.

Proof: $\mathbb{P}(S_{n}-\mathbb{E}S_{n}\geq t)\leq \inf\limits_{s>0}e^{-st}\mathbb{E}e^{s\sum_{i=1}^{n}(X_{i}-\mathbb{E}X_{i})}=\inf\limits_{s>0}e^{-st}\prod_{i=1}^{n}\mathbb{E}e^{s(X_{i}-\mathbb{E}X_{i})}\leq \inf\limits_{s>0}e^{-st} \exp\left( \frac{s^{2}}{8} \sum_{i=1}^{n}(b_{i}-a_{i})^{2}\right)$. So if we take $s= \frac{4t}{\sum_{i=1}^{n}(b_{i}-a_{i})^{2}}$ we get $\mathbb{P}(S_{n}-\mathbb{E}S_{n}\geq t)\leq \exp\left( -\frac{4t^{2}}{\sum_{i=1}^{n}(b_{i}-a_{i})^{2}} \right) \exp\left( \frac{2t^{2}}{\sum_{i=1}^{n}(b_{i}-a_{i})^{2}} \right)=\exp\left( -\frac{2t^{2}}{\sum_{i=1}^{n}(b_{i}-a_{i})^{2}} \right)$.

Note we can get the same bound in the reverse direction by applying to $-X_{i}$, but since we have $(b_{i}-a_{i})^{2}=(a_{i}-b_{i})^{2}$ we get the same bound: $$
\mathbb{P}(S_{n}-\mathbb{E}S_{n}\leq t)\leq \exp\left( -\frac{2t^{2}}{\sum_{i=1}^{n} (b_{i}-a_{i})^{2}} \right)
$$
Thus we have $$
\mathbb{P}(|S_{n}-\mathbb{E}S_{n}|\geq t)\leq 2 \exp\left( -\frac{2t^{2}}{\sum_{i=1}^{n} (b_{i}-a_{i})^{2}} \right)
$$
Example:
Let $X_{1},\dots,X_{n}$ be independent $\text{Bernoulli}(p)$ (note they don't all have to have the same p, but in this example we will use same p). Then $\mathbb{E}X_{i}=p$ and $0\leq X_{i}\leq1$. Thus, we have $\mathbb{P}\left( \sum_{i=1}^{n}X_{i}-np\geq t \right)\leq \exp\left( -\frac{2t^{2}}{n} \right)\implies \mathbb{P}\left( \frac{1}{n}\sum_{i=1}^{n}X_{i}-p \geq s \right)=\mathbb{P}\left( \sum X_{i}-np\geq ns \right)\leq e^{-2s^{2}n}$ (since this is true for all $t$ we can multiply by finite $n$).

Example:
Let $X_{1},\dots,X_{n}$ be iid $U(-\theta,\theta)$ thus $\mathbb{E}X_{i}=0$ and $-\theta\leq X_{i}\leq\theta$.
Thus, $\mathbb{P}\left( \frac{1}{n}\sum X_{i}\geq s \right)=\mathbb{P}\left( \sum X_{i}\geq ns \right)\leq \exp\left( -\frac{2(ns)^{2}}{n(2\theta)^{2}} \right)=\exp\left( -\frac{ns^{2}}{2\theta^{2}} \right)$.

>Note: Hoeffding's bound only depends on the support, not variance which seems to be wasteful. I.e. if a random variable was very concentrated in the support we would expect convergence(?) to mean much faster.

### Bennet-Bernstein Inequality
Idea is same as Hoeffding's: bound $M_{X}(s)$
Take r.v. $X$ s.t. $\mathbb{E}X=0,\mathbb{E}X^{2}=\sigma^{2},|X|\leq c$.
$\mathbb{E}e^{sX} = \mathbb{E}\left( 1+sX+\sum_{r=2}^{\infty} \frac{s^{r}X^{r}}{r!} \right)=1+0+\sum_{r=2}^{\infty} \frac{s^{r}\mathbb{E}X^{r}}{r!}$ (i)
$\mathbb{E}X^{r}\leq \mathbb{E}|X^{r}|\leq\mathbb{E}X^{2}c^{r-2}$
So continuing (i) above we now have $\leq1+\sum_{r=2}^{\infty} \frac{\sigma^{2}s^{r}c^{r-2}}{r!}=1+\frac{\sigma^{2}}{c^{2}} \sum_{r=2}^{\infty} \frac{(sc)^{r}}{r!} = 1+\frac{\sigma^{2}}{c^{2}} (e^{sc}-1-sc)\leq \exp\left( \frac{\sigma^{2}}{c^{2}}( e^{sc}-1-sc) \right)$ from fact $1+x\leq e^{x}$.

Let $X_{1},\dots,X_{n}$ be independent with $\mathbb{E}X_{i}=0,\mathbb{E}X_{i}^{2}=\sigma_{i}^{2},|X_{i}|\leq c$ for $t>0$ we have $\mathbb{P}\left( \sum_{i=1}^{n}X_{i}\geq t \right)\leq \inf\limits_{s>0}e^{-st}\prod_{i=1}^{n}\mathbb{E}e^{sX_{i}}\leq\inf\limits_{s>0}e^{-st}\exp\left( \frac{\sum_{i=1}^{n}\sigma_{i}^{2}}{c^{2}}( e^{sc}-1-sc)n \right)$
We need to find the optimal $s=\frac{1}{c} \log\left( 1+\frac{tc}{\sum \sigma_{i}^{2}} \right)$ 

**Theorem (Bennet's Inequality)**:
Given iid $X_{1},\dots,X_{n}$ with $\mathbb{E}X_{i}=0,\mathrm{Var}(X_{i})=\sigma_{i}^{2},|X_{i}|\leq c$. Then for all $t>0$ we have $$
\mathbb{P}\left( \sum_{i=1}^{n} X_{i}\geq t \right)\leq \exp \left( \frac{\left( -\sum_{i=1}^{n} \sigma_{i}^{2}\right)}{c^{2}}h\left( \frac{ct}{\sum\sigma_{i}^{2}} \right)\right)
$$
where $h(u)=(1+u)\log(1+u)-u$.

Observe that $h(u)\geq \frac{u^{2}}{2+ \frac{2u}{3}}$ for all $u\geq0$.

**Corollary (Bernstein's)**:
Under the same assumptions as Bennet's we have $$
\mathbb{P}\left( \sum_{i=1}^{n} X_{i}\geq t \right)\leq \exp\left( -\frac{t^{2}}{2\sum_{i=1}^{n} \sigma_{i}^{2}+\frac{2ct}{3}} \right)
$$
Example:
$X_{1},\dots,X_{n}$ are iid Bernoulli($p$) (using Bernstein's)
So getting $\mathbb{E}X_{i}=0$ we shift by $p$: $Y_{i}=X_{i}-p\implies c=max(p,1-p)$ (since $-p\leq X_{i}-p\leq1-p$).
Then $\mathbb{P}\left( \frac{1}{n}\sum_{i=1}^{n}X_{i}-p\geq t \right)=\mathbb{P}\left( \sum_{i=1}^{n}Y_{i}\geq nt \right)\leq \exp\left( -\frac{n^{2}t^{2}}{2np(1-p)+\frac{2}{3}max(p,1-p)nt} \right)=\exp\left( -\frac{nt^{2}}{2p(1-p)+\frac{2}{3}max(p,1-p)t} \right)$
>Notice if $p=\frac{1}{2}$ then we have $\exp\left( -\frac{nt^{2}}{\frac{1}{2}+\frac{t}{3}} \right)$ is not that great because this is definitely worse than Hoeffding's. However, if $p$ is close to 0 or 1 then the same inequality will be much nicer/better than Hoeffding's because the denominator is much smaller making entire expression much larger and since negative the exp($\cdot$) is much closer to 0.


9/8
### Sub-gaussian RVs
Let $X$ be a random variable such that $\mathbb{P}(|X|\geq t)\leq ae^{-bt^{2}}$. This tells us that the tails of $X$ decay with rate $e^{-bt^{2}}$. This has a name: **Sub-Gaussian Random Variable**. We call $b$ a variance proxy (recall Gaussian decays at $e^{-\sigma^{2}t^{2}/2}$) so $b$ takes on form of $\frac{\sigma^{2}}{2}$ in a Normal RV.
Then for $t>0$ $$\mathbb{E}|X|\leq \sqrt{ \frac{1+\log a}{b}}$$
Proof: $\mathbb{E}|X|^{2}=\int_{0}^{\infty}\mathbb{P}(X^{2}\geq t)dt=\int_{0}^{s}\mathbb{P}(X^{2}\geq t)dt+\int_{s}^{\infty} \mathbb{P}(X^{2}\geq t)dt\leq s+ \int_{s}^{\infty} ae^{-bt}=s+\frac{-ae^{-bt}}{b}|_{t=s}^{\infty}=s+\frac{a}{b} e^{-bs}$. Now we pick the best $s$ which is $s=\frac{\log a}{b}$. Thus, we have $\mathbb{E}|X|^{2}\leq \frac{\log a}{b}+\frac{1}{b}$. And from Jensen's we know $(\mathbb{E}|X|)^{2}\leq \mathbb{E}X^{2}\implies \mathbb{E}|X|\leq \sqrt{ \frac{1+\log a}{b} }$.

Tail integral: For RV $X>0$ we have $\mathbb{E}X=\int_{0}^{\infty} \mathbb{P}(X\geq t)dt$.
Proof: $\mathbb{E}X=\int_{0}^{\infty}xf(x)dx=\int_{0}^{\infty}\int_{0}^{x}dsf(x)dx=\int_{0}^{\infty}\int_{0}^{\infty} \mathbb{I}_{s<x}f(x)dsdx=\int_{0}^{\infty}\int_{s}^{\infty}f(x)dx ds=\int_{0}^{\infty}\mathbb{P}(X\geq s)ds$.

### Sample Mean & Sample Variance
Recall for $X_{1},\dots,X_{n}$ the sample mean is $\bar{X}_{n}=\frac{1}{n}\sum_{i=1}^{n}X_{i}$ and sample variance is $S_{n}^{2}=\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\bar{X}_{n})^{2}$. We will assume that $X_{1},\dots,X_{n}$ are independent, $\mathbb{E}X_{i}=\mu,\mathrm{Var}(X_{i}=\sigma^{2})$ and statements about $S^{2}$ we will assume $\mathbb{E}(X_{i}-\mu)^{3}=\mu_{3},\mathbb{E}(X_{i}-\mu)^{4}=\mu_{4}$ (third and fourth central moments respectively).
#### Properties
**Theorem**: $\mathbb{E}\bar{X}_{n}=\mu,\mathrm{Var}(\bar{X}_{n})=\frac{\sigma^{2}}{n}$.
Proof: we have properties of expectation.

**Theorem**: $\mathbb{E}S_{n}^{2}=\sigma^{2}$, $\mathrm{Var}(S_{n}^{2})=\frac{1}{n}\left( \mu_{4}- \frac{n-3}{n-1}\sigma^{4} \right)$

**Lemma**: $S_{n}^{2}=\frac{1}{2n(n-1)}\sum_{i=1}^{n}\sum_{j=1}^{n}(X_{i}-X_{j})^{2}=\frac{1}{2n(n-1)}\sum \sum_{i\neq j}(X_{i}-X_{j})^{2}$
Proof: $\sum_{i=1}^{n}\sum_{j=1}^{n}(X_{i}-X_{j})^{2}=\sum_{i=1}^{n}\sum_{j=1}^{n}((X_{i}-\bar{X})-(X_{j}-\bar{X}))^{2}$ $=\sum_{i=1}^{n}\sum_{j=1}^{n}[(X_{i}-\bar{X})^{2}-2(X_{i}-\bar{X})(X_{j}-\bar{X})+(X_{j}-\bar{X})^{2}]$
$=n\sum_{i=1}^{n}(X_{i}-\bar{X})^{2}-2\sum_{i=1}^{n}(X_{i}-\bar{X})\sum_{j=1}^{n}(X_{j}-\bar{X})+n\sum_{j=1}^{n}(X_{j}-\bar{X})^{2}$
$=2n\sum_{i=1}^{n}(X_{i}-\bar{X})^{2}$ (middle term above goes to zero and combine first and last term)
Result follows by multiplying both sides by constant $\frac{1}{2n(n-1)}$.

Proof (of sample variance expectation):
$\mathbb{E}S_{n}^{2}=\frac{1}{2n(n-1)}\sum \sum_{i\neq j}\mathbb{E}(X_{i}-X_{j})^{2}$
Note that $\mathbb{E}(X_{i}-X_{j})^{2}=\mathbb{E}[(X_{i}-\mu)^{2}-2(X_{i}-\mu)(X_{j}-\mu)+(X_{j}-\mu)^{2}]=\mathrm{Var}(X_{i})+\mathrm{Var}(X_{j})=2\sigma^{2}$
Thus we have $\mathbb{E}S_{n}^{2}=\frac{1}{2n(n-1)}\sum \sum_{i\neq j}\mathbb{E}(X_{i}-X_{j})^{2} =\frac{1}{2n(n-1)}(n(n-1)2\sigma^{2})=\sigma^{2}$. (second to last inequality comes from fact there are only $n(n-1)$ nonzero terms where $i\neq j$).

**Theorem**: $\mathrm{Cov}(\bar{X}_{n},S_{n}^{2})=\frac{\mu_{3}}{n}$
Proof: $\mathrm{Cov}(\bar{X}_{n},S_{n}^{2})=\mathrm{Cov}\left( \frac{1}{n}\sum_{i=1}^{n}X_{i}, \frac{1}{2n(n-1)}\sum \sum_{k\neq j}(X_{k}-X_{j})^{2} \right)$
$=\mathrm{Cov}\left( \frac{1}{n}\sum_{i=1}^{n}(X_{i}-\mu), \frac{1}{2n(n-1)}\sum \sum_{k\neq j}(X_{k}-\mu+\mu-X_{j})^{2} \right)$
$=\frac{1}{2n^{2}(n-1)}\sum_{i=1}^{n}\sum_{j=1}^{n}\sum_{k=1}^{n}\mathrm{Cov}(X_{i}-\mu,(X_{j}-\mu)^{2}-2(X_{j}-\mu)(X_{k}-\mu)+(X_{k}-\mu)^{2})$
$=\frac{1}{2n^{2}(n-1)}\sum_{i=1}^{n}\sum_{j=1}^{n}\sum_{k=1}^{n}\mathbb{E}(X_{i}-\mu)(X_{j}-\mu)^{2} -2\mathbb{E}(X_{i}-\mu)(X_{j}-\mu)(X_{k}-\mu)+\mathbb{E}(X_{i}-\mu)(X_{k}-\mu)^{2}$
Now note that $$\mathbb{E}(X_{i}-\mu)(X_{j}-\mu)(X_{k}-\mu)=\begin{cases}
\mu_{3} & \text{if }i=j=k \\
0 & o.w.
\end{cases}$$because if $i\neq j$ or $j\neq k$ or $i\neq k$ then one of these is independent so we can factor out but $\mathbb{E}(X_{i}-\mu)=0$.
Using this logic on the terms above we have the final equality:
$=\frac{1}{2n^{2}(n-1)}(n^{2}\mu_{3}-2n\mu_{3}+n^{2}\mu_{3})$ (note the $n^{2}$ terms come from the fact that for every $i=j$ we have another n terms from the k sum)
$=\frac{1}{2n^{2}(n-1)}2n(n-1)\mu_{3}=\frac{\mu_{3}}{n}$.
A similar argument follows for proving $\mathrm{Var}(S_{n}^{2})$, but with more terms. I.e. we would have $$
\mathbb{E}(X_{i}-\mu)(X_{j}-\mu)(X_{k}-\mu)(X_{l}-\mu)=\begin{cases}
\mu_{4} & i=j=k=l \\
\sigma^{4} & \text{exactly 2 are equal and other 2 equal }i=j\neq k=l
\end{cases}
$$
>Note: For symmetric (about its mean) random variables the sample mean and sample variance are uncorrelated (because $\mu_{3}=0$ so $\mathrm{Cov}(\bar{X}_{n},S_{n}^{2}=0)$). So if our random variable is skewed then the sample mean and variance are correlated.

**Theorem**: Suppose $X_{1},\dots,X_{n}$ are iid $N(\mu,\sigma^{2})$. Then
1. $\bar{X}_{n}\sim N\left( \mu, \frac{\sigma^{2}}{2} \right)$
2. $\bar{X}_{n}\perp\!\!\!\perp S_{n}^{2}$
3. $\frac{(n-1)S_{n}^{2}}{\sigma^{2}}\sim \chi_{n-1}^{2}$ (Chi-squared with $n-1$ d.o.f.)

9/10
## Order Statistics
$X_{1},\dots,X_{n}\in \mathbb{R}$
Then the order statistics are $X_{(1)}=min(X_{1},\dots,X_{n})$, $X_{(2)}$ is second smallest, etc. with $X_{(n)}=max(X_{1},\dots,X_{n})$.

Note some properties:
1. $X_{(1)}\leq\dots\leq X_{(n)}$
2. If $(X_{1},\dots,X_{n})$ is continuous (has a joint density with respect to a Lebesgue measure i.e. jointly continuous), then $X_{(1)}<X_{(2)}<\dots<X_{(n)}$.

Consider $X_{1},\dots,X_{n}$ iid. (Note if there is dependence then order statistics "lose" some information, but with iid nothing is really lost, just reshuffled).
$F_{X_{(r)}}(s)=\mathbb{P}(X_{(r)}\leq s)=\mathbb{P}(\text{at least r of the Xs }\leq s)=\sum_{k=r}^{n}\mathbb{P}(\text{exactly k}\leq s)$
$=\sum_{k=r}^{n} \binom{n}{k} F_{X}(s)^{k}(1-F_{X}(s))^{n-k}$ where $F_{X}(s)=\mathbb{P}(X_{1}\leq s)$ is CDF of all $X_{i}$'s as iid.

If additionally, $X_{1},\dots,X_{n}$ are iid continuous with density $f_{X}(s)$, then $$
f_{X_{(r)}}(s)=\frac{d}{ds} F_{X_{(r)}}(s)=\sum_{k=r}^{n} \binom{n}{k} [kF_{X}(s)^{k-1}f_{X}(s)(1-F_{X}(s))^{n-k}-(n-k)F_{X}(s)^{k}(1-F_{X}(s))^{n-k-1}f_{X}(s)]
$$
This looks bad, but then we notice it is telescoping.
Note that $k \binom{n}{k}=n \binom{n-1}{k-1}$ and $(n-k)\binom{n}{k}=n \binom{n-1}{k}$
Thus, simplifying above we have $$
\sum_{k=r}^{n} nf_{X}(s)\left[\binom{n-1}{k-1}F_{X}(s)^{k-1}(1-F_{X}(s))^{n-k}-\binom{n-1}{k}F_{X}(s)^{k}(1-F_{X}(s))^{n-k-1}\right]
$$
$$
=n \binom{n-1}{r-1}F_{X}(s)^{r-1}(1-F_{X}(s))^{n-r}f_{X}(s)
$$

Next consider the joint distribution of $(X_{(1)},\dots,X_{(n)})$. Getting the CDF is very messy because you have to consider the joint ways you can organize the order statistics into buckets. I.e. For some set of constants (that would be plugged into the joint CDF) $x_{1},\dots,x_{n}$ you need at least one order statistic to be less than $x_{1}$, at least 2 to be less than $x_{2}$, etc.
**Try yourself just for n=3**. From brief discussion of approach in class you have many combinations within the buckets so for 1,1,1 it would be $3!F(X_{1})(F(x_{2})-F(x_{1}))(F(x_{3})-F(x_{2}))$

Things get much easier if $X_{1},\dots,X_{n}$ are iid continuous with density $f_{X}(s)$.
Recall the joint density of the original data is $f_{X_{1},\dots,X_{n}}(x_{1},\dots,x_{n})=\prod_{i=1}^{n}f_{X}(x_{i})$.
The joint density of the order statistics is $f_{X_{(1)},\dots,X_{(n)}}(x_{1},\dots,x_{n})=n!\prod_{i=1}^{n}f_{X}(x_{i})\mathbb{I}_{\{ x_{1}<x_{2}<\dots<x_{n} \}}$.
Think about it as the original density doesn't care when we reshuffle, but all that is really happening is we condition on landing in the $i$th previous regions iteratively which is where the indicator comes from and then integrating this gives us $\frac{1}{n!}$ so we need $n!$ as an integrating constant to still get valid density.

Assume $X_{1},\dots,X_{n}$ are iid continuous with density $f$.
The joint density between $X_{(i)},X_{(j)}$ for $i<j$ is $$
f_{X_{(i)},X_{(j)}}(s,v)=\frac{n!}{(i-1)!(j-i-1)!(n-j)!}F(s)^{i-1}(F(v)-F(s))^{j-i-1}(1-F(v))^{n-j}f(s)f(v)\mathbb{I}_{\{ s<v \}}
$$
Sketch of proof for simply remembering:
One could think of a density as being $f_{X_{(i)},X_{(j)}}(s,v)dsdv \approx \mathbb{P}(X_{(i)}\in(s,s+ds),X_{(j)}\in(v,v+dv))$
Think about it as this will happen if we have $i-1$ observations before s, $j-i-1$ observations in between $s+ds$ and $v$ and then $n-j$ observations after $v+dv$. This gives us our leading constant of factorials (as all different ways to order the observations). Then for the $i-1$ observations we need them below $s$, hence $F(s)^{_{i-1}}$ and then the one observation for $i$ which is $f(s)$ and similar logic follows for $(1-F(v))^{n-j}$ for the $n-j$ observations above $v$, the one observation at $j$ as $f(v)$ and the $(F(v)-F(s))^{j-i-1}$ is for the $j-i-1$ observations in between.

Example:
Let $X_{1},\dots,X_{n}$ be iid with some density $f(x)$.
What is the joint distribution of $(M,R)$ which is the midrange and range respectively i.e. $R=X_{(n)}-X_{(1)},M= \frac{X_{(1)}+X_{(n)}}{2}$?
First calculate $f_{X_{(1)},X_{(n)}}(u,v)=\frac{n!}{(n-2)!}(F(v)-F(u))^{n-2}f(s)f(v)\mathbb{I}_{\{ u<v \}}$ from formula above.
Then we can just use Jacobian method for transformation to $R,M$.
We have $X_{(1)}=M-\frac{R}{2}$ and $X_{(n)}=M+\frac{R}{2}$
Thus our Jacobian is $$J=\det 
\begin{pmatrix}
1 & \frac{1}{2} \\
1 & -\frac{1}{2}
\end{pmatrix}=-1$$
Thus we have $f_{M,R}(m,r)=f_{X_{(1)},X_{(n)}}\left( m-\frac{r}{2},m+\frac{r}{2} \right)|-1|=n(n-1)[]$ **fill out rest from phone**

Now lets make the above example concrete by making them all be $U(0,1)$. Then $f(s)=\mathbb{I}_{(0,1)}(s)$
and $F(s)=s$ for $0\leq s\leq1$. Then we have $$f_{M,R}(m,r)=n(n-1)\left[ m+\frac{r}{2}-\left( m-\frac{r}{2} \right) \right]^{n-2}\mathbb{I}_{(0,1)}\left( m+\frac{r}{2} \right)\mathbb{I}_{(0,1)}\left( m-\frac{r}{2} \right)\mathbb{I}_{\{ r>0 \}}$$
$$
=n(n-1)r^{n-2}\mathbb{I}_{(0,1)}(r)\mathbb{I}_{\left( \frac{r}{2},1-\frac{r}{2} \right)}(m)
$$
We are able to condense the above indicators by examining the inequalities they produce: $0<m+\frac{r}{2}<1,0<r,0<m-\frac{r}{2}<1$.

What is $M|R=r$? It follows $U\left( \frac{r}{2},1-\frac{r}{2} \right)$ as seen by the fact that the only term involving $m$ is an indicator.
What is the distribution of $R$? $f_{R}(r)=\int f_{M,R}(m,r)dm=n(n-1)r^{n-2}\int_{\frac{r}{2}}^{1-r/2}dm\mathbb{I}_{(0,1)}(r)=n(n-1)r^{n-2}(1-r)\mathbb{I}_{(0,1)}(r)$ which is a beta distribution namely $Beta(n-1,2)$.

Up next is typical families of distributions.

9/15
### Exponential Families
Families are useful for isolating certain structures and proving properties & theorems about these structures/families.

Suppose we have family of probability densities $\mathcal{P}=\{ f_{\theta}:\theta\in\Theta \}$, where $f_{\theta}$ is density or mass function (on $\mathbb{R}$ or $\mathbb{R}^{p}$).

**Definition (Exponential family)**: The family $\mathcal{P}$ is an exponential family if for some integer $k$ we can write $$f_{\theta}(x)=h(x)\exp\left( \sum_{i=1}^{k}w_{i}(\theta)T_{i}(x)-c(\theta) \right)$$
Where we have :
- $h:X\to[0,\infty)$
- $w_{i}:\Theta\to \mathbb{R}$
- $c:\Theta\to \mathbb{R}$
- $T_{i}:X\to \mathbb{R}$
>Note sometimes this is written differently as $f_{\theta}(x)=h(x)\exp(w^{T}(\theta)T(x)-c(\theta))$ where $w$ and $T$ are vectors.

Example 1: Binomial distribution at fixed n
$\mathcal{P}=\{ Bin(n,\theta) \}:0<\theta<1$ so naturally we have $X\in \{ 0,1,\dots,n \}$.
$f_{\theta}(x)=\binom{n}{x}\theta^{x}(1-\theta)^{n-x}=\binom{n}{x}(1-\theta)^{n}\left( \frac{\theta}{1-\theta} \right)^{x}=\binom{n}{x}\exp\left[ x\log\left( \frac{\theta}{1-\theta} \right)+n\log(1-\theta) \right]$
We can see that this is an exponential family with $k=1$, $h(x)=\binom{n}{x}$,$w_{1}(\theta)=\log\left( \frac{\theta}{1-\theta} \right)$,$T_{1}(x)=x$,$c(\theta)=-n\log(1-\theta)$
>Note for statistics, what really matters are the $T_{i}$'s as they carry the information about the actual values e.g. number of coin flips. Will go into more depth later.

Example 2: Poisson distribution
$\mathcal{P}=\{ Pois(\theta):\theta>0 \}$
$X=\{ 0,1,\dots \}$
$f_{\theta}(x)=\frac{\theta^{x}e^{-\theta}}{x!}=\frac{1}{x!}\exp(x\log\theta-\theta)$ so $k=1$ again
$h(x)=\frac{1}{x!}$
$w_{1}(\theta)=\log\theta$
$T_{1}(x)=x$
$c(\theta)=\theta$

Example 3: Normal with unknown mean and variance
$\mathcal{P}=\{ N(\mu,\sigma^{2}):\mu\in \mathbb{R},\sigma^{2}>0 \}$
$\theta=(\mu,\sigma^{2})$
$f(x;\mu,\sigma^{2})=\frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)=\frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{\mu^{2}}{2\sigma^{2}}\right)\exp\left( \frac{\mu x}{\sigma^{2}}-\frac{x^{2}}{2\sigma^{2}} \right)$
So we have $k=2$
$h(x)=1$
$w_{1}(\mu,\sigma^{2})=\frac{\mu}{\sigma^{2}}$
$w_{2}(\mu,\sigma^{2})=-\frac{1}{2\sigma^{2}}$
$T_{1}(x)=x$
$T_{2}(x)=x^{2}$
$c(\mu,\sigma^{2})=\frac{\mu^{2}}{2\sigma^{2}}+\frac{1}{2}\log(2\pi\sigma^{2})$

We can see that $f_{\theta}(x)\propto h(x)\exp\left( \sum_{i=1}^{k}T_{i}(x)w_{i}(\theta) \right)$ so we can always find $\exp(c(\theta))$ by the fact that $f_{\theta}(x)$ should integrate/sum to 1: $$1=\int_{\mathbb{R}}f_{\theta}(x)dx=e^{-c(\theta)}\int_{\mathbb{R}}h(x)e^{w^{T}(\theta)T(x)}dx\implies c(\theta)=\log\left[ \int_{\mathbb{R}}h(x)e^{w^{T}(\theta)T(x)}dx \right]$$
>Note that in exponential families the support never depends on parameter $\theta$, only on $x$. This can be seen by the fact that $h(x)$ may be 0 at some points. So for example, the distribution $U(0,\theta)$ can never be represented as an exponential family because the support depends on $\theta$.

**Proposition**: Let $X_{1},\dots,X_{n}$ be iid with common distribution/mass function in an exponential family. Then $(X_{1},\dots,X_{n})$ also belongs to an exponential family.
Proof: Let $g_{\theta}(x_{1},\dots,x_{n})$ be the joint density. Then we have $$g_{\theta}(x_{1},\dots,x_{n})=\prod_{j=1}^{n}f_{\theta}(x_{j})=\prod_{j=1}^{n}h(x_{j})\exp\left(w^{T}(\theta)T(x_{j})-c(\theta) \right)=\left( \prod_{j=1}^{n}h(x_{j}) \right)\exp\left( \sum_{i=1}^{n}w^{T}(\theta)T(x_{j})-nc(\theta) \right)$$
So is this an exponential family? Yes!
$h(x) = \prod_{j=1}^{n}h(x_{j})$
$w(\theta)=w(\theta)$
$T(x)=\sum_{i=1}^{n}T(x_{j})$
$c(\theta)=nc(\theta)$

### Natural Exponential Family and Natural Parameter Space
Fix $h:X\to[0,\infty)$ and $T:X\to \mathbb{R}^{k}$
Define $G(\eta)=\int_{X}h(x)e^{\eta^{T}T(x)}dx$ where $\eta\in \mathbb{R}^{k}$
So we want some density $$f_{\eta}(x)=\frac{h(x)\exp(\eta^{T}T(x))}{G(\eta)}=h(x)\exp(\eta^{T}T(x)-A(\eta))$$ where $A(\eta)=\log G(\eta)$.
Something of this form is a natural exponential family.

**Definition (Natural Parameter Space)**: The natural parameter space is defined as $\mathcal{H}=\{ \eta\in \mathbb{R}^{k}: 0<G(\eta)<\infty\}$.

**Definition**: $\mathcal{P}=\{ f_{\eta}: \eta\in \mathcal{H} \}$ is the exponential family generated by $h$ and $T$.

Example: Normal distribution (unknown $\mu$ and $\sigma^{2}$)
Recall from above that $f(x;\mu,\sigma^{2})=\frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{\mu^{2}}{2\sigma^{2}}\right)\exp\left( \frac{\mu x}{\sigma^{2}}-\frac{x^{2}}{2\sigma^{2}} \right)$ with $h(x)=1,T_{1}(x)=x,T_{2}(x)=x^{2},w_{1}(\theta)=\frac{\mu}{\sigma^{2}},w_{2}(\theta)=-\frac{1}{2\sigma^{2}},c(\theta)=\frac{\mu^{2}}{2\sigma^{2}}+\frac{1}{2}\log(2\pi\sigma^{2})$
So now if we want to get this into natural form we take $\eta_{1}=\frac{\mu}{\sigma^{2}}$ and $\eta_{2}=-\frac{1}{2\sigma^{2}}$ and get $$
f_{\eta}(x)=\exp(\eta_{1}x+\eta_{2}x^{2}-A(\eta_{1},\eta_{2}))
$$
where $A(\eta_{1},\eta_{2})=\log \int_{\mathbb{R}}\exp(\eta_{1}x+\eta_{2}x^{2})dx$. Thus we have $\mathcal{H}=\mathbb{R}\times (-\infty,0)$ as the $\mathbb{R}$ represents $\eta_{1}$ and $(-\infty,0)$ for $\eta_{2}$.

**Theorem**:  Let $h,T$ generate a natural exponential family, then $\mathcal{H}\subseteq \mathbb{R}^{k}$ is convex and $A:\mathcal{H}\to \mathbb{R}$ is a convex function.
Proof: Fix $\eta_{0},\eta_{1}\in \mathcal{H}$ and some constant $\alpha\in(0,1)$. Intuition is that $\mathcal{H}$ is defined such that $G(\eta)$ is finite, so taking convex combination of finite should be finite.
Define $U(x)=\exp(\alpha \eta_{0}^{T}T(x))$ and $V(x)=\exp((1-\alpha)\eta_{1}^{T}T(x))$.
Then $G(\alpha \eta_{0}+(1-\alpha)\eta_{1})=\int_{\mathbb{R}^{p}}U(x)V(x)h(x)dx$
Now using Holder's inequality with $p=\frac{1}{\alpha},q=\frac{1}{1-\alpha}\implies \frac{1}{p}+\frac{1}{q}=1$ we have $$
G(\alpha \eta_{0}+(1-\alpha)\eta_{1})=\int_{\mathbb{R}^{p}}U(x)V(x)h(x)dx\leq\left( \int_{\mathbb{R}^{p}}U(x)^{1/\alpha}h(x)dx \right)^{\alpha}\left( \int_{\mathbb{R}^{p}}V(x)^{1/(1-\alpha)}h(x)dx \right)^{1-\alpha}
$$ Note in this equation that $U(x)^{1/\alpha}=G(\eta_{0})$ and $V(x)^{1/(1-\alpha)}=G(\eta_{1})$
Thus continuing the above quality we have $$
=G(\eta_{0})^{\alpha}G(\eta_{1})^{1-\alpha}<\infty
$$Since $\eta_{0},\eta_{1}\in \mathcal{H}\implies G(\eta_{0}),G(\eta_{1})<\infty$. Thus, $G(\alpha \eta_{0}+(1-\alpha)\eta_{1})<\infty\implies\alpha \eta_{0}+(1-\alpha)\eta_{1}\in \mathcal{H}$ proving $\mathcal{H}$ is convex.
Additionally, taking logarithms on both sides of $G(\alpha \eta_{0}+(1-\alpha)\eta_{1})\leq G(\eta_{0})^{\alpha}G(\eta_{1})^{1-\alpha}$ we get $$
A(\alpha \eta_{0}+(1-\alpha)\eta_{1})\leq\alpha A(\eta_{0})+(1-\alpha)A(\eta_{1})
$$which is the definition of convexity. Thus, $A$ is convex.