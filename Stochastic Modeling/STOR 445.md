# Probability Review
## Conditional Probability
$$\bp(E | F) = \frac{\bp(E \cap F)}{\bp(F)}$$
Remember that $\bp(E \cap F) \neq \bp(E) \bp(F)$  unless $E \indep F$. 
Note that $\mathbb{P}(E\cap F) = \mathbb{P}(EF)$.
Example: An urn has r red balls, b blue balls. Pick a ball at random and add a balls of that color to the urn. Suppose that this is repeated 3 times. What is the probability a red ball is drawn each pick? 
$E_i$ : the ith draw yields a red ball
Finding $\bp(E_1 E_2 E_3)$. Break it down.
$\bp(E_1E_2E_3) = \bp(E_2E_3|E_1) * \bp(E_1) = \bp(E_3|E_2E_1) * \bp(E_2|E_{1}) * \bp(E_{1})$
$\bp(E_1) = \frac{r}{r+b}$
$\bp(E_{2}|E_{1}) = \frac{r+a}{r+a+b}$
$\bp(E_{3}|E_{1}E_{2}) = \frac{r+2a}{r+2a+b}$

## Law of Total Probability
Let $E_1, E_2, E_3$ be a set of mutually exclusive and exhaustive events. Then for any event $E$, we know $$\bp(E) = \sum_{n=1}^{\infty}$$
Mutually exclusive - events cannot happen at the same time (intersection is empty set)
Exhaustive - the union of the events covers everything that can happen
Example: An urn has r red balls, b blue balls. Pick a ball at random and add a balls of that color to the urn. Suppose that this is repeated 3 times. What is the probability that a red ball is drawn on the second pick?

$E_i$ : the ith draw yields a red ball
$E_1$ and $E_1^c$ are mutually exclusive and exhaustive
Finding $\mathbb{P}(E_{2})$
$\mathbb{P}(E_{2}|E_{1})=\frac{r}{r+a+b}$
$\mathbb{P}(E_{2}|E_{1})=\frac{r+a}{r+a+b}$
$\mathbb{P}(E_{2}|E_{1})*\mathbb{P}(E_{1})+\mathbb{P}(E_{2}|E_{1}^c)*\mathbb{P}(E_1^c)$

## Independence
Events E and F are said to be independent if $\mathbb{P}(EF)=\mathbb{P}(E)*\mathbb{P}(F)$
If $E$ and $F$ are independent then $\mathbb{P}(E|F)=\mathbb{P}(E)$ and $\mathbb{P}(F|E)=\mathbb{P}(F)$

## Random Variables and Distributions
A random variable is a mathematical formalization of a quantity of objects which depend on random events.
A random variable can be expressed as a function from the sample space of an event into the set of real numbers.

## Cumulative Distribution Function (CDF)
The function $\mathbb{P}(X \leq x)$ is called the CDF of a random variable $X$.
Let $F(x) = \mathbb{P}(X\leq x)$. $F(*)$ is a nondecreasing function of x, i.e. $x \leq y \implies F(x) \leq F(y)$. 
Example: Let $X$ denote the lifetime of a bulb with the following CDF: 
$$
F(x) = \begin{cases}
0, & x<0,\\ \\
\frac{x}{100}, & 0 \leq x \leq 100, \\ \\
1, & x > 100
\end{cases}
$$
What is the probability that the bulb lasts more than 10 hours and less than 50 hours?
$$\mathbb{P}(10 \leq X \leq 50) = \mathbb{P}(X \leq 50) - \mathbb{P}(X \leq 10) = F(50)-F(10)=\frac{50}{100}-\frac{10}{100} = 0.4$$

## Discrete Random Variables
A discrete random variable takes values in a countable set, $S = \{x_{1}, x_{2}, \dots, x_{n}\}$. The set doesn't have to be finite, but must be countable.
A discrete random variable has a CDF that jumps at points in $S$. Let $P_k = \mathbb{P}(X=x_{k})$, then $P_{k}=F(x_{k})-F(x_{k-})$ (CDF from the left to $x_{k}$). $P_{k}$ is called the probability mass function (PMF) for $X$.
Some of the commonly used discrete random variables:
1. Bernoulli RV
	$$
