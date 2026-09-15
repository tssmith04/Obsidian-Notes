---
aliases:
  - Queueing Theory, Renewal Processes, 642, Queues, M/G/1, G/M/1, M/M/1
---

# Introduction to Queueing Models
January 8
Examples of queues:
- Security checkpoints at airports
- Emergency Departments
- Call centers
- Communication networks
- Manufacturing systems
- Transplant waiting lists

## Description of a Single-station Queueing System (Kendall's Notation)
Need to know a few things to explain. Note that single-station just indicates that there is one station that jobs/clients show up to and then get processed and leave. There can be multiple servers at one station, but think about the station being the store itself.
1. The arrival process (described with letters)
	- $M$: Exponential (Markovian) interarrival times
	- $E_{k}$ : Erlang(Sum of k iid exp RVs)
	- $D$ : Deterministic
	- PH : Phase-type
	- $G$ : General (arrival process not specific)
2. Service Times (same letter specification as arrival process)
3. Number of servers (typically denoted by $S$, but could be any integer)
4. System capacity (max allowed number of customers in the system at any time)
5. Service discipline (sequence with which the customers are served)
	- Typically understood to be first come first server (FCFS)
	- Last come first server (LCFS)
	- Random
	- PS (processor sharing)
We use the numbers 1-5 above to describe a queue 1/2/3/4/5 i.e. interarrival distribution/service distribution/number of servers/system capacity/service discipline. If capacity is not specified we assume it is infinite.
Example: M/M/5 is a queue where arrivals follow a Poisson process, service times are exponential, there are 5 servers, and infinite capacity.
Example: M/G/4/20/LCFS is a queue with Poisson arrivals, general service times, 4 servers, 20 capacity, and last come first server discipline.

## Notation
- $X(t)$ : number of customers in the system at time t ($\{X(t), \ t \geq 0\}$ is a continuous time stochastic process)
- $X_{n}$ : number of customers in the system just after the nth customer departs ($\{X_{n}, n\geq{0}\}$ is a discrete time stochastic process)
- $X_{n}^{*}$ : number of customers in the system just before the nth customer enters the queue
- $\hat{X_{n}}$ : number of customers in the system just before the nth customer arrives
	- Note that if there is infinite capacity then $X_{n}^{*}$ and $\hat{X_{n}}$ will be the same
	- Note that if there is a capacity limit k then $X_{n}^{*}$ would only consider customers who are able to join the queue (so if someone arrives and the capacity is full then the customer will leave and $X_{n}^{*}$ would not be affected, but $\hat{X_{n}}$ would be updated since this was an arrival)
- $W_{n}$ : time spent by the nth customer in the system
- For $j=1,2,\dots$
	- $P_{j}=\lim_{ t \to \infty } \mathbb{P}(X(t)=j)$
	- $\Pi_{j}=\lim_{ n \to \infty }\mathbb{P}(X_{n}=j)$
	- $\Pi_{j}^{*}=\lim_{ n \to \infty }\mathbb{P}(X_{n}^{*}=j)$
	- $\hat{\Pi_{j}}=\lim_{ n \to \infty }\mathbb{P}(\hat{X_{n}}=j)$
	- $F(x)=\lim_{ n \to \infty }\mathbb{P}(W_{n}\leq x)$ for $x \in [0,\infty)$
	- $L=\lim_{ t \to \infty }\mathbb{E}[X(t)]$
	- $W=\lim_{ n \to \infty }\mathbb{E}[W_{n}]$
	- All of these can also be interpreted as long run averages. For example, $P_{j}$ is the long-run proportion of time there are j customers in the system. $\Pi_{j}$ is the long run proportion of departures who leave behind j customers. Limits as defined above may not exist, but even when they don't the long-run averages exist. When we use superscript "q" in notation above, we are referring to the queue alone, excluding customers who may be in service. Example: $\hat{X_{n}^{q}}$ is the number of customers in the queue (waiting, not in service) at the time of nth customers arrival
## Properties of General Queueing Systems
### Relationship between $\Pi_{j}^{*}$ and $\hat{\Pi_{j}}$
Let $I_{n}$=1 if nth arriving customer enters, 0 otherwise
And $\alpha=\lim_{ n \to \infty }\mathbb{P}(I_{n}=1)$ and $\alpha_{j}=\lim_{ n \to \infty }\mathbb{P}(I_{n}=1|\hat{X_{n}}=j)$ for $j \geq 0$ assuming the limits exist.
#### Theorem 7.1
Suppose $\alpha > 0$ and either one of the limits that define $\hat{\Pi_{j}}$ and $\Pi_{j}^{*}$ exists. Then the other limit also exists and $$\frac{\alpha_{j}}{\alpha}\Pi_{j}^{*}=\hat{\Pi_{j}}, \ j\geq0 \tag 1$$
Proof: Define $N(n)=\sum_{i=1}^{n}I_{i}, \ n\geq 0$. This sum represents the number of customers who join among the first $n$ arrivals. Then $\mathbb{P}(I_{n}=1|\hat{X_{n}}=j)$ (probability that conditioned on the nth arriving customer seeing j customers, the nth customer joins) $*\mathbb{P}(\hat{X_{n}}=j)$ $$=\mathbb{P}(\hat{X_{n}}=j, I_{n}=1)=\mathbb{P}(\hat{X}_{n}=j|I_{n}=1)\mathbb{P}(I_{n}=1)=\mathbb{P}(X_{N(n)}^{*}=j|I_{n}=1)\mathbb{P}(I_{n}=1)$$
Now let $n\to \infty$ on both sides, assuming one of the limits exist we get $\alpha_{j}\hat{\Pi_{j}}=\alpha \Pi_{j}^{*}$. Then the result follows.
If $\sum_{j=0}^{\infty}\Pi_{j}^{*}=1$, then $\alpha=\sum_{j=0}^{\infty}\alpha_{j}\hat{\Pi_{j}}$ and then $$\Pi_{j}^{*}=\frac{\alpha_{j}\hat{\Pi_{j}}}{\sum_{i=0}^{\infty}\alpha_{i}\hat{\Pi_{i}}} \tag{key equation}$$
If $\alpha_{j}=1$, i.e. all arriving customers enter, then $\Pi_{j}^{*}=\hat{\Pi_{j}}, \forall j\geq 0$.

### Relationship between $\Pi_{j}^{*}$ and $\Pi_{j}$
#### Theorem 7.2
If customers enter and depart the queue one at a time, and either one of the $$\Pi_{j}=\lim_{ n \to \infty }\mathbb{P}(X_{n}=j)$$ or $$\Pi_{j}^{*}=\lim_{ n \to \infty }\mathbb{P}(X_{n}^{*}=j)$$ exists, then the other limit also exists and $$\Pi_{j}^{*}=\Pi_{j}, \forall j\geq 0$$
Proof: (Little different from the one in the book)
Define the following:
- $e_{n}(t)$ : number of unit upward jumps from state n occurring in (0,t)
- $d_{n}(t)$ : number of unit downward jumps to state n occurring in (0,t)
Since jumps are of size $\pm1$, we have $|e_{n}(t)-d_{n}(t)| \leq 1$ (we must return back to state n in order to jump from it again i.e. $e_{n}(t)$ goes up, must increase $d_{n}(t)$ in order to potentially increase $e_{n}(t)$ again).
Now we define:
- $e(t)$ : number of arrivals until t
- $d(t)$ : number of departures until t
Then we see $X(t) = X(0) + e(t) - d(t) \implies d(t) = e(t)+X(0)-X(t)$
Thus, $\frac{d_{j}(t)}{d(t)}=\frac{e_{j}(t)+d_{j}(t)-e_{j}(t)}{e(t)+X(0)-X(t)}$.
Recall that $d_{j}(t)-e_{j}(t)$ is bounded by 1. Note that $X(0)-X(t)$ is also bounded (due to limits existing).
Then assuming $\Pi_{j}=\lim_{ t \to \infty } \frac{d_{j}(t)}{d(t)}$ exists, we set $\lim_{ t \to \infty } \frac{d_{j}(t)}{d(t)}=\lim_{ t \to \infty } \frac{e_{j}(t)}{e(t)} = \Pi_{j}^{*}$.
In summary, what the departing customer and arriving customers see (of the system) is the same if customers arrive and leave one by one. (The proof fails if customers can arrive in batches, since this would make $e_{n}(t)-d_{n}(t)$ no longer bounded by 1).

### Relationship between $\hat{\Pi_{j}}$ and $p_{j}$ (PASTA)
PASTA: Poisson Arrivals See Time Averages
#### Theorem 7.3
If the arrival process is Poisson then $\hat{\Pi_{j}}=p_{j},\;j\geq 0$ when either one of the limits $\hat{\Pi_{j}}$ or $p_{j}$ exists.

Example: Our results imply that for the M/G/1 queue, we have $\hat{\Pi_{j}}=\Pi_{j}^{*}$ (since all arriving customers enter the system; i.e. no max capacity) = $\Pi_{j}$ (since arrival and departures happen 1 by 1) = $p_{j}$ (since arrivals are Poisson).
Example: For the G/M/1 queue, we have $\hat{\Pi_{j}}=\Pi_{j}^{*}=\Pi_{j}$ but $\hat{\Pi_{j}}\neq p_{j}$ (since arrivals are not Poisson).
Example: Consider the M/M/1/1 queue with $\lambda$ as the arrival rate and $\mu$ as the service rate. (Simple 2 state CTMC). We can show that $p_{0}=\frac{\mu}{\lambda+\mu}$ and $p_{1}=\frac{\lambda}{\lambda+\mu}$. Then we also know from PASTA, that $\hat{\Pi_{0}}=p_{0}$ and $\hat{\Pi_{1}}=p_1$. However, $\Pi_{0}=\Pi_{0}^{*}=1$ and $\Pi_{1}=\Pi_{1}^{*}=0$ since arriving customers must arrive to an empty system and when a customer leaves they leave the system empty. Thus, customers cannot arrive or depart with 1 person in the system (hence probability 0 for $\Pi_{1}=\Pi_{1}^{*}$).

### Little's Law (Theorem 7.5)
$X(t)$: number of customers in the system at time t
$A(t)$: number of arrivals over (0,t)
$W_{n}$: time spent in the system by the nth customer (waiting time + service time)
Define the following:
- $L = \lim_{ t \to \infty } \frac{\int_{0}^{t}X(n)dn}{t}$
- $\lambda=\lim_{ t \to \infty } \frac{A(t)}{t}$ (arrival rate)
- $W=\lim_{ n \to \infty } \frac{\sum_{k=1}^{n}W_{n}}{n}$ (expected time in system)
#### Theorem
Suppose that the second and third limits above exist (namely $W$ and $\lambda$). Then, the first limit also exists and is given by $L=\lambda W$. (Intuitively arrival rate * expected time in system = long run number of people in system).

Proof: Let $S_{0}$ = 0, $D_{0}=0$ and define
- $S_{n}$: the arrival time of the nth customer for $n\geq 1$
- $D_{n}$: the departure time of the nth customer for $n\geq 1$
- $A(t)$: number of arrivals over (0,t]
- $D(t)$: number of departures over (0,t]
Assuming, WLOG, $X(0)=0$. Define $W_{n}=D_{n}-S_{n}$. We have $$X(t)=\sum_{n=1}^{\infty} I(S_{n}\leq t\leq D_{n})$$$$A(t)=sup\{n\geq 0:S_{n}\leq t\}$$
$$D(t) = sup\{n\geq 0 : D_{n} \leq t\}$$
$$
X(t)=A(t)-D(t)
$$
Existence of the limits imply $\frac{X(t)}{t}\to 0$ with probability 1 (this requires proof, but we skip it; its in the book). Thus, $\lim_{ t \to \infty } \frac{D(t)}{t} = \lim_{ t \to \infty } \frac{A(t)-X(t)}{t} = \lambda$ (since $\frac{X(t)}{t}\to 0$). 
Thus, $\sum_{n=1}^{D(t)}W_{n} \leq \int_{0}^{t}X(n)dn\leq \sum_{n=1}^{A(t)}W_{n}\implies$(multiply by $\frac{1}{t}$) to get $$
\frac{D(t)}{t} \frac{\sum_{n=1}^{D(t)}W_{n}}{D(t)}\leq \frac{\int_{0}^{t}X(n)dn}{t}\leq \frac{A(t)}{t} \frac{\sum_{n=1}^{A(t)}W_{n}}{A(t)} \tag{1}
$$
Assume $A(t)\to \infty$ as $t\to \infty\implies D(t)\to \infty$ as $t\to \infty$. Thus, $\lim_{ t \to \infty } \frac{1}{D(t)}\sum_{n=1}^{D(t)}W_{n}=\lim_{ t \to \infty } \frac{1}{A(t)}\sum_{n=1}^{A(t)}W_{n}$. Letting $t\to \infty$ in (1) we get $\lambda W\leq L\leq\lambda W\implies L=\lambda W$.
This leads to an important result of $L_{q}=\lambda W_{q}$ (expected number in the queue = expected waiting time in the queue).

## Birth and Death Queues
Recall the birth and death process from CTMCs
Transition rate from state i to i+1 is $\lambda_{i}$
Transition rate from state i to i-1 is $\mu_{i}$
Barrier at 0
Let $\rho_{0}=1$ and $$\rho_{n}=\frac{\lambda_{0}\lambda_{1}\dots\lambda_{n-1}}{\mu_{1}\mu_{2}\dots \mu_{n}} \tag{6.74}$$
The chain is positive recurrent if and only if $\sum_{n=0}^{\infty}\rho_{n}<\infty$ in which case the limiting distribution is $$p_{j}=\frac{\rho_{j}}{\sum_{n=0}^{\infty}\rho_{n}},\;j\geq0 \tag{6.75}$$
Note that $\rho=\frac{\lambda}{\mu}$ is called the **traffic intensity**.
Many queueing models are special cases of birth and death processes.
### 1) M/M/1 Queue
Poisson arrival with rate $\lambda$, service times exponential with mean rate $\mu$ 
Note that $\lambda_{n}=\lambda$ and $\mu_{n}=\mu$ for all $n\geq0$. (All birth-death transition rates are the same in M/M/1)
Also note that this implies that $\rho_{n}=\rho^{n}$ where $\rho=\frac{\lambda}{\mu}$ for $n\geq0$. This immediately gives our stability condition.
Note that:$$
\sum_{n=0}^{\infty}\rho_{n}=\sum_{n=0}^{\infty}\rho^{n}=
\begin{cases}
\frac{1}{1-\rho}, & \rho <1,\\
\infty, & \text{otherwise.}
\end{cases}
$$
Hence the chain is positive recurrent if and only if $\rho<1$.
**Stability Condition**: $\rho<1$.
If $\rho<1$ (stable queue), then our **limiting distribution** is $$
p_{j}=\rho^{j}(1-\rho),\;j\geq0\tag{7.17}
$$(since sum is $\frac{1}{1-\rho}$ and $\rho_{n}=\rho^{n}$).
We can then write $$
L=\sum_{n=0}^{\infty} jp_{j}=\sum_{j=0}^{\infty} j(1-\rho)\rho^{j}=(1-\rho)\rho \sum_{j=1}^{\infty} j\rho^{j-1}=(1-\rho)\rho \sum_{j=1}^{\infty} \frac{d}{d\rho}\rho^{j}
$$
$$
=(1-\rho)\rho\frac{d}{d\rho}\sum_{j=1}^{\infty} \rho^{j}=(1-\rho)\rho\frac{d}{d\rho}\left( \frac{1}{1-\rho}-1 \right)=\frac{\rho}{1-\rho}=\frac{\lambda}{\mu-\lambda}
$$
**So in summary** $$L=\frac{\lambda}{\mu-\lambda} \tag{7.18}$$

Suppose FCFS discipline. Lets compute $F(x)=\lim_{ n \to \infty }\mathbb{P}(W_{n}\leq x)$.
From PASTA, we know that $\Pi_{j}^{*}=p_{j},\;j\geq0$.
$$
1-F(x)=\lim_{ n \to \infty } \sum_{j=0}^{\infty} \mathbb{P}(W_{n}>x| X_{n}^{*}=j)\mathbb{P}(X_{n}^{*}=j)=\sum_{j=0}^{\infty} \lim_{ n \to \infty } \mathbb{P}(W_{n}>x | X_{n}^{*}=j)\mathbb{P}(X_{n}^{*}=j)
$$
$$
=\sum_{j=0}^{\infty} \Pi_{j}^{*}\lim_{ n \to \infty } \mathbb{P}(W_{n}>x | X_{n}^{*}=j)
$$
Note that we can express $\mathbb{P}(W_{n}>x|X_{n}^{*}=j)$ as the probability that the nth customer waits at least x time given there are j customers at the arrival of nth customer which tells us that this follows Erlang distributions. Intuitively we must wait for j customers to complete service before nth customer gets to be serviced. This leads to the following continuation of the above equality:
$$
=\sum_{j=0}^{\infty} \Pi_{j}^{*}\sum_{i=0}^{j} \frac{e^{-\mu x}(\mu x)^{i}}{i!}=\sum_{j=0}^{\infty} (1-\rho)\rho^{j}\sum_{i=0}^{j} \frac{e^{-\mu x}(\mu x)^{i}}{i!}=\sum_{i=0}^{\infty} \sum_{j=1}^{\infty} \frac{(1-\rho)\rho^{j}e^{-\mu x}(\mu x)}{i!}
$$
$$
=e^{-\mu x}(1-\rho)\sum_{i=0}^{\infty} \frac{(\mu x)^{i}}{i!} \sum_{j=i}^{\infty} \rho^{j}=e^{-\mu x}(1-\rho)\sum_{i=0}^{\infty} \frac{(\mu x)^{i}}{i!} \frac{\rho^{i}}{1-\rho}=e^{-\mu x}\sum_{i=0}^{\infty} \frac{(\lambda x)^{i}}{i!}=e^{-(\mu-\lambda)x},\;x>0.
$$
Thus, $F(.)$ is an exponential distribution with parameters $\mu-\lambda$. Thus,

$$
W=\frac{1}{\mu-\lambda}
$$
Note that $L=\frac{\rho}{1-\rho}=\frac{\lambda}{\mu-\lambda}=\lambda W$ which confirms Little's Law holds.

### 2) M/M/1/K Queue
This is again a birth-death process with rates $$
\lambda_{n}=\lambda,\;0 \leq n < K
$$
$$
\mu_{n}=\mu,\;1\leq n\leq K
$$
This queue is always positive recurrent (so always stable) since it is finite state CTMC.
Let $\rho=\frac{\lambda}{\mu}$ once again, then from example 6.36 we see once against $\rho_{n}=\rho^{n},\;0\leq n\leq K$.
Thus, we have $$
\sum_{n=0}^{K}\rho_{n}=
\begin{cases}
\frac{1-\rho^{K+1}}{1-\rho} & \rho\neq1 \\
K+1 & \rho=1
\end{cases}
$$
which is always finite so this queue is always stable.
This gives us our **limiting distribution** by equation 6.75 $$
p_{j}=
\begin{cases}
\frac{(1-\rho)\rho^{j}}{1-\rho^{K+1}} & \rho\neq1 \\
\frac{1}{K+1} & \rho=1
\end{cases} \tag{7.19}
$$
From example 7.5 in the book we have $$
\hat{\Pi_{j}}=p_{j},\;0\leq j\leq K
$$
and $$
\Pi_{j}=\Pi_{j}^{*}=\frac{p_{j}}{1-p_{K}},\;0\leq j\leq K-1
$$
Using the limiting distribution one can compute $$
L=\sum_{j=0}^{K} jp_{j} =
\begin{cases}
\frac{\rho}{1-\rho}[1-(K+1)p_{K}] & \rho\neq1 \\
\frac{K}{2} & \rho=1
\end{cases} \tag{7.20}
$$
A natural question is what fraction of customers are blocked from entering the system? Answer: $p_{K}$

### 3) M/M/S Queue
Poisson arrivals, exponential service times, but $S$ servers
Thus we have $\lambda_{n}=\lambda$ and $\mu_{n}=min(s,n)\mu$
Let $r=\frac{\lambda}{\mu}$ and $\rho=\frac{\lambda}{s\mu}$. Then from equation 6.74 we get $$
\rho_{n}=
\begin{cases}
\frac{r^{n}}{n!} & 0\leq n\leq s \\
\frac{s^{s}}{s!}\rho^{n} & n\geq s
\end{cases}
$$
And this directly leads to the following result
$$
\sum_{n=0}^{\infty} \rho_{n}=
\begin{cases}
\sum_{n=0}^{s-1} \rho_{n}+\frac{s^{s}}{s!} \frac{\rho^{s}}{1-\rho} & \rho<1 \\
\infty & \rho\geq1
\end{cases}
$$
Hence the **stability condition** is: $\rho < 1$.
this condition says that the queue is stable if the arrival rate is less than the maximum service rate $s\mu$ which makes intuitive sense.
For the following equations assume stability (as they would not hold otherwise).
From equation 6.75 we can find the limiting distribution as
$$
p_{0}=\left( \sum_{n=0}^{\infty} \rho_{n}  \right)^{-1}=\left[ \sum_{n=0}^{s-1} \rho_{n}+ \frac{s^{s}}{s!} \frac{\rho^{s}}{1-\rho} \right]^{-1}
$$
which directly leads to
$$
p_{n}=\rho_{n}p_{0}=
\begin{cases}
\frac{r^{n}}{n!}p_{0} & 0\leq n<s \\
\frac{s^{s}}{s!}\rho^{n}p_{0} & n\geq s
\end{cases}
$$
A natural question, is what fraction of the time are all servers busy? Answer (the limiting probability that all servers are busy):
$$
\sum_{n=s}^{\infty} p_{n}= \frac{s^{s}}{s!} \frac{\rho^{s}}{1-\rho}p_{0} = \frac{p_{s}}{1-\rho}
$$
**(Note the following is extra from the book and was not covered in class).**
This probability, called the blocking probability is commonly parameterized by r rather than $\rho$ and is denoted $C(s,r)$ as given below. This is called the Erlang-$C$ formula.
$$
C(s,r)= \frac{\left( \frac{r^{s}}{s!} \frac{s}{s-r} \right)}{\sum_{j=0}^{s-1} \frac{r^{j}}{j!}+\frac{r^{s}}{s!} \frac{s}{s-r}}
$$
This formula is useful for expressing the following
$$
L_{q}=\frac{\rho}{1-\rho}C(s,r)
$$
$$
W_{q}=\frac{L_{q}}{\lambda}=\frac{1}{\mu} \frac{1}{s-r}C(s,r) \tag{7.22}
$$
This naturally leads to
$$
L=r+L_{q} \tag{7.23}
$$
$$
W=\frac{1}{\mu}+W_{q}
$$
### 4) M/M/$\infty$ Queue
Note that we don't necessarily need to think about it as having infinite servers. It can be a good approximation of queues that often aren't full like a library.
We have the following birth and death rates
$$
\lambda_{n}=\lambda,\;n\geq0
$$
$$\mu_{n}=n\mu,\;n\geq0$$
From equation 6.74 we get $\rho_{n}=\frac{\left( \frac{\lambda}{\mu} \right)^{n}}{n!}$
Note that $\sum_{n=0}^{\infty} \rho_{n}=e^{\lambda/\mu} \implies$ always stable.
Equation 6.75 gives us the following limiting distribution ($r=\frac{\lambda}{\mu}$):
$$
p_{j}=\frac{e^{-r}r^{j}}{j!},\;j\geq0
$$
Note that all conditions are met for equating limiting distributions thus
$$
\hat{\Pi_{j}}=\Pi_{j}^{*}=\Pi_{j}=p_{j}=\frac{e^{-r}r^{j}}{j!},\;j\geq0
$$
Note that the **limiting distribution is a Poisson distribution** with rate $r=\frac{\lambda}{\mu}$.
Transient analysis: $P_{0j}(t)=\mathbb{P}(X(t)=j|X(0)=0)=e ^{-\frac{\lambda}{\mu}(1-e^{-\mu t})} \frac{(\frac{\lambda}{\mu}(1-e^{-\mu t}))^{j}}{j!}$ from Nonhomogeneous Bernoulli splitting. Thus, if $X(0)=0$ then $X(t)$ is a Poisson random variable with mean $r(1-e^{-\mu t})$ as seen by the equation for $P_{0j}(t)$. Recall this registers events of a system. So in this context we can think of it as registering people who entered the system and are still in the system at time t. From this we get
$$
\mathbb{E}(X(t)|X(0)=0)=r(1-e^{ -\mu t })
$$
In comparison the transient analysis of the M/M/1 and M/M/s queues is quite messy.