X = \begin{cases}
1 &E\ occurs \\
0 &E\ does\ not\ occur
\end{cases}
$$
	- Only two possible outcomes
	- Dependent on $p$, the probability that E occurs
	- PMF: $P_{0} = \mathbb{P}(X=0)=1-p$ and $P_{1} = \mathbb{P}(X=1)=p$
2. Binomial RV
	- Repeat n independent Bernoulli trials
	- $X$ denotes the # of trials that result in event $E$ (success).
	- $P_{k} = \mathbb{P}(X=k)=\binom{n}{k} * p^k*(1-p)^{(n-k)}$. $p^k*(1-p)^{(n-k)}$ is one sequence of getting k successes and $\binom{n}{k}$ is all of the combinations (intuition behind the math).
3. Geometric RV
	- Repeat n independent Bernoulli trials until the first event $E$ occurs (success).
	- $X$ denotes the # of trials needed to observe $E$ for the first time
	- $P_{k}=\mathbb{P}(X=k)=(1-p)^{k-1} * p$.
4. Poisson RV
	- $P_{k} = e^{-\lambda} * \frac{\lambda^{k}}{k!}$

## Continuous Random Variables
These are random variables that can take any value on the real line.
A random variables CDF $F(*)$ is said to be continuous if there exists a function $f(*)$ such that $F(X)=\int_{-\infty}^{x}f(x)dx$ for all $x$. $f(x)$ is called the probability density function (PDF). For a continuous random variable $X$, $\mathbb{P}(X=x)=0$ for any x.
If $F(*)$ is differentiable, then $f(x)=\frac{dF(x)}{dx}$ (derivative of $F(x)$ with respect to x).
Some commonly used continuous random variables:
1. Uniform random variable with parameters $a$ and $b$, $a<b$
	$$
f(x) = \begin{cases}
0 & x < a \\
\frac{1}{b-a} & a \leq x \leq b \\
0 & x > b
\end{cases}
$$

$$
F(x) = \begin{cases}
0 & x < a \\
\frac{x-a}{b-a} & a \leq x \leq b \\
1 & x > b
\end{cases}
$$
2. Exponential random variable with parameter $\lambda > 0$
$$
f(x) = \begin{cases}
0 & x < 0 \\
\lambda e^{-\lambda x} & x \geq{0}
\end{cases}
$$
$$
F(x) = \begin{cases}
0 & x < 0 \\
1-e^{-\lambda x} & x \geq 0
\end{cases}
$$
## Functions of a random variable
Let $X$ be a random variables and let $g(*)$ be a function $Y=g(X)$ is a random variable.
One might be able to determine the distribution of $Y$ given the distribution of $X$. 
Example: $Y$ = $aX+b$. Find $F_{Y}(*)$ given $F_{X}(*)$. Assuming $F_{Y}(*)$ is differentiable find $f_{Y}(*)$.
$F_{Y}(y)=\mathbb{P}(Y\leq y)=\mathbb{P}(aX+b\leq y)=\mathbb{P}\left( X\leq \frac{y-b}{a} \right) \implies f_{Y}(y)=\frac{f_{X}\left( \frac{y-b}{a} \right)}{a}$

## Expectation of Discrete Random Variables
Let $X$ be a discrete random variable with state space $S$ = $\{x_{0}, x_{1}, \dots, \infty\}$. Then $\mathbb{E}X=\sum_{k=0}^{\infty}x_{k}\mathbb{P}(X=x_{k})$. Essentially take each value and multiply it by its probability of occurring and sum.
Example: Suppose $X$ ~ $Binomial(n,p)$. Find $\mathbb{E}X$.
$$\mathbb{E}X=\sum_{k=0}^{n}k\mathbb{P}(X=k)=\sum_{k=0}^{n}k \binom{n}{k}p^{k}(1-p)^{n-k}=\sum_{k=1}^{n} \frac{kn!}{k!(n-k)!}p^{k}(1-p)^{n-k}$$$$=np\sum_{k=1}^{n} \frac{(n-1)!}{(k-1)!(n-k)!}p^{k-1}(1-p)^{n-k}=np\sum_{k=0}^{n} \frac{(n-1)!}{k!(n-k)!}p^{k}(1-p)^{n_{0}k}=np(p+1-p)^{n-1}=np$$
The last step comes from the Binomial expansion form.
Example: Let $X$ ~ $Poisson(\lambda)$. Find $\mathbb{E}X$.
$$
\mathbb{E}X=\sum_{k=0}^{\infty} \frac{ke^{-\lambda}\lambda^{k}}{(k-1)!}=\lambda e^{-\lambda}\sum_{k=1}^{\infty} \frac{\lambda^{k-1}}{(k-1)!}=\lambda e^{-\lambda}\sum_{k=0}^{\infty} \frac{\lambda^{k}}{k!}=\lambda e^{-\lambda}e^{\lambda}=\lambda
$$