### 5) Queues with Finite Population
Example: suppose there are $S$ doctors serving the needs of population N
Each individual needs to see a doctor with some exponential distribution with rate $\lambda$
Assume it takes an exp amount of time to serve each patient
$X(t)$: number of individuals waiting to be seen by a doctor or are currently being seen
$\{X(t),\;t\geq0\}$ will be birth and death process with $S=\{0,1,2,\dots,N\}$ so $\lambda_{n}=\lambda(N-n),\;0<n\leq N$ (since there are $N-n$ people out there still following exponential distribution to arrive) and $\mu_{n}=min(s,n)\mu,\;0<n\leq N$ (either all s doctors are full or they aren't in which case we only have n servers working, thus $min(s,n)$ times rate $\mu$).
Since this is a finite state queue, it is always stable.
### 6) M/M/1 Queue with Balking and Reneging
Balking is when they show up and decide not to join.
Reneging is they join and then decide to leave later.
Suppose that incoming customers who see n customers join with probability $\alpha_{n}$.
Also suppose each customer has independent patience time that is exponential with parameter $\theta$. (If patience time is met the customer leaves)
If patience < time it would take to start service, the customer leaves (called reneging). I.e. they join the queue and their patience exponential timer starts and if it goes off before they start service they leave.
Thus, $\lambda_{n}=\lambda \alpha_{n},\;n\geq0$ and $\mu_{n}=\mu+(n-1)\theta,\;n\geq1$ (1 person being served is the $\mu$ and the n-1 customers waiting will leave with their patience rate $\theta$). Note that $\mu_{0}=0$. 
If $\theta>0$, the queue is always stable.

## Open Jackson Networks
A queueing network is called a Jackson network if it satisfies the following assumptions:
1. It has $N$ service stations (nodes).
2. There are $s_{i}$ servers at node $i$, $1 \leq s_{i}\leq \infty$, $1\leq i\leq N$. Service times of customers at node $i$ are iid exp($\mu_{i}$) random variables. They are independent of service times of customers in other nodes.
3. There is an infinite waiting room at each node.
4. External arrivals at node $i$ form a PP($\lambda_i$). All the arrival processes are independent of each other and the service times.
5. After completing service at node $i$, a customer departs the system with probability $r_{i}$, or joins the queue at node $j$ with probability $r_{i,j}$, independent of the number of customers at any node in the system. $r_{i,i}$ can be positive. We have $$
r_{i}+\sum_{j=1}^{N} r_{i,j}=1,\;1\leq i\leq N \tag{7.28}
$$
6. The routing matrix $R=[r_{i,j}]$ is such that $I-R$ is invertible. Note that the invertibility of $I-R$ implies that no customer stays in the network indefinitely.
Let $X_{i}(t)$ be the number of customers at node $i$ at time $t$, and let $X(t)=[X_{1}(t),\dots,X_{N}(t)]$ be the state of the queueing network at time $t$. The state space of $\{X(t),\;t\geq0\}$ process is $S=\{0,1,2,\dots\}^{N}$.
Let $e_{i}$ be the vector of dimension $N$ with a 1 in the ith coordinate and 0 in all others.
Suppose the system is in state $x = [x_{1},\dots,x_{N}]\in S$.
It can be seen that $\{X(t),\;t\geq0\}$ is a multidimensional CTMC with the following transition rates:
$$
\begin{align}
q(x,x+e_{i})=\lambda_{i} \\
q(x,x-e_{i})=min(x_{i},s_{i})\mu_{i}r_{i} \\
q(x,x-e_{i}+e_{j})=min(x_{i},s_{i})\mu_{i}r_{i,j},\;i\neq j
\end{align}
$$
Think of the first equation as an arrival to node i.
Think of the second equation as a service completion that results in a departure from the system at node i.
Think of the third equation as a service completion where the customer goes to a different node within the network.
Hence we get
$$
q(x,x)=-q(x)=-\sum_{i=1}^{N} \lambda_{i}-\sum_{i=1}^{N} min(x_{i},s_{i})\mu_{i}(1-r_{i,i})
$$
Now we let
$$
p(x)=\lim_{ t \to \infty } \mathbb{P}(X(t)=x)=\lim_{ t \to \infty } \mathbb{P}(X_{1}(t)=x_{1},\dots,X_{N}(t)=x_{N})
$$be the limiting distribution, assuming it exists.

Before we give an expression for $p(x)$, let's focus on a single node j.
Define $a_{j}$ as the total arrival rate to node $j$. So $$
a_{j}=\lambda_{j}+\sum_{i=1}^{N} a_{i}r_{i,j},\;1\leq j\leq N\tag{7.29}
$$Note that this follows because in steady state the rate out must be the same as rate in, hence why we have $a_{i}r_{i,j}$ portion. Otherwise the queue would be blowing up or decreasing to 0. We call $\lambda_{i}$ the external input and the sum the internal input.
Thus, we say
$$
a=\lambda+aR\implies a(I-R)=\lambda\implies
$$
$$
a=\lambda(I-R)^{-1} \tag{7.30}
$$

Now consider an M/M/$s_{i}$ queue with arrival rate $a_{i}$ and service rate $\mu_{i}$. From earlier we know such a queue is stable if $\rho_{i}= \frac{a_{i}}{s_{i}\mu_{i}}<1$.
The steady state probability that there are n customers in the system is given by $$
\phi_{i}(n)=\frac{s_{i}^{min(n,s_{i})}}{min(n,s_{i})!}\rho_{i}^{n}\phi_{i}(0),\;n\geq0
$$where $$
\phi_{i}(0)=\left[ \sum_{n=0}^{s_{i}-1} \frac{s_{i}^{n}}{n!}\rho_{i}^{n}+\frac{s_{i}^{s_{i}}}{s_{i}!} \frac{\rho_{i}^{s_{i}}}{1-\rho_{i}} \right]^{-1}
$$
With these preliminaries we can now cover the main result of Jackson networks.

### Theorem 7.7 Open Jackson Networks
The CTMC $\{X(t),\;t\geq0\}$ is positive recurrent if and only if
$$
a_{i}<s_{i}\mu_{i},\;1\leq i\leq N
$$
where $a=[a_{1},\dots,a_{N}]$ is given by equation 7.30 above. When it is positive recurrent, its steady state distribution is given by
$$
p(x)=\prod_{i=1}^{N} \phi_{i}(x_{i})\tag{7.31}
$$
Proof is quite long and in textbook if interested. It follows by direct substitution of the balance equations.
Majors takeaways from this theorem:
- This form of distribution is called product form (1 term for each node and you multiply them to find the joint distribution)
- The queue length of each node is independent of other queue lengths in steady state.
- Furthermore, each node behaves as if it is an independent M/M/$S$ queue in the limit.

Examples in textbook and in Google Doc notes.

### State-Dependent Service (generalization)
This is a modification to the assumptions above, namely assumption 2.
We now assume that the service rate is $\mu_{i}(n)$ where $\mu_{i}(0)=0$ and $\mu_{i}(n)>0,\;n\geq1,\;1\leq i\leq N$ (when there are n customers at node i).
Note that the service rate at node i is not allowed to depend on the state of node $j\neq i$. Now define $$
\begin{align}
\phi_{i}(0)=1 \\
\phi_{i}(n)=\prod_{j=1}^{n} \frac{a_{i}}{\mu_{i}(j)},\;n\geq1,\;1\leq i\leq N
\end{align} \tag{7.32}
$$
### Theorem 7.8 Jackson Networks with State-Dependent Service
A Jackson network with state-dependent service rates is stable if and only if
$$
c_{i}=\sum_{n=0}^{\infty} \phi_{i}(n) < \infty,\;1\leq i\leq N
$$
If the network is stable, the limiting state distribution is given by $$
p(x)=\prod_{i=1}^{N} \frac{\phi_{i}(x_{i})}{c_{i}},\;x \in S
$$
Thus, in steady state, the queues at various nodes in a Jackson network with state-dependent service are independent.


### State-Dependent Arrivals and Service (generalization)
It is also possible to further generalize by allowing the external arrival rate to the network to depend on the total number of customers in the network. Specifically, we are relaxing the 4th condition above.
Define the following:
$\lambda(n)$: the total external arrival rate to the network when there are n customers in the network in total
$u_{i}$: the probability that an incoming customer joins node i independently of everything else
Note that $\sum_{i=1}^{N}u_{i}=1$.
Thus the external arrival rate to a specific node i is $u_{i}\lambda(n)$.
To keep the $\{X(t),\;t\geq0\}$ process irreducible, we assume there is a $K\leq \infty$ such that $\lambda(n)>0,\;0\leq n<K$ and $\lambda(n)=0,\;n\geq K$.
Then notice that our unique solution to $a_{i}$ is now $$
a_{j}=u_{j}+\sum_{i=1}^{N} a_{i}r_{i,j},\;1\leq j\leq N
$$
Also define $|x|=\sum_{i=1}^{N}x_{i}$ i.e. the total number of customers in the system for state x.
Using all of this we have the following theorem.

### Theorem 7.9 Jackson Networks with State-Dependent Arrivals and Service
The limiting state distribution in a Jackson network with state-dependent arrivals and service is given by $$
p(x)=c\prod_{i=1}^{N} \phi_{i}(x_{i})\prod_{j=1}^{|x|} \lambda(j),\;x \in S
$$ where c is the normalizing constant given by $$
c=\left( \sum_{x\in S}\prod_{i=1}^{N} \phi_{i}(x_{i})\prod_{j=1}^{|x|} \lambda(j) \right)^{-1}
$$
The network is stable if and only if c > 0.

## Closed Queueing Networks
Unlike Open Networks, closed networks have no external arrivals and no departures from the network.
A queueing network is called a closed Jackson network if it satisfies the following
1. It has $N$ service stations (nodes) and a total of $K$ customers
2. The service rate at node $i$, when there are $n$ customers at that node, is given by $\mu_{i}(n)$ with $\mu_{i}(0)=0$ and $\mu_{i}(n)>0$ for $1\leq n\leq K,\;1\leq i\leq N$.
3. After completing service at node $i$, a customer joins the queue at node $j$ with probability $r_{ij}$ independent of the number of customers at any node in the system. $r_{ii}$ can be positive.
4. The routing matrix $R=[r_{ij}]$ is a transition probability matrix of an irreducible DTMC
Once again, $X_{i}(t)$ denotes the number of customers at node $i$ at time $t$ and $X(t)=[X_{1}(t),\dots,X_{N}(t)]$.
Thus, our state space is $S=\{x=[x_{1},\dots,x_{N}] : x_{i}\geq0,\;\sum_{i=1}^{N}x_{i}=K\}$
And the transitions between states is given by
$$
\begin{align}
q(x,x-e_{i}+e_{j})=\mu_{i}(x_{i})r_{ij},\;i\neq j,x\in S \\
q(x,x)=-q(x)=-\sum_{i=1}^{N} \mu_{i}(x_{i})(1-r_{ii}),\;x \in S
\end{align}
$$
Since the CTMC has a finite state space and is irreducible it is positive recurrent. Let $$
p(x) = \lim_{ t \to \infty } \mathbb{P}(X(t)=x)=\lim_{ t \to \infty } \mathbb{P}(X_{1}(t)=x_{1},\dots,X_{N}(t)=x_{N}) 
$$ be the limiting distribution.
$$
\pi=\pi R,\;\sum_{i=1}^{N} \pi_{i}=1 \tag{7.33}
$$
Lastly, define $$
\phi_{i}(0)=1,\;\phi_{i}(n)=\prod_{j=1}^{n} \frac{\pi_{i}}{\mu_{i}(j)},\;1\leq n\leq K,1\leq i\leq N \tag{7.34}
$$
### Theorem 7.10 (Closed Jackson Networks)
The limiting distribution of the CTMC $\{X(t),\;t\geq0\}$ is given by $$
p(x)=G_{N}(K)\prod_{i=1}^{N} \phi_{i}(x_{i})
$$
where the normalizing constant $G_{N}(K)$ is chosen so that $\sum_{x\in S}p(x)=1$.
Thus the closed Jackson network has a "product form" limiting distribution. The hard part is actually finding $G_{N}(K)$.


### DTMCs with transition probability matrix in the form of Upper Hessenberg
$$
P = 
\begin{bmatrix}
\alpha_{0} & \alpha_{1} & \alpha_{2} & \dots \\
\alpha_{0} & \alpha_{1} & \alpha_{2} & \dots \\
0 & \alpha_{0} & \alpha_{1} & \dots \\
0 & 0 & \alpha_{0} &\dots \\
\dots & \dots & \dots & \dots
\end{bmatrix}
$$
$P_{0j}=\alpha_{j}, j\geq 0$
$P_{ij}=\alpha_{j-i+1}, j\geq i-1 \geq 0$
$\pi_{j}=\sum_{i=1}^{\infty}\Pi_{i}P_{ij},\ j\geq 0$
$\Pi_{j}=\Pi_{0}\alpha_{j}+\sum_{i=1}^{j+1}\Pi_{i}\alpha_{j-i+1},\ j\geq 0$
Let $\phi(z)=\sum_{i=0}^{\infty}\Pi_{j}z^{j}$, $\psi(z)=\sum_{i=0}^{\infty}\alpha_{j}z^{j}$
$\phi(z)=\sum_{j=1}^{\infty}\Pi_{j}z^{j}=\Pi_{0}\sum_{j=0}^{\infty}$ more
Pic on Phone
$$\implies\phi(z)=\frac{\Pi_{0}\psi(z)(1-z)}{\psi(1)-z} \tag{key result}$$

$\lim_{ z \to 1}\phi(z)=\sum_{i=0}^{\infty}\Pi_{i}=1=\Pi_{0}\lim_{ z \to 1 } \frac{\psi(z)(1-z)}{\psi(z)-z}$
$\implies\Pi_{0}\lim_{ z \to 1 } \frac{\psi'(z)(1-z)-\psi(z)}{\psi'(z)-1}$ ($L$'Hospitals)
$=\frac{\Pi_{0}*(-\psi(1))}{\psi'(1)-1}$ ($L$'Hospitals)
$\implies 1=\frac{\Pi_{0}}{1-\psi'(1)}$
To have a nonnegative solution to $\Pi_{0}$ we must have $\psi'(1)<1$
$$
\psi'(1) = \sum_{k=0}^{\infty} k\alpha_{k} < 1
$$
Under that condition, we have $$
\Pi_{0}=1-\sum_{k=0}^{\infty} k\alpha_{k}
$$
### DTMCs with a transition probability matrix in the form of Lower Hessenberg
$$
P = 
\begin{bmatrix}
\beta_{0} & \alpha_{0} & 0 & 0 & \dots \\
\beta_{1} & \alpha_{1} & \alpha_{0} & 0 & \dots \\
\beta_{2} & \alpha_{2} & \alpha_{1} & \alpha_{0} & 0 \\
\dots & \dots & \dots & \dots & \dots
\end{bmatrix}
$$
$P_{ij}=\alpha_{i-j+1},\ 0 < j \leq i+1$
$P_{i0}=\beta_{i}=\sum_{k=i+1}^{\infty}\alpha_{k}$
Assume that $\alpha_{0}>0$
$\Pi_{j}=\sum_{i=0}^{\infty}\Pi_{i}P_{ij}$
$\implies\Pi_{j}=\Pi_{j-1}\alpha_{0}+\Pi_{j}\alpha_{1}+\Pi_{j+1}\alpha_{2}+\dots$
$$
\Pi_{j}=\sum_{i=0}^{\infty} \alpha_{i}\Pi_{i+j-1}, \;j\geq 1
$$
Note j=0 is a special case
Let us guess $\Pi_{j}=c\rho^{j}$ where c and $\rho$ are constants independent of $j$.
$c\rho^j=\sum_{i=0}^{\infty}a_{i}c\rho^{i+j-1}$
$\implies \rho=\sum_{i=0}^{\infty}\alpha_{i}\rho^{i}$
$$
\implies \rho = \psi(\rho)
$$
where $\psi(z)=\sum_{i=0}^{\infty}\alpha_{i}z^{i}$
Thus, we have $\psi(0)=\alpha_{0}>0$
$\psi(1) = 1$
$\psi'(\rho)\geq 0$ and $\psi''(\rho)\geq 0$
We want $0 < \rho < 1$ because if it is 0 or 1 we don't have a solution to $\Pi_{j}$'s.
We will determine if $\rho$ satisfies this based on the derivative of $\psi(\rho)$. Pic on phone of graphical drawing (not the best though).
We have a solution to $\psi(\rho)=\rho$ for which $0 < \rho < 1 \iff \psi'(1)=\sum_{k=0}^{\infty}k\alpha_{k} > 1$ in which case $\Pi_{j}=c\rho^{j} \implies \sum_{i=0}^{\infty}\Pi_{i}=\sum_{i=0}^{\infty}c\rho^{j}>1$
$$\implies c=1-\rho\implies\Pi_{j}=(1-\rho)\rho^{j}, \;j\geq 0 \tag{key result}$$
## The M/G/1 Queue
Poisson arrivals with rate $\lambda$. Assume that $G(\cdot)$ is the service time CDF with mean $\tau$ and variance $\sigma^{2}$. Service times are iid and independent of the arrival process.
Recall that
	$X_{n}$ is the number of customers in the system after the nth departure
	$X_{n}^{*}$ is the number of customers in the system before the nth customer joins
	$\hat{X_{n}}$ is the number of customers in the system before the nth arrival
Recall that if $\{X_{n},n\geq{0}\}$ has a limiting distribution so does $\{\hat{X_{n}},n\geq{0}\}$ and $\Pi_{i}=\hat{\Pi_{i}}\;\forall i \in S$
Also from PASTA, we know that $p_{i}=\Pi_{i}=\hat{\Pi_{i}}=\Pi_{i}^{*}$ for $i \in S$.
### Theorem 7.11
$\{X_{n},n\geq{0}\}$ is an irreducible and aperiodic DTMC with state space $S = \{0,1,2,\dots\}$ and transition probability matrix
$$
P = 
\begin{bmatrix}
\alpha_{0} & \alpha_{1} & \alpha_{2} & \dots \\
\alpha_{0} & \alpha_{1} & \alpha_{2} & \dots \\
0 & \alpha_{0} & \alpha_{1} & \dots \\
0 & 0 & \alpha_{0} &\dots \\
\dots & \dots & \dots & \dots
\end{bmatrix}
$$
where $$\alpha_{i}=\int_{0}^{\infty} \frac{e^{-\lambda t}(\lambda t)^{i}}{i!} dG(t)$$
Proof: Let $A_{n}$ denote the number of arrivals during the service of customer n.
If $X_{n}=0 \implies X_{n+1}=A_{n+1}$ (number of people in the system after (n+1)th person departs is number of people who showed up while they were being serviced)
if $X_{n} > 0\implies X_{n+1}=X_{n}+A_{n+1}-1$ (number of people in the system after (n+1)th person departs is number of people who showed up - person who left + people in system after nth departure).
Then the result follows from $\mathbb{P}(A_{n}=i)=\int_{0}^{\infty} \frac{e^{-\lambda t}(\lambda t)^{i}}{i!} dG(t)$.

### Theorem 7.12 
$\{X_{n},n\geq{0}\}$ is positive recurrent if and only if $\rho = \lambda \tau < 1$. (Recall $\tau$ is mean service time). If it is positive recurrent then the limiting distribution has a generating function given by $\phi(z)=\sum_{i=0}^{\infty}\Pi_{j}z^{j}= \frac{(1-\rho)(1-z)\tilde{G}(\lambda-\lambda z)}{\tilde{G}(\lambda-\lambda z)-z}$ where $\tilde{G}(s) = \int_{0}^{\infty}e^{-st}dG(t)$ is the Laplace-Stieltjas Transform for sojourn time distribution.

Proof: $P$ is an upper Hessenberg matrix. Thus, we know that the chain is positive recurrent if and only if $\sum k\alpha_{k} < 1$. Then $\sum_{k=0}^{\infty}k\alpha_{k}=\sum_{k=0}^{\infty}k\int_{0}^{\infty}\frac{e^{-\lambda t}(\lambda t)^{k}}{k!} dG(t)$.
$$\implies \int_{0}^{\infty} e^{-\lambda t} \sum_{k=1}^{\infty} \frac{(\lambda t)^{k}}{(k-1)!}=\int_{0}^{\infty} e^{-\lambda t}(\lambda t)e^{\lambda t}dG(t)=\lambda \tau$$
Thus, the condition we need is $\lambda\tau<1$.

February 5
Reminder: Generally M/G/1 Queue will not be able to be modeled as a CTMC. Perhaps we can model it a different way to satisfy the Markovian property. 
Recall the matrix $P$ above and $\alpha_{i}=\int_{0}^{\infty} \frac{e^{-\lambda t}(\lambda t)^{i}}{i!} dG(t)$. Think of $\alpha_{i}$ as the probability of i customers arriving during time t. $\{X_{n},\;n\geq0\}$ is a DTMC with this transition probability matrix.
We know from our analysis of the Upper Hessenberg DTMC that $\phi(z)=\sum_{j=0}^{\infty} \Pi_{j}z^{j}=\frac{(1-\rho)(1-z)\psi(z)}{\psi(z)-z}$.
$$
\implies \psi(z) = \sum_{j=0}^{\infty} \alpha_{j}z^{j}=\sum_{j=0}^{\infty} z^{j}\int_{0}^{\infty} \frac{e^{-\lambda t}(\lambda t)^{j}}{j!}dG(t)=\int_{0}^{\infty} e^{\lambda t}\sum_{j=0}^{\infty} \frac{(\lambda zt)^{j}}{j!}dG(t) 
$$
$$
=\int_{0}^{\infty}e^{-\lambda t}e^{\lambda zt}dG(t)=\int_{0}^{\infty}e^{-(\lambda-\lambda t)z} dG(t)\implies \psi(t)=\tilde{G}(\lambda-\lambda t)
$$
Then we get
$$
\phi(z) = \frac{(1-\rho)(1-z)\tilde{G}(\lambda-\lambda z)}{\tilde{G}(\lambda-\lambda z)-z}
$$
The theorem implies that
$$
P_{0}=\Pi_{0}=\phi(0)=1-\rho
$$
I.e. the limiting probability of having zero customers in the system is $1-\rho$.
We can also find the expected number in the system in the following theorem.
### Theorem 7.13
If $\lambda \tau<1$, then $L$, the expected number in steady state is given by $$
L = \rho + \frac{1}{2} \frac{\rho^{2}}{(1-\rho)}\left( 1+ \frac{\sigma^{2}}{\tau^{2}} \right) =\rho + \frac{\lambda^{2}s^{2}}{2(1-\rho)}
$$
Note that $s^{2}$ is the second moment of service time and $\sigma^{2}$ is the variance of service time. (Service time means total service time; i.e. if they have a chance of reentering queue after one service then service time here would be until they've completed service enough times to leave).
This formula is called the Pollaczek-Khinchine Formula.
The proof of this theorem follows using the fact that $L = \lim_{ z \to 1 }\phi'(z)$ along with the previous theorem.

Let $W_{n}$ denote the system time of the nth customer under first come first serve. 
We define $F_{n}(.)$ to be the CDF for $W_{n}$. 
We define $\tilde{F_{n}(s)}=\mathbb{E}e^{-sW_{n}}$ which is the [[Useful Math#Laplace-Stieltjas Transforms|LST]] for $W_{n}$.
Define $\tilde{F}(s)=\lim_{ n \to \infty }\tilde{F_{n}}(s)$ as the LST for the waiting time distribution in steady-state.
These definitions are important for the following theorem.
### Theorem 7.14
In a stable M/G/1 queue (recall stable means positive recurrent $\implies\lambda \tau<1$) we have $$
\tilde{F}(s)= \frac{(1-\rho)s\tilde{G(s)}}{s-\lambda(1-\tilde{G}(s))}
$$
Proof: 
$A_{n}$: number of arrivals during the nth customers system time
$X_{n}$: number of customers left behind in the system after nth departure
Since we have FCFS, we have $A_{n}=X_{n}$.
Since arrivals are Poisson we can show as in the previous theorem that $$
\mathbb{E}z^{A_{n}}=\tilde{F_{n}}(\lambda-\lambda z)
$$
Thus, $$
\phi(z) = \lim_{ n \to \infty } \mathbb{E}z^{X_{n}}=\lim_{ n \to \infty } \mathbb{E}z^{A_{n}}=\lim_{ n \to \infty } \tilde{F}_{n}(\lambda-\lambda z)=\tilde{F}(\lambda-\lambda z)
$$
Then, letting $\lambda-\lambda z=s$ we get $$
\tilde{F}(s)=\phi\left( \frac{\lambda-s}{\lambda} \right)= \frac{(1-\rho) \frac{s}{\lambda} \tilde{G}(s)}{\tilde{G}(s)-1+ \frac{s}{\lambda}}= \frac{(1-\rho)s\tilde{G(s)}}{s-\lambda(1-\tilde{G}(s))}
$$
Setting $s=0$ at $\frac{d \tilde{F}(s)}{ds}$, we get $$
W=\tau + \frac{\lambda s^{2}}{2(1-\rho)}
$$ which is also known as the Pollaczek-Khinchine formula.
Note that $s^{2}$ above is the second moment of service time.
You could also find the same expression for $W$ using Littles Law.

## G/M/1 Queue
We have $\hat{\Pi_{j}}=\Pi_{j}=\Pi_{j}^{*}$, but we've lost the equality with $p_{j}$ since we don't necessarily have Poisson arrivals.
Interarrival times are iid with $G(\cdot)$.
Let $$\alpha_{i}=\int_{0}^{\infty} \frac{e^{-\mu t}(\mu t)^{i}}{i!}dG(t)$$
and $$
\beta_{i}=\sum_{j=i+1}^{\infty} \alpha_{j},\;i\geq0
$$
Recall that $\hat{X_{n}}$ is the number of customers at the time of the nth arrival.
### Theorem 7.15
$\{\hat{X_{n}},\;n\geq0\}$ is an irreducible and aperiodic DTMC on $S$ = $\{0,1,2,\dots\}$ with transition probability matrix
$$
P = 
\begin{bmatrix}
\beta_{0} & \alpha_{0} & 0 & 0 & \dots \\
\beta_{1} & \alpha_{1} & \alpha_{0} & 0 & \dots \\
\beta_{2} & \alpha_{2} & \alpha_{1} & \alpha_{0} & 0 \\
\dots & \dots & \dots & \dots & \dots
\end{bmatrix}
$$
Proof: Let $D_{n}$ denote the number of service completions the server would achieve during the nth interarrival time if there were infinitely may customers.
Then $\{D_{n},\;n\geq1\}$ is a sequence of iid random variables with pmf described by $\alpha_{i}$'s.
Then we can expression $\hat{X}_{n+1}=max\{\hat{X_{n}}+1-D_{n},0\}$. (customers at nth arrival + 1 arrival - number of departures during this arrival time).
Then $\{\hat{X}_{n}, n\geq0\}$ is a DTMC. Thus, probability of going from i to j when $j\geq1$ and $i\geq j-1$ is $\alpha_{i+1-j}$. When $j=0$ and $i \geq0$ then probability of going from i to j is $\sum_{k=i+1}^{\infty}\alpha_{k}=\beta_{i}$.
### Theorem 7.16
The DTMC $\{\hat{X_{n}},\;n\geq0\}$ is positive recurrent if and only if $\rho=\frac{\lambda}{\mu}<1$. Where $\lambda$ is 1/mean interarrival team. When it is positive recurrent its limiting distribution is given by $\hat{\Pi_{j}}=\Pi_{j}^{*}=(1-\alpha)\alpha^{j},\;j\geq0$ where $\alpha$ is the unique solution in (0,1) to $$
\alpha=\int_{0}^{\infty}e^{-\mu(1-\alpha)t}dG(t)=\tilde{G}(\mu(1-\alpha))
$$
Here, $$
\lambda = \frac{1}{\int_{0}^{\infty}tdG(t)}
$$
and $\mu$ is the reciprocal of the mean service time.
Proof: We know from our earlier analysis that $P$ is a lower Hessenberg matrix and the DTMC is positive recurrent if and only if $\sum_{k=0}^{\infty} k\alpha_{k}>1$ (expectation of $\alpha_{k}$ probabilities). Then 
$$
\sum_{k=0}^{\infty} k\alpha_{k}=\sum_{k=0}^{\infty} k \int_{0}^{\infty} \frac{e^{-\mu t}(\mu t)^{k}}{k!}dG(t)=\mu \int_{0}^{\infty}t\sum_{k=0}^{\infty} \frac{(\mu t)^{k}}{k!}e^{-\mu t}dG(t)
$$$$=\mu \int_{0}^{\infty}te^{\mu t}e^{-\mu t}dG(t)=\mu \int_{0}^{\infty}tdG(t)=\frac{\mu }{\lambda}
$$
hence the DTMC is positive recurrent if and only if $\frac{\lambda}{\mu}<1$.

2/10

We know that the limiting distribution is given by $$
\hat{\Pi_{j}}=(1-\alpha^{*})\alpha^{*j}
$$ where alpha-star is the unique solution in (0,1) for $$
\alpha^{*} = \sum_{i=0}^{\infty} \alpha^{*i}\alpha_{i}
$$
Thus, we get $$
\alpha^{*}=\sum_{i=0}^{\infty} \alpha^{*i}\int_{0}^{\infty} \frac{e^{-\mu t}(\mu t)^{i}}{i!}dG(t)=\int_{0}^{\infty}\sum_{i=0}^{\infty} \frac{e^{-\mu t}(\mu \alpha^{*i}t)^{i}}{i!}dG(t)=\int_{0}^{\infty}e^{-\mu t(1-\alpha^{*})}dG(t)=\tilde{G}(\mu(1-\alpha^{*}))
$$
If interarrival times were exponentially distributed then $G(x) = 1-e^{-\lambda x}$ for $x\geq0$. This implies that (alpha-star) $\alpha=\int_{0}^{\infty}e^{-\mu(1-\alpha)t}\lambda e^{-\lambda t}dt=\lambda \int_{0}^{\infty}e^{-t(\mu(1-\alpha)+\lambda)}dt=\frac{\lambda}{\mu(1-\alpha)+\lambda}=\frac{\lambda}{\mu}$.
Then we get $\hat{\Pi_{j}}=\left( 1-\frac{\lambda}{\mu} \right)\left( \frac{\lambda}{\mu} \right)^{j},\;j\geq0$.

### Theorem 7.17
For the stable G/M/1 queue, $$
p_{j}=\lim_{ n \to \infty } \mathbb{P}(X(t)=j)=
\begin{cases}
1-\rho & j=0 \\
\rho \Pi_{j-1}^{*} & j\geq1
\end{cases}
$$
Proof: Skipping for now; based on some results from renewal theory.

### Limiting Distribution of System Time 7.18
$$
\lim_{ n \to \infty } \mathbb{P}(W_{n}>x)=\lim_{ n \to \infty } \sum_{j=0}^{\infty} \Pi_{j}^{*}\mathbb{P}(W_{n}>x|X_{n}^{*}=j)=\sum_{j=0}^{\infty} \Pi_{j}^{*}\lim_{ n \to \infty } \mathbb{P}(W_{n}>x|X_{n}^{*}=j)
$$
$$
=\sum_{j=0}^{\infty} (1-\alpha)\alpha^{j}\sum_{i=0}^{j} \frac{e^{-\mu x}(\mu x)^{i}}{i!}=\sum_{i=0}^{\infty} \sum_{j=i}^{\infty} (1-\alpha)\alpha^{j} \frac{e^{-\mu x}(\mu x)^{i}}{i!}=(1-\alpha)e^{-\mu x}\sum_{i=0}^{\infty} \frac{(\mu x)^{i}}{i!} \frac{\alpha^{i}}{1-\alpha}
$$
$$
=e^{-\mu x}e^{\alpha \mu x}=e^{-\mu x(1-\alpha)}
$$
Thus, it turns out that the limiting distribution for $W_{n}$ (waiting time) is exponential with rate parameter $\mu(1-\alpha)$.
Hence, the mean system time in steady state is$$
W=\frac{1}{\mu(1-\alpha)}
$$
And using Little's Law we see that $$
L=\frac{\lambda}{\mu(1-\alpha)}
$$
### Theorem 7.18 (Waiting Times)
The limiting distribution of the waiting time in a stable G/M/1 queue with FCFS service discipline is given by $$
F(x)=\lim_{ n \to \infty } \mathbb{P}(W_{n}\leq x)=1-e^{-\mu(1-\alpha)x},\;x\geq0
$$


### M/G/1/1 Retrial Queue
Not covering in lecture. Got notes from book on my own.

Customers arrive from outside to a single server according to a PP($\lambda$) and require iid service times with common distribution $G(\cdot)$ and mean $\tau$. If an arriving customer finds the server idle, he immediately enters service. Otherwise he joints the "orbit" where he stays for an exp($\theta$) amount of time called the retiral time. At the end of retrial time he returns to the server and behaves like a new customer.
$X(t)$: number of customers in the system (those in service + those in orbit) at time $t$
$X_{n}$: number of customers in system upon nth departure
Since every arriving customer enters the system (service or orbit), the arrival process is Poisson, and customers enter/leave one by one we have $$
\hat{\Pi_{j}}=\Pi_{j}^{*}=\Pi=p_{j},\;j\geq0
$$
### Theorem 7.19 (Embedded DTMC in a M/G/1/1 Retrial Queue)
$\{X_{n},\;n\geq0\}$ is an irreducible and aperiodic DTMC on $S=\{0,1,\dots\}$

### Theorem 7.20 (Limiting Distribution of M/G/1/1 Retrial Queue)
The DTMC $\{X_{n},\;n\geq0\}$ with $\theta>0$ is positive recurrent if and only if $\rho=\lambda \tau<1$.
If it is positive recurrent, its limiting distribution has the generating function given by $$
\phi(z)=\sum_{j=0}^{\infty} \Pi_{j}z^{j}=(1-\rho) \frac{(1-z)\tilde{G}(\lambda-\lambda z)}{\tilde{G}(\lambda-\lambda z)-z}\exp \left( -\frac{\lambda}{\theta}\int_{z}^{1} \frac{1-\tilde{G}(\lambda-\lambda u)}{\tilde{G}(\lambda-\lambda u)-u} du\right) \tag{7.52}
$$
where $$
\tilde{G}(s)=\int_{0}^{\infty}e^{-st}dG(t)
$$
Note that equation 7.52 has an immediate consequence that the probability that the system is empty in steady state can be computed as $$
p_{0}=\Pi_{0}=\phi(0)=(1-\rho)\exp \left( -\frac{\lambda}{\theta}\int_{z}^{1} \frac{1-\tilde{G}(\lambda-\lambda u)}{\tilde{G}(\lambda-\lambda u)-u} du\right)
$$
But note that this is not the same as the server being idle since the server can be idle even if the system is not empty. Using Little's Law we can show that the server is idle in steady state with probability $1-\rho$.

### Theorem 7.21 (Expected Number in an M/G/1/1 Retrial Queue)
The expected number in steady state in a stable M/G/1/1 retrial queue with $\theta>0$ is given by $$
L=\rho +\frac{\lambda^{2}s^{2}}{2(1-\rho)}+\frac{\lambda \rho}{\theta(1-\rho)} \tag{7.59}
$$
where $\tau$ and $s^{2}$ are the mean and second moment of the service time.

### M/G/$\infty$ Queue
Can be a good approximation for areas that are never practically full (like a library).
$X(t)$: number of customers at time $t$
Let $X(0)=0$.
The results come from the analysis for Nonhomogeneous Bernoulli Splitting.
We know that $X(t)$ is a Poisson RV with parameter $\lambda m(t)$ where $m(t)=\int_{0}^{t}(1-G(s))ds$ where $G(.)$ is the service time distribution.
As $t\to \infty$, $m(t)\to \tau$ the expected service time.
So $\lim_{ t \to \infty }\mathbb{P}(X(t)=x)=\frac{e^{-\lambda \tau}(\lambda \tau)^{x}}{x!}$ Poisson with $\lambda \tau$.
The limiting result will hold even if $X(0)=i>0$ (i.e. $X(0)\neq0$).


# Renewal Processes
Basically a counting process that counts the number of events that occur over time. The information we need is that the time between two consecutive events is iid (doesn't have to be exponential).

Formally, a renewal process is a stochastic process that keeps track of the number of events that occur over time.

Notation:
- $S_{n}$: the occurrence time of the nth event ($S_{0}=0$). Assume that the events are ordered i.e. $0\leq S_{1}\leq S_{2}\leq\dots$
	- Note that in PP's we couldn't have events occur at the same time, but we relax that here because $S_{n}$'s are not necessarily continuous.
- $X_{n}$: nth interevent time i.e. $X_{n}=S_{n}-S_{n-1}$. Note that $X_{n}$'s are iid.
- $N(t)=sup\{n\geq0:S_{n}\leq t\}$: Number of events by time t

Examples:
1) Poisson Process
2) $\{X(t),\;t\geq0\}$ is a CTMC in $S=\{0,1,2,\dots\}$. Let $X(0)=1$ with probability 1. Let $S_{n}$ be the time of the nth entry into state 0.

#### Definition
$\{S_{n},\;n\geq0\}$ is said to be a renewal sequence and the counting process $\{N(t),\;t\geq0\}$ is said to be a renewal process generated by these interevent times $\{X_{n},\;n\geq0\}$ if $\{X_{n},\;n\geq0\}$ is a sequence of non-negative iid random variables.

### Theorem 8.1
The renewal process $\{N(t),\;t\geq0\}$ is completely characterized by the interrenewal distribution G(.).

Proof: Let $0\leq t_{1}\leq t_{2}\leq\dots\leq t_{n}$ and $0\leq k_{1}\leq k_{2}\leq\dots\leq k_{n}$. Then $\mathbb{P}(N(t_{1})=k_{1},\dots,N(t_{n})=k_{n})=\mathbb{P}(S_{k_{1}}\leq t_{1},S_{k_{1}+1}>t_{1},\dots,S_{k_{n}}\leq t_{n},S_{k_{n}+1}>t_{n})$.
This is completely a function of G(.) and thus the result follows.
Timeline pic on phone. Essentially $S_{k_{1}}$ must be to the left of $t_{1}$ (occurs before $t_{1}$) and $S_{k_{2}}$ must be to the right of $t_{1}$ (occurs after $t_{1}$).


### Theorem 8.2
$\{N(t),\;t\geq0\}$ and $\{N(t+X_{1})-1,\;t\geq0\}$ (starts counting after the first event) are stochastically identical.
Thus, we call $S_{1}$ the first renewal epoch and $S_{n}$ the nth renewal epoch.


## Properties of $N(t)$
$G(t)=\mathbb{P}(X_{n}\leq t),\;n\geq1$
$\tau=\mathbb{E}X_{n}$
$s^{2}=\mathbb{E}X_{n}^{2}$
$\sigma^{2}=\mathrm{Var}(X_{n})$
We also assume that $\mathbb{P}(X_{n}=0)\neq1,\;\forall n$ which implies that $\tau>0$.

### Theorem 8.3
$$\mathbb{P}(N(t)<\infty)=1,\;\forall t\geq0$$
Proof: From the strong law of large numbers, $\mathbb{P}\left( \frac{S_{n}}{n}\to \tau \right)=1$ ($\mathbb{P}\left( \lim_{ n \to \infty }\frac{S_{n}}{n}= \tau \right)=1$).
Since $\tau>0$, we have $\mathbb{P}(\lim_{ n \to \infty } S_{n}=\infty)=1$.
Thus, for any $0\leq t<\infty$, $\mathbb{P}(N(t)=\infty)=\mathbb{P}(\lim_{ n \to \infty }S_{n}\leq t)=1-\mathbb{P}(\lim_{ n \to \infty }S_{n}>t)=0$.

### Theorem 8.4
Let $G_{k}(t)=\mathbb{P}(S_{k}\leq t)$ for $t\geq 0.$ Then $p_{k}(t)=\mathbb{P}(N(t)=k)$ (k events happen by time t) = $G_{k}(t)-G_{k+1}(t),\;t\geq0$.

Proof: Intuitively this makes sense because in order for $N(t)=k$ we need the $S_{k}\leq t$ and $S_{k+1}>t$.
$\mathbb{P}(N(t)=k)=\mathbb{P}(N(t)\geq k)-\mathbb{P}(N(t)\geq k+1)=\mathbb{P}(S_{k}\leq t)-\mathbb{P}(S_{k+1}\leq t)=G_{k}(t)-G_{k+1}(t)$.



The function $G_{k}(\cdot)$ is called the k-fold convolution of $G(\cdot)$ with itself. With the initial condition $G_{0}(\cdot)=1$, we can write $$
G_{k}(t)=\int_{0}^{t}G_{k-1}(t-u)dG(u)
$$ or we can also write it as
$$
G_{k}(t)=\int_{0}^{t}G(t-u)dG_{k-1}(u)
$$
Let $\tilde{G(s)}$ denote the LST for $G(t)$ $$
\tilde{G}(s)=\int_{0}^\infty e^{-st}dG(t)
$$
We know that the LST of a convolution is the product of the LSTs of individual distributions.
Thus, we can write the LST for $G_{k}(\cdot)$ as $$\tilde{G}_{k}(s)=(\tilde{G}(s))^{k}$$
Recall $p_{k}(t)=\mathbb{P}(N(t)=k)$. Then using the previous theorem we see that $$
\tilde{p}_{k}(s)=\tilde{G}_{k}(s)-\tilde{G}_{k+1}(s)=(\tilde{G}(s))^{k}(1-\tilde{G}(s))
$$
---
An important tool in renewal theory is renewal argument (conditioning on first event and work from there). 
Example (renewal argument): Suppose that we want to find an expression for $p_{k}(t)=\mathbb{P}(N(t)=k)$ with k > 0.

$$\mathbb{P}(N(t)=k|S_{1}=u)=
\begin{cases}
0 & u>t \\
p_{k-1}(t-u) & u\leq t
\end{cases}
$$
Thus,
$$
p_{k}(t)=\int_{0}^{\infty}\mathbb{P}((N(t)=k|S_{1}=u)dG(u)=\int_{0}^{t}\mathbb{P}(N(t-u)=k-1)dG(u)
$$
Which can be seen as
$$
p_{k}(t)=\int_{0}^{t}p_{k-1}(t-u)dG(u)
$$
We also have $p_{0}(t)=\mathbb{P}(N(t)=0)=1-G(t)$
In general, this doesn't seem very helpful to find a closed form expression for $p_{k}(t)$. However, it would be helpful if $X_{n}$'s are integer valued. Suppose $\alpha_{1}=\mathbb{P}(X_{n}=i)$ for $i=0,1,2,\dots$. Then we can write $p_{0}(n)=1-\sum_{i=0}^{n}\alpha_{i}\implies p_{k}(n)=\sum_{i=0}^{n}\alpha_{i}p_{k-1}(n-i)$ which can be used to determine $p_{k}(n)$.

---

Define $N(\infty)$ as the almost sure limit of $N(t)$ as $t\to \infty$. Note that "almost sure" here means converges with probability 1.$$
N(\infty)=\lim_{ t \to \infty } N(t)\;\;w.p. 1
$$
Also let $$
G(\infty)=\lim_{ t \to \infty } G(t)
$$
### Theorem 8.5
i) $G(\infty)=1\implies \mathbb{P}(N(\infty)=\infty)=1$
ii) $G(\infty)<1\implies \mathbb{P}(N(\infty)=k)=(G(\infty))^{k}(1-G(\infty))$

Proof: $N(\infty)=k<\infty \iff X_{n}<\infty$ for $1<n\leq k$ and $X_{k+1}=\infty$.
Note that $X_{n}<\infty$ for $1<n\leq k$ and $X_{k+1}=\infty$ has zero probability if $G(\infty)=\mathbb{P}(X_{n}<\infty)=1$. Otherwise, the probability is $(G(\infty))^{k}(1-G(\infty))$.

Definition: $\{N(t),\;t\geq0\}$ is called 
i) recurrent if $\mathbb{P}(N(\infty)=\infty)=1$
ii) transient if $\mathbb{P}(N(\infty)=\infty)<1$
From now on we assume recurrent renewal processes.

### Elementary Renewal Theorem 8.6
For a recurrent $\{N(t),\;t\geq0\}$ with mean interevent time $\tau>0$, we have $$\frac{N(t)}{t} \to \frac{1}{\tau}\;\;w.p. 1$$
If $\tau=\infty$, $\frac{N(t)}{t} \to 0\;\; w.p. 1$.

Proof: (For the case $\tau <\infty$).
Note that $S_{N(t)}\leq t<S_{N(t)+1}$, so now consider $\frac{S_{N(t)}}{N(t)} \leq \frac{t}{N(t)} <\frac{S_{N(t)+1}}{N(t)}$. Now we let $t\to \infty$. Since $\{N(t),\;t\geq0\}$ is recurrent we know that $N(t)\to \infty$ as $t\to \infty$ and then using the Strong Law of Large Numbers we get $\lim_{ t \to \infty } \frac{S_{N(t)}}{N(t)}=\lim_{ n \to \infty } \frac{S_{n}}{n}=\tau$ with probability 1.
Similarly $\lim_{ t \to \infty } \frac{S_{N(t)+1}}{N(t)}=\lim_{ n \to \infty } \frac{S_{n+1}}{n}=\tau$.
Thus, $\lim_{ t \to \infty } inf \frac{t}{N(t)} \geq \lim_{ t \to \infty } \frac{S_{N(t)}}{N(t)}=\tau$.
And $\lim_{ t \to \infty } sup \frac{t}{N(t)} \leq \lim_{ t \to \infty } \frac{S_{N(t)+1}}{N(t)+1}=\tau$.
Hence, $\lim_{ t \to \infty } \frac{t}{N(t)}=\tau$ with probability 1 and thus $\lim_{ t \to \infty } \frac{N(t)}{t} =\frac{1}{\tau}$ with probability 1 (see the book for the case of $\tau=\infty$).

### Theorem 8.7 (CLT for $N(t)$)
For a recurrent $\{N(t),\;t\geq0\}$ with interevent times $\tau$ ($0<\tau<\infty$) and variance $\sigma^{2}<\infty$ we have $$
\lim_{ t \to \infty } \mathbb{P}\left( \frac{N(t)-\frac{t}{\tau}}{\sqrt{ \frac{\sigma^{2}t}{\tau^{3}} }}\leq x \right)=\Phi(x)
$$
Which is the standard normal. Hence for large t, $N(t)$ is approximately normal with mean $\frac{t}{\tau}$ and variance $\frac{\sigma^{2}t}{\tau^{3}}$.
Think about it as interevent times occur with rate $\frac{1}{\tau}$ so when trying to find the expectation the amount of events you would expect after t time is $\frac{t}{\tau}$ (multiplying time * rate).

### The Renewal Function (Theorem 8.8)
Define $M(t)=\mathbb{E}N(t),\;t\geq0$.
$M(t)$ is called the renewal function.
$$
M(t)=\sum_{k=0}^{\infty} k\mathbb{P}(N(t)=k)=\sum_{k=0}^{\infty} k(G_{k}(t)-G_{k+1}(t))=\sum_{k=1}^{\infty} G_{k}(t) \tag{8.14}
$$


Define the LST of $M(t)$ as $$\tilde{M}(s)=\int_{0}^{\infty}e^{-st}dM(t)$$
### Theorem 8.9 The Renewal Equation
We have $$M(t)=G(t)+\int_{0}^{t} M(t-u)dG(u),\;t\geq0\tag{8.15}$$ and $$
\tilde{M}(s)=\frac{\tilde{G}(s)}{1-\tilde{G}(s)} \tag{8.16}
$$
Proof: Using the renewal argument, $$\mathbb{E}(N(t)|S_{1}=u)=
\begin{cases}
0 & u>t \\
1+M(t-u) & u\leq t
\end{cases}
$$
Then, $$
M(t)=\int_{0}^{\infty} \mathbb{E}[N(t)|S_{1}=u]dG(u)=\int_{0}^{t}(1+M(t-u))dG(u)=G(t)+\int_{0}^{t}M(t-u)dG(u)
$$
Taking LSTs of both sides we get
$$
\tilde{M}(s)=\tilde{G}(s)+\tilde{M}(s)\tilde{G}(s)
	$$ (property is in appendix of the book, but we will show shortly). This equation can be rearranged to $$
\tilde{M}(s)=\frac{\tilde{G}(s)}{1-\tilde{G}(s)}
$$

To show how we get $\tilde{M}(s),\tilde{G}(s)$ let $$
H(t)=\int_{0}^{t}M(t-u)dG(u) \implies \tilde{H}(s)=\int_{0}^{\infty} e^{-st}dH(t) = \int_{0}^{\infty}e^{-st} \left( \int_{0}^{t}dM(t-u) \right) dG(u)
$$
We use Leibniz rule for the second equality. Then next we just pull the integral inside and $\pm$ u to exponential with the goal of finding LST.
$$
=\int_{0}^{\infty}\int_{0}^{t}e^{-s(t-u)}dM(t-u)e^{-su}dG(u) =\int_{0}^{\infty}e^{-su}dG(u)\int_{0}^{\infty}e^{-st}dM(t)=\tilde{G}(s)\tilde{M}(s)
$$

### Theorem 8.10
The renewal function $\{M(t),\;t\geq0\}$ completely characterizes the renewal process $\{N(t),\;t\geq0\}$.
This tells us that given a renewal function we have a unique renewal process.
Proof: We can rearrange equation 8.16 to get $$
\tilde{G}(s)=\frac{\tilde{M}(s)}{1+\tilde{M}(s)}\tag{8.18}
$$Which tells us that $\tilde{M}(s)$ is all that is necessary to determine $\tilde{G}(s)$ which defines the RP.

2/17

Recall that $\{N(t),\;t\geq0\}$ is a Renewal Process and $M(t) = \sum_{i=0}^{\infty} k\mathbb{P}(N(t)=i)=\sum_{k=1}^{\infty} G_{k}(t)$.

Example of above theorem (renewal function gives unique renewal process): Suppose that the interevent time distributions is $G(x)=1-e^{-\lambda x}$ for $x\geq0$ i.e. exponential. Then $\tilde{G}(s)=\frac{\lambda}{\lambda+s}$ and then $\tilde{M}(s)=\frac{\lambda}{s}$. Inverting this, we get $M(t)=\lambda t$ for $t\geq0$.
Additionally, this means if we can find $M(t)=ct$ for some constant $c$ then we can conclude that this is a PP(ct) (since $M(t)$ uniquely characterizes it).
**This means that if an RP has a linear renewal function M(t) then it is a PP**

### Theorem 8.11
$M(t)<\infty$ for all $t\geq0$ for a renewal process with mean interevent times $\tau>0$.
Proof: See the book.

### Elementary Renewal Theorem 8.12
$$
\lim_{ t \to \infty } \frac{M(t)}{t} = \frac{1}{\tau}\tag{8.19}
	$$ if $\tau<\infty$. (Expected rate of events converges to $\frac{1}{\tau}$) and $$
\lim_{ t \to \infty } \frac{M(t)}{t}=0
$$
if $\tau=\infty$. (I.e. the expected value of N(t)/t converges to $\frac{1}{\tau}$ or 0 respectively).

We showed before that $\frac{N(t)}{t}\to \frac{1}{\tau}$ with probability 1. Since convergence in probability does not imply convergence in expectation we need to prove the result.
To prove this result (ERT) we need the following lemma/theorem 8.13: $$\mathbb{E}[S_{N(t)+1}]=\tau(M(t)+1)$$ for $t\geq0$
Proof: Using a renewal argument lets define $H(t)=\mathbb{E}[S_{N(t)+1}]$.
$\mathbb{E}[S_{N(t)+1}|S_{1}=u]=$ (consider now if u is before or after t)
$$
\mathbb{E}[S_{N(t)+1}|S_{1}=u]=
\begin{cases}
u & u>t \\
u+H(t-u) & u\leq t
\end{cases}
$$
The second case is because you are interested in the expected event of $N(t-u)$.
$$
H(t)=\int_{0}^{\infty}\mathbb{E}[S_{N(t)+1}|S_{1}=u]dG(u)=\int_{0}^{t}(u+H(t-u))dGu+\int_{t}^{\infty}udG(u)
$$
$$
=\int_{0}^{\infty}udG(u)+\int_{t}^{\infty}H(t-u)dG(u)=\tau+\int_{0}^{\infty}H(t-u)dG(u)
$$
Taking the LSTs on both sides we get $\tilde{H}(s)=\tau+\tilde{H}(s)\tilde{G}(s)$. Then solving for $\tilde{H}(s)$ we get $$
\tilde{H}(s)=\frac{\tau}{1-\tilde{G}(s)}=\tau\left( 1+\frac{\tilde{G(s)}}{1-\tilde{G}(s)} \right)=\tau(1+\tilde{M}(t))
$$
Inverting we get $$
H(t)=\mathbb{E}[S_{N(t)+1}]=\tau(1+M(t))
$$

Note that it is **not true** that $\mathbb{E}S_{N(t)}=\tau M(t)$ although this may seem intuitive. Lets show why for practice with renewal argument. Define $I(t)=\mathbb{E}S_{N(t)}$
$$
\mathbb{E}[S_{N(t)}|S_{1}=u]=
\begin{cases}
0 & u>t \\
u+I(t-u) & u\leq t
\end{cases}
$$
Thus, $$
I(t)=\int_{0}^{t}u+I(t-u)dG(u)=\int_{0}^{t}udG(u)+\int_{0}^{t}I(t-u)dG(u)
$$
this results in $\tilde{I}(s)=a+\tilde{I}(s)\tilde{G(s)}$ where a is just a constant representing the first integrals evaluation. Converting this we get, $I(t)=a(1+M(t))$. Thus, $$
\mathbb{E}[S_{N(t)}]\neq \tau M(t)
$$

Returning to the previous proof above ($H(t)=\mathbb{E}[S_{N(t)+1}]=\tau(1+M(t))$).
Let $\tau<\infty$ (the infinite case is straightforward). We have $S_{N(t)+1}>t$ (which implies the expectation / t is greater than 1 in line below) and we now have an expression for $\mathbb{E}[S_{N(t)+1}]$.
Thus, $$
\frac{\mathbb{E}[S_{N(t)+1}]}{t} = \frac{\tau(M(t))+\tau}{t}>1 \implies \frac{M(t)}{t}+\frac{1}{t}> \frac{1}{\tau}\implies \frac{M(t)}{t} > \frac{1}{\tau} - \frac{1}{t}
$$
Then if we take the limit inferior,
$$
\liminf_{ t \to \infty } \frac{M(t)}{t}\geq \frac{1}{\tau} \tag{*}
$$
Now for fixed $0<T<\infty$, define $X_{n}'=min(X_{n},T)$. 
Let $\{N'(t),\;t\geq0\}$ be the corresponding renewal process and $M'(t)$, $t\geq0$ be the corresponding renewal function. Then, $S_{N'(t)+1}\leq t+T$ (we know that the next event after the $S_{N'(t)}$ event is at most $T$ units of time later due to $X_{n}'=min(X_{n},T)$) with probability 1. Now taking expected value on both sides, we know that $\tau'(M'(t)+1)\leq t+T$ where $\tau'=\mathbb{E}[X_{n}']$.
This results in $$
\frac{M'(t)+1}{t}\leq \frac{t+T}{t\tau'}\implies \frac{M'(t)}{t} \leq \frac{t+T-\tau'}{t\tau'} \implies \frac{M'(t)}{t} \leq \frac{1}{\tau'}+ \frac{T-\tau'}{t\tau'}
$$
Thus,
$$
\frac{M(t)}{t} \leq \frac{M'(t)}{t} \leq \frac{1}{\tau'} + \frac{T-\tau'}{t\tau'}
$$Then we have $$
\limsup_{ t \to \infty } \frac{M(t)}{t} \leq \frac{1}{\tau'}
$$As $T\to \infty$, $\tau'\to \tau$ and thus letting $T\to \infty$ we get $\limsup_{ t \to \infty } \frac{M(t)}{t}  \leq\frac{1}{\tau}$. The result (of original theorem being proved) follows from this and the fact that $\tau<\infty$.

## Renewal Type Equations
Equations in the form of $$
H(t)=D(t)+\int_{0}^{t}H(t-u)dG(u)\tag{8.25}
$$ which typically appear when the renewal argument is used. In this equation we have
- G(.): cdf of a random variable with G(0)=0 and G($\infty$)=1
- D(.): some known function that appears when using renewal argument
- H(.): to be determined/what we want to find
We've seen the special case where $D(t)=G(t)$, where $M(t)=G(t)+\int_{0}^{t}M(t-u)dG(u)$ which we called the renewal equation. Thus, the renewal type equation is a generalization of the renewal equation.
When $D(t)\neq G(t)$ we call that a renewal-type equation.

### Theorem 8.15
Suppose that $|D(t)|<\infty, \forall t\geq0$. Then, there exists a unique solution to the renewal-type equation such that $H(t)<\infty,\forall t\geq0$ and the solution is given by $$
H(t)=D(t)+\int_{0}^{\infty}D(t-u)dM(u)
$$where M(.) is the renewal function associated with G(.).

Proof: (Introduce the following notation: $A*B(t)=\int_{0}^{t}A(t-u)dB(u)$). Thus, $H(t)=D(t)+H*G(t)$ is a renewal-type equation form. Plugging in $H=D+H*G$ on the left hand side we get, $H=D+(D+H*G)*G=D+(D*G)+H*G_{2}$ if we plug in $H=D+H*G$ again and do this n times in total then we get $$
H=D+D*\sum_{k=1}^{n-1} G_{k}+H*G_{n},\;n\geq1 \tag{**}
$$
Let $n\to \infty$ on both sides then we get $$
H=D+D*\sum_{k=1}^{\infty} G_{k}
$$because $G_{n}\to0$ using the fact that $G_{k}$ is decreasing in k and $M(t)<\infty$. ($G_{k}$ is probability of being more than k events up to time t, so having infinite events in finite time is probability 0).
Thus, we get $H=D+D*M$ as the infinite sum of $G_{k}$ evaluates to $M$ (see above).
Thus, we have shown that $H$ as described in the renewal-type equation has a solution.
Now we just want to show it is a unique solution.
Define $c=\sup_{ 0\leq x\leq t}|D(x)| < \infty$. Then, from our result $H=D+D*M$ we get $|H(t)|\leq|D(t)| + \int_{0}^{t}|D(t-u)|dM(u)\leq c+cM(t)<\infty$.
Thus, $H(\cdot)$ is bounded. For uniqueness, suppose $H_{1}\neq H_{2}$ are two solutions. Then, $\bar{H}=H_{1}-H_{2}=(H_{1}-H_{2})*G_{n}$ (from equation $(**)$ above). And as $n\to \infty$ we must have that $\bar{H}\to0$ indicating a unique solution.

2/19 **Quick Summary/Review** at beginning of class:
Recall $N(t)$ is a renewal process if the interarrival times between events ($X_{1},X_{2},\dots$) are iid random variables where $N(t)$ is the number of events by the time $t$.
Also recall $\frac{N(t)}{t}\to \tau$ with probability 1 if $\tau<\infty$ and $\frac{N(t)}{t}\to0$ with probability 1 if $\tau=\infty$.
Also recall $M(t)=\mathbb{E}[N(t)]$ for $t\geq0$.
Last class we also showed the renewal equation: $M(t)=G(t)+\int_{0}^{t}M(t-u)dG(u)$ for $t\geq0$.
We can get this in form of LSTs: $\tilde{M}(s)=\frac{\tilde{G}(s)}{1-\tilde{G}(s)}$
$M(t)<\infty$ for $t\geq0$ if $\tau>0$
Recall the Elementary Renewal Theorem (ERT): $\frac{M(t)}{t} \to \frac{1}{\tau}$ if $\tau<\infty$ and $\frac{M(t)}{t} \to0$ if $\tau=\infty$ as $t\to \infty$.
Recall renewal argument is essentially conditioning on first event and constructing an equation that must be true in the future; i.e. by focusing on one cycle and building a recursive equation.
Also the renewal-type equations come directly from this renewal argument way of thinking (by creating a recursive equation): $H(t)=D(t)+\int_{0}^{t}H(t-u)dG(u)$
There is a unique solution to this renewal-type equation: $H(t)=D(t)+\int_{0}^{\infty}D(t-u)dM(u)$

### Theorem 8.16
If $D(t)$ has an LST $\tilde{D}(s)$ then $\tilde{H}(s)=\frac{\tilde{D}(s)}{1-\tilde{G}(s)}$
Proof: Take LSTs of both sides of the equation above so that you get $\tilde{H}(s)=\tilde{D}(s)+\tilde{D}(s)\tilde{M}(s)$. Then use the fact that $\tilde{M}(s)=\frac{\tilde{G}(s)}{1-\tilde{G}(s)}$ to conclude that $\tilde{H}(s)=\frac{\tilde{D}(s)}{1-\tilde{G}(s)}$

**Example:** Consider a machine that alternates between two states: up and down. Successive up times are iid exp($\mu$) and when the machine fails it goes to the down state and then the repair time is directly proportional to the preceding up time. So if the previous up time is $U$ then the downtime is $cU$ where $c>0$ is some constant. Suppose the machine is up at time 0. Find the probability that the machine is up at time $t>0$.
Lets define (our variable of interest) $H(t)=\mathbb{P}(X(t)=1)$ where $X(t)=1$ means the machine is up at time t.
We'll look at renewal points where the machine transitions back to up state (so $S_{0}=0$ and $S_{1}$ occurs when the machine has transitioned to down state then up again).
Let $S_{1}=U_{1}+D_{1}\implies S_{1}=(1+c)U_{1}\implies S_{1}$ ~ $\exp\left( \frac{\mu}{1+c}\right)$.
$$\mathbb{P}(X(t)=1|S_{1}=u)
=\begin{cases}
H(t-u) & u\leq t \\
\mathbb{P}(U_{1}>t|S_{1}=u) & u>t
\end{cases}$$
So we can further write, $\mathbb{P}(X(t)=1)=H(t)=\int_{0}^{\infty}\mathbb{P}(X(t)=1|S_{1}=u)dG(u)=\int_{0}^{t}H(t-u)dG(u)+\int_{t}^{\infty}\mathbb{P}(U_{1}>t|S_{1}=u)dG(u)$ where $G(u)$ is the CDF for $S_{1}$.
For $u\leq t$, $\mathbb{P}(U_{1}>t|S_{1}=u)=0$. Thus, our expression simplifies to $$
H(t)=\int_{0}^{t}H(t-u)dG(u)+\int_{0}^{\infty}\mathbb{P}(U_{1}>t|S_{1}=u)dG(u)
$$Furthermore, we can now get $$
H(t)=\mathbb{P}(U_{1}>t)+\int_{0}^{t}H(t-u)dG(u)=e^{-\mu t}+\int_{0}^{t}H(u-t)dG(u)
$$
This is a renewal type equation with $D(t)=e^{-\mu t}$ and $G(\cdot)$ is the cdf of exponential random variable with rate $\frac{\mu}{1+c}$.
The solution to $H(t)$ is $H(t)=D(t)+\int_{0}^{t}D(t-u)dM(t)$.
Since $G(\cdot)$ is exp we can say that $M(t)=\frac{\mu}{1+c}t$.
Then, $$H(t)=e^{-\mu t}+\int_{0}^{t}e^{-\mu(t-u)} \frac{\mu}{1+c}du=\frac{1+ce^{-\mu t}}{1+c}$$

**Example:** We will look at busy periods in an M/G/$\infty$ queue. Assume arrivals are Poisson with rate $\lambda$ and service times are iid with cdf $B(\cdot)$. Let $X(t)$ denote the number of customers in the system at time t.
Suppose that a customer has just arrived at an empty system.
Define $T=min\{t\geq0:X(t)=0\}$. Thus, $T$ is essentially the length of busy period. We want to find the LST of $T$ and $\mathbb{E}[T]$. We can view renewal points as the start of another busy period (i.e. one entire busy period + the following idle period) to use a renewal argument.
Define $S_{n}$ to be the nth time a customer enters an empty system, $\{S_{n},\;n\geq0\}$ is a renewal process.
Let $H(t)=\mathbb{P}(X(t)=0)$. We can now use a renewal argument.
$$\mathbb{P}(X(t)=0|S_{1}=u)
=\begin{cases}
H(t-u) & u\leq t \\
\mathbb{P}(T\leq t|S_{1}=u) & u>t
\end{cases}$$
Let $G(\cdot)$ be the CDF of $S_{1}$ we find $H(t)=\int_{0}^{\infty}\mathbb{P}(X(t)=0|S_{1}=u)dG(u)=\int_{0}^{t}H(t-u)dG(u)+\int_{t}^{\infty}\mathbb{P}(T\leq t|S_{1}=u)dG(u)$
Similar to the previous example, lets examine $\mathbb{P}(T\leq t|S_{1}=u)=1$ for $u\leq t$ (intuitively because the $S_{1}$ occurring means that a busy period and idle period have occurred so our first busy period ending i.e. $T$ must have happened, thus probability 1).
So we can now simplify the above expression as $$
\int_{t}^{\infty}\mathbb{P}(T\leq t|S_{1}=u)dG(u)=\int_{0}^{\infty}\mathbb{P}(T\leq t|S_{1}=u)dG(u)-\int_{0}^{t}1dG(u)=\mathbb{P}(T\leq t)-G(t)\implies
$$
$$
H(t)=\mathbb{P}(T\leq t)-G(t)+\int_{0}^{t}H(t-u)dG(u)\tag{*}
$$
Note that $S_{1}=T+M$ where $M$~exp($\lambda$) (idle period).
Therefore, $\tilde{G}(s)=\tilde{F}(s)\tilde{M}(s)=\tilde{F}(s) \frac{\lambda}{\lambda+s}$ where $\tilde{F}(s)$ is the LST for $T$ and $\tilde{G}(s)$ is the LST for $S_{1}$.
Let $\tilde{H}(s)$ be the LST for $H(\cdot)$ then we can use equation (\*). Taking LST of both sides of (\*) we get $$
\tilde{H}(s)=\tilde{F}(s)-\tilde{F}(s) \frac{\lambda}{\lambda+s}+\tilde{H}(s)\tilde{F}(s) \frac{\lambda}{\lambda+s}\implies
$$
$$
\tilde{F}(s)=\frac{(s+\lambda)\tilde{H}(s)}{s+\lambda\tilde{H}(s)}
$$
$\tilde{H}(s)$ is the LST for $H(t)=\exp\left( -\lambda \int_{0}^{t}(1-B(u))du \right)$ (from M/G/$\infty$ results; recall $B(u)$ is the distribution of service times).
We then know that $\lim_{ s \to \infty } \tilde{H}(s)=H(\infty)=e^{-\lambda \tau}$.
Then differentiating $\tilde{F}(s)$ with respect to s and letting $s=0$, we get $$
\mathbb{E}[T]= \frac{e^{\lambda \tau}-1}{\lambda}
$$
2/24
Midterm 2 weeks from Thursday, will cover as much from Renewal processes as possible by next Thursday (week before exam) is material that will be up to for the exam
Previous exams may be helpful, but every question will be quite different so may not be super helpful (but still worth doing)

Recall: $H(t)=D(t)+\int_{0}^{t}H(t-u)dG(u)$ where $D(t)$ is known and $G(u)$ is the distribution of a renewal process. We want to find $H(t)$ which has a solution of $H(t)=D(t)+\int_{0}^{t}D(t-u)dM(u)$ where $M(u)$ is a renewal function.
### Asymptotic solution ($t\to \infty$) to the renewal-type equations (KRT)
#### Periodicity
Definition: A non-negative random variable $X$ (or its distribution) is called periodic (or arithmetic)  if there exists some $d>0$ such that $\sum_{k=0}^{\infty} \mathbb{P}(X=kd)=1$ (i.e. $X$ can only take on values that are a multiple of d. Then the largest value of $d$ for which the above equality is valid is called the span or period of $X$ (or its distribution). If there is no such $d$ then the random variable $X$ is called aperiodic.
A renewal process is periodic if the random variable that governs interrenewal times is periodic. Otherwise, it is aperiodic.

Example: All continuous random variables are aperiodic
Example: If $X$ is a discrete random variable with sample space $S$ = {1,$\sqrt{ 2 }$} then $X$ is aperiodic.
Example: If $X$ is a discrete random variable with sample space $S$ = {0,$\sqrt{ 2 }$} then $X$ is periodic with $d=\sqrt{ 2 }$.
Example: Lastly if sample space is all non-negative integers then periodic with $d=1$.

### Key Renewal Theorem 8.17
Let $H$ be a solution to the following renewal-type equation:$$
H(t)=D(t)+\int_{0}^{t}H(t-u)dG(u)
$$
Suppose that $D(\cdot)$ is the difference of two non-negative bounded, monotone functions and $\int_{0}^{\infty}|D(u)|du<\infty$. Then,
1. If $G(\cdot)$ is aperiodic with mean $\tau>0$, then $\lim_{ t \to \infty } H(t)=\frac{1}{\tau}\int_{0}^{\infty}D(u)du$
2. If $G(\cdot)$ is periodic with mean $\tau>0$, then $\lim_{ k \to \infty } H(kd+x)=\frac{d}{\tau}\sum_{k=0}^{\infty} D(kd+x)$ for $0\leq x<d$

### Blackwell's Renewal Theorem 8.18
Direct consequence of Key Renewal Theorem.
Let $M(\cdot)$ be the renewal function of a renewal process with mean interrenewal time $\tau>0$.
1. If the renewal process is aperiodic, $\lim_{ t \to \infty } M(t+h)-M(t)=\frac{h}{\tau}$ for $h\geq0$.
2. If the renewal process is periodic with period $d$, $\lim_{ t \to \infty }[M(t+kd)-M(t)]=\frac{kd}{\tau}$ for $k=0,1,2,\dots$
Basically says that, in the limit, the number of events within an interval of length h is $\frac{h}{\tau}$.
Recall that if this was true for any t (rather than just in the limit) then it is a Poisson Process, look above/previous classes.
Proof: Part 1
Consider the renewal-type equation with $$
D(t)=
\begin{cases}
1 & 0\leq t\leq h \\
0 & t>h
\end{cases}
$$
we know from the solution to the renewal-type equation theorem that $$
H(t)=D(t)+\int_{0}^{t}D(t-u)dM(u)
$$ For $t>h$ this reduces to $$
H(t)=\int_{t-h}^{t}dM(u)=M(t)-M(t-h)
$$Then from the KRT, we get $$
\lim_{ t \to \infty } M(t+h)-M(t)=\lim_{ t \to \infty } H(t+h)=\frac{1}{\tau}\int_{0}^{\infty}D(u)du=\frac{h}{\tau}
$$

## Recurrence Times
For an aperiodic renewal process $\{N(t),\;t\geq0\}$, define
- $A(t)=t-S_{N(t)}$ for $t\geq0$ (how much time has passed since the last event) called the age process (also called backward recurrence process)
- $B(t)=S_{N(t)+1}-t$ for $t\geq0$ (how much time until the next event) called the remaining life process (also called forward recurrence process)
- $C(t)=X_{N(t)}=S_{N(t)+1}-S_{N(t)}$ (how long is the renewal time at time t) called the total life process. Note that $C(t)=A(t)+B(t)$
Note that $A(t)$'s graph will look like lines with slope 1 and that reset to 0 at a renewal (so piecewise all with slope 1).
Note that $B(t)$'s graph will be the opposite of $A(t)$ all with slope negative 1 until it hits 0 (where a renewal occurs) where it resets up to the length of remaining time until next event.
Lastly, note that $C(t)$'s graph will look like a piecewise step function where it is just constant at the value of the length one renewal.

### Theorem: Remaining Life Process 8.19
For a given $x>0$, $H(t)=\mathbb{P}(B(t)>x)$ satisfies the renewal-type equation $$
H(t)=1-G(x+t)+\int_{0}^{t}H(t-u)dG(u)
$$and $$
\lim_{ t \to \infty } \mathbb{P}(B(t)>x)=\frac{1}{\tau}\int_{x}^{\infty}(1-G(u))du
$$
Proof: Conditioning on $S_{1}$ we get $$
\mathbb{P}(B(t)>x|S_{1}=u)=
\begin{cases} \\
H(t-u) & u\leq t \\
0 & t<u\leq t+x \\
1 & u>t+x
\end{cases}
$$
Thus, we get $$
H(t)=\int_{0}^{\infty}\mathbb{P}(B(t)>x|S_{1}=u)dG(u)=1-G(x+t)+\int_{0}^{t}H(t-u)dG(u)
$$
Which is the first part proven.
Note that $D(t)=1-G(x+t)$ is monotone and satisfies the condition of the KRT.
So using KRT we immediately get $$
\lim_{ t \to \infty } H(t)=\lim_{ t \to \infty } \mathbb{P}(B(t)>x)=\frac{1}{\tau}\int_{0}^{\infty}(1-G(x+u))du=\frac{1}{\tau}\int_{x}^{\infty}(1-G(u))du
$$Thus proving the second portion.

### Theorem: Age Process 8.20
We have $$
\lim_{ t \to \infty } \mathbb{P}(A(t)\geq x)=\frac{1}{\tau}\int_{x}^{\infty}(1-G(u))du
$$Note it is the same as the theorem for remaining life process. Intuitively, why should the last event be any different than the next event given that we are showing up randomly.
Proof: {$A(t)\geq x$} is the same as saying no renewals over $(t-x,t]$ which is the same as saying {$B(t-x)>x$} (time remaining is greater than x so that no renewals happen up to $t-x+x=t$). So when you take limits as $t\to \infty$ the x in $B(t-x)$ drops and we get $$
\lim_{ t \to \infty } \mathbb{P}(A(t)\geq x)=\lim_{ t \to \infty } \mathbb{P}(B(t-x)>x)=\lim_{ t \to \infty } \mathbb{P}(B(t)>x)=\frac{1}{\tau}\int_{x}^{\infty}(1-G(u))du
$$

### Theorem: Joint Distribution 8.21
We have $$
\lim_{ t \to \infty } \mathbb{P}(A(t)\geq y,B(t)\geq x)=\frac{1}{\tau}\int_{x+y}^{\infty}(1-G(u))du
$$
Proof: For $t>y$, {$A(t)\geq y,B(t)>x$} is the same as saying no renewals in $(t-y,t+x]$ which is also equivalent to {$B(t-y)>x+y$} from similar logic as Age Process theorem. Thus,
$$
\lim_{ t \to \infty } \mathbb{P}(A(t)\geq y,B(t)\geq x)=\lim_{ t \to \infty } \mathbb{P}(B(t-y)>x+y)=\lim_{ t \to \infty } \mathbb{P}(B(t)>x+y)=\frac{1}{\tau}\int_{x+y}^{\infty}(1-G(u))du
$$

Define $G_{e}(t)=\frac{1}{\tau}\int_{0}^{t}(1-G(u))du$ we call it the equilibrium distribution corresponding to $G(\cdot)$.
Note if we plug in $t=\infty$ then the integral evaluates to $\tau$ so $Ge(\infty)=1$.
Note that $$
\frac{1}{\tau}\int_{x}^{\infty}(1-G(u))du+\frac{1}{\tau}\int_{0}^{x}(1-G(u))du=\frac{1}{\tau}\int_{0}^{\infty}(1-G(u))du=1\implies
$$
$$
G_{e}(x)=\frac{1}{\tau}\int_{0}^{x}(1-G(u))du=1-\frac{1}{\tau}\int_{x}^{\infty}(1-G(u))du=\lim_{ t \to \infty } \mathbb{P}(A(t)<x)
$$
Let $X_{e}$~$G_{e}(\cdot)$. Then $$
\mathbb{E}[X_{e}]=\frac{1}{\tau}\left(\frac{\sigma^{2}+\tau^{2}}{2} \right)
$$which we will show next class. 

2/26
Recall:
$A(t)=t-S_{N(t)}$ for $t\geq0$
$B(t)=S_{N(t)+1}-t$ for $t\geq0$
$C(t)=X_{N(t)}=A(t)+B(t)$ for $t\geq0$
$\lim_{ t \to \infty }\mathbb{P}(A(t)\geq x)=\frac{1}{\tau}\int_{x}^{\infty}(1-G(u))du$ and the same is true for remaining lifetime $B(t)$
Define $G_{e}(t)=\frac{1}{\tau}\int_{0}^{t}(1-G(u))du$
$X_{e}$~$G_{e}(\cdot)$
$\mathbb{E}X_{e}=\tau_{e}=\int_{0}^{\infty}(1-G_{e}(t))dt=\int_{0}^{\infty}\left( 1-\frac{1}{\tau}\int_{0}^{t}(1-G(u))du \right)dt=\frac{1}{\tau}\left( \int_{0}^{\infty}\left( \tau-\int_{0}^{t}(1-G(u))du \right)dt \right)$
$=\frac{1}{\tau}\int_{0}^{\infty}\int_{t}^{\infty}(1-G(u))dudt=\frac{1}{\tau}\int_{0}^{\infty}\int_{0}^{u}(1-G(u))dtdu=\frac{1}{\tau}\int_{0}^{\infty}u(1-G(u))du$
$=\frac{1}{\tau}\int_{0}^{\infty}u\int_{u}^{\infty}dG(x)du=\int_{0}^{\infty}\int_{0}^{x}ududG(x)=\frac{1}{2\tau}\int_{0}^{\infty}x^{2}dG(x)=\frac{1}{2\tau}(\sigma^{2}+\tau^{2})$ (integral evaluates to second moment)
Recall that we defined $\sigma^{2}$ as the variance for the interevent time distribution.

Because convergence in distribution does not imply convergence in mean, we **cannot** conclude that $\lim_{ t \to \infty } \mathbb{E}A(t)=\lim_{ t \to \infty }\mathbb{E}B(t)=\mathbb{E}X_{e}$ (**IS NOT TRUE**).

### Theorem 8.22
If $\sigma^{2}<\infty$ then $$
\lim_{ t \to \infty } \mathbb{E}[B(t)]=\frac{\sigma^{2}+\tau^{2}}{2\tau}
$$
Proof: Let $H(t)=\mathbb{E}[B(t)]$. Then using a renewal argument, $$
\mathbb{E}[B(t)|S_{1}=u]=
\begin{cases}
u-t & u>t \\
H(t-u) & u\leq t
\end{cases}
$$
So $H(t)=\int_{0}^{\infty}\mathbb{E}[B(t)|S_{1}=u]dG(u)=\int_{t}^{\infty}(u-t)dG(u)+\int_{0}^{u}H(t-u)dG(u)$.
We can now use this renewal type equation where $\int_{t}^{\infty}(u-t)dG(u)=D(t)$.
Note that $D(t)$ is monotone since if you take the derivative of $D(t)$ to get $-(1-G(t))<0$ using Leibniz rule.
We can also show that $\int_{0}^{\infty}D(u)du=\frac{\sigma^{2}+\tau^{2}}{2}<\infty$.
Then using the Key Renewal theorem we get $$
\lim_{ t \to \infty } H(t)=\lim_{ t \to \infty } \mathbb{E}[B(t)]=\frac{1}{\tau}\int_{0}^{\infty}D(u)du=\frac{\sigma^{2}+\tau^{2}}{2\tau}
$$
Using similar arguments we can also show that if $\sigma^{2}<\infty$ then (Theorem 8.23)$$
\lim_{ t \to \infty } \mathbb{E}[A(t)]=\frac{\sigma^{2}+\tau^{2}}{2\tau}
$$

These then imply that (Theorem 8.24) $$
\lim_{ t \to \infty } \mathbb{E}[C(t)]=\frac{\sigma^{2}+\tau^{2}}{\tau}
$$
Note that $$
\frac{\sigma^{2}+\tau^{2}}{\tau}=\tau+\frac{\sigma^{2}}{\tau}\geq \tau
$$which is seemingly a paradox called the inspection paradox. It is a paradox because $C(t)$ is essentially the interevent times which we would expect to be $\tau$. The intuition is that we are sampling points and we are more likely to land in larger intervals which is what gives the bias term $\frac{\sigma^{2}}{\tau}$.

## Delayed Renewal Processes
A counting process $\{N(t),\;t\geq0\}$ generated by $\{X_{n},\;n\geq0\}$ is called a delayed RP if $X_{1}$ has CDF $F(\cdot)$, $\{X_{n},\;n\geq0\}$ are iid random variables with CDF $G(\cdot)$ and are independent of $X_{1}$.
We will use the superscript $D$ to denote a delayed renewal process.
If $F(\cdot)=G(\cdot)$ then the delayed RP reduces to a standard RP. Also, $$
\{N^{D}(t+X_{1})-1,\;t\geq0\}
$$ is a standard RP.

Example: Let $\{N(t),\;t\geq0\}$ be a standard RP. For fixed $s$ define $N_{s}(t)=N(s+t)-N(s)$.
Essentially pick a time point $s$ and count events after time point $s$. Since $s$ will take place during some interevent time, the first event will have its own CDF, but the following events will follow the same CDF (different from first event). Thus, this is a DRP.

Example: Let $\{X(t),\;t\geq0\}$ be an irreducible CTMC on state space $S=\{0,1,2,\dots\}$ and define $N_{j}(t)$ as the number of entries into state $j$ up to time $t$. Note if we start in state $j$ then this would reduce to a standard RP. However, if we start in any other state then the first entry to state $j$ will have a different CDF than the following interevent times, making $N_{j}(t)$ a DRP. Formally, if $X(0)=j$ then $\{N_{j}(t),\;t\geq0\}$ is an RP. If $X(0)\neq j$ then $\{N_{j}(t),\;t\geq0\}$ is a DRP.

Example: Define $X(t)$ to be the number of customers at time $t$ in an M/G/1 queue. Define $N(t)$ as the number of busy cycles completed by time $t$. If the system starts empty, i.e. $X(0)=0$ then $\{N(t),\;t\geq0\}$ is an RP, otherwise it is a delayed RP.


Here we assume that $F(0-)=0$, $G(0-)=0$, $G(0)<1$, $F(\infty)=G(\infty)=1$.
Delayed renewal processes have many of the same properties as standard RPs.
Let $M^{D}(t)=\mathbb{E}[N^{D}(t)]$ for $t\geq0$.

### Theorem 8.25
The renewal function for the delayed RP is $$
M^{D}(t)=F(t)+\int_{0}^{t}M(t-u)dF(u)
$$
where $M(\cdot)$ is the renewal function for the standard portion of the DRP $N^{D}(t)$.
Its LST is given by $$
\tilde{M^{D}}(s)=\frac{\tilde{F}(s)}{1-\tilde{G}(s)}
$$
Proof: Conditioning on $S_{1}$ we get $$
\mathbb{E}[N^{D}(t)|S_{1}=u]=
\begin{cases}
0 & u>t \\
M(t-u)+1 & u\leq t
\end{cases}
$$
Thus, $$
M^{D}(t)=\int_{0}^{\infty}\mathbb{E}[N^{D}(t)|S_{1}=u]dF(u)=\int_{0}^{t}(M(t-u)+1)dF(u)=F(t)+\int_{0}^{t}M(t-u)dF(u)
$$
Thus proving our first result. Now taking LST's of both sides we get
$$
\tilde{M^{D}}(t)=\tilde{F}(t)+\tilde{M}(t)\tilde{F}(t)=\tilde{F}(t)+\frac{\tilde{F}(t)\tilde{G}(t)}{1-\tilde{G(t)}}=\frac{\tilde{F}(s)}{1-\tilde{G}(s)}
$$
Thus proving the second result of LSTs.


The renewal function $M^{D}(t)$ inherits most properties of $M(t)$. For example, $$\frac{M^{D}(t)}{t}\to \frac{1}{\tau}$$However, $M^{D}(t)$ does not uniquely characterize the delayed RP.

When we use renewal argument in a delayed RP, we get an equation in the form of $$
H^{D}(t)=C(t)+\int_{0}^{t}H(t-u)dF(u),\;t\geq0\tag{1}
$$Which is not a renewal-type equation because $H^{D}(\cdot)\neq H(\cdot)$ which is inside the integral.
However, there is a version of KRT that works for delayed RPs.

### Theorem 8.26
Let $C(\cdot)$ and $H(\cdot)$ be bounded functions with finite limits as $t\to \infty$. Let $H^{D}(\cdot)$ be given as in equation (1) above where $F(\cdot)$ is the CDF of a non-negative random variable. Then it can be shown that $$
\lim_{ t \to \infty } H^{D}(t)=\lim_{ t \to \infty } C(t)+\lim_{ t \to \infty } H(t)
$$
Proof: In textbook. Not going to cover in class. Ziya "Doesn't see this as crucial."

## Equilibrium Renewal Processes
A special DRP in which the first renewal time is given by the equilibrium distribution talked about earlier. If you start the first renewal time with that equilibrium distribution then you know the remaining life and age distributions. Similar to how if you start a DTMC with the stationary distribution then it remains in that stationary distribution as time goes on.

3/3

Recall for DRPs that $X_{1}$~$F(\cdot)$ and $\{X_{n},\;n\geq2\}$~$G(\cdot)$.
Also recall $\tilde{M}^{D}(s)= \frac{\tilde{F}(s)}{1-\tilde{G}(s)}$.
We now shift our focus to Equilibrium Renewal Processes (ERPs) which is a special case of DRPs in which the first time is given by the equilibrium distribution derived earlier.

A delayed RP is an equilibrium RP if $F(\cdot)$ is related to $G(\cdot)$ as follows: $$
F(x)=G_{e}(x)=\frac{1}{\tau}\int_{0}^{x}(1-G(u))du,\;x\geq0
$$ as defined before.
Denote the equilibrium RP as $\{N^{e}(t),\;t\geq0\}$.

### Theorem 8.27
Let $M^{e}(t)=\mathbb{E}[N^{e}(t)]$ denote the renewal equation for the ERP by time $t\geq0$.
Then, $$
M^{e}(t)=\mathbb{E}[N^{e}(t)]=\frac{t}{\tau},\;t\geq0
$$
Note that this does not contradict what we've said previously that only RP's with linear $M(\cdot)$ are PPs because this is not a standard RP. (The delayed aspect makes it non-standard).
Proof: $$
\tilde{F}(s)=\int_{0}^{\infty}e^{-st}dF(t)
$$
where $F(t)=\frac{1}{\tau}\int_{0}^{t}(1-G(u))du$
Thus, $$
\tilde{F}(s)=\frac{1}{\tau}\int_{0}^{\infty}e^{-st}(1-G(t))dt=\frac{1}{\tau} \left[ \int_{0}^{\infty}e^{-st}dt-\int_{0}^{\infty}e^{-st}G(t)dt \right]=\frac{1}{\tau}\left[ \frac{1}{s}-\frac{\tilde{G}(s)}{s} \right]=\frac{1}{\tau} \frac{1-\tilde{G}(s)}{s}
$$
Then, $$
\tilde{M}^{e}(s)=\frac{\tilde{F}(s)}{1-\tilde{G}(s)}=\frac{1}{\tau s}
$$
Inverting it, we set the expression $M^{e}(t)=\frac{t}{\tau}$ for $t\geq0$.

Note that this is not a contradiction to the fact PP is the only renewal process with a linear renewal function since an equilibrium RP is a delayed RP (not standard RP).

Note that $$
\frac{M^{e}(t)}{t}=\frac{1}{\tau},\;t\geq0
$$for any $t\geq0$, not only in the limit unlike the standard RP result.

One can show that $G=G_{e}$ iff $G(\cdot)$ is an exponential distribution.

### Theorem 8.28
Let $B^{e}(t)$ be the lifetime at t in an equilibrium renewal process. Then $$
\mathbb{P}(B^{e}(t)\leq x)=G_{e}(x),\;x\geq0,\;t\geq0
$$
Proof: Skipped in class, can take a look in book.

## Alternating Renewal Processes
A stochastic process that alternates between two states (up and down). Define the following:
$U_{n}$: nth uptime length
$D_{n}$: nth downtime length
Let $$
X(t)=
\begin{cases}
1 & up \\
0 & down
\end{cases}
$$
The stochastic process $\{X(t),\;t\geq0\}$ as described above is called an alternating renewal process (ARP) if $\{(U_{n},D_{n}),\;n\geq0\}$ is a sequence of iid non-negative bivariate random variables.
Note that an ARP is **not** a counting process.

### Theorem 8.30
Suppose the ARP $\{X(t),\;t\geq0\}$ starts in state 1 at time $t=0$. Then, $H(t)=\mathbb{P}(X(t)=1)$ satisfies the following equation $$
H(t)=\mathbb{P}(U_{1}>t)+\int_{0}^{t}H(t-u)dG(u)
$$ where $G(x)=\mathbb{P}(U_{1}+D_{1}\leq x)$ for $x\geq0$.
If $G(\cdot)$ is aperiodic and $\mathbb{E}[U_{1}+D_{1}]<\infty$, then $$
\lim_{ t \to \infty } \mathbb{P}(X(t)=1)=\frac{\mathbb{E}[U_{1}]}{\mathbb{E}[U_{1}]+\mathbb{E}[D_{1}]}
$$
If $G(\cdot)$ is periodic with period $d$ then the limit holds if $t=nd$ and $n\to \infty$.

Proof: Let $S_{n}$ be the nth time the ARP enters state 1. I.e. $$
S_{n}=\sum_{i=1}^{n} (U_{i}+D_{i}),\;n\geq1
$$
Then we can see that $S_{n}$ is a renewal sequence. 
$$
\mathbb{P}(X(t)=1|S_{1}=u)=
\begin{cases}
H(u-t) & u\leq t \\
\mathbb{P}(U_{1}>t|S_{1}=u) & u>t
\end{cases}$$
Let $G(u)=\mathbb{P}(S_{1}\leq u)$. Then $$
H(t)=\int_{0}^{\infty}\mathbb{P}(X(t)=1|S_{1}=u)dG(u)=\int_{0}^{t}H(t-u)dG(u)+\int_{t}^{\infty}\mathbb{P}(U_{1}>t|S_{1}=u)dG(u)
$$Since $\mathbb{P}(U_{1}>t|S_{1}=u)=0$ if $t>u$ we have
$$
\int_{t}^{\infty}\mathbb{P}(U_{1}>t|S_{1}=u)dG(u)=\int_{0}^{\infty}\mathbb{P}(U_{1}>t|S_{1}=u)dG(u)=\mathbb{P}(U_{1}>t)
$$
This proves the first part of the theorem as we now have $$
H(t)=\mathbb{P}(U_{1}>t)+\int_{0}^{t}H(t-u)dG(u)
$$Then, because $\mathbb{P}(U_{1}>t)$ is bounded and monotone and $\int_{0}^{\infty}\mathbb{P}(U_{1}>u)du=\mathbb{E}[U]<\infty$ we can use KRT to get $$
\lim_{ t \to \infty } H(t)=\lim_{ t \to \infty }\mathbb{P}(X(t)=1)=\frac{\mathbb{E}[U_{1}]}{\mathbb{E}[U_{1}]+\mathbb{E}[D_{1}]} 
$$

Example: Remaining life distribution in the limit.
For fixed $x>0$ define $$
X(t)=
\begin{cases}
1 & B(t)>x \\
0 & o.w.
\end{cases}
$$
Pic on phone to help visualize (10:20, 3/3/2026)
Define $U_{n}=max(X_{n}-x,0)$ and $D_{n}=min(X_{n},x)$. Thus when we add $U_{n}+D_{n}=X_{n}$ is satisfied as expected. Note that $U_{n}$ and $D_{n}$ are dependent on each other through $X_{n}$, but this is okay because we just said that we needed $(U_{n},D_{n})$ to be bivariate iid. Formally in class, $U_{n}$ and $D_{n}$ are dependent, but $\{(U_{n},D_{n}),\;n\geq0\}$ is a bivariate iid sequence. Then, assuming $X_{n}$ is aperiodic, we can write $$
\lim_{ t \to \infty } \mathbb{P}(B(t)>x)=\lim_{ t \to \infty } \mathbb{P}(X(t)=1)=\frac{\mathbb{E}[U_{1}]}{\mathbb{E}[U_{1}]+\mathbb{E}[D_{1}]}\tag{1}
$$ from previous theorem. Evaluating this further in the context of this example we have $$
(1)=\frac{\mathbb{E}[max(X_{1}-x,0)]}{\mathbb{E}[X_{1}]}=\frac{1}{\tau}\int_{x}^{\infty}(1-G(u))du
$$

ARPs can be useful for analyzing queues as well. The following are some examples.

Example: M/G/1/1 queue with $\lambda$ as the arrival rate, $\tau$ mean service time and we want to compute the limiting distribution.
Define $X(t)$ as the number of customers in the system at time $t\geq0$.
Then $\{X(t),\;t\geq0\}$ is an ARP if there are no customers initially in the system or someone has just arrived at time $t=0$ to an empty system.
$D_{n}$'s state 0 times are iid exp($\lambda$) and $U_{n}$'s state 1 times are iid service times $G(\cdot)$.
In this case $U_{n}$ and $D_{n}$ are independent of each other.
Thus,$$
P_{1}=\lim_{ t \to \infty }\mathbb{P}(X(t)=1)=\frac{\mathbb{E}[U_{1}]}{\mathbb{E}[U_{1}]+\mathbb{E}[D_{1}]}=\frac{\tau}{\tau+\frac{1}{\lambda}}
$$

Example: G/M/1/1 Queue
$\frac{1}{\lambda}$ is the mean interarrival time and service times are exp($\mu$)
Now $\{U_{n},\;n\geq1\}$ are iid exp($\mu$) and arrivals are iid with cdf $G(\cdot)$ and mean $\frac{1}{\lambda}$.
Note that $\{D_{n},\;n\geq1\}$ does NOT follow the cdf $G(\cdot)$.
So $\{(U_{n}+D_{n}),\;n\geq1\}$ is a sequence of iid bivariate random variables. In order to have a standard RP and this bivariate to hold we need to assume that at time $t=0$ someone has just arrived to an empty system. Example finished below.


3/5
Finish up Renewal Processes and start semi-Markov processes
Recall the above example from last class. We will start off by finishing up this example.

Example: G/M/1/1 Continued
$X(t)$: number of customers in the system at time $t$
Thus, $\{(U_{n}+D_{n}),\;n\geq1\}$ is a sequence of iid random variables (where $D_n$ is the time until next arrival after completion of previous customer). Note that $D_{n}$ does not follow $G(\cdot)$ since some time may have already passed for an arrival during service time $U_{n}$.
Thus, $\{X(t),\;t\geq0\}$ is an alternating renewal process.
Let $N(t)$ be the number of arrivals (may or may not enter) up to time t and let $A_{n}$ be the time of the nth arrival. Recall that in an RP, if you let $S_{n}$ be the time of the nth event then $$
\mathbb{E}[S_{N(t)+1}]=\tau(1+M(t))
$$where $\tau=\frac{1}{\lambda}$ in this specific example by assumption.
From this result, we get $$
\mathbb{E}[U_{1}+D_{1}|U_{1}=t]=\frac{1}{\lambda}(1+M(t))
$$
This is mainly due to the fact that $S_{N(t)+1}$ is the next arrival after time t.
So $$
\mathbb{E}[U_{1}+D_{1}]=\int_{0}^{\infty} \frac{1}{\lambda}(1+M(t))\mu e^{-\mu t}dt=\frac{1}{\lambda}(1+\int_{0}^{\infty} M(t)\mu e^{-\mu t}dt)
$$
From the relationship between Laplace Transform and LST we can write $$
\int_{0}^{\infty}e^{-\mu t}M(t)dt=\frac{1}{\mu}\int_{0}^{\infty}e^{-\mu t}dM(t)
$$
Thus, $$
\mathbb{E}[U_{1}+D_{1}]=\frac{1}{\lambda}\left( 1+\int_{0}^{\infty}e^{-\mu t}dM(t) \right)=\frac{1}{\lambda}(1+\tilde{M}(\mu))=\frac{1}{\lambda}\left( 1+\frac{\tilde{G}(\mu)}{1-\tilde{G}(\mu)} \right)=\frac{1}{\lambda(1-\tilde{G}(\mu))}
$$
Assuming that $G(\cdot)$ is aperiodic we get $$
P_{1}=\lim_{ t \to \infty } \mathbb{P}(X(t)=1)=\frac{\mathbb{E}U_{1}}{\mathbb{E}U_{1}+\mathbb{E}D_{1}}=\rho(1-\tilde{G}(\mu))
$$
where $\rho=\frac{\lambda}{\mu}$.
Hence, $$
P_{0}=\lim_{ t \to \infty } \mathbb{P}(X(t)=0)=1-P_{1}
$$
## Delayed Alternating Renewal Process
The stochastic process $\{X(t),\;t\geq0\}$ with state space $S=\{0,1\}$ with $U_{n}$ being the nth uptime and $D_{n}$ the nth downtime is called a delayed alternating renewal process if $\{(U_{n},D_{n}),\;n\geq2\}$ is a sequence of iid nonnegative bivariate random variables and are independent of $(U_{1},D_{1})$.

A simple example is considering the G/M/1/1 queue above, except without the assumption that we are starting the process with a customer arriving to an empty system. Thus, we can consider $U_{1}=0$ and $D_{1}$ is whatever the time is until the next arrival (which may not follow $G(\cdot)$ since we don't know when the last arrival was to cause this arrival to start).

### Theorem 8.31
Suppose $\{X(t),\;t\geq0\}$ is a delayed ARP that enters state 1 at time $S_{1}=U_{1}+D_{1}$. If $\mathbb{P}(S_{1}<\infty)=1$ and $U_{2}+D_{2}$ is aperiodic with $\mathbb{E}[U_{2}+D_{2}]<\infty$. Then, $$
\lim_{ t \to \infty } \mathbb{P}(X(t)=1)=\frac{\mathbb{E}[U_{2}]}{\mathbb{E}[U_{2}]+\mathbb{E}[D_{2}]}
$$
Essentially the first time doesn't matter.

If $U_{1}+D_{1}$ and $U_{2}+D_{2}$ both have a common period d, then the limit holds if $t=nd$ as $n\to \infty$.


## Semi-Markov Processes
Relaxation of the exponential assumption in CTMCs essentially.
Informal description: Consider a stochastic process $\{X(t),\;t\geq0\}$ with a countable state space $S$. Start at some initial state $X_{0}$ at time $t=0$, stay there for some time $Y_{1}$ and then jumps to state $X_{1}$. We stay there for some time $Y_{2}$ then jump to $X_{2}$, etc.
In general, the process stays at state $X_{n}$ for some time $Y_{n+1}$ and then jumps to state $X_{n+1}$.
Note that $Y_{i}$'s may depend on the state.
Definition: The stochastic process $X(t)$ as described above is called a Semi-Markov process if it has a countable state space $S$ and if the sequence $\{X_{0},(X_{n},Y_{n}),\;n\geq1\}$ satisfies $$\mathbb{P}(X_{n+1}=j,Y_{n+1}\leq y|X_{n}=i,Y_{n},X_{n-1},Y_{n-1},\dots,X_{1},Y_{1},X_{0})$$
$$
=\mathbb{P}(X_{n+1}=j,Y_{n+1}\leq y|X_{n=i})=\mathbb{P}(X_{1}=j,Y_{1}\leq y|X_{0}=i)=G_{ij}(y),\;i,j \in S,\;n\geq0
$$
Note that the second to last equality is just saying time-homogeneity.
A Semi-Markov process has Markov property only at every jump point. We call $G(y)$ the kernel.
$$
G(y)=[G_{ij}(y)]_{i,j\in S},\;y\geq0
$$
We will also call $$
a_{i}=\mathbb{P}(X(0)=i),\;i\in S
$$
our initial distribution.
$\{X_{n},\;n\geq0\}$ is a DTMC (embedded DTMC) with transition probabilities 
$$P_{ij}=G_{ij}(\infty)=\mathbb{P}(X_{n+1}=j|X_{n}=i)$$
Since setting $y=\infty$ essentially removes the $Y_{i}$ component from the joint that $G_{ij}$ represents.
If $\exists i\in S$ for which $G_{ij}(y)=0,\;\forall j\in S$ and $y\geq0$ then $i$ is absorbing and we let $P_{ii}=1$. Then, $$
\sum_{j\in S}P_{ij}=1,\;i\in S
$$
Let $G_{i}(y)$ be the sojourn time distribution for state $i$.$$
G_{i}(y)=\sum_{j\in S}G_{ij}(y)=\mathbb{P}(Y_{1}\leq y|X_{0}=i),\;i\in S,\;y\geq0
$$

Example: An ARP $\{X(t),\;t\geq0\}$ in general is not an SMP. It is an SMP only if there is independence between $U_{n}$ and $D_{n}$ for all n. In that case, we have
$$
G(y)=
\begin{bmatrix}
0 & \mathbb{P}(D_{n}\leq y) \\
\mathbb{P}(U_{n}\leq y) & 0
\end{bmatrix}
$$

Example: CTMC with generator matrix $Q$ is an SMP with kernel $G(y)=[G_{ij}(y)]$ and let $Q=[q_{ij}]$.
Then $G_{ii}(y)=0$ for any $y\geq0$ since in a CTMC you can't transition back to yourself.
Then $G_{ij}(y)=P_{ij}(1-e^{-q_{i}y})$ for $i\neq j$ and $y\geq0$ where $P_{ij}=\frac{q_{ij}}{q_{i}}$, $q_{i}=\sum_{j\neq i}q_{ij}$ for $i\in S$. Essentially, its just the ratio of rate from i to j over total transition rate out of state i times the CDF of exponential as this relates to y.
For $q_{ii}=0$ we let $P_{ii}$=1 and $G_{ij}(y)=0$ (to avoid dividing by 0 above).

Example: Series System
A system that consists of $N$ components in series. All components must be working for the system to function properly. Lifetime of component i is exp($\lambda_{i}$) random variable. At time 0, all components are up. Once a component fails, the system fails and repair starts immediately. Repair time for component i follows $H_{i}(\cdot)$; assume independence from past component lifetimes. We also assume that no failures occur during repair.
Using SMPs, we need N+1 states ($N$ states to represent which state is being repaired and the +1 state for if all are functioning so the system is up).
Formally, let $X(t)=0$ if the system is functioning and $X(t)=i$ for $1\leq i\leq N$ if component i is being repaired at time t. Thus $\{X(t),\;t\geq0\}$ is a SMP. We now need to specify the kernel.
Sojourn time in state 0 is exp($\lambda$) where $\lambda=\sum_{i=1}^{N}\lambda_{i}$.
$P_{0j}=\frac{\lambda_{j}}{\lambda}$ for all $1\leq j\leq N$.
Sojourn time in state i is $H_{i}(\cdot)$ for $i\neq0$.
$P_{ij}=1$ for $j=0$ and $i\neq0$.
Thus we get $$
G(y)=
\begin{bmatrix}
0 & \frac{\lambda_{1}}{\lambda}(1-e^{-\lambda y}) & \dots & \frac{\lambda_{N}}{\lambda}(1-e^{-\lambda y}) \\
H_{1}(y) & 0 & \dots & 0 \\
H_{2}(y) & 0 & \dots & 0 &  \\
\dots & 0 & \dots & 0 \\
H_{N}(y) & 0 & \dots & 0
\end{bmatrix}
$$
Can use a cheat sheet for exam, front and back single sheet.
Up to the end of delayed renewal processes.
Homework will be assigned, but due after spring break.
2 or 3 questions. Can look at posted previous exam questions.
If a question is taking too much time, then you may be on the wrong track.
Ask questions to think a little bit, but if the right approach is used then getting to the answer should be pretty quick.

3/10
Recall kernel $G(y)$ and transition probabilities $G_{ij}(y)=\mathbb{P}(X_{1}=j,Y_{1}\leq y|X_{0}=i)$
## Limiting Behavior of SMPs
Firstly lets define some notation.
Define $T_{j}=min\{t\geq Y_{1}:X(t)=j\}$ for $j\in S$ is the first sojourn time.
Let $\tau_{i}=\mathbb{E}[Y_{1}|X(0)=i]$ for $i\in S$.
Also let $\tau_{ij}=\mathbb{E}[T_{j}|X(0)=i]$ for $i,j \in S$

### Theorem 8.32: First passage Times in SMPs
$\{\tau_{ij}\}$'s satisfy the following equations
$$
\tau_{ij}=\tau_{i}+\sum_{k\neq j}p_{ik}\tau_{kj}
$$
Where $\tau_{i}$ is how much time you stay in i before first transition then the sum is remaining time to return.
This result is used in the result of the next theorem.

### Theorem 8.33
Suppose the embedded DTMC $\{X_{n},\;n\geq0\}$ has a transition probability matrix $P=[p_{ij}]$ that is irreducible and recurrent. Let $\pi$ be a positive solution to $\pi=\pi P$. Then $$
\tau_{jj}=\frac{\sum_{i\in S}\pi_{i}\tau_{i}}{\pi_{j}},\;j\in S
$$
Proof is in the book.

**Definition**: An SMP is said to be irreducible and recurrent if its embedded DTMC is irreducible and recurrent.
**Definition**: An irreducible SMP is said to be positive recurrent if the mean return time to state j is finite ($\tau_{jj}<\infty$) for any $j\in S$.
A necessary and sufficient condition for positive recurrence for the SMP is $$
\sum_{i\in S}\pi_{i}\tau_{i}<\infty
$$
**Definition:** An irreducible and recurrent SMP is called aperiodic if the first passage time $T_{i}$ starting from state i ($X(0)=i$) is an aperiodic random variable for any state $i\in S$. If it is periodic with period d then the SMP is said to be periodic with period d.

We can now use these theorems and definitions to find the limiting distribution of the SMPs.

### Theorem 8.34
Let $\{X(t),\;t\geq0\}$ be an irreducible, positive recurrent, and aperiodic SMP with kernel $G[\cdot]$. Let $\pi$ be a positive solution to $\pi=\pi G(\infty)$. Then $\{X(t),\;t\geq0\}$ has a limiting distribution $[p_{j},j\in S]$ and it is given by for any $i\in S$ $$
p_{j}=\lim_{ t \to \infty } \mathbb{P}(X(t)=j|X(0)=i)=\frac{\pi_{j}\tau_{j}}{\sum_{k\in S}\pi_{k}\tau_{k}},\;j\in S
$$
If the SMP is periodic with period d then the limit holds if $t=nd$ as $n\to \infty$.
Proof (aperiodic case): Fix $j\in S$. Define $$
Z(t)=
\begin{cases}
1 & X(t)=j \\
0 & o.w.
\end{cases}
$$
Then $\{Z(t),\;t\geq0\}$ is an ARP if $X(0)=j$ and we have just moved to state j. Alternatively, $\{Z(t),\;t\geq0\}$ is a delayed ARP if $X(0)\neq j$ or $X(0)=j$ and process $X(t)$ has been in state j for some time.
Let $S_{n}$ denote the nth entry into state j. Consider the time interval $[S_{1},S_{2})$ (since this interval will determine limiting distribution regardless of whether $Z(t)$ is ARP or delayed APR as first event may be based on delayed ARP).
So $X(S_{1})=j$ and we know that $\mathbb{E}[U_{2}]=\tau_{j}$ (expected uptime/time spent in j) and $\mathbb{E}[U_{2}+D_{2}]=\mathbb{E}[S_{2}-S_{1}]=\tau_{jj}$. 
We now want to show that we can use the limiting Theorem for ARPs. 
#### Check the following paragraph after spreak; Ziya wasn't sure in class

Suppose i is such that $T_{i}$ is aperiodic. Then, every $T_{j}$ for $j\in S$ must be aperiodic because the embedded chain is irreducible having a positive probability of visiting every state $k\in S$. We also have that $G_{i}(\infty)=1$ for all i and the DTMC is recurrent which implies that $T_{j}<\infty$ with probability 1 for any given $X(0)=i$.

Then the conditions of the theorem that describe the limiting behavior of the ARP (for the aperiodic case) holds. Thus, $$
\lim_{ t \to \infty } \mathbb{P}(X(t)=j|X(0)=\lim_{ t \to \infty } \mathbb{P}(Z(t)=1)=\frac{\mathbb{E}[U_{2}]}{\mathbb{E}[U_{2}]+\mathbb{E}[D_{2}]}=\frac{\tau_{j}}{\tau_{jj}}
$$
Plugging in $\tau_{jj}$ from theorem above we get the result we are trying to prove.


Example: Recall the Series system from last class.
Plugging in $\infty$ we get $$
P=G(\infty)=
\begin{bmatrix}
0 & \frac{\lambda_{1}}{\lambda} & \dots & \frac{\lambda_{N}}{\lambda} \\
1 & 0 & \dots & 0 \\
\dots & \dots & \dots & \dots \\
1 & 0 & \dots & 0
\end{bmatrix}
$$
So to find the limiting distribution we just get the solution to $\pi=\pi P$. This results in $\pi_{0}=\lambda$ and $\pi_{i}=\lambda_{i}$ for $1\leq i\leq N$.
Let $r_{i}$ be the mean repair time of component i. We set $\tau_{0}=\frac{1}{\lambda}$ and $\tau_{i}=r_{i}$ for $1\leq i\leq N$. Thus we have $$
p_{0}=\frac{\pi_{0}\tau_{0}}{\sum \pi_{k}\tau_{k}}=\frac{1}{1+\sum_{i=1}^{N} \lambda_{i}r_{i}}
$$
and $$
p_{j}=\frac{\lambda_{j}r_{j}}{1+\sum_{i=1}^{N} \lambda_{i}r_{i}},\;1\leq j\leq N
$$

## Renewal Processes with Costs/Rewards
Suppose $\{N(t),\;t\geq0\}$ is a standard RP generated by $\{X_{n},\;n\geq1\}$.
Define $R_{n}$ as the reward earned at the end of the nth cycle (end of the $X_{n}$ interevent time).
Define $Z(t)=\sum_{n=1}^{N(t)} R_{n}$ as the total reward up to time t. Process $\{Z(t),\;t\geq0\}$ is called a renewal reward process if $\{(X_{n},R_{n}),\;n\geq0\}$ constitute a sequence of iid bivariate random variables.

Example: Batch arrivals with $\mathbb{P}$(batch size = k) = $\alpha_{k}$ for $k\geq0$. This gives $Z(t)$ which counts the number of customer arrivals by t.
If arrivals are Poisson, then $\{Z(t),\;t\geq0\}$ is a Compound Poisson Process and is a renewal reward process. Here $R_{n}$ is the size of batch n.

Example: Machine maintenance
Replace a machine upon failure or upon reaching age $T$. Suppose $L_{i}$ is the lifetime of machine i (as if we know what its ultimate lifetime will be initially). Assume $L_{i}$'s are iid and nonnegative random variables. Replacing a machine by a new one costs $ $C_{r}$ and failure costs $ $C_{f}$. Let $Z(t)$ denote the total cost incurred by time t. Then $Z(t)$ is a renewal reward process with $S_{n}-S_{n-1}=X_{n}=min(L_{n},T)$ so that this will be a sequence of iid random variables. So $$
R_{n}=
\begin{cases}
C_{r} & L_{n}>T \\
C_{r}+C_{f} & L_{n}\leq T
\end{cases}
$$
Thus, $\{(X_{n},R_{n})\}$ is a series of iid bivariate random variables.

### Theorem 8.35: Almost Sure ERT for Renewal Reward Processes
Let $r=\mathbb{E}[R_{n}]<\infty$ and $\tau=\mathbb{E}[X_{n}]<\infty$. Then $$
\lim_{ t \to \infty } \frac{Z(t)}{t}=\frac{r}{\tau}
$$
with probability 1. Intuitively makes sense, reward for one cycle divided by length of one cycle gives you cost/reward per unit time as $t\to \infty$.

Proof:
$$
\frac{Z(t)}{t}=\frac{\sum_{n=1}^{N(t)} R_{n}}{t}=\sum_{n=1}^{N(t)} \frac{R_{n}}{N(t)} \frac{N(t)}{t}
$$
Since $N(t)\to \infty$ with probability 1 we can write $$
\lim_{ t \to \infty } \sum_{n=1}^{N(t)} \frac{R_{n}}{N(t)}=r
$$
with probability 1. similarly $$
\lim_{ t \to \infty } \frac{N(t)}{t}=\frac{1}{\tau}
$$
with probability 1. Thus, $$
\lim_{ t \to \infty } \frac{Z(t)}{t}=\frac{r}{\tau}
$$
with probability 1.

There is also the expected value version of this result, which says that under the same conditions we have (Theorem 8.38)$$
\lim_{ t \to \infty } \frac{\mathbb{E}[Z(t)]}{t}=\frac{r}{\tau}
$$

Example: Machine maintenance
Suppose that $L_{i}$'s are iid with $F(\cdot)$ and $\tau=\mathbb{E}[X_{n}]=\mathbb{E}[min(L_{n},T)]=\int_{0}^{T}(1-F(u))du$.
Also $r=\mathbb{E}[R_{n}]=C_{r}+C_{f}F(t)$
So $$
\lim_{ t \to \infty } \frac{\mathbb{E}[C(t)]}{t}=\frac{r}{\tau}=\frac{C_{r}+C_{f}F(t)}{\int_{0}^{T}(1-F(u))du}
$$
Note that rewards $R_{n}$ don't actually need to occur at the end of a cycle. They can occur anytime during $X_{n}$ and the results will hold.

## Regenerative Processes
Informal definition: These are processes that exhibit the same probabilistic behavior over consecutive cycles that start with regeneration points.
Formal definition: A stochastic process $\{X(t),\;t\geq0\}$ is called a regenerative process (RGP) if there exists a non-negative random variable $S_{1}$ such that the following is true:
1. $\mathbb{P}(S_{1}=0)<1$ and $\mathbb{P}(S_{1}<\infty)=1$
2. $\{X(t),\;t\geq0\}$ and $\{X(t+S_{1}),\;t\geq0\}$ are stochastically identical
3. $\{X(t+S_{1}),\;t\geq0\}$ is independent of $\{X(t),\;0\leq t\leq S_{1}\}$
This definition implies the existence of regeneration points i.e. increasing random variables $\{S_{n},\;n\geq1\}$ such that $\{X(t),\;t\geq0\}$ and $\{X(t+S_{n}),\;t\geq0\}$ are stochastically identical and $\{X(t+S_{n}),\;t\geq0\}$ is independent of $\{X(t),\;0\leq t<S_{n}\}$.
We call $S_{n}$ the nth regeneration epoch and the interval $[S_{n-1},S_{n})$ the nth regenerative cycle.

### Delayed Regenerative Process
We also have delayed regenerative processes as defined below.
A stochastic process $\{X(t),\;t\geq0\}$ is called a delayed RGP if there exists a non-negative random variable $S_{1}$ such that
1. $\mathbb{P}(S_{1}<\infty)=1$
2. $\{X(t+S_{1}),\;t\geq0\}$ is independent of $\{X(t),\;0\leq t<S_{1}\}$
3. $\{X(t+S_{1}),\;t\geq0\}$ is a regenerative process

Example:
Alternating renewal process is an RGP
Renewal process is not an RGP (is counting process, so never returns to count 0)
Age and remaining life processes are RGPs (return to 0)
CTMCs can be viewed as RGPs if we let $S_{n}$ denote the nth entry time to state 0. If $X(0)=0$ then we have a standard RGP, if $X(0)\neq0$ then the CTMC is a delayed RGP.
SMPs are the same as CTMCs since there is Markov property at transition times.
G/G/1 Queue we define $S_{n}$ to be the nth time a customer enters an empty system and this is RGP if we start with an arrival/customer entering empty system at time 0 and delayed RGP otherwise.

### Theorem 8.39
Let $\{X(t),\;t\geq0\}$ be an RGP with state space $(-\infty,\infty)$ with right continuous sample paths with left limits. Let $S_{1}$ be the first generation epoch and $U_{1}(x)$ is the time the process spends in the interval $(-\infty,x]$ during $(0,S_{1}]$. If $S_{1}$ is aperiodic with $\mathbb{E}S_{1}<\infty$ then $$F(x)=\lim_{ t \to \infty }\mathbb{P}(X(t)\leq x)=\frac{\mathbb{E}[U_{1}(x)]}{\mathbb{E}[S_{1}]}$$If $S_{1}$ is periodic with period d, then the limit above holds if $t=nd$ and as $n\to \infty$.
Intuitively, we are looking at the proportion of time spent in state x over the expected length of one cycle to get the probability of the process being in state x.

Proof:
Let $H(t)=\mathbb{P}(X(t)\leq x)$. Using renewal argument we have $$
\mathbb{P}(X(t)\leq x|S_{1}=u)=
\begin{cases}
H(t-u) & u\leq t \\
\mathbb{P}(X(t)\leq x|S_{1}=u) & u>t
\end{cases}
$$
Thus,
$$
H(t)=\int_{0}^{\infty}\mathbb{P}(X(t)\leq x|S_{1}=u)dG(u)
$$
where $G(u)=\mathbb{P}(S_{1}\leq u)$. Thus,$$
H(t)=\mathbb{P}(X(t)\leq x,S_{1}>t)+\int_{0}^{t}H(t-u)dG(u)
$$
Where the first term is $D(t)$. It can be shown using the sample path assumptions for $X(t)$ that $D(t)$ is satisfying the conditions of the key renewal theorem.
Define $$
Z(t)=
\begin{cases}
1 & X(t)\leq x \\
0 & o.w.
\end{cases}
$$
Then, $\mathbb{E}[U_{1}(x)]=\mathbb{E}\left[ \int_{0}^{S_{1}}Z(t)dt \right]=\int_{0}^{\infty}\mathbb{E}\left[ \int_{0}^{u}Z(t)dt|S_{1}=u \right]dG(u)$
$$
=\int_{0}^{\infty}\int_{0}^{u}\mathbb{E}[Z(t)|S_{1}=u]dtdG(u)
=\int_{0}^{\infty}\int_{0}^{u}\mathbb{P}(X(t)\leq x|S_{1}=u)=u]dtdG(u)
$$
$$
=\int_{0}^{\infty}\int_{t}^{\infty}\mathbb{P}(X(t)\leq x|S_{1}=u)dG(u)dt
=\int_{0}^{\infty}\mathbb{P}(X(t)\leq x,S_{1}>t)dt=\int_{0}^{\infty}D(t)dt=\mathbb{E}[U_{1}(x)]
$$
Then, using KRT, we get $$
\lim_{ t \to \infty } H(t)=\frac{\mathbb{E}[U_{1}(x)]}{\mathbb{E}[S_{1}]}
$$
The theorem holds even if it a delayed RGP.

If the state space is discrete, say $\{0,1,2,\dots\}$ we can define $$
p_{j}=\lim_{ t \to \infty } \mathbb{P}(X(t)=j)=\frac{\mathbb{E}[U_{1j}]}{\mathbb{E}[S_{1}]}
$$
Where $U_{1j}$ is the time spent in state j over the first cycle.

### RGPs with Costs/Rewards
Define $r(x)$ as the system earns rewards at a rate $r(x)$ when in state $x$.
Thus, $\int_{0}^{t}r(X(u))du$ is the total reward accumulated up to t.
Furthermore, $\frac{1}{t}\int_{0}^{t}r(X(u))du$ is the reward rate up to time t.
### Theorem 8.40
$\{X(t),\;t\geq0\}$ is an RGP on $S=(-\infty,\infty)$ with limiting distribution $F(\cdot)$. Let $r:S\to(-\infty,\infty)$ be bounded from either above or below. Then $$
\lim_{ t \to \infty } \frac{1}{t}\int_{0}^{t}r(X(u))du=\int_{-\infty}^{\infty}r(u)dF(u)
$$with probability 1.
Similarly, $$
\lim_{ t \to \infty } \frac{1}{t} \mathbb{E}\left[ \int_{0}^{t}r(X(u))du \right]=\int_{-\infty}^{\infty}r(u)dF(u)
$$

One small note: If the state space of the RGP is discrete and the limiting pmf is given by $p_{j}$ then the long run reward rate reduces to $\sum_{j=0}^{\infty}p_{j}r(j)$ (mirrors result for CTMC).

Example: Suppose that a manufacturing facility produces limited goods one at a time according to a renewal process with mean production time $\tau<\infty$ per item and stores them in a warehouse. As soon as there are k items, they are cleared by shipping them to the retailers. The clearing is instantaneous. It costs $h to hold an item in the warehouse per unit time and it costs $c to clear the warehouse. Find the optimal value of k that minimizes the long-run cost per unit time.
$X(t)$: number of items in warehouse at time t
Let $X(0)=0$ and a production is just starting and define $S_{n}$ as the time of the nth clearing time.
Looking at $X(t)$ for a given k, the graph is stepwise increasing until reaching k where we jump back to 0 and the process repeats.
We can see that $\{X(t),\;t\geq0\}$ is an RGP with state space $\{0,1,\dots,k-1\}$ (we exclude k since we jump to 0 immediately upon hitting k items). Our representative epochs are $\{S_{n},\;n\geq0\}$ with $\mathbb{P}(S_{1}<\infty)=1$ and $\mathbb{E}S_{1}=k\tau$ (k productions multiplied by expected time per production).
Then, $$
p_{j}=\lim_{ t \to \infty } \mathbb{P}(X(t)=j)=\frac{\mathbb{E}[U_{1j}]}{\mathbb{E}[S_{1}]}=\frac{\tau}{k\tau}=\frac{1}{k}
$$
for $0\leq j\leq k-1$.
Intuitively, this makes sense since production times are the same we would expect the long-run time spent in states to be the same for every state.
Define $C_{h}$ as the long-run expected holding cost per unit time. Then, $$
C_{h}=\sum_{j=0}^{k-1} jhp_{j}=\frac{h}{k}\sum_{j=0}^{k-1} j=\frac{1}{2}h(k-1)
$$
We can find the long-run clearing cost per unit time to be 
$$
C_{c}=\frac{c}{k\tau}
$$
Thus, our long-run total cost dependent on k is $$
C(k)=C_{h}+C_{c}= \frac{1}{2}h(k-1) +\frac{c}{k\tau}
$$
which is minimized by $k^{*}=\sqrt{ \frac{2c}{h\tau} }$


3/26

$$
P_{ij}(p_{t})=
\begin{cases}
\mathbb{P}(D(p_{t})=i-j+1) & 1<j\leq10,i\in S,0\leq i-j+1\leq10 \\
\mathbb{P}(D(p_{t})\geq i) & j=1,i\in S \\
\mathbb{P}(D(p_{t})\leq1) & j=10,i=10 \\
0 & o.w.
\end{cases}
$$
## Markov Decision Processes
### Finite Stage Models
Let state space be the set of integers.
Decision epochs are numbered from 1 through $N$.
	$A$: the set of all possible actions (finite set)
$R(i,a)$: reward earned when the state is i and action $a\in A$ is chosen.
$P_{ij}(a)$: probability that the system will be in state j at the next decision epoch if action a is taken and the current state is state i
$V_{n}(i)$: maximum expected return for an n stage problem (n more epochs to go) starting from i.
If $n=1$, then $V_{1}(i)=\max_{a}R(i,a)$.
Now suppose that we are at stage n, in state i, and we take action a and in the following stages we employ an optimal policy. Then, the expected total reward will be $R(i,a)+\sum P_{ij}(a)V_{n-1}(j)$. Then, $$
V_{n}(i)=\max_{a\in A}R(i,a)+\sum_{j} P_{ij}(a)V_{n-1}(j) \tag{optimality equation}
$$Note that this is called the optimality equation for this type of problem.

This suggests a recursive solution procedure and is used to prove structural results on optimal policies (such as given more time you'll sell more product, or given more supply/inventory you'll make more, etc.).

#### Computation of the optimal policy
Use Backward Induction algorithm which is quite straightforward.
1. Set $n=1$ and solve for $V_{1}(i)=\max_{a\in A}R(i,a)$ for all states i. We get $A_{1}^{*}(i)=argmax_{a\in A}R(i,a)$.
2. Now using the optimality equation set $n=2$ and solve once again for $V_{2}(i)$'s and $A_{2}^{*}(i)$'s.
3. Continue this recursively by setting $n=n+1$ and solving optimality equation.
4. If we get $n=N$ stop otherwise go back to step 3.
Intuitively, we can get the optimal value of individual steps so we start at the end and build backwards to get the best/optimal policy.

Example: Stochastic Inventory Control
Suppose that each month the manager of a warehouse determines current inventory (stock on hand) of a product. Based on this info, she decides whether or not to order additional stock from a supplier.
Assumptions:
i) The decision to order additional products is made at the beginning of each month and delivery occurs instantaneously
ii) Demand for the product arrives throughout the month, but all orders are filled on the last day of the month.
iii) If demand exceeds inventory the demand above the existing inventory is lost (no backlogging).
Define the following for the problem:
$S_{n}$: inventory on hand at the beginning of month n.
$a_{n}$: number of units ordered in month n
$D_{n}$: random demand in month n, $P_{j}=\mathbb{P}(D_{t}=j),\;j=0,1,2,\dots$ for all $t\geq0$.
Thus, $S_{n+1}=max(S_{n}+a_{n}-D_{n},0)$.
**Ordering Cost**: $$
O(u)=
\begin{cases}
K+c(u) & u>0 \\
0 & o.w.
\end{cases}
$$
where $K$ is a fixed cost (shipping fee, etc.).
$h(u)$: Inventory cost of u units of inventory kept over a month.
$g(u)$: Value of u units of inventory at the end of the horizon. I.e. whatever you have left at the end is still worth something, but most likely not as much (Halloween costumes being super cheap a few days after for example).
$f(u)$: revenue obtained from the sale of u units
$M$: capacity of the warehouse for that item

**MDP Formulation** for inventory example
Decision epochs: $T=\{N,N-1,\dots,1\}$
States: $S=\{0,1,\dots,M\}$
Actions: amount ordered in month n when on hand inventory is i so $A(i)=\{0,1,\dots,M-i\}$
Rewards: $$R(i,a)=\sum_{j=0}^{i+a}P_{j}f(j)+\sum_{j=i+a+1}^{\infty}P_{j}f(i+a)-O(a)
$$Breaking this down it is the probability of demand being j times revenue of selling j units up to maximum capacity and if demand is larger than max capacity ($i+a$) then all demand is met and the rest is lost, then we subtract the ordering cost of obtaining $a$ units.
Transition probability: $$
P_{ij}(a)=
\begin{cases}
0 & M\geq j>i+a \\
P_{i+a-j} & M\geq i+a\geq j>0 \\
\sum_{k=i+a}^{\infty} P_{k} & M\geq i+a,j=0
\end{cases}
$$
For first case, intuitively we can have zero demand and thus just transition to state $i+a$, but we cannot have more than that since demand is non-negative. For second case it is just the probability of having demand $i+a-j$. For final case it is just the probability of demand being greater than or equal to $i+a$ (max capacity on hand).
Now let $K=4,c(u)=2u,g(u)=0,h(u)=u,M=3,N=3,f(u)=8u$, $$
P_{j}=
\begin{cases}
\frac{1}{4} & j=0 \\
\frac{1}{2} & j=1 \\
\frac{1}{4} & j=2
\end{cases}
$$
Start with $n=0$. Thus, $V_{0}(i)=0$ because $g(u)=0$ (because with no stages left the maximum expected revenue is just $g(u)$).
$n=1$ case: $V_{1}(i)=maxR(i,a),\;\forall i\in S$. Thus, $V_{1}(0)=max\{0,-4-2+\frac{3}{4}*8-1,-4-4-2+\frac{1}{2}*8+\frac{1}{4}*16,-10-3+\frac{1}{2}*8+\frac{1}{4}*16\}=max(0,-1,-2,-5)=0$ for cases $a=0,1,2,3$ respectively. For further breakdown note that the $a=1$ case has -4 for ordering cost $K$, -2 for ordering cost c(1)=2, 3/4 times 8 for probability of selling the item times f(1), then -1 for holding cost (since we hold until the end of the month). So $A_{1}^{*}(0)=\{0\}$.
Now we solve for the other states i.e. getting $V_{1}(1)=max(a=0,a=1,a=2)$ where cases are only $a=0,1,2$ since we can't exceed inventory level 3. Solving this out further we can show that $V_{1}(1)=5,A_{1}^{*}(1)=\{0\},V_{1}(2)=6,A_{1}^{*}(2)=\{0\},V_{1}(3)=5,A_{1}^{*}(3)=\{0\}$.
$n=2$ case: $V_{2}(0)=max\left( 0+1*0,-4-2-1+\frac{3}{4}*8+\frac{3}{4}*0+\frac{1}{4}*5,\dots, \dots \right)=max\left( 0, \frac{1}{4},2, \frac{1}{2} \right)=2$ where the 0 in case $a=0$ from $1*0$ comes from $V_{1}(0)=0$. Similarly for the $a=1$ case we see we have the ordering cost initially then the probability of selling the one unit this cycle times its value plus the probability of going to state 0 (3/4) times $V_{1}(0)$ and probability of going to state 1 (1/4) times $V_{1}(1)=5$. Further calculations can provide the values of $V_{2}(i)$ for all i.
We can then setup a table to show the values of these results:
$$
\begin{bmatrix}
i & a=0 & a=1 & a=2 & a=3 & V_{2}(i) & A_{2}^{*}(i) \\
0 & 0 & \frac{1}{4} & 2 & \frac{1}{2} & 2 & 2 \\
1 & \frac{25}{4} & 4 & \frac{5}{2} & - & \frac{25}{4} & 0 \\
2 & 10 & \frac{9}{2} & - & - & 10 & 0 \\
3 & \frac{21}{2} & - & - & - & \frac{21}{2} & 0
\end{bmatrix}
$$
Pics on phone of remaining results for $V_3(i)$'s.

3/31
### Discounted MDPs with Infinite Horizon
Observe a process at time points 0,1,2,...
State space is $S=\{0,1,2,\dots\}$
$A$ is the set of all possible actions
$R(i,a)$: expected reward in state $i$ if action $a$ is taken
$P_{ij}(a)$: transition probability from $i$ to $j$ if action $a$ is taken
$X_{n}$: state of the process at time point $n$
$a_{n}$: decision made at time point $n$
$\mathbb{P}(X_{n+1}=j|X_{0},a_{0},X_{1},a_{1},\dots,X_{n}=i,a_{n}=a)=\mathbb{P}(X_{n+1}=j|X_{n}=i,a_{n}=a)=P_{ij}(a)$ (assuming Markov Property)
Assume that rewards are bounded: assume there exists $B<\infty$ such that $|R(i,a)|<B,\;\forall i,a$.
Policies may be randomized meaning we might chose action $a$ in state $i$ with some probability $\alpha_{ia}$
#### Stationary Policies
A policy is said to be stationary if it is non-randomized (deterministic) and the action at $t$ only depends on the state of the process at time $t$.
Hence, a stationary policy is characterized by a function $f:S\to A$ mapping the state space to the action space. Thus, $f(i)$ is the action to be taken when in state $i$.
Under a stationary policy $f$, $\{X_{n},\;n\geq0\}$ is a DTMC with transition probabilities defined as $P_{ij}=P_{ij}(f(i))$.

**Objective:** Maximize total expected discounted return.
So mathematically, find a policy $\Pi$ that maximizes $V_{\Pi}(i)$ where $$V_{\Pi}(i)=\mathbb{E}_{\Pi}\left[ \sum_{n=0}^{\infty} R(X_{n},a_{n})\alpha^{n}|X_{0}=i \right] \tag{1}$$
So this is the expected value under policy $\Pi$ where $\alpha$ is the discount factor $0<\alpha<1$. $V_{\Pi}(i)$ is the expected total discounted return under $\Pi$.
Note that $$
V_{\Pi}(i)\leq \sum_{n=0}^{\infty} \alpha^{n}B=\frac{B}{1-\alpha}<\infty
$$
since the rewards are bounded as mentioned above.

#### Optimality Equation and the Optimal Policy
Let $V(i)=\sup_{\Pi}V_{\Pi}(i)$
A policy is said to be optimal if this supremum is achieved for all i:$$V_{\Pi^{*}}(i)=V(i),\;\forall i\geq0$$.
#### Theorem 1
$V(i)$ for all i, satisfy the following optimality equation: $$
V(i)=\max_{a}[R(i,a)+\alpha \sum_{j}P_{ij}(a)V(j)]
$$
Proof: Let $\Pi$ be any policy and suppose $\Pi$ chooses action $a$ at time 0 with probability $p_{a},\;a\in A$. Then, $$V_{\Pi}(i)=\sum_{a\in A}p_{a}\left[ R(i,a)+\sum_{j}P_{ij}(a)W_{\Pi}(j) \right]$$
Where $W_{\Pi}(j)$ is the expected discounted return from time 1 onwards under policy $\Pi$ and state at time 1 is $j$.
Then it must be the case that $W_{\Pi}(j)\leq \alpha V(j)$.
Then $$V_{\Pi}(i)\leq \sum_{a\in A}p_{a}\left[ R(i,a)+\alpha \sum_{j}P_{ij}(a)V(j) \right]\leq \sum_{a\in A}p_{a}\max_{a'}\left[ R(i,a')+\alpha \sum_{j}P_{ij}(a')V(j) \right]$$
$$
=\max_{a'}\left[ R(i,a')+\alpha \sum_{j}P_{ij}(a')V(j) \right] \tag{*}
$$
Since $\Pi$ is arbitrary, we get $V(i)\leq \max_{a}\left[ R(i,a)+\alpha \sum_{j}P_{ij}(a)V(j) \right]$.
Now let $a_{0}$ be such that $$R(i,a_{0})+\alpha \sum_{j}P_{ij}(a)V(j)=\max_{a}\left[ R(i,a)+\alpha \sum_{j}P_{ij}(a)V(j) \right]$$
Let $\epsilon>0$ and $\Pi$ be the policy that chooses $a_{0}$ at time 0 and if the next state is j follows the policy $\Pi_{j}$ such that $V_{\Pi_{j}}(j)\geq V(j)-\epsilon$.
Then $V_{\Pi}(i)=R(i,a_{0})+\alpha \sum_{j}P_{ij}(a_{0}V_{\Pi_{j}}(j))\geq R( i,a_{0})+\alpha \sum_{j}P_{ij}(a_{0})V(j)-\alpha\epsilon$
Then, $$
V(i)\geq \max_{a}\left[ R(i,a)+\alpha \sum_{j}P_{ij}(a)V(j) \right]-\alpha\epsilon
$$
Then using the fact that $\epsilon>0$ is arbitrary and inequality (\*) we get the optimality equations in the statement of the theorem.

#### Theorem 2
Let $f$ be the stationary policy that, when the process is in state $i$ it selects an action $a$ that maximizes the RHS of the optimality equation, i.e. $$
\left[R(i,f(i))+\alpha \sum_{j}P_{ij}(f(i))V(j)\right]=\max_{a}\left[ R(i,a)+\alpha \sum_{j}P_{ij}(a)V(j) \right],\;i\geq0
$$
Then $V_{f}(i)=V(i),\;\forall i\geq0$ i.e. policy $f$ is optimal.

Proof:
$$
V(i)=\max_{a}\left[ R(i,a)+\alpha \sum_{j}P_{ij}(a)v(j) \right]=R(i,f(i))+\alpha \sum_{j}P_{ij}(f(i))V(j)
$$
From here we can think of this like a 2-stage process where once we transition to state j it is over and we just get our total discounted reward $V(j)$. So its like a two stage process minimizing total expected discounted return where $V(\cdot)$ is the terminal reward.
Then writing $V(j)$ in open form it can be seen that $f(\cdot)$ gives the optimal total discounted expected return over 3 time periods (with $V(\cdot)$ giving the terminal reward). We can use this argument repeatedly we get $V(i)=\mathbb{E}$\[n-stage return under f | $X_{0}=i$]$+\alpha^{n}\mathbb{E}[V(X_{n})|X_{0}=i]$. Letting $n\to \infty$ the second term drops and we have $V(i)=V_{f}(i)$.


Define the operators $T_{f}$ and $T_{\alpha}$ (from bounded functions to bounded functions) as follows:
$$
(T_{f}u)(i)=R(i,f(i))+\alpha \sum P_{ij}(f(i))u(j)
$$
So we think of $i$ as the initial state and then we use $f$ for one stage (first reward term) and then stop with terminal rewards $u(j)$ (second term sum of discounted rewards).
The other operator is defined as $$
(T_{\alpha}u)(i)=\max_{a}\left[ R(i,a)+\alpha \sum P_{ij}(a)u(j) \right]
$$
So $T_{\alpha}V(i)=V(i)$ which is what Theorem 1 says.

Also define $T_{f}^{1}=T_{f}$ and $T_{f}^{n}=T_{f}(T_{f}^{n-1}),\;n\geq2$.
Similarly for $T_{\alpha}$ we have $T_{\alpha}^{1}=T_{\alpha}$ and $T_{\alpha}^{n}=T_{\alpha}(T_{\alpha}^{n-1}),\;n\geq2$.

#### Lemma
For $u,v\in B(I)$ ($B(I)$ is set of bounded functions over non-negative integers) and $f$ a stationary policy. We get:
(i) $u\leq v\implies T_{f}u\leq T_{f}v$
(ii) $T_{f}V_{f}=V_{f}$
(iii)$T_{f}^{n}u\to V_{f}$ as $n\to \infty$ for all $u\in B(I)$

Proof:
(i) Follows simply from plugging in larger values ($u\leq v$) to $T_{f}$ into the sum in second term of $T_{f}$.
(ii) Says that $V_{f}(i)=R(i,f(i))+\alpha \sum_{j}P_{ij}(f(i))V_{f}(j)$ which comes from first-step analysis i.e. we have the reward in state j then sum the discounted rewards for stepping into any state j afterwards.
(iii) Very similar to the proof of Theorem 2 above. Lets examine a small case first, n=2:
$$
(T_{f}^{2}u)(i)=R(i,f(i))+\alpha \sum_{j}P_{ij}(f(i))(T_{f}u)(j)
$$
$$
=R(i,f(i))+\alpha \sum_{j}P_{ij}(f(i))\left[ R(j,f(j))+\alpha \sum_{k}P_{jk}(f(k))u(k) \right]
$$
$$
=R(i,f(i))+\alpha \sum_{j}P_{ij}(f(i))R(j,f(j))+\alpha^{2}\sum_{j}\sum_{k}P_{ij}(f(i))P_{jk}(f(j))u(k)
$$
This is essentially how we are viewing it as an n-stage problem for proving Theorem 2.
Hence, $T_{f}^{2}u$ is the expected cost if we use $f$ over two periods and receive a final reward of $u(\cdot)$. Then using an induction argument this generalizes to $T_{f}^{n}u$ being an n-stage problem. Thus, $T_{f}^{n}u$ is the expected reward if $f$ is used for n periods with final reward function $u(\cdot)$.
Since $\alpha<1$ and $u(\cdot)$ is bounded we get $T_{f}^{n}u\to V_{f}$ for any $u\in B(I)$.
This Lemma can be shown to prove Theorem 2.
Statement of Theorem 2 says $T_{f}V=V$. So $T_{f}^{n}V=T_{f}^{n-1}T_{f}V=T_{f}^{n-1}V$. Thus, $T_{f}^{n}V=V$ so that means $T_{f}^{n}V\to V$ and Lemma part (iii) says $T_{f}^{n}V\to V_{f}$ so we must have $V_{f}=V$ (which is the conclusion of theorem 2).

4/7
Recall from last class:
$V(i)=max\left[ R(i,a)+\alpha \sum P_{ij}(a)V(j) \right]$
$(T_{f}u)(i)=R(i,f(i))+\alpha \sum P_{ij}(f(i))u(j)$
$(T_{\alpha}u)(i)=\max_{a}\left[ R(i,a)+\alpha \sum P_{ij}(a)u(j) \right]$
$T_{\alpha}V(i)=V(i)$
$u\leq v\implies T_{f}u\leq T_{f}v$
$T_{f}V_{f}=V_{f}$
$T_{f}^{n}u\to V_{f}$ as $n\to \infty$

### Contraction Mapping
For any function $u\in B(i)$, let $$
||u||=\sup_{i}|u(i)|
$$
Definition: A mapping $T: B(D)\to B(I)$ is said to be a contraction mapping if $$
||T_{u}-T_{v}||\leq \beta||u-v||
$$ for some $0<\beta<1$ and for $u,v\in B(I)$.

#### Theorem (Contraction Mapping Fixed Point Theorem)
If $T:B(I)\to B(I)$ is a contraction mapping then there exists a unique function $g\in B(I)$ such that $Tg=g$. Furthermore, for all $u\in B(I)$, $T^{n}u\to g$ as $n\to \infty$.

Proof: We first prove the second statement. Define a sequence $\{u^{n}\}$ such that $u^{0}=u$, $u^{n+1}=Tu^{n}=T^{n+1}u$. Then for any $n\geq1$, $||u^{n+1}-u^{n}||\leq \sum_{k=0}^{n-1}||u^{n+k+1}-u^{n+k}||$.
Continuing this we get $$
\sum_{k=0}^{n-1} ||T^{n+k}u^{1}-T^{n+k}u^{0}||\leq \sum_{k=0}^{n-1} \beta^{n+k}||u^{1}-u^{0}||=\frac{\beta^{n}(1-\beta^{n})}{1-\beta}||u^{1}-u^{0}||$$
So $||u^{n+m}-u^{n}||\leq \frac{\beta^{n}(1-\beta^{m})}{1-\beta}||u^{1}-u^{0}||$.
Now since $0<\beta<1$, we conclude that $||u^{n+m}-u^{n}||$ can be made arbitrarily small for sufficiently large n and $\{u^{n}\}$ is a Cauchy sequence. Thus, $u^{n}$ has a limit, we call $g\in B(I)$. Then using again the properties of the norm, $$
0\leq||Tg-g||\leq||Tg-u^{n}||+||u^{n}-g||\leq||Tg-Tu^{n-1}||+||u^{n}+g||\leq \beta||g-u^{n-1}||+||u^{n}-g||
$$
Note that both terms in the final inequality go to 0 as $n\to \infty$. Since $0<\beta<1$, we can then conclude that $||Tg-g||=0$ and thus $Tg=g$.
For uniqueness, let $Tg'=g'$ and $g\neq g'$. Then $||g-g'||=||Tg-Tg'||\leq\beta||g-g'||$. Since $0<\beta<1$ the uniqueness follows.

Recall that $$(T_{\alpha}u)(i)=\max_{a}\left[ R(i,a)+\alpha \sum P_{ij}(a)u(j) \right]$$
#### Theorem
The mapping $T_{\alpha}$ is a contraction mapping.
Proof:
$$(T_{\alpha}u)(i)-(T_{\alpha}v)(i)=\max_{a}\left[ R(i,a)+\alpha \sum P_{ij}(a)u(j) \right]-\max_{a}\left[ R(i,a)+\alpha \sum P_{ij}(a)v(j) \right]$$
Let $\bar{a}$ be such that $R(i,\bar{a})+\alpha \sum P_{ij}(\bar{a})u(j)=max\left[ R(i,a)+\alpha \sum P_{ij}(a)u(j) \right]$. AKA $\bar{a}$ is the optimal action $a$.
Then, $(T_{\alpha}u)(i)-(T_{\alpha}v)(i)=R(i,\bar{a})+\alpha \sum P_{ij}(\bar{a})u(j)-max[\dots]$. Following this further we get $$
=R(i,\bar{a})+\alpha \sum P_{ij}(\bar{a})(u(j)-v(j))+\alpha \sum P_{ij}(\bar{a})v(j)-\max_{a}\left[ R(i,a)+\alpha \sum P_{ij}(a)v(j) \right]
$$
We then conclude that $R(i,\bar{a})+\alpha \sum P_{ij}(\bar{a})v(j)-\max_{a}\left[ R(i,a)+\alpha \sum P_{ij}(a)v(j) \right]$ is negative since $\bar{a}$ is an arbitrary action so with respect to $v(j)$ so the first term can be at most the optimal $a$ otherwise the max will be larger. Now we can just drop this negative term to have an upper bound on $(T_{\alpha}u)(i)-(T_{\alpha}v)(i)$. Thus, continuing the above we have$$
\leq \alpha \sum P_{ij}(\bar{a})(u(j)-v(j))\leq \alpha \sum P_{ij}(\bar{a})\sup_{k}(u(k)-v(k))=\alpha \sup_{k}(u(k)-v(k))
$$
So $(T_{\alpha}u)(i)-(T_{\alpha}v)(i)\leq \alpha\sup_{k}(u(k)-v(k))=\alpha||u-v||$.
And then, switching $v$ and $u$ in the above proof, we can similarly get $(T_{\alpha}v)(i)-(T_{\alpha}u)(i)\leq \alpha||u-v||$. Thus, $||T_{\alpha}v-T_{\alpha}u||\leq \alpha||v-u||$.
And since $0<\alpha<1$, we can conclude that $T_{\alpha}$ is a contraction mapping.

#### Corollary
$V(\cdot)$ is a unique solution to the optimality equations.
$$
V(i)=\max_{a}\left[ R(i,a)+\alpha \sum P_{ij}(a)V(j) \right],\;\forall i\in S
$$
Furthermore, for any $u\in B(I)$ we have $T_{\alpha}^{n}u\to V$ as $n\to \infty$.

**One can also prove that $T_{f}$ is a contraction mapping.**
Hence, $V_{f}(\cdot)$ is the unique solution $V_{f}(i)=R(i,f(i))+\alpha \sum P_{ij}(f(i))V_{f}(j)$.

### Value-Iteration Algorithm
Step 1: Select $u^{0}\in B(I)$ and set $\epsilon>0$ and $n=0$.
Step 2: For each $i\in S$ compute $u^{n+1}(\cdot)$ by $u^{n+1}(i)=\max_{a\in A(i)}\left[ R(i,a)+\alpha \sum P_{ij}(a)u^{n}(j) \right]$
Step 3: If $||u^{n+1}-u^{n}||< \frac{\epsilon(1-\alpha)}{2\alpha}$ (equation 1) go to step 4, otherwise increase $n$ by 1 and go back to step 2.
Step 4: For each $i\in S$ choose $a_{\epsilon}(i)=\arg\max_{a\in A(i)}\left[ R(i,a)+\alpha \sum P_{ij}(a)u^{n+1}(j) \right]$ (equation 2) and conclude optimal policy (even though we aren't necessarily there, we are quite close).

We already proved that $u^{n}$ converges to $V$ and that there exists a finite $n$ such that (1) holds. Thus, the algorithm terminates.
#### Theorem
The stationary policy $a_{\epsilon}$ found by the above Value-Iteration algorithm is $\epsilon$-optimal (at most $\epsilon$ away from optimal policy) and $||u^{n+1}-V||< \frac{\epsilon}{2}$ whenever the inequality in step 3 holds (equation 1).
Proof: Suppose the inequality holds (equation 1).
$$
||V_{a_{\epsilon}}-V||\leq||V_{a_{\epsilon}} - u^{n+1}|| + ||u^{n+1}-V||
$$
From (2) we have $$
T_{a_{\epsilon}}u^{n+1}=T_{\alpha}u^{n+1}
$$
Continuing from first inequality in this proof, $$
||V_{a_{\epsilon}}-u^{n+1}||=||T_{a_{\epsilon}}V_{a_{\epsilon}}-u^{n+1}||\leq||T_{a_{\epsilon}}V_{a_{\epsilon}}-T_{\alpha}u^{n+1}||+||T_{\alpha}u^{n+1}-u^{n+1}||
$$
$$
=||T_{a_{\epsilon}}V_{a_{\epsilon}}-T_{a_{\epsilon}}u^{n+1}||+||T_{\alpha}u^{n+1}-T_{\alpha}u^{n}||\leq \alpha||V_{a_{\epsilon}}-u^{n+1}||+||u^{n+1}-u^{n}||
$$
Due to both $T_{a_{\epsilon}}$ and $T_{\alpha}$ being contraction mappings. Then we can write $$
||V_{a_{\epsilon}}-u^{n+1}|| \leq \frac{\alpha}{1-\alpha}||u^{n+1}-u^{n}||
$$
Similarly, we can show that $$
||u^{n+1}-V||\leq \frac{\alpha}{1-\alpha}||u^{n+1}-u^{n}||
$$
Then if (1) holds $$
||V_{a_{\epsilon}}-V||\leq \frac{\alpha}{1-\alpha}*2* \frac{\epsilon(1-\alpha)}{2\alpha}
$$
So when (1) holds $$
||V_{a_{\epsilon}}-V||\leq\epsilon
$$


For final, Ziya's intention is to mainly ask from queueing and renewal processes. There may be one question on MDPs. He'll probably ask 5-6 questions.

4/9
#### Theorem
Let $g$ be a stationary policy with expected return $V_{g}$ and let $h$ be the policy such that $$
R(i,h(i))+\alpha \sum_{j} P_{ij}(h(i))V_{g}(j)=\max_{a}\left[ R(i,a)+\alpha \sum_{j} P_{ij}(a)V_{g}(j) \right]
$$
Then, $V_{h}(i)\geq V_{g}(i),\; \forall i$ and if $V_{h}(i)=V_{g}(i)$ for all i then $V_{g}=V_{h}=V$.

Proof: $(T_{h}V_{g})(i)=R(i,h(i))+\alpha \sum P_{ij}(h(i))V_{g}(j)\geq R(i,g(i))+\alpha \sum P_{ij}(g(i))V_{g}(j)=V_{g}(i)$
Hence, $(T_{h}V_{g})(i)\geq V_{g}(i)$.
Since, $T_{h}$ is monotone $(T_{h}^{2}V_{g})(i)\geq (T_{h}V_{g})(i)\geq V_{g}(i)$
So in general $(T_{h}^{n}V_{g})(i)\geq V_{g}(i)$ for any $n\geq1$.
So taking $n\to \infty$ we get $V_{h}(i)\geq V_{g}(i)$.
Now suppose $V_{h}(i)=V_{g}(i)$. Then from the definition of $h$ we can see that $V_{h}$ satisfies the optimality equations and thus $V_{h}=V_{g}=V$.

### Policy Improvement Algorithm
Last thing necessary for project.
Step 1: Set $n=0$ and select an arbitrary policy $g(\cdot)$ (usually that you think is good for faster convergence).
Step 2: (Policy Evaluation) Obtain $V_{g_{n}}$ by solving the set of equations $V_{g_{n}}(i)=R(i,g_{n}(i))+\alpha \sum_{j} P_{ij}(g_{n}(i))V_{g_{n}}(j)$ for $i\in S$.
Step 3: (Policy Improvement step) Choose a new policy $g_{n+1}$ such that $g_{n+1}(i)\in argmax\left( R(i,a)+\alpha \sum_{j}P_{ij}(a)V_{g_{n}}(i) \right),\;\forall i$ setting $g_{n+1}(i)=g_{n}(i)$ when possible.
Step 4: (Check convergence) If $g_{n}(i)=g_{n+1}(i),\;\forall i\in S$ then stop and set $a(i)=g_{n}(i)$. Otherwise, increase $n$ by 1 and return to step 2.
The algorithm terminates in a finite number of steps as long as the number of actions and number of states are finite.
Note you can approximate $V_{g_{n}}(i)$ using the Value-Iteration approach rather than actually solving the true system of linear equations. This works because Value-Iteration algorithm is pretty quick.

### Solution by Linear Programming
Helpful for adding constraints to your problem. For example, you can't take a specific action more than 10% of the time or you must be in a specific state 5% of the time, etc.
#### Proposition
Suppose that $u(i)$ is a bounded function such that $u(i)\geq max\left[ R(i,a)+\alpha \sum P_{ij}(a)u(j) \right]$.
Then $u(i)\geq V(i),\;\forall i$.
Proof: We have $u\geq T_{\alpha}u\implies u\geq T_{\alpha}u\geq T_{\alpha}^{2}u$. Thus, $u\geq T_{\alpha}^{n}u$ so as $n\to \infty$ we get $u\geq V$.

Based on this result, consider the following LP (linear programming) problem (P):
$$
\min_{u}\left[ \sum_{i=0}^{\infty} \beta(i)u(i) \right] \tag{P}
$$
subject to $$
u(i)\geq R(i,a)+\alpha \sum_{j}P_{ij}(a)u(j),\;i\geq0,a\in A_{i}
$$
where $\beta(i)$'s are positive constants.

#### Theorem
An optimal solution $u^{*}(\cdot)$ to problem (P) satisfies the optimality equation hence $u^{*}=V$.
Proof: We need to show since there's a unique solution to the optimality equations that $$
u^{*}(i)=R(i,a)+\alpha \sum_{j}P_{ij}(a)u^{*}(j)
$$
for all $i\in S$ and at least one $a\in A_{i}$.
Suppose that we have a feasible solution $\{u(i),i\in S\}$ for which this is not the case. Then, there exists $i\in S$ such that $$
u(i)>R(i,a)+\alpha \sum_{j}P_{ij}(a)u(j),\;\forall a\in A_{i}
$$
Thus, $\exists\epsilon>0$ such that $u(i)-\epsilon\geq R(i,a)+\alpha \sum_{j}P_{ij}(a)u(j)$ for all $a\in A_{i}$.
To show that $u(i)$ cannot be optimal, define $u'(i)=u(i)-\epsilon$ and $u'(j)=u(j)$ for $j\neq i$.
Then, $u'(i)=u(i)-\epsilon\geq R(i,a)+\alpha \sum_{j}P_{ij}(a)u'(j)$.
So for all $j\neq i$ we have $$
u'(j)=u(j)\geq R(j,a)+\alpha \sum_{k}P_{jk}(a)u(k)
$$
so $$
u'(j)=u(j)\geq R(j,a)+\alpha \sum_{k}P_{jk}(a)u'(k)
$$
Hence, $u'(\cdot)$ is a feasible solution and is a better solution because $\sum_{k}\beta(k)u'(k)=\sum_{k}\beta(k)u(k)-\epsilon \beta(i)$.

Note that these $\beta(i)$'s can be set to any positive values. Let's set them so that $\sum_{i\in S}\beta(i)=1$.
Also assume that the action space is the same for all states (not necessary, but just makes things easier).
Note that LP has $|S|$ variables and up to $|S|$x$|A|$ constraints. So solving the dual might actually be more efficient.
#### Dual Linear Program
$$
\max_{x}\sum_{i\in S}\sum_{a\in A_{i}}R(i,a)x(i,a)
$$
subject to constraints
$\sum_{a\in A_{i}}x(i,a)-\sum_{j\in S}\sum_{a\in A_{j}}\alpha P_{ji}(a)x(j,a)=\beta(i)$
$x(i,a)\geq0,\;\forall i\in S$ and $a\in A_{i}$

#### Theorem
part a) For each Markovian randomized policy $\pi$, $i\in S$, $a\in A_{i}$ we define $$
x_{\pi}(i,a)=\sum_{j\in S}\beta(j)\sum_{n=1}^{\infty} \alpha^{n-1} P_{\pi}(X_{n}=i,A_{n}=a|X_{1}=j)
$$
Then, $x_{\pi}(i,a)$ is a feasible solution to the dual problem. 

part b) Suppose $x(i,a)$ is a feasible solution to the dual problem. Then for each $i\in S$ we have $\sum_{a\in A_{i}} x(i,a)>0$. Define a randomized stationary policy $\pi$ by $$P(a_{\pi}(i)=a)=\frac{x(i,a)}{\sum_{a'\in A_{i}}x(i,a')}$$
(Probability of choosing action a under policy $\pi$ for state i).
Then $x_{\pi}(i,a)$ defined in part a is a feasible solution to the dual LP and $x_{\pi}(i,a)=x(i,a)$ for all $a\in A_{i}$ and $i\in S$.

4/14
## Solving MDPs Using Linear Programming

### GMDPs with Infinite Horizon Discounting

#### Linear Programming Formulation

**Problem (P)** and **Dual Problem (D)**

- $X(i, a)$ are decision variables
- Recall part b of theorem above: A solution to (D) corresponds to a specific policy $\pi$, where $$\mathbb{P}(a_\pi(i)=a) = \frac{X(i,a)}{\sum_{b \in A_i} X(i,b)}$$

---

#### Basic Facts About Solutions to Linear Programs

**Definition:** $X$ is a **basic feasible solution** of an LP if it cannot be expressed as a convex combination of any other feasible solutions of the LP.

**Key facts:**
- When an LP with $m$ rows (constraints) has a bounded optimal solution, then any basic feasible solution has at most $m$ positive components.
- From the previous theorem (part b): if $\{X(i,a)\}_{i \in S, a \in A_i}$ is a basic feasible solution to the LP, then $\sum_{a\in A_{i}} X(i,a) > 0$ for each $i \in S$.
- Problem (D) has $|S|$ rows, so for a basic feasible solution, there are at most $|S|$ positive components.
- It must be the case that $X(i,a) > 0$ for only one $a \in A_i$ for each $i \in S$.
- The $\mathbb{P}$ in part (b) of the theorem will be $= 1$ for one action and $0$ for all others for each $i$. Thus, there exists an optimal policy which is **deterministic**.

---

### Theorem

Assume $R(i,a)$ is bounded $\forall\, i \in S,\, a \in A_i$. Then:

1. There exists a bounded optimal basic feasible solution $X^*$ to the dual LP.
2. Suppose $X^*$ is an optimal solution. Then the randomized stationary policy defined in part (b) of the previous theorem is an optimal policy.
3. If $X^*$ is an optimal basic feasible solution to the dual LP, then the policy in part (b) is a **deterministic stationary policy**.

---

### Continuous Time MDPs

#### Setup

Consider the reward/cost function:

$$\lim_{n \to \infty} \mathbb{E}\left[\int_0^{t_{n}} e^{-\alpha t} g(x(t), a(t))\, dt \mid X_0 = i\right]$$

where $t_n$ is the time of the $n$-th transition with $t_0 = 0$, and $\alpha>0$ is the continuous-time discount factor.

- $g(x(t), a(t))$ represents the reward obtained when action $a(t)$ is selected at state $x(t)$.
- $X_n$ and $a_n$ denote the state and action selected at $t_n$, so $X_n = x(t)$ and $a_{n} = a(t)$ for $t_n \leq t < t_{n+1}$.
#### Reward Structure

Suppose $g(x(t), a(t))$ consists of 2 parts:

1. $k(x(t), a(t))$ — lump-sum reward gained when action $a(t)$ is taken and the process transitions from $x(t)$.
2. $c(x(t), a(t))$ — continuous reward accumulated while the state is $x(t)$ and the last action taken was $a(t)$.

The objective is to find a policy $\pi$ that maximizes:

$$V_\pi(i) = \mathbb{E}_\pi\left[\sum_{n=0}^{\infty} e^{-\alpha t_n}\left(k(X_n, a_n) + \int_{t_{n}}^{t_{n+1}} e^{-\alpha (t-t_{n})} c(X_n, a_n)\, dt\right) \mid X_0 = i\right]$$

#### Derivation (IID Exponential Inter-transition Times)

Define $\tau_{n+1} = t_{n+1} - t_n$, with $t_0 = 0$.

First, assume that $\{\tau_{n},\, n \geq 0\}$ are i.i.d. and exponentially distributed with parameter $\beta$.

Then we can rewrite $V_\pi(i)$ as:

$$V_{\pi}(i) = \mathbb{E}_{\pi}\left[\sum_{n=0}^{\infty} e^{-\alpha t_n} k(X_n, a_n) \mid X_0 = i\right] + \mathbb{E}_{\pi}\left[\sum_{n=0}^{\infty} e^{-\alpha t_n} c(X_n, a_n) \int_{0}^{\tau_{n+1}}e^{-\alpha t}dt \mid X_0 = i\right]$$
$$
=\mathbb{E}_{\pi}\left[ \sum_{n=0}^{\infty}e^{-\alpha(\tau_{1}+\dots +\tau_{n})}k(X_{n},a_{n})|X_{0}=i  \right]+\mathbb{E}_{\pi}\left[ \sum_{n=0}^{\infty} e^{-\alpha(\tau_{1}+\dots+\tau_{n})} \frac{1-e^{-\alpha \tau_{n+1}}}{\alpha}c(X_{n},a_{n})|X_{0}=i \right]
$$
$$
=\sum_{n=0}^{\infty} \mathbb{E}_{\pi}[k(X_{n},a_{n})](\mathbb{E}_{\pi}[e^{-\alpha \tau_{1}}])^{n}+\sum_{n=0}^{\infty} \mathbb{E}_{\pi}[c(X(n),a_{n})]\cdot \frac{1}{\alpha}(\mathbb{E}_{\pi}[e^{-\alpha \tau_{1}}])^{n}(1-\mathbb{E}_{\pi}[e^{-\alpha \tau_{1}}])
$$

Let $\lambda = \mathbb{E}[e^{-\alpha \tau_1}]$. Then:

$$V_\pi(i) = \sum_{n=0}^{\infty}  \mathbb{E}[k(X_n, a_n)] \lambda^n + \sum_{n=0}^{\infty} \mathbb{E}_{\pi}[c(X_{n},a_{n})]\cdot \frac{1}{\alpha}\lambda^{n}(1-\lambda)$$

Computing $\lambda$:

$$\lambda = \mathbb{E}[e^{-\alpha \tau_1}] = \int_0^\infty e^{-\alpha t} \beta e^{-\beta t}\, dt = \frac{\beta}{\alpha + \beta}$$

Then:

$$\frac{1}{\alpha}\cdot(1-\lambda)=\frac{\alpha}{\alpha+\beta} \cdot \frac{1}{\alpha}=\frac{1}{\alpha+\beta}$$

Thus:

$$V_\pi(i) = \mathbb{E}_{\pi}\left[ \sum_{n=0}^{\infty} \lambda^{n}\left( k(X_{n},a_{n})+ \frac{c(X_{n},a_{n})}{\alpha+\beta} \right) \right] =\mathbb{E}_{\pi}\left[\sum_{n=0}^{\infty}  \lambda^n R(X_n, a_n)\right]$$

where

$$R(X_n, a_n) = k(X_n, a_n) + \frac{c(X_n, a_n)}{\alpha + \beta}$$

This is the **same form as the discounted discrete-time version**, and the problem can be handled using discrete-time theory:

$$V(i) = \max_{a\in A_{i}} \left\{ R(i,a) + \lambda \sum_{j\in S} P_{ij}(a) V(j) \right\}$$

---

#### Non-Uniform Transition Rates: Uniformization

Now suppose that the rates for the inter-decision epochs are not the same. Let:

$$\beta(i, a) = \text{transition rate out of state } i \text{ when action } a \text{ is taken}$$

**Uniformization approach:**

Assume $\exists\, \beta$ s.t. $\beta(i, a) \leq \beta\,\, \forall\, i \in S,\, a \in A_i$ ($\beta$ is the **uniformization constant**).

The trick is to allow **fictitious transitions** from each state back to itself:

$$\tilde{P}_{ij}(a) = \begin{cases} \frac{\beta(i,a)}{\beta} P_{ij}(a), & i \neq j \\[6pt] \frac{\beta(i,a)}{\beta} \cdot P_{ii}(a) + 1 - \frac{\beta(i,a)}{\beta}, & i = j \end{cases}$$

Then the **Bellman/optimality equations** are:

$$V(i) = \max_{a\in A_{i}} \left\{ R(i,a) + \lambda \sum_{j\in S} \tilde{P}_{ij}(a) V(j) \right\} = \max_{a\in A_{i}} \left\{ k(i,a) + \frac{c(i,a)}{\alpha+\beta} +\frac{\beta}{\alpha+\beta}\sum_{j\in S}\tilde{P}_{ij}(a)V(j) \right\}$$

---

### Example: M/M/1 Queue with Controlled Service Rate

- Single-server queueing system; customers arrive according to a Poisson process with rate $\lambda$.
- Service time $\sim \text{Exp}(\mu)$, which can be **controlled** by the service provider depending on the number of customers in the system.
- Service requirements are independent of each other and of interarrival times.
- The service rate can be selected from a **finite subset** $\mathcal{M}$ of the interval $[0, \bar{\mu})$. It can be changed at any time when a customer arrives or departs.
- There is a cost $q(\mu)$ per unit time of using rate $\mu$, and a cost $c(i)$ per unit time when there are $i$ customers in the system.
- **Objective:** Minimize the expected total discounted cost with discount factor $\alpha$.

4/16
$\beta(i,a)\leq\beta$ for all $i\in S,a\in A_{i}$
$$\tilde{P}_{ij}(a)=
\begin{cases}
\frac{\beta(i,a)}{\beta}P_{ij}(a) & i\neq j \\
\frac{\beta(i,a)}{\beta}P_{ij}(a)+\left( 1-\frac{\beta(i,a)}{\beta} \right) & i=j
\end{cases}$$

Last time showed that $$
V(i)=\max_{a\in A_{i}}K(i,a)+\frac{C(i,a)}{\alpha+\beta}+\frac{\beta}{a+\beta}\sum_{j\in S}\tilde{P}_{ij}(a)V(j)
$$
Recall $K$ is lump sum reward/cost when you take action a in state i
Recall $C$ is continuous time cost/reward for action a in state i
Recall $\beta$ is the uniformization constant
Recall $\alpha$ is discount factor

Example: $\mu\in M$ is the service rate is in some set $M$ which is a subset of $[0,\bar{\mu}]$ ($\bar{\mu}$ is just a maximum rate $\mu$ can be) and we are trying to find optimal service rate within this acceptable set $M$. 
Recall $\lambda$ is the arrival rate
$q(\mu)$ is per unit time cost for using rate $\mu$
$c(i)$ is per unit time cost of having i customers in the system
So our objective is minimize the expected long-run total discounted cost with $\alpha$ being the discount parameter.
So our state space here is $S=\{ 0,1,2,\dots \}$
$$
\beta(i,\mu)=
\begin{cases}
\lambda & i=0 \\
\lambda+\mu & i\geq1
\end{cases}
$$
Set $\beta=\lambda+\bar{\mu}$.
So $\tilde{P}_{01}(\mu)=\frac{\lambda}{\beta}$ and $\tilde{P}_{00}(\mu)=1-\frac{\lambda}{\beta}$ from equations at beginning of this class by plugging in $\beta(i,\mu)$ and recognizing $P_{01}(\mu)=1$ since we can only have an arrival. Continuing on for further states we get $\tilde{P}_{i,i-1}=\frac{\mu}{\beta}$, $\tilde{P}_{i,i+1}=\frac{\lambda}{\beta}$,$\tilde{P}_{i,i}(\mu)=1-\frac{\lambda}{\beta}-\frac{\mu}{\beta}$
Thus, $$
R(i,\mu)=\frac{1}{\alpha+\beta}(c(i)+q(\mu))
$$
We can now write down our optimality equation $$
V(0)=\frac{1}{\alpha+\beta}\min_{\mu\in M}\left( c(0)+q(\mu)+\beta \frac{\lambda}{\beta}V(1)+\frac{\beta(\beta-\lambda)}{\beta}V(0) \right)
$$
$$
=\frac{1}{\alpha+\beta}\min_{\mu\in M}(c(0)+q(\mu)+\lambda V(1)+(\beta-\lambda V(0)))
$$
We can get optimality in general form as $$
V(i)=\frac{1}{\alpha+\beta}\min_{\mu\in M}(c(i)+q(\mu)+\mu V(i-1)+\lambda V(i+1)+(\beta-\mu-\lambda)V(i))
$$
Notice that the optimality equation fully describes the MDP as it includes the rewards/costs per action and state.

To find the optimal service rate for $i>0$ you need to minimize the above function. We can bring the $V(i)$ term from RHS to LHS. Also $\lambda V(i+1)$ term isn't dependent on $\mu$. Thus, $$
\mu^{*}(i)=\arg\!\min_{\mu\in M}q(\mu)-\mu \Delta(i)
$$
where $\Delta(i)=V(i)-V(i-1)$.
If $c(i)$ is nonnegative, nondecreasing and convex on i, then one can show that this $\Delta$ function is also nondecreasing in i. This strictly implies that $\mu^{*}(i)$ is nondecreasing in i. Being able to determine structural properties like this is very important for applying MDPs to real world complex problems where ideal assumptions may not hold, but general structural properties may. 

### Average Reward Problems
Looking at infinite horizon, but looking at cost and reward per unit time.
Assumptions:
- $R(i,a)$ are bounded for all $i\in S$ and $a\in A_{i}$
- Finite set of feasible actions of reach $i$ ($A_{i}$ is finite for all $i\in S$)
Let $\phi_{\pi}(i)=\liminf_{n\to \infty}\mathbb{E}_{\pi}\left[ \sum_{j=0}^{n}R(X_{i},a_{j})|X_{0}=i \right]$ where the expectation is essentially $n+1$ step.
Define $\pi^{*}$ to be average reward optimal if $\phi_{\pi^{*}}(i)=\sup_{\pi}\phi_{\pi}(i)$ for all $i\in S$.
Question: Does an optimal policy always exist? No
Example: $S=\{ 1,\hat{1},2,\hat{2},\dots \}$ and the actions available in each state are $A=\{ 1,2 \}$.
$P_{n,n+1}(1)=1$,$P_{n,\hat{n}}(2)=1$ for all $n\geq1$ (so if you take action 1 you go to state $n+1$ if you take action 2 you go to state $\hat{n}$).
Additionally, $P_{\hat{n},\hat{n}}(1)=1$, $P_{\hat{n},\hat{n}}(2)=1$ for $n\geq1$.
Also define $R(n,a)=0$ and $R(\hat{n},a)=1-\frac{1}{n}$ for $n\geq1$.
So notice that once we get to a state $\hat{n}$ we will be in that state forever.
Let $X_{0}=1$. For any $\pi$, $\phi_{\pi}(1)<1$ because as soon as you take action 2 your long-run average reward will be $1-\frac{1}{n}<1$. If you choose 2 at some state n, then the average reward is $1-\frac{1}{n}$. But then you can find another policy $\pi$ that performs better. So an optimal policy does not exist.

Question: Suppose that an optimal policy exists. Is it sufficient to consider stationary policies? No
Example: $S=\{ 1,2,3,\dots \}$ and actions available are $A=\{ 1,2 \}$ for each $i\in S$.
$P_{i,i+1}(1)=1,P_{i,i}(2)=1$ and rewards are $R(i,1)=0,R(i,2)=1-\frac{1}{i}$ for all $i\in S$.
So in this case you don't get stuck. You either receive nothing and go to state $i+1$ or receive $1-\frac{1}{i}$ and stay in state i. Suppose that $X_{0}=1$ and that $\pi$ is a deterministic stationary policy. There are only two types of possible deterministic stationary policies for $\pi$:
- Type 1: $\pi$ always choose action 1 $\implies \phi_{\pi}(i)=0$
- Type 2: $\pi$ always chooses 2 in some state $n$. Then since it will stay in state $n$ forever, it will earn $1-\frac{1}{n}$ at each period and so $\phi_{\pi}(i)=1-\frac{1}{n}<1$ for any $n$.
Thus, $\phi_{\pi}(i)<1$ for any deterministic stationary $\pi$.
Now consider the following nonstationary policy: when the process enters state $i$ it chooses action 2, $i$ consecutive times then chooses 1. Then the sequence of rewards received are $0,0,0, \frac{1}{2}, \frac{1}{2},0, \frac{2}{3}, \frac{2}{3}, \frac{2}{3}, 0, \frac{3}{4}, \frac{3}{4}, \frac{3}{4}, \frac{3}{4}, 0,\dots$ So the long-run average reward is $$
=\frac{\sum_{k=1}^{n}(k-1)}{\sum_{k=1}^{n} (k+1)}=\frac{\frac{n(n+1)}{2}}{\frac{(n+1)(n+2)}{2}}=\frac{n}{n+2}
$$
So taking the limit we see the long-run average reward is $\lim_{ n \to \infty } \frac{n}{n+2}=1$. Thus there is a non-stationary policy that is better than all stationary policies.

4/21
## Average Rewards

### Motivating Example

**State space:** $S = \{\theta,1,\hat{1}, 2, \hat{2}, \ldots, n, \hat{n}, \ldots\}$ 

- For any $1 \leq n < \infty$: $A(n) = \{1, 2\}$
- **Transition probabilities:**
  - $P_{n,\, n+1}(1) = 1$
  - $P_{n,\, \hat{n}}(2) = \alpha_n$
  - $P_{n,\, \theta}(2) = 1 - \alpha_n$
  - $P_{\theta,\, \theta}(a) = 1 \quad \forall\, a \in A(\theta) = \{1, 2\}$
- For any $\hat{1} \leq \hat{n} < \infty$: $A(\hat{n}) = \{1\}$ and $P_{\hat{n},\, \hat{n}-1}(1) = 1$, $n \geq 2$
- Lastly, $P_{\hat{1},\, 1}(1) = 1$

**Rewards:**
- $R(n, a) = 0$ for $n = 1, 2, \ldots$
- $R(\theta, a) = 0$
- $R(\hat{n}, a) = 2$ for $n = 1, 2, \ldots$

Choose $\alpha_n \in [0, 1]$ s.t. $$
\prod_{n=1}^{\infty} \alpha_{n}=\frac{3}{4}
$$
where $\frac{3}{4}$ can be any constant $c$ s.t. $0 < c < 1$.

Suppose $X_0 = 1$.

- Under any **stationary policy**, the state will hit state $\theta$ eventually w.p. 1, so a positive reward will be collected only in a finite number of periods. Thus, under any stationary policy, the average reward will be $0$ w.p. 1.
- Consider a **non-stationary policy**: initially chooses action 2, and on its $n$-th return to state 1, chooses action 1 $n$ times and then chooses action 2. The average reward is:
  - $0$ w.p. $1-\prod_{n=1}^{\infty}\alpha_n$
  - $1$ w.p. $\prod_{n=1}^{\infty}\alpha_{n}$

Thus, the expected average reward is $$
\prod_{n=1}^{\infty} \alpha_{n}=\frac{3}{4}
$$

---

### Existence of Optimal Stationary Policies

**Theorem.** If there exists a bounded function $h(i)$, $i \geq 0$, and a constant $g$ s.t.

$$g + h(i) = \max_{a \in A(i)}\left\{R(i, a) + \sum_{j=0}^{\infty}  P_{ij}(a)\, h(j)\right\}, \quad i \geq 0 \tag{1}$$

then there exists a stationary policy $\pi^*$ s.t. $g = \phi_{\pi^{*}}(i) = \max_{\pi}\phi_{\pi}(i)$ for all $i \geq 0$.

Furthermore, $\pi^*$ is any policy that, for each $i$, prescribes an action that maximizes the RHS of (1).

---

#### Intuition for the Theorem

- Recall the discounted infinite horizon problem. Here we don't have any discounting, but it is reasonable to believe that in some limiting region where $\alpha \to 1$, the average reward problem might be obtained.
- Define $V_\alpha(i)$ = optimal expected $\alpha$-discounted return function. Then:

$$V_\alpha(i) = \max_{a\in A(i)}\left\{R(i, a) + \alpha \sum_j P_{ij}(a)\, V_\alpha(j)\right\}, \quad i \geq 0 \tag{2}$$

- Recall also that the $\alpha$-optimal policy chooses the action that maximizes the bracketed term on the RHS of (2).
- For the average reward optimal policy, consider choosing actions that maximize:

$$\lim_{ \alpha \to 1 } \left[ R(i, a) + \alpha \sum_j P_{ij}(a)\, V_\alpha(j) \right]$$

The limit may not exist and could be infinite for many actions. Thus, we consider an alternative approach.

---

#### Derivation via Bias Function

Fix a state, say state $0$. Define:

$$h_\alpha(i) := V_\alpha(i) - V_\alpha(0)$$

Then from (2):

$$h_\alpha(i) + V_\alpha(0) = \max_{a\in A(i)}\left\{R(i, a) + \alpha \sum_j P_{ij}(a)\left[h_\alpha(j) + V_\alpha(0)\right]\right\}$$

$$\Rightarrow\quad (1 - \alpha)V_\alpha(0) + h_\alpha(i) = \max_{a\in A(i)}\left\{R(i, a) + \alpha \sum_j P_{ij}(a)\, h_\alpha(j)\right\}$$

Now, for some sequence $\{\alpha_{n}\}$ s.t. $\alpha_{n} \to 1$, suppose $h_{\alpha_{n}}(j) \to h(j)$ and $(1 - \alpha_{n})V_{\alpha_{n}}(0) \to g$, where $g$ is some constant. Then, assuming we can exchange the limit and the sum on the RHS, we get:

$$g + h(i) = \max_{a \in A(i)}\left\{R(i, a) + \sum_{j=0}^{\infty}  P_{ij}(a)\, h(j)\right\}$$

> **Note:** $h(\cdot)$ is called the **bias** or **relative reward**. It gives the difference in total rewards by starting the process in state $i$ as opposed to state $0$.

---

#### Formal Theorem

**Theorem.** If there exists a constant $N < \infty$ s.t.

$$\left|V_\alpha(i) - V_\alpha(0)\right| < N \quad \forall\, \alpha,\, i$$

then:

1. There exists a bounded function $h$ and a constant $g$ satisfying (1).
2. For some sequence $\alpha_{n} \to 1$: $h(i) = \lim_{n\to\infty}\left[V_{\alpha_{n}}(i) - V_{\alpha_{n}}(0)\right]$.
3. $\lim_{ \alpha \to 1 }(1-\alpha)V_{\alpha}(0)=\lim_{n\to\infty}(1 - \alpha_{n})V_{\alpha_{n}}(0) = g$.

> **Note:** Part (ii) implies that $h(\cdot)$ inherits the structural properties of $V_\alpha(i)$.

---

#### Sufficient Condition for the Theorem

Define $M_{ij}(f_\alpha)$ to denote the expected time to go from state $i$ to state $j$ when using the $\alpha$-discounted optimal policy $f_\alpha$.

If, for some state (say state $0$), there exists a constant $N<\infty$ s.t.

$$M_{i0}(f_\alpha) < N \quad \forall\, i,\, \alpha$$

then $V_\alpha(i) - V_\alpha(0)$ is uniformly bounded, and thus the condition of the previous theorem holds.

---

#### Corollary

If the state space is **finite** and every stationary policy gives rise to an **irreducible Markov chain**, then $V_\alpha(i) - V_\alpha(0)$ is uniformly bounded, and hence the conditions of the theorem hold.

4/23 (LDOC)
## Long-Run Average Reward Problems (Cont.)
Final will most likely  consist of 5-6 questions most of which will come from queueing theory and renewal processes (probably one question on MDPs)
Can use previous cheat sheet and add one more piece of paper
Know main results from CTMC/DTMCs like balance equations, basic analysis, etc. (don't need to know all of 641, but it is still interconnected)
Will have time for questions May 6 (sending out an announcement)

Recall
$$
g + h(i) = \max_{a \in A(i)}\left\{R(i, a) + \sum_{j=0}^{\infty}  P_{ij}(a)\, h(j)\right\}\quad\forall i\in S
$$
So now how do we find $h(i)$ and $g$ in general?
Finding an optimal policy will give us $g$ and $h(i)$.
### Solution Methods
#### LP Solution
Assuming finite state space $\{ 1,2,\dots,M \}$
We assume under any stationary policy, the Markov Chain is irreducible
Allow randomized policies $\beta=\{ \beta_{i}(a) : a\in A_{i},i\in \{ 1,2,\dots,M \} \}$ where $\beta_{i}(a)$ is the probability of choosing action $a$ in state $i$. Thus, $0\leq\beta_{i}(a)\leq1$ and $\sum_{a\in A_{i}} \beta_{i}(a)=1\quad\forall i\in S$.
Under any given policy $\beta$ the sequence of states $\{X_{n},\;n\geq1\}$ is a DTMC with transition probability matrix $P_{ij}(\beta)$ where $$
P_{ij}(\beta)=\mathbb{P}_{\beta}(X_{n+1}=j|X_{n}=i)=\sum_{a\in A_{i}}P_{ij}(a)\beta_{i}(a)
$$
For any policy $\beta$, let $\pi_{ia}$ denote the limiting probability that the process will be in state $i$ and action $a$ is chosen. Then $$
\pi_{ia}=\lim_{ n \to \infty } \mathbb{P}_{\beta}(X_{n}=i,a_{n}=a)
$$
So $\pi=\{ \pi_{ia} \}_{i\in S,a\in A_{i}}$ must satisfy:
1. $\pi_{ia}\geq0$
2. $\sum_{i\in S}\sum_{a\in A_{i}}\pi_{ia}=1$
3. $\sum_{a}\pi_{ja}=\sum_{i}\sum_{a\in A_{i}}\pi_{ia}P_{ij}(a)\;,\forall j\in S$
Furthermore, it can be shown that if there exists $\{ \pi_{ia} \}$ satisfying (1), (2), and (3), then there exists a policy $\beta$ such that $\pi_{ia}$ is equal to the steady state probability of being in state $i$ and choosing action $a\in A_{i}$ when $\beta$ is used and $\beta$ is defined as $$
\beta_{i}(a)=\frac{\pi_{ia}}{\sum_{a\in A_{i}}\pi_{ia}}
$$
#### Expected Average Reward under $\beta$
The expected average reward under $\beta$ is
$$
\sum_{i\in S}\sum_{a\in A_{i}}\pi_{ia}R(i,a)
$$
Then the problem of determining the policy that maximizes average reward is $$
\max\left[ \sum_{i\in S}\sum_{a\in A_{i}}\pi_{ia}R(i,a) \right]
$$
subject to
1. $\pi_{ia}\geq0\quad\forall i\in S,a\in A_{i}$
2. $\sum_{i\in S}\sum_{a\in A_{i}}\pi_{ia}=1$
3. $\sum_{a\in A_{j}}\pi_{ja}=\sum_{i\in S}\sum_{a\in A_{i}}\pi_{ia}P_{ij}(a)\quad\forall j\in S$
If $\pi^{*}=\{ \pi_{ia}^{*} \}_{i\in S,a\in A_{i}}$ maximizes the LP then the optimal policy will be given by $$\beta^{*}_{i}(a)=\frac{\pi_{ia}^{*}}{\sum_{a\in A_{i}}\pi_{ia}^{*}}$$
Using similar argument to previously using LP for discounted version of this under infinite horizon, solving with LP means there exists a deterministic optimal policy. Formally expressed below.

>Note: Just as for the infinite horizon discounted problem, it can be shown that for each $i$, $\pi_{ia}^{*}$ is positive for only one $a$. Hence, there exists an optimal policy which is stationary and non-randomized.

>Note that it is easy to add constraints to an LP which is a considerable benefit.
>For example, $\sum_{i}\pi_{ia}\leq \alpha$ can just be added as a constraint (only want to accept a particular action $\alpha$% of the time)

### Policy Improvement Algorithm
Need a particular assumption in order for algorithm to converge:
**Unichain Assumption**: For each stationary policy the associated DTMC has no two disjoint closed sets.
#### Theorem
Let $g$ and $h_{i}\;,i\in S$ are given numbers. Suppose that the stationary policy $f$ has the property that $$R(i,f(i))-g+\sum_{j\in S}P_{ij}(f(i))h_{j}\geq h_{i}\quad\forall i\in S$$ If this is true then the long-run average reward for policy $f$, which is defined as $g_{f}$ satisfies $$
g_{f}\geq g
$$
Note that if we move $g$ to the RHS of the inequality then we have the optimality equation.

**The Algorithm**
Step 1 Initialization: Choose a stationary policy $f$
Step 2 Value Determination: For policy $f$ compute the unique solution $\{ g_{f},h_{i}^{f} \}_{i\in S}$ to the following system of linear equations: $h_{i}^{f}=R(i,f(i))-g_{f}+\sum_{j\in S}P_{ij}(f(i))h_{j}^{f}\;,\forall i\in S$ and $h_{s}^{f}=0$ where $s$ is an arbitrarily chosen state (think of $h_{s}^{f}$ as being a baseline/starting state)
Step 3 Policy-Improvement Step: For each state $i\in S$ determine an action $a_{i}$ yielding the maximum in $$
\max_{a\in A_{i}}\left\{  R(i,a)-g_{f}+\sum_{j\in S}P_{ij}(a)h_{j}^{f}  \right\}
$$
Then the new policy $\bar{f}$ is obtained by choosing $\bar{f}(i)=a_{i}$ with the convention that $\bar{f}(i)=f(i)$ when $f(i)$ is one of the maximizing actions.
Step 4 Convergence Check: If $f(i)=\bar{f}(i),\;\forall i\in S$ then stop. Otherwise, go to step 2 with $f$ replaced by $\bar{f}$.

### Value Iteration Algorithm
Define $V_{n}(\cdot)$ recursively as $$
V_{n}(i)=\max_{a\in A_{i}}\left\{  R(i,a)+\sum_{j}P_{ij}(a)V_{n-1}(j)  \right\},\;\forall i\in S \tag{*}
$$
with an arbitrarily bounded function $V_{0}(\cdot)$.
So $V_{n}(i)$ is the maximum total reward with $n$ periods left and initial state is $i$ and $V_{0}(\cdot)$ is the terminal reward function.
We want to look at the difference $V_{n}(i)-V_{n-1}(i)$ and look at how large the increment in reward is by adding one more time step (starting from same starting state $i$). This difference should converge to something that is independent of the starting state $i$ or large $n$.
Formally, for large $n$ $V_{n}(i)-V_{n-1}(i)$ will be very close to maximum average reward per unit time and the stationary policy that maximizes the RHS $\forall i\in S$ will be very close in rewards to the maximum average reward.
Let $M_{n}=\max_{j\in S}\{ V_{n}(j)-V_{n-1}(j) \}$
Let $m_{n}=\min_{j\in S}\{ V_{n}(j)-V_{n-1}(j) \}$
#### Theorem
Suppose that for each average reward optimal stationary policy, the associated DTMC has no two disjoint closed sets (this is the Weak Unichain Assumption; it is weak because it isn't for all stationary policies). For any $n\geq1$, let $f_{n}(\cdot)$ be a stationary policy whose actions maximize the RHS of (\*) $\forall i\in S$. Then, $$
m_{n}\leq g_{f_{n}}\leq g\leq M_{n},\quad\forall i\in S,n\geq1
$$
where $g$ is the maximum average reward per unit time. Moreover, the sequence $\{ m_{n},n\geq1 \}$ is nondecreasing and the sequence $\{ M_{n},n\geq1 \}$ is nonincreasing.

**The Algorithm**
Step 1: Choose $V_{0}(i)=0$ $\forall i\in S$
Step 2: Compute the value function $V_{n}(i),\;\forall i\in S$ from (\*) equation above and determine $f_{n}(\cdot)$ as a stationary policy which chooses the action that maximizes the RHS.
Step 3: Compute $M_{n}$ and $m_{n}$ using the equations above. Stop with policy $f_{n}$ if $0\leq M_{n}-m_{n}\leq \epsilon m_{n}$ where $\epsilon>0$. Otherwise go to step 4.
Step 4: $n:=n+1$ and go to step 2.

The algorithm itself isn't guaranteed to converge. The algorithm converges if we additionally assume that the average reward optimal policy is aperiodic.