## Expectation of a Continuous Random Variable
Let $X$ be a continuous random variable whose PDF is $f(*)$. Then $\mathbb{E}X=\int_{-\infty}^{\infty} xf(x) \, dx$.
Example: $X$ ~ $Unif{(a,b)}$. So $\mathbb{E}X=\int_{a}^{b}xf(x)dx=\int_{a}^{b} \frac{x}{b-a}dx=\frac{x^{2}}{2(b-a)}|_{a}^{b}=\frac{a+b}{2}$.
We can also prove that for a nonnegative continuous random variable $X$, $\mathbb{E}X=\int_{0}^{\infty}(1-F(X))dx$.
Example: $X$ ~ $Exp(\lambda) \implies F(X) = 1-e^{-\lambda x},\ x>0$. So $\mathbb{E}X =\int_{0}^{\infty}(1-F(x))dx=\int_{0}^{\infty}e^{-\lambda x}dx=\frac{1}{\lambda}$.
Let $X$ be a random variable and $Y=g(X)$. Now to find $\mathbb{E}Y$.
$\mathbb{E}Y=\sum_{i}g(x)P_{X}(x_{i})$ if $X$ is a discrete RV or $\mathbb{E}X=\int_{i}g(x)f_{X}(x)dx$ if $X$ is a continuous RV.

## Joint Distributions
Consider a collection of RVs, $X_{1}, X_{2}, \dots, X_{n}$. The function $F(x_{1},x_{2},\dots,x_{n})=\mathbb{P}(X_{1}\leq x_{1},X_{2}\leq x_{2},\dots,X_{n}\leq x_{n})$ for $x_{i}$ element of $(-\infty,\infty),\ 1\leq i \leq n$ is called the joint CDF of $X_{1},X_{2},\dots,X_{n}$.
If $X_{i}$'s are discrete RVs we can define joint PMF as $\mathbb{P}(X_{1}=x_{1},\dots,X_{n}=x_{n})$. If there is a function $f(*)$ such that $F(x_{1},\dots,x_{n})=\int_{-\infty}^{x_{n}}\int_{-\infty}^{x_{n-1}}\dots \int_{-\infty}^{x_{1}}f(u_{1},\dots,u_{n})du_{1}du_{2}\dots du_{n}$ then $X_{1},\dots,X_{n}$ are jointly continuous and $f(*)$ is called the joint PDF.
If $X_{1},\dots,X_{n}$ are discrete RVs then the marginal CDF of $X_{i}$ is $F_{X_{i}}(x_{i})=\mathbb{P}(X_{i}\leq x_{i})=\mathbb{P}(X_{1}\leq \infty, \dots, X_{i}\leq x_{i}, \dots, X_{n} \leq \infty)=F(\infty,\infty,\dots,x_{i},\dots,\infty)$.
If $X_{i}$ is a continuous RV with PDF$f(x_{i})$ then $F_{X_{i}}(x)=\int_{x_{1}}\int_{x_{2}}\dots \int_{x_{i-1}}\int_{x_{i+1}}\dots \int_{x_{n}}f(x_{1},x_{2},\dots,x_{i},\dots,x_n)dx_{1}dx_{2}\dots dx_{n}$ which is the marginal PDF for $X_{i}$.
$X_{1},\dots,X_{n}$ are said to be identically distributed if their marginals CDFs are identical. In other words $F_{X_{1}}(*)=F_{X_{2}}(*)=\dots=F_{X_{n}}(*)$.
Independent of joint distributions: $X_{1},\dots,X_{n}$ are independent if $F(x_{1},\dots,x_{n})=F_{X_{1}}(x_{1})F_{X_{2}}(x_{2})\dots F_{X_{n}}(x_{n})$.

## Sums of Random Variables
