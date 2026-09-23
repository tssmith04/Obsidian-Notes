8/17 *scribing*
Introductory element reviewing course resources and introductions of classmates
## Linear Algebra Review
### Basics
Working with matrices and vectors
Recall Matrix is typically represented with capital letters $A \in \mathbb{R}^{mxn}$ to denoted a $m$ by $n$ matrix (m rows, n columns)
Recall Vectors are represented with lower case letters $u\in \mathbb{R}^{p}=\mathbb{R}^{px1}$ (column vector)
Recall Diagonal vectors are represented as $diag(a_{1},\dots,a_{n})$ which is a matrix with $a_{1},\dots,a_{n}$ down the diagonal and 0's everywhere else in the matrix.
Recall the Identity matrix is $diag(1,1,\dots,1)$ which is denoted as $I_{n}$ where there are n 1's.
Recall a vector of 1's is denoted $1_{n}$ and similarly a vector of 0's is denoted $0_{n}$.
Recall transpose is denoted $A^{T}$ and flips the elements across the diagonal of the matrix, thus $A\in \mathbb{R}^{mxn} \implies A^{T}\in \mathbb{R}^{nxm}$.
Recall a symmetric matrix is one such that $A=A^{T}$

### Vector Inner Products and Outer Products
Let $u\in \mathbb{R}^{n}, v\in \mathbb{R}^{n},w\in \mathbb{R}^{p}$
Inner Product is then denoted $<u,v> =u^{T}v=u_{1}v_{1}+u_{2}v_{2}+\dots+u_{n}v_{n}$.
Outer Products are defined between two vectors of potentially different lengths. For example, $uw^{T}$. This results in a matrix with entries being all of the possible pairwise cross products of elements of $u$ and $w$.

### Matrix Sums
Requires two matrices of the same dimensions to be well defined.
Let $A\in \mathbb{R}^{mxn},B\in \mathbb{R}^{mxn}$ then $A+B\in \mathbb{R}^{mxn}$ and $A+B$ has each corresponding element added together e.g. $a_{11}+b_{11}$ as the top left entry.

### Matrix Products
Let $A\in \mathbb{R}^{mxn},B\in R^{nxp}$ then $AB\in \mathbb{R}^{mxp}$ with $AB=[c_{ij}]_{1\leq i\leq m,\;1\leq j\leq p}$ and $c_{ij}=\sum_{k=1}^{n}A_{ik}B_{kj}$.
One property of the transpose of a matrix product is $(AB)^{T}=B^{T}A^{T}$ i.e. the order of matrix multiplication is flipped by transpose.

### Trace
The trace requires a square matrix, $A\in \mathbb{R}^{mxm}$
The trace is the sum of diagonal elements: $tr(A)=\sum_{k=1}^{m}a_{kk}$
One nice property of the trace is the **cyclic property** which states $tr(AB)=tr(BA)$. 
Generally, $AB\neq BA$. Furthermore, $AB=CB$ does not imply $A=C$.

### Five Views of Matrix Multiplication
1. Definition view: Let $A\in \mathbb{R}^{mxn},\;B\in \mathbb{R}^{nxp}$ and $AB=[c_{ij}]_{1\leq i\leq m,\;1\leq j\leq p}$ with $c_{ij}=\sum_{k=1}^{n}A_{ik}B_{kj}$.
2. $A$ acting on the columns of $B$ i.e. we can think of $A$ as a map from $\mathbb{R}^{nxp}\to \mathbb{R}^{mxp}$. $AB=A[B[:,1]\;B[:,2]\;\dots\;B[:,p]]=[AB[:,1]\;AB[:,2]\;\dots\;AB[:,p]]$. Note that $B[:,i]$ are column vectors of $B$. 
3. $B$ acting on the rows of $A$. Similar to view 2 we have $[A[1,:]\;\dots\;A[m,:]]^{T}B=[A[1,:]B\;\dots\;A[m,:]B]^{T}$ where $A[i,:]$ is a row vector. 
>Note that despite the seemingly simple nature of this it can be very useful to switch views on the fly when dealing with complicated matrices as one complicated matrix acting on data on the left or vice versa depending on how you can group matrices.
4. Outer products of Inner Products. So $AB=[A[1,:]\;\dots\;A[m,:]]^{T}[B[:,1]\;\dots\;B[:,p]]$ where $A[i,:]$ are row vectors and $B[:,i]$ are columns vectors. This results in a matrix whose entries are inner products e.g. $A[1,:]B[:,1]$ is the top left entry. This is the conventional way for solving matrix multiplication by hand. To recap, we initially take the outer product between rows of $A$ and columns of $B$ to generate a matrix of inner products between their rows and columns.
5. Inner products of Outer products. So $AB=[A[:,1]\;\dots\;A[:,n]][B[1,:]\;\dots\;B[n,:]]^{T}=A[:,1]B[1,:]+A[:,2]B[2,:]+\dots+A[:,n]B[n,:]$. Note here that $A[:,i]$ are now column vectors and $B[i,:]$ are now row vectors. To recap, we take an inner product between columns of $A$ and rows of $B$ to be able to add the outer products (matrices) of each column in $A$ and row in $B$.

### Projection Matrices
>In this class we will use "orthogonal projection" interchangeably with "projection."
#### Properties/Definitions
A matrix $P$ is **idempotent** if $P=P^{2}=PP$.
A symmetric idempotent matrix is called a **projection matrix.**


8/19
### Linear Independence
A collection of vectors $a_{1},a_{2},\dots,a_{n}\in \mathbb{R}^{p}$ for all $i$ are said to be linearly independent iff $\sum_{i=1}^{n}c_{i}a_{i}=0_{p}\iff c_{i}=0\;\forall i$. I.e. if we have a vector $c_{i}$ that is non-zero then the sum would not result in the 0 vector because you can't have two $a_{i}$'s cancel each other out.
### Orthogonality
Two vectors $u,v\in \mathbb{R}^{p}$ are orthogonal if $u^{T}v=0$
### Column Space
$Col(A)$ for matrix $A\in \mathbb{R}^{nxp}$ is the vector space spanned by the columns of $A$
### Row Space
$Row(A)$ is the vector space spanned by the rows of $A$
### Span
Given a set of vectors $a_{1},\dots,a_{n}\in \mathbb{R}^{p}$, the span$(a_{1},\dots,a_{n})=\left\{  \sum_{i=1}^{n}c_{i}a_{i},\;\forall c_{i}\in \mathbb{R}  \right\}$.
### Rank
The rank of a matrix $A\in \mathbb{R}^{nxp}$  is
- the number of linearly independent columns which is also $dim(Col(A))$
	- Recall dimension is number of columns required to build a basis to span $A$
- the number of linearly independent rows which is also $dim(Row(A))$
$$rank(AB)\leq\min(rank(A),rank(B))$$
### Null Space
For matrix $A\in \mathbb{R}^{nxp}$ we have $\mathcal{N}(A):=\{ x:Ax=0_{n},\;x\in \mathbb{R}^{p} \}$
### Matrix Inverses
The square matrix $A\in \mathbb{R}^{nxn}$ is said to be invertible (or non-singular) if there exists $A^{-1}\in \mathbb{R}^{nxn}$ satisfying $AA^{-1}=A^{-1}A=I_{n}$.
Results:
 - $A$ is invertible iff $rank(A)=n$
- If $A,B$ are both invertible matrices, $(AB)^{-1}=B^{-1}A^{-1}$
>Note: When should we actually invert matrices (in practice)? Trick question, almost never since computing inverses are computationally expensive compared to other computational methods. Thus, what we do at the board (math wise) may be different from what we do at the keyboard (computationally).

### Generalized Inverses
Suppose matrix $A\in \mathbb{R}^{mxn}$. The matrix $G\in \mathbb{R}^{nxm}$ is a generalized inverse if it satisfies $AGA=A$.
- $G$ always exists
- $G$ may not be unique
>Note: $G$ doesn't need to be unique. For example, suppose $A=0_{m,n}$ (0 matrix mxn), $G=0_{n,m}$ and $G=1_{n,m}$ (matrix of all 1's) (or for that matter any nxm matrix works).
### Vector Norm
If $u,v\in \mathbb{R}^{n}$ then the $l_{2}$-norm of $u$ is $||u||_{2}=||u||=\sqrt{u^{T}u }$
### Orthogonal Matrix
$A\in \mathbb{R}^{nxn}$ is an orthogonal matrix if $A^{T}A=I_{n}$
>Note: For matrices, "orthogonality" really means all columns are orthogonal and normalized. If a matrix is orthonormal it just means its columns are normalized.

### Eigenvalues and Eigenvectors
Consider $A\in \mathbb{R}^{nxn}$. If $Ax=\lambda x$ for some $x\in \mathbb{R}^{n},\;x\neq0_{n}$ and $\lambda\in \mathbb{R}$, then $\lambda$ is an eigenvalue of $A$ and $x$ is an eigenvector of $A$.
>Intuition: Eigenvectors "pass through" the operator $A$ without rotation, only experiencing rescaling or reflection as characterized by $\lambda$.
#### Useful Properties
- If $A$ has eigenvalues $\lambda_{1},\dots,\lambda_{n}$ then $rank(A)=$ #$\{ i:\lambda_{i}\neq0 \}$ (number of non-zero eigenvalues).
- $tr(A)=\sum_{i=1}^{n}\lambda_{i}$
### Positive Definite Matrices
The symmetric matrix $A\in \mathbb{R}^{nxn}$ is positive definite (PD) if $\forall x\neq0_{n},\;x^{T}Ax>0\equiv$ All eigenvalues are positive.
#### Properties of PD Matrix $A\in \mathbb{R}^{nxn}$
	1. All diagonal entries are positive
1. $A$ is invertible, $A^{-1}$ is also PD
2. $tr(A)>0$ (inherent from property 1)
3. $\exists$ non-singular $R$ s.t. $A=RR^{T}$
### Positive Semidefinite Matrices
The symmetric matrix $A\in \mathbb{R}^{nxn}$ is positive semidefinite (PSD) if $\forall x\neq0_{n},\;x^{T}Ax\geq0\equiv$ All eigenvalues are non-negative.
#### Properties of PSD Matrix $A\in \mathbb{R}^{nxn}$
1. Diagonal is non-negative
2. $tr(A)\geq0$
### Projection and Geometry
Recall that a matrix $P$ is a projection matrix if $P$ is
1. Symmetric: $P=P^{T}$
2. Idempotent: $P=PP=P^{2}$
#### Projection onto lines and subspaces
Let $\Omega$ be a subspace of $\mathbb{R}^{n}$. We write $P_{\Omega}$ to denote the unique projection matrix with $Col(P_{\Omega})=\Omega$.
Special case: $n=2$. Suppose line $y=x$ is $\Omega$ so $\Omega$ is a 1-$D$ subspace of $\mathbb{R}^{2}$. Then $u=P_{\Omega}z$ where $u$ is the vector that minimizes the distance to $z$ from $\Omega$ where $z$ is some vector coming out from the origin.

8/24
Projections are really at the heart of regression, hence the significant time spent on the topic.
From example above (**projection onto lines**) note that with vectors $x,y\in \mathbb{R}^{n}$ coming out from origin then the vector that minimizes the distance between $x$ and $y$ is solved as $$
P_{x}(y)=\frac{x^{T}y}{x^{T}x}x
$$
Revisiting **Projections onto subspaces**: Let $\Omega$ be a subspace of $\mathbb{R}^{n}$ with $dim(\Omega)=p\leq n$. Find $a_{1},a_{2},\dots,a_{p}\in \mathbb{R}^{n}$ such that $span(\{ a_{1},\dots,a_{p} \})=\Omega$.
Let $A=[a_{1}\;a_{2}\dots a_{p}]\in \mathbb{R}^{nxp}$ (where $a_{i}$ are column vectors). Then the projection operator onto $\Omega$ written $P_{\Omega}$ is given by $$P_{\Omega}=A(A^{T}A)^{-1}A^{T}$$
By construction $A$ has full column rank because we state above that $span(\{ a_{1},\dots,a_{p} \})=\Omega$ thus the columns of $A$ form a span and each $a_{i}$ are linearly independent. Since $A^{T}A$ is square and $A$ has full column rank, we know that $A^{T}A$ is always invertible here (by construction).

**Definition (Orthogonal Complement):** For a subspace $\Omega$ of $\mathbb{R}^{n}$, the orthogonal complement of $\Omega$ with respect to $\mathbb{R}^{n}$ written $\Omega^{\perp}$, is $\Omega^{\perp}=\{ v\in \mathbb{R}^{n} : v^{T}u=0\;\forall u\in \Omega \}$.
Fact: $dim(\mathbb{R}^{n})=n$, $dim(\Omega)=p\implies dim(\Omega^{\perp})=n-p$.
The projection onto $\Omega^{\perp}$ is given by $$
P_{\Omega^{\perp}}=P_{\Omega}^{\perp}=I-P_{\Omega}=P_{\mathbb{R}^{n}}-P_{\Omega}
$$
Is $P_{\Omega}^{\perp}$ a projection matrix? Yes, check symmetry and idempotent.
- Idempotent: $P_{\Omega}^{\perp}P_{\Omega}^{\perp}=(I-P_{\Omega})(I-P_{\Omega})=I+P_{\Omega}P_{\Omega}-IP_{\Omega}-P_{\Omega}I=I+P_{\Omega}-P_{\Omega}-P_{\Omega}=I-P_{\Omega}=P_{\Omega}^{\perp}$
- Symmetry: $(P_{\Omega}^{\perp})^{T}=(I-P_{\Omega})^{T}=I^{T}-P_{\Omega}^{T}=I-P_{\Omega}=P_{\Omega}^{\perp}$

#### Projection onto Column Spaces
Let $X\in \mathbb{R}^{nxp}$ with $rank(X)=p$  (i.e. the columns of $X$ are linearly independent)
	Then the projection onto $Col(X)$ is written $$P_{Col(X)}=:P_{X}$$ (always true), is given by $P_{X}=X(X^{T}X)^{-1}X^{T}$ (if full column rank)
>Remark: In regression, $P_{X}$ is often called the **hat matrix** because it puts "the hat" on y. I.e. $\hat{y}=P_{X}y$.

We can decompose any vector $y$ into its projection onto $X$ and onto its projection onto orthogonal complement: $$
y=P_{X}y+P_{X}^{\perp}y=\hat{y}+\hat{\epsilon}=P_{X}y+(I-P_{X})y=P_{X}y+Iy-P_{X}y=y
$$
8/26
## Regression
Check Chapter 3.1 in Seber and Lee for more information

Terminology:
- Observations $y\in \mathbb{R}^{n}$ or $y_{1},\dots,y_{n}$
- Design Matrix $X\in \mathbb{R}^{nxp}$ which can sometimes be thought of as $n$ row vectors stacked on top of each other and similarly can sometimes be thought of as $p$ columns vectors stacked next to each other
- Coefficients $\beta\in \mathbb{R}^{p}$ or $\beta_{1},\dots,\beta_{p}$
- Errors $\epsilon\in \mathbb{R}^{n}$ or $\epsilon_{1},\dots,\epsilon_{n}$. We will think about errors distributionally later.

### Model
Our model is $y_{i}=X_{i1}\beta_{1}+X_{i2}\beta_{2}+\dots+X_{ip}\beta_{p}+\epsilon_{i}$ ($X_{i1}$ is the $i$th row and first 1 column entry) written more compactly as $\sum_{k=1}^{p}X_{ik}\beta_{k}+\epsilon_{i}=X[i,:]\beta+\epsilon_{i}$. In matrix form we can write this entire thing as $y=X\beta+\epsilon$. Can be thought of as trying to create $y$ through a linear combination of the columns of $X$ where $\beta$ is our coefficients that lead to this linear combination. Typically, $y,X$ are observed and $\beta,\epsilon$ are unknown.

 Under a candidate $\tilde{\beta}$ we have $y=X \tilde{\beta}+\tilde{\epsilon}$ where $\tilde{\epsilon}:=y-X \tilde{\beta}$
 The goal is to choose $\tilde{\beta}$ to make $\tilde{\epsilon}$ small
 >Note: For today, assume $rank(X)=p$ (full column rank).
 
We want to find $\hat{\beta}\in argmin_{\tilde{\beta}\in \mathbb{R}^{p}}||\tilde{\epsilon}||_{2}$ and for simplicity use $b$ as optimization variable for $\tilde{\beta}$
This is equivalent to trying to find $argmin_{b\in \mathbb{R}^{p}}||y-Xb||_{2}$ which is equivalent to finding $argmin_{b\in \mathbb{R}^{p}}||y-Xb||_{2}^{2}$ since $||\cdot||_{2}\geq0$.
How would we solve for this argmin:
1. Calculus: $||y-Xb||_{2}^{2}=(y-Xb)^{T}(y-Xb)=y^{T}y+b^{T}X^{T}Xb-b^{T}X^{T}y-y^{T}Xb=y^{T}y+b^{T}X^{T}Xb-2b^{T}X^{T}y=:s(b)$. Now $\frac{ds}{db}=2X^{T}Xb-2X^{T}y=0\implies X^{T}Xb=X^{T}y\implies b=(X^{T}X)^{-1}X^{T}y$. Since we assumed that $rank(X)=p$ then $(X^{T}X)^{-1}$ exists. This gives $b$ as a stationary point, but we need to check second derivative to ensure $b$ is a minimizer. Thus, $\frac{d^{2}s}{dbdb^{T}}=2X^{T}X$ which is positive definite meaning $b$ is a minimizer.
2. Geometric: $\hat{\beta}\in argmin_{b\in \mathbb{R}^{p}}||y-Xb||_{2}^{2}$ which we can instead rewrite as $\hat{\theta}\in argmin_{\theta\in Col(X)}||y-\theta||_{2}^{2}$. I.e. instead of finding a $b\in \mathbb{R}^{p}$ which is a linear combination of the columns of $X$ we can think about the entire term $Xb=\theta$ as living in the column space of $X$. Claim: The minimizer $\hat{\theta}$ will satisfy
	1. $\hat{\theta}\in Col(X)$ (Feasibility)
	2. $(y-\hat{\theta})\in Col^{\perp}(X)$
	Suppose $\hat{\theta}=P_{X}y$ and let $\tilde{\theta}$ be some other candidate solution. Then consider $y-\tilde{\theta}=y-\hat{\theta}+\hat{\theta}-\tilde{\theta}$. Also note that $||y-\tilde{\theta}||_{2}^{2}=||y-\hat{\theta}+\hat{\theta}-\tilde{\theta}||_{2}^{2}=(y-\hat{\theta}+\hat{\theta}-\tilde{\theta})^{T}(y-\hat{\theta}+\hat{\theta}-\tilde{\theta})=[(y-\hat{\theta})+(\hat{\theta}-\tilde{\theta})]^{T}[(y-\hat{\theta})+(\hat{\theta}-\tilde{\theta})]$ and multiplying these out we get $(y-\hat{\theta})^{T}(y-\hat{\theta})+2(y-\hat{\theta})^{T}(\hat{\theta}-\tilde{\theta})+(\hat{\theta}-\tilde{\theta})^{T}(\hat{\theta}-\tilde{\theta})$. Now focusing on the middle term (dropping 2) we have $(y-\hat{\theta})^{T}(\hat{\theta}-\tilde{\theta})=(y-P_{X}y)^{T}(P_{X}y-\tilde{\theta})=(y-P_{X}y)^{T}(P_{X}y-P_{X}\tilde{\theta})$ (since $\tilde{\theta}$ is a candidate solution $\implies\tilde{\theta}\in Col(X)$ so we can multiply by $P_{X}$ with no consequence) $=(y-P_{X}y)^{T}P_{X}(y-\tilde{\theta})=(P_{X}^{T}y-P_{X}^{T}P_{X}y)^{T}(y-\tilde{\theta})$ (now use projection properties) $=(P_{X}y-P_{X}y)^{T}(y-\tilde{\theta})=0^{T}(y-\tilde{\theta})=0$
	Now going back up to $||y-\hat{\theta}||_{2}^{2}=(y-\hat{\theta})^{T}(y-\hat{\theta})+(\hat{\theta}-\tilde{\theta})^{T}(\hat{\theta}-\tilde{\theta})=||y-\hat{\theta}||_{2}^{2}+||\hat{\theta}-\tilde{\theta}||_{2}^{2}$. Note the second term is minimized to 0 when $\hat{\theta}=\tilde{\theta}$. We can't do anything with first term since we already fixed $\hat{\theta}=P_{X}y$. Thus, we conclude that $\hat{\theta}=P_{X}y$ is the minimizer (among all $\theta\in Col(X)$ ) of $||y-\theta||_{2}^{2}$. Moreover, since $\hat{\theta}\in Col(X)$ there exists a $\hat{\beta}$ such that $\hat{\theta}=X\hat{\beta}$. And since we are assuming $X$ has full column rank there is one and only one such $\hat{\beta}$. Also since $y-\hat{\theta}\in Col^{\perp}(X)$ (from Seeber and Lee appendix first property + existence proven above) we know that $X^{T}(y-\hat{\theta})=0\implies X^{T}y=X^{T}\hat{\theta}\implies X^{T}y=X^{T}X\hat{\beta}\implies\hat{\beta}=(X^{T}X)^{-1}X^{T}y$. Can look at picture on phone (8/26 12:18) as well for visualization which essentially says that $\hat{\theta}$ is the vector in the column space of $X$ that lies directly under $y$ i.e. the projection of $y$ onto the column space. Any other $\tilde{\theta}$ would be rotated around thus meaning the distance is further (not minimal).

### Projection Computations
To construct a projection matrix onto $Col(X)$ we could use $P_{X}=X(X^{T}X)^{-1}X^{T}$ but this includes an explicit inverse which we would like to avoid. If instead we have an orthonormal basis $\alpha_{1},\dots,\alpha_{p}$ such that $Col(X)=span(\{ \alpha_{1},\dots,\alpha_{p} \})$ we can build a $Q=[\alpha_{1}\;\dots\;\alpha_{p}]$ ($\alpha_{i}$ are column vectors). Then $Q^{T}Q=I_{p}$ and $P_{X}=QQ^{T}$. So the question is how can we get $Q$ from $X$?
1. Gram-Schmidt (Intuition: work one column at a time left to right and project onto orthogonal complement of preceding columns then normalize)
2. SVD (a little more stable than (1); take first $p$ columns of $U$ to make $Q$ since only first $p$ entries down diagonal of $\Sigma$ are nonzero)
3. QR decomposition (directly gives us a $Q$ and $R$ will generally have nonzero entries on and above diagonal and 0's below diagonal)

### Notes from Homework (to review before class)
1. $Col(A)=\{ 0_{n} \}\implies A=0$
2. $Col(AB)\subseteq Col(A)$
3. For matrix $A\in \mathbb{R}^{nxm}$ we have $y\in Col(A)\implies y\in \{ Ax:x\in \mathbb{R}^{m} \}$
4. The leading dimension is always what the column space will be a subset of e.g. for $A\in \mathbb{R}^{nxm},B\in \mathbb{R}^{mxp}$ we have $Col(A)\subseteq \mathbb{R}^{n},Col(B)\subseteq \mathbb{R}^{m},Col(AB)\subseteq \mathbb{R}^{n}$
5. For any matrix $A\in \mathbb{R}^{nxm}$ if $Col(A)=\mathbb{R}^{n}\implies n\leq m$.
6. test_that(description, {testing code}) is unit testing function typically containing expect_equal(actual, expected) where actual is what is actually calculated and expected is what it should be
7. Roxygen creates documentation
8. Use %\*% for matrix multiplication in R
9. $A[i,]$ gives $i$th row, $A[,j]$ gives $j$th column
10. For PD/PSD proofs the following is useful: $x^{T}Ax=\sum_{i=1}^{n}\sum_{j=1}^{n}x_{i}A_{ij}x_{j}$
11. Typical strategy for PD/PSD proofs is choose an $x$ that allows for comparison to desired property. For example, showing if $A$ is PD then sum of all entries is strictly positive: $x^{T}Ax>0\implies$ choose $x=\vec{1}$ then $x^{T}Ax=\sum_{i=1}^{n}\sum_{j=1}^{n}x_{i}A_{ij}x_{j}=\sum_{i=1}^{n}\sum_{j=1}^{n}A_{ij}>0$ and thus we have shown our desired property must hold. 
12. Recall for any $A\in \mathbb{R}^{nxm}$ we have rank(A) + dim Null(A) = $m$. Thus, if $Col(A)=\mathbb{R}^{n}\implies rank(A)=n\implies dim(\mathcal{N}(A))=m-n$.
13. Important theorem: $A$ square and trivial nullspace i.e. $\mathcal{N}(A)=\{ 0 \}\implies A$ invertible.
14. **Key connection**: For any matrix $A\in \mathbb{R}^{nxm}$ $$
rank(A)=m\iff A^{T}A\text{ is PD}\iff A^{T}A\text{ invertible}\iff \mathcal{N}(A)=\{ 0 \}
$$$$
\iff\text{All eigenvalues of }A^{T}A>0
$$
15. Note that $\mathcal{N}(A^{T}A)=\mathcal{N}(A)$ for any $A\in \mathbb{R}^{nxm}$ and this immediately gives $rank(A^{T}A)=rank(A)$

8/31
## Programming Projections
$X\in \mathbb{R}^{nxp}$ with $rank(X)=p$ (full column rank)
In general we want to construct projection matrix onto column space of $X$: $$P_{X}=X(X^{T}X)^{-1}X^{T}$$
If we have an orthonormal basis for $Col(X)$, say $\alpha_{1},\dots,\alpha_{p}\in \mathbb{R}^{n}$ we can build $Q=[\alpha_{i}]_{i=1,\dots,p}$ where $\alpha_{i}$ are column vectors. Then $P_{X}=QQ^{T}$.
Suppose instead we find a different orthonormal basis $\tilde{\alpha}_{1},\dots,\tilde{\alpha}_{p}$ and $\tilde{Q}=[\tilde{\alpha}_{i}]$. Then $P_{X}=\tilde{Q}\tilde{Q}^{T}$. I.e. we get the same $P_{X}$. This works because there exists some orthogonal matrix $U$ such that $\tilde{Q}=QU$ as $Q$ and $\tilde{Q}$ are both orthonormal basis' spanning the column space of $X$. Thus, $\tilde{Q}\tilde{Q}^{T}=QUU^{T}Q^{T}=QQ^{T}$ since $U$ is orthogonal we have $UU^{T}=I$.

Verify that $P_{X}$ is a projection matrix.
1. Idempotence: $P_{X}P_{X}=QQ^{T}QQ^{T}=QI_{p}Q^{T}=P_{X}$
2. Symmetry: $P_{X}^{T}=(QQ^{T})^{T}=QQ^{T}=P_{X}$

How can we get $Q$ from $X$?
1. Gram-Schmidt
2. SVD
3. QR Decomposition (typically the one that is used computationally)

### Gram-Schmidt
Given matrix $X\in \mathbb{R}^{nxp}$ where $X=[x_{1},\dots,x_{p}]$. We start by finding $\tilde{u}_{1}=x_{1}$ and then find $u_{1}=\frac{\tilde{u}_{1}}{||\tilde{u}_{1}||_{2}}$. Note that one issue we could run into is if $||\tilde{u}_{1}||=0$, but since we are working under the assumption that $X$ has full column rank we know that there are no columns that are all 0's i.e. $||\cdot||>0$.
Moving on, we find $\tilde{u}_{2}=x_{2}-P_{u_{1}}x_{2}$ and then $u_{2}=\frac{\tilde{u}_{2}}{||\tilde{u}_{2}||}$.
Then $\tilde{u}_{3}=x_{3}-P_{u_{1}}x_{3}-P_{u_{2}}x_{3}$ and then $u_{3}=\frac{\tilde{u}_{3}}{||\tilde{u}_{3}||}$
We can continue this for all $u_{i}$ for $i=1,\dots,p$: $\tilde{u}_{k}=x_{k}-\sum_{i=1}^{k-1}P_{u_{i}}x_{k},u_{k}=\frac{\tilde{u}_{k}}{||\tilde{u}_{k}||}$
>Note: $P_{x_{1}}=P_{u_{1}}$ since projection matrices don't care about scale, just the space onto which they are being projected. But $P_{x_{2}}=P_{u_{2}}$ only if $x_{1}$ is orthogonal to $x_{2}$ since this makes $P_{x_{1}}x_{2}=0\implies \tilde{u}_{2}=x_{2}$.

*Interlude*: Order of Operators
$P_{u_{j}}x_{k}=u_{j}u_{j}^{T}x_{k}$
In R it would compute this as $u_{j}$ %\*% t($u_{j}$) %\*% $x_{k}$ from left to right which would give us a $nxn$ matrix first then multiply by $x_{k}$ to get our final $nx1$ vector. Computationally, this is much worse than doing $t(u_{j})$ %\*% $x_{k}$ first which gives a scaler first which is then very easy to make the final computation. If we have large $n$ your computer may not even have space for this $nxn$ matrix.

### Singular Value Decomposition (SVD)
We have $X\in \mathbb{R}^{nxp}$ we can always find a decomposition into $X=UDV^{T}$ where $U\in \mathbb{R}^{nxn},D\in \mathbb{R}^{nxp},V\in \mathbb{R}^{pxp}$ and $UU^{T}=U^{T}U=I_{n}$, $VV^{T}=V^{T}V=I_{p}$ and $D$ is a diagonal matrix with nonnegative diagonal entries in a non-increasing order.
It can be useful to partition $U=[U_{1} | U_{2}]$ because assuming $n>p$ then $D$ will have a bunch of zeros below the $p$th row (as the diagonal hits the "wall" or end of $D$ matrix). So it doesn't matter what we pick for $u_{2}$. Thus giving $X=U_{1}D_{1}V^{T}$ which are referred to as the left singular vectors, diag($D_{1}$) are singular values, and the right singular vectors respectively. We can follow similar logic to partition $V$ if $p>n$. See picture on phone for visualization.
So if we take $X=U_{1}D_{1}V^{T}$ we can consider when does $Col(X)=Col(U_{1})$? $Col(X)=Col(U_{1})$ always given $rank(X)=p$.
If you have the SVD of $X$ then we know that $X^{T}X=VD_{1}^{T}U_{1}^{T}U_{1}D_{1}V^{T}=VD_{1}^{2}V^{T}$. Note that there is a very fast way to invert this matrix: $(X^{T}X)^{-1}=V(D_{1}^{2})^{-1}V^{T}$. I.e. if you've already gone through the effort of finding the SVD, getting the inverse of $X^{T}X$ is easy.

### QR Decomposition
$X=QR$ where $X\in \mathbb{R}^{nxp},Q\in \mathbb{R}^{nxn},R\in \mathbb{R}^{nxp}$ and $Q$ is orthogonal, $R$ is upper triangular. Note that this $Q$ is a little too big for the $Q$ we are looking for ($P_{X}=QQ^{T}$).
We can break up $Q=[Q_{1}|Q_{2}]$ and $R^{T}=[R_{1}|0_{n-p,p}]$. Thus, $X=Q_{1}R_{1}+Q_{2}0_{n-p,p}=Q_{1}R_{1}$ which is sometimes called the thin/skinny/economy QR decomposition.
Suppose we have this decomposition. Then finding $\hat{\beta}=(X^{T}X)^{-1}X^{T}y=(R_{1}^{T}Q_{1}^{T}Q_{1}R_{1})^{-1}R_{1}^{T}Q_{1}^{T}y=(R_{1}^{T}R_{1})^{-1}R_{1}^{T}Q_{1}^{T}y$. Note that (we will go over next time) $R_{1}^{T}R_{1}$ is invertible and has a very easily computable inverse. Thus continuing the above we have $\hat{\beta}=R_{1}^{-1}R_{1}^{-T}R_{1}^{T}Q_{1}^{T}y=R_{1}^{-1}Q_{1}^{T}y$. This allows us to have the system $R_{1}\hat{\beta}=Q_{1}^{T}y$ which makes a triangular system of equations which is easy to back substitute and solve quickly.


9/2
R Notes:
- You can access public functions through package::function()
- You can access private functions through package:::function()

**QR Decomposition continued**
Consider matrix $X\in \mathbb{R}^{nxp}$ and assume $n>p$ and $rank(X)=p$.
	There always exists a decomposition $X=QR$ where $Q\in \mathbb{R}^{nxn}$ is orthogonal and $R\in \mathbb{R}^{nxp}$ is right triangular.
We will first decompose $Q$ and $R$ into block matrices $Q=[Q_{1}|Q_{2}]$ and $R^{T}=[R_{1}^{T}|0_{n-p,p}]$ (just decomposing vertically into block matrices). Thus, $X=QR=Q_{1}R_{1}$ which is called the thin/skinny/economy QR decomposition. Note $R_{1}\in \mathbb{R}^{pxp}$ and $Q_{1}\in \mathbb{R}^{nxp}$.
Then we have $Q_{1}^{T}Q_{1}=I_{p}$.
$X=QR\implies Q^{T}X=Q^{T}QR\implies Q^{T}X=R$.
Now we decompose $Q^{T}=H_{p}H_{p-1}\dots H_{2}H_{1}\implies H_{p}H_{p-1}\dots H_{2}H_{1}X=R$
Now we are going to learn how to "cook" the $H$'s to get a right triangular matrix $R$.
We want $H_{1}X=[H_{1}X_{1}\;\dots\;H_{1}X_{p}]$ ($X_{i}$ are columns of $X$)
Now we choose $H_{1}$ such that $H_{1}X_{1}=[*|0_{n-1}]\propto e_{1}$ and the norm of $X_{i}$ is conserved: $||X_{1}||_{2}^{2}=||H_{1}X_{1}||_{2}^{2}=X_{1}^{T}H_{1}^{T}H_{1}X_{1}=X_{1}^{T}X_{1}=||X_{1}||_{2}^{2}$. This is done by searching through the set of unitary matrices ($H$ orthogonal). Note that finding proceeding $H_{i}$'s will get progressively easier since the ambient space we are working in will get smaller as we go.
Define $\tilde{b}= \frac{x_{1}}{||x_{1}||_{2}}+e_{1}$ as the bisector between $X_{1}$ and $e_{1}$, then we have $b= \frac{\tilde{b}}{||\tilde{b}||_{2}}$ (normalized).
Then we have $H_{1}=(I-2P_{b})$. To understand why consider $H_{1}X_{1}=(I-2P_{b})X_{1}=X_{1}-2P_{b}X_{1}$. This is saying we start at $X_{1}$ then we find the projection from $X_{1}$ onto $b$ ($P_{b}X_{1}$) then subtract this projection twice from starting point $X_{1}$. Note that one subtraction will put us in the orthogonal complement of $b$, but a second subtraction lands us on $||x_{1}||e_{1}$. **Look into this for better understanding**
Indeed we now have $H_{1}$ is orthogonal since $H_{1}=(I-2P_{b})\implies H^{T}H=(I-2P_{b})^{T}(I-2P_{b})=I+4P_{b}^{2}-2P_{b}-2P_{b}=I$. (Last equality is just idempotence).
We now have that $H_{1}X=[*|0_{n-1},\;H_{1}X_{2},\;\dots,\;H_{1}X_{p}]$. I.e. the first column has the first entry nonzero and all remaining $n$-1 entries as zero. The remaining columns have $H_{1}$ acted upon the original columns of $X$. We can now take the $(n-1)x(p-1)$ submatrix of $H_{1}X$ called $\tilde{X}$ on bottom right (removing left most column and top row). Then we can do the same thing to $\tilde{X}$ to get $\tilde{H}_{2}$, to have $\tilde{H}_{2} \tilde{X}$. Then to get back to $H_{2}$ we put 1 in top left corner, all 0's in rest of first row and column then put $\tilde{H}_{2}$ in bottom right (remaining) rows/columns. I.e. just add one row and column above and before $\tilde{H}_{2}$ with all zeros except a 1 in top left.
We can now rinse and repeat this process to have $H_{2}H_{1}X$ and choose submatrix that is $(n-2)x(p-2)$ as $\tilde{X}$ and find $\tilde{H}_{3}$ then get $H_{3}$ by placing $\tilde{H}_{3}$ as bottom right submatrix of $H_{3}$ with two leading rows and columns with 1's on the diagonal. We can follow this process all the way through until we have all $H_{i}$'s.
Note the computationally efficient way to compute this is $(I-2P_{b_{i}})X_{i}=(I-2b_{i}b_{i}^{T})X_{i}$ (since we can construct a projection matrix from outer product of basis) $=X_{i}-2b_{i}(b_{i}^{T}X_{i})$ this is the key step due to parentheses because we avoid creating a $nxn$ matrix with outer product and instead get a scaler which makes calculations fast.

Suppose we want to find $\hat{\beta}=(X^{T}X)^{-1}X^{T}y=R_{1}^{-1}Q_{1}^{T}y\implies R_{1} \hat{\beta}=Q_{1}^{T}y$. We never actually construct $Q_{1}^{T}$ though. We can just apply the subtractions from householding reflectors ($H_{i}$'s) to get $Q^{T}y=[z|d]$ where $z\in \mathbb{R}^{px1}$, $d\in \mathbb{R}^{(n-p)x1}$. Thus we have $Q_{1}^{T}y=z$.


9/9
### Distributional Properties of Linear Models
Ingredients
- $y\in \mathbb{R}^{n}$ are observed responses
- $X\in \mathbb{R}^{nxp}$ is design matrix
- $\beta\in \mathbb{R}^{p}$ are regression coefficients
- $\epsilon\in \mathbb{R}^{n}$ are errors
- $y=X\beta+\epsilon$ is our model
Note that $y,X$ are typically observed, $\beta$ is fixed but unknown and $\epsilon$ is also unobserved.
Since we consider $X$ fixed (will flag later when we deviate from fixed $X$), the randomness enters through $\epsilon$.

Two Typical Assumption Regimes
1. Assume $\mathbb{E}\epsilon_{i}=0,\;\forall i$ and $\mathrm{Cov}(\epsilon_{i},\epsilon_{j})=\sigma^{2}\delta_{ij}$ where $\delta_{ij}=1$ if $i=j$ and $0$ o.w.
2. Assume $\epsilon \sim N_{n}(0_{n},\sigma^{2}I_{n})$ (multivariate normal). Equivalently, $\epsilon_{i}\overset{\text{iid}}{\sim}N(0,\sigma^{2})$.
>Note that $2\implies1$,but not the converse.

#### Quick Refresher on Expectations and Covariances
Let $U\in \mathbb{R}^{q},V\in \mathbb{R}^{q},W\in \mathbb{R}^{d}$ be random vectors on a common probability space.
Let $a,b\in \mathbb{R}$ be fixed scalars.
Let $t\in \mathbb{R}^{q}$ be a fixed vector.
Let $A\in \mathbb{R}^{mxq}$ be a fixed matrix.

**Expectation is linear**: $\mathbb{E}[aU+bV+t]=a\mathbb{E}U+b\mathbb{E}V+t$ and $\mathbb{E}[t^{T}U]=t^{T}\mathbb{E}[U]=\sum_{i=1}^{q}t_{i}\mathbb{E}U_{i}$. It is linearly, however, in general $\mathbb{E}[U^{T}V]\neq \mathbb{E}[U]^{T}\mathbb{E}[V]$. Think of linearity as working because we are mixing one fixed thing and one random thing, but once we start mixing multiple random things we tend to lose this and need to consider covariance and variance.

**Covariance of random vectors**
$\mathrm{Cov}(U,W)=\mathbb{E}[(U-\mathbb{E}U)(W-\mathbb{E}W)^{T}] =\mathbb{E}[UW^{T}-U\mathbb{E}[W]^{T}-\mathbb{E}[U]W^{T}+\mathbb{E}[U]\mathbb{E}[W]^{T}]$
$=\mathbb{E}[UW^{T}]-\mathbb{E}[U\mathbb{E}[W]^{T}]-\mathbb{E}[\mathbb{E}[U]W^{T}]+\mathbb{E}[\mathbb{E}[U]\mathbb{E}[W]^{T}]$
$=\mathbb{E}[UW^{T}]-\mathbb{E}[U]\mathbb{E}[W]^{T}-\mathbb{E}[U]\mathbb{E}[W]^{T}+\mathbb{E}[U]\mathbb{E}[W]^{T}$
$=\mathbb{E}[UW^{T}]-\mathbb{E}[U]\mathbb{E}[W]^{T}$
This will be a $qxd$ matrix.

Sometimes with just a single vector we may examine $\mathrm{Cov}(U)=\mathrm{Var}(U)=\mathrm{Cov}(U,U)=\mathbb{E}[UU^{T}]-\mathbb{E}[U]\mathbb{E}[U^{T}]$.

Compare this with the scalar definition: Suppose $Z$ is random variable. Then $\mathrm{Var}(Z)=\mathbb{E}Z^{2}-(\mathbb{E}Z)^{2}=\mathbb{E}[ZZ^{T}]-\mathbb{E}Z\mathbb{E}Z^{T}$ where we just treat $Z$ as a 1x1 vector.

**Expectation with fixed matrix**
$\mathbb{E}[AU]=A\mathbb{E}[U]$ (by linearity)

**Variance with fixed matrix**
$\mathrm{Var}(AU)=A\mathrm{Var}(U)A^{T}$
Proof: $\mathrm{Cov}(AU,AU)=\mathbb{E}[AUU^{T}A^{T}]-\mathbb{E}[AU]\mathbb{E}[U^{T}A^{T}]=A\mathbb{E}[U^{T}U]A^{T}-A\mathbb{E}[U]\mathbb{E}[U^{T}]A^{T}$
$=A(\mathbb{E}[UU^{T}]-\mathbb{E}U\mathbb{E}U^{T})A^{T}=A\mathrm{Var}(U)A^{T}$.
$\mathrm{Cov}(AU,BU)=A\mathrm{Var}(U)B^{T}$

**Variance with fixed vector**
$\mathrm{Var}(U+t)=\mathrm{Var}(U)$
Proof: $\mathbb{E}[(U+t)(U+t)^{T}]-\mathbb{E}[U+t]\mathbb{E}[U+t]^{T}=\mathbb{E}[UU^{T}]+2\mathbb{E}[ut^{T}]+tt^{T}-\mathbb{E}[U]\mathbb{E}[U^{T}]-2\mathbb{E}[Ut^{T}]-tt^{T}$
$=\mathbb{E}[UU^{T}]-\mathbb{E}[U]\mathbb{E}[U^{T}]$.

#### Back to our model
$\mathbb{E}[y]=\mathbb{E}[X\beta+\epsilon]=X\beta+\mathbb{E}[\epsilon]$. Then under either regime 1 or regime 2 we have $\mathbb{E}[\epsilon]=0_{n}\implies \mathbb{E}[y]=X\beta$.
Similarly, $\mathrm{Var}(y)=\mathrm{Var}(X\beta+\epsilon)=\mathrm{Var}(\epsilon)=\sigma^{2}I_{n}$.

Now thinking about $\hat{\beta}$: Suppose that $rank(X)=p$ then $\hat{\beta}=(X^{T}X)^{-1}X^{T}y$ so we have $$
\mathbb{E}[\hat{\beta}]=(X^{T}X)^{-1}X^{T}X\beta=\beta
$$from fact that $\mathbb{E}[y]=X\beta$ above.
Now we have $$
\mathrm{Var}(\hat{\beta})=(X^{T}X)^{-1}X^{T}\mathrm{Var}(y)((X^{T}X)^{-1}X^{T})^{T}=(X^{T}X)^{-1}X^{T}\sigma^{2}I_{n}X(X^{T}X)^{-1}=\sigma^{2}(X^{T}X)^{-1}
$$
In inference we may be interested in finding $\mathbb{E}[\hat{\beta_{1}}-\hat{\beta_{2}}]=\beta_{1}-\beta_{2}$ and $\mathrm{Var}(\hat{\beta_{1}}-\hat{\beta_{2}})$ as well.
Note expectation is easy, variance is a little more messy and recall that it is $$
\mathrm{Var}(\hat{\beta}_{1}-\hat{\beta}_{2})=\mathrm{Var}(\hat{\beta_{1}})+\mathrm{Var}(\hat{\beta}_{2})-2\mathrm{Cov}(\hat{\beta}_{1},\hat{\beta}_{2})
$$, but we can find it by noting that  $$
\hat{\beta}_{1}-\hat{\beta}_{2}=e_{1}^{T}\hat{\beta}-e_{2}^{T}\hat{\beta}=(e_{1}^{T}-e_{2}^{T})\hat{\beta}
$$Let $\gamma \in \mathbb{R}^{p}$ be fixed. Then $\mathrm{Var}(\gamma^{T}\hat{\beta})=\gamma^{T}\mathrm{Var}(\hat{\beta})\gamma=\sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma$. Now suppose that $\gamma=e_{1}-e_{2}$. Look at picture on phone to see factored out version of how this ends up getting you to final result. The methodology is important as it can apply more generally to find something more arbitrary like $\mathrm{Var}(3\hat{\beta}_{1}-4\hat{\beta}_{2}+5\hat{\beta}_{3})$.
This idea of setting a $\gamma$ as the combination of two elementary vectors can be very helpful for doing inference between different groups (e.g. group 1 and group 2). This can let you examine sort of "arbitrary inferential targets." **Look into more**

#### Interpretation of Coefficients
For model $y=X\beta+\epsilon$ suppose each column of $X$ corresponds to a distinct covariate (aka predictor). What is the interpretation of $\beta_{j}$ in terms of expectations?
$e_{i}^{T}y=e_{i}^{T}(X\beta+\epsilon)=\sum_{j=1}^{p}X_{ij}\beta_{j}+\epsilon_{i}$. Consider $\tilde{X}=X+e_{i}e_{j}^{T}$ (perturbing $X$ in ith row and jth column by 1). Then $\mathbb{E}[e_{i}^{T}y(\tilde{X})]-\mathbb{E}[e_{i}^{T}y(X)]=\beta_{j}$. I.e. one unit shift in covariate will result in change of $\beta_{j}$ units on the expectation of our model/output $y$.

Example:
Consider an experiment investigating the effect of two drugs and placebo on blood pressure.
How can we express this as a linear model?
Suppose first 30 are placebo, next 30 are treatment A, last 30 are treatment $B$.
We could choose to parameterize our design matrix $X=[1_{30}|0_{60},0_{30}|1_{30}|0_{30},0_{60}|1_{30}]$ where each "," separates the columns of $X$. Note that if we add an intercept to $X$ then $X$ would no longer be full rank so we would not want to add an intercept.

9/14
Missed first 10 minutes of lecture. Looking at example above $y\in \mathbb{R}^{90}$.
How do we estimate the effect of treatment A relative to placebo?
We do $[-1\;1\;0]\hat{\beta}=\hat{\beta}_{2}-\hat{\beta}_{1}$ since first column is 30 placebo patients and second 30 is treatment A patients, thus giving us the effect of A relative to placebo.
Notice that $X^{T}X=Diag(30)$ thus $(X^{T}X)^{-1}=\frac{1}{30}I$. Thus, $\hat{\beta}=(X^{T}X)^{-1}X^{T}y=\frac{1}{30}X^{T}y=$ vector with each entry being sum of 30 entries divided by 30 i.e. $\hat{\beta}_{i}= \frac{1}{30}\sum_{k=(i-1)*30+1}^{30i}y_{k}$.
Now examining this reformulated with $\tilde{X}$ as having an intercept in first column and placebo in second column (first 30 rows are 1's), and third column is treatment $B$ (last 30 rows are 1's in third column). We notice that the intercept captures the effect of treatment A as a baseline. Now answering the same question as above notice that $\mathbb{E}[y(T_{\tilde{X}}A)]-\mathbb{E}[y(T_{\tilde{X}}P)]=[1\;0\;0]-[1\;1\;0]=[0\;-1\;0]$ where we are subtracting the effect of treatment A on placebo and arrive at the vector $[0\;-1\;0]\hat{\beta}$ to answer our question of the effect of treatment A relative to placebo.

Example 2: Instead of drugs, each participant in our study will undergo an intervention where they engage in moderate exercise for $M_{i}$ minutes per day, where $M_{i}\overset{\text{iid}}{\sim}U(0,120)$. We want to estimate how blood pressure changes per minute of daily exercise.
$X\in \mathbb{R}^{90x2}$ where $X=[1_{90}\;M_{i}'s]$ so to answer our question of how blood pressure changes we get $[0\;1]\hat{\beta}=\hat{\beta}_{2}$.

We now also want to control for BMI, which we believe has a quadratic effect on blood pressure. Let $W_{i}$ be the BMI of the $i$th participant.
We now have the same $X$ as above except with two new columns $W_{i}$ and $W_{i}^{2}$ running down the columns. Note that having the additional $W_{i}$ column is important for making the model more flexible than just adding the quadratic term. So once again to get the effect of exercise on blood pressure we just use vector $[0\;1\;0\;0]$.

Now forget about BMI. But suppose we think minutes of exercise has diminishing returns e.g. going from 2 to 3 minutes has a bigger impact than 118 to 119. Now our original question isn't very well posed since we believe that each minute doesn't have the same effect. Now we are more generally trying to model how blood pressure varies in terms of minutes of exercise (as more of a curve than a direct linear effect). We can have a design matrix now with columns being $\log(M_{i})$ or $\sqrt{ M_{i} }$ and can choose to include the linear term $M_{i}$ if we want as it just adds more flexibility. Additionally, we can adjust to $\log(1+M_{i})$ if we want as it makes the intercept not have to do as much work.

## Inference
So far, we have covered the following topics for linear models:
- Estimation (i.e. finding $\hat{\beta}$)
- Interpretation (i.e. what does $\beta$ signify)
- Articulation (i.e. words $\to$ design matrix)

So what's missing?
- Uncertainty quantification: We will always get a $\hat{\beta}$ what does it actually tell us about $\beta$?
- Model Misspecification: Is our model even correct? Most of the time probably not, but is it close enough to be useful and what does it mean to do valid inference for the wrong model?

### Inference for Scalar Targets
Recall $y=X\beta+\epsilon$ where $y,X$ both observed, $\beta$ unknown, $\epsilon$ not directly observed
Suppose $\epsilon \sim N_{n}(0_{n},\sigma^{2}I_{n})$.
$\hat{\beta}=(X^{T}X)^{-1}X^{T}y$ and since we have the above distribution for $\epsilon$ we know that $\hat{\beta}\sim N_{p}(\beta,\sigma^{2}(X^{T}X)^{-1})$.
Let $\gamma\in \mathbb{R}^{p}$ be fixed, but arbitrary.
Goal: Inference for $\gamma^{T}\beta$

#### Inference via Confidence Intervals
**(Informal) Definition (Confidence set):** Let $w\sim P_{\theta}$ for some $\theta\in\Theta$. A random subset $c(w)$ of the parameter space $\Theta$ is called $(1-\alpha)$ confidence set (or $100(1-\alpha)$%) if $\forall\theta\in\Theta,\;\mathbb{P}_{w\sim\theta}(\{ \theta\in c(w) \})=1-\alpha$ (probability that $\theta$ is in the confidence set when $w$ follows distribution under $\theta$ as true parameter).
>Note: If $\Theta$ is an ordered set and $c(w)$ can almost surely be written as an interval, then $c$ can be called a confidence interval.

#### Inference via Testing
Consider a null hypothesis of the form $H_{0}:\theta=\theta_{0}$. A function $$\delta_{\alpha}(w)=\begin{cases}
1 & \text{if reject }H_{0} \\
0 & o.w.
\end{cases}$$is a size $\alpha$ test if $\mathbb{E}_{H_{0}:w\sim P_{\theta_{0}}}[\delta_{\alpha}(w)]=\alpha$ or a level $\alpha$ test if $\mathbb{E}_{H_{0}:w\sim P_{\theta_{0}}}[\delta_{\alpha}(w)]\leq\alpha$.

#### Confidence Interval for $\gamma^{T}\beta$
Approach: Find a pivot, (a function of the data and some unknown parameters with a fixed distribution free from the parameters we are working with).
For now, assume $\sigma^{2}$ is known and $\beta$ is unknown. Consider $Z=\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}\sim N(0,1)$.
Let $\Phi$ be the CDF of a standard normal, $\Phi^{-1}$ its quantile function.
Note that $Z$ is a function of $y$ since $Z$ is a function of $\hat{\beta}$ which is a function of $y$.
Thus, define the event $c(y):=\left\{  \Phi^{-1}\left( \frac{\alpha}{2} \right)\leq Z\leq\Phi^{-1}\left( 1-\frac{\alpha}{2} \right)  \right\}$ then $\mathbb{P}(c(y))=1-\alpha$.
Plugging in our definition of $Z$ above we get $$
\Phi^{-1}\left( \frac{\alpha}{2} \right)\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }-\gamma^{T}\hat{\beta}\leq-\gamma^{T}\beta\leq\Phi^{-1}\left( 1-\frac{\alpha}{2} \right)\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }-\gamma^{T}\hat{\beta}
$$
## Homework 2 Takeaways

### Constraints on Fitted Values and Residuals
Setup: $X\in \mathbb{R}^{n\times p}$ with $rank(X)=p$, $1\leq p<n$, $\gamma\in \mathbb{R}^{n}$ fixed and nonzero, $\hat{y}=P_{X}y$, $\hat{\epsilon}=P_{X}^{\perp}y$.

**Lemma:** $v^{T}y=0\;\forall y\in \mathbb{R}^{n}\iff v=0_{n}$ (take $y=e_{i}$ for each $i$). Since projection matrices are symmetric, $\gamma^{T}P_{X}y=(P_{X}\gamma)^{T}y$, so a condition "for every $y$" reduces to a condition on $P_{X}\gamma$ or $P_{X}^{\perp}\gamma$.

**Fitted values:**
$$
\gamma^{T}\hat{y}=0\;\;\forall y\iff X^{T}\gamma=0_{p}\iff \gamma\in Col(X)^{\perp}
$$
- $(\Rightarrow)$ The lemma gives $P_{X}\gamma=0_{n}$. Multiply on the left by $X^{T}$: $X^{T}X(X^{T}X)^{-1}X^{T}\gamma=X^{T}\gamma=0_{p}$.
- $(\Leftarrow)$ $X^{T}\gamma=0_{p}\implies P_{X}\gamma=X(X^{T}X)^{-1}X^{T}\gamma=0_{n}\implies \gamma^{T}\hat{y}=(P_{X}\gamma)^{T}y=0$.
- **Recipe:** Choose $k$ with $\gamma_{k}\neq 0$. Since $p\leq n-1$, choose distinct indices $j_{1},\dots,j_{p}\neq k$ and set
$$
x_{i}=\gamma_{k}e_{j_{i}}-\gamma_{j_{i}}e_{k},\qquad X=\begin{bmatrix} x_{1} & \cdots & x_{p}\end{bmatrix}
$$
  Check: $\gamma^{T}x_{i}=\gamma_{k}\gamma_{j_{i}}-\gamma_{j_{i}}\gamma_{k}=0$, and coordinate $j_{i}$ is nonzero only in $x_{i}$, so $rank(X)=p$.

**Residuals:**
$$
\gamma^{T}\hat{\epsilon}=0\;\;\forall y\iff \gamma\in Col(X)
$$
- $(\Rightarrow)$ The lemma gives $P_{X}^{\perp}\gamma=0_{n}$. **Decomposition trick:**
$$
\gamma=P_{X}\gamma+P_{X}^{\perp}\gamma=P_{X}\gamma\in Col(P_{X})=Col(X)
$$
- $(\Leftarrow)$ If $\gamma=Xa$, then $P_{X}^{\perp}\gamma=(I_{n}-P_{X})Xa=Xa-Xa=0_{n}$.
- **Recipe:** Choose $k$ with $\gamma_{k}\neq 0$ and distinct indices $j_{1},\dots,j_{p-1}\neq k$. Set
$$
X=\begin{bmatrix} \gamma & e_{j_{1}} & \cdots & e_{j_{p-1}}\end{bmatrix}
$$
  Check: coordinate $k$ is nonzero only in $\gamma$, so the columns are independent and $rank(X)=p$. The constraint holds because $\gamma$ is a column.

>Note: The fitted-value case forces all $p$ columns to be orthogonal to $\gamma$, which needs $p\leq n-1$. The residual case forces only one direction into $Col(X)$.

### QR: $\hat{\beta}$, $\|\hat{y}\|_{2}^{2}$, and RSS
Full QR: $X=QR$, $Q=[Q_{1}|Q_{2}]$ with $Q_{1}\in \mathbb{R}^{n\times p}$, $Q_{2}\in \mathbb{R}^{n\times(n-p)}$. Split after the first $p$ entries:
$$
Q^{T}y=\begin{bmatrix} z \\ d \end{bmatrix},\qquad z=Q_{1}^{T}y\in \mathbb{R}^{p},\quad d=Q_{2}^{T}y\in \mathbb{R}^{n-p}
$$
**Coefficients** (solve by back substitution):
$$
R_{1}\hat{\beta}=Q_{1}^{T}y=z
$$
**Projections:**
$$
P_{X}=Q\begin{bmatrix} I_{p} & 0_{p\times(n-p)} \\ 0_{(n-p)\times p} & 0_{(n-p)\times(n-p)} \end{bmatrix}Q^{T}=Q_{1}Q_{1}^{T}
$$
$$
P_{X}^{\perp}=I_{n}-P_{X}=Q\begin{bmatrix} 0_{p\times p} & 0_{p\times(n-p)} \\ 0_{(n-p)\times p} & I_{n-p} \end{bmatrix}Q^{T}=Q_{2}Q_{2}^{T}
$$
**Norms:** $Q$ is orthogonal, so it preserves norms: $\|Q^{T}v\|_{2}^{2}=v^{T}QQ^{T}v=v^{T}v$. Apply this to $\hat{y}=P_{X}y$ and use $Q^{T}Q=I_{n}$:
$$
\|\hat{y}\|_{2}^{2}=\|Q^{T}\hat{y}\|_{2}^{2}=\left\|\begin{bmatrix} I_{p} & 0 \\ 0 & 0 \end{bmatrix}Q^{T}y\right\|_{2}^{2}=\left\|\begin{bmatrix} z \\ 0_{n-p} \end{bmatrix}\right\|_{2}^{2}=\|z\|_{2}^{2}
$$
The same argument with $P_{X}^{\perp}$ gives $$ RSS=\|\hat{\epsilon}\|_{2}^{2}=\left\|\begin{bmatrix} 0_{p} \\ d \end{bmatrix}\right\|_{2}^{2}=\|d\|_{2}^{2} $$
Takeaway: One Householder pass (computing $Q^{T}y$ without ever forming $Q$) gives both $\hat{\beta}$ (back substitute on $z$) and the RSS (from $d$). $R_{1}$ is not needed for the RSS. Always check $p$ before splitting $Q^{T}y$.

#### Covariance
$\mathrm{\mathrm{Var}}(aX+bY+cZ)=a^{2}\mathrm{Var}(X)+b^{2}\mathrm{Var}(Y)+c^{2}\mathrm{Var}(Z)+2ab\mathrm{Cov}(X,Y)+2ac\mathrm{Cov}(X,Z)+2bc\mathrm{Cov}(Y,Z)$ which can be seen more generally as $\mathrm{Var}(a^{T}U)=a^{T}\Sigma a=\sum_{i} \sum_{j} a_{i}a_{j}\Sigma_{ij}$ where $\Sigma$ is the covariance matrix of the random variables in random vector $U$.

### Sampling Distributions in the Normal Linear Model
Setup: $y=X\beta+\epsilon$, $\epsilon \sim N_{n}(0_{n},\sigma^{2}I_{n})$, $X\in \mathbb{R}^{n\times p}$ fixed with $rank(X)=p<n$, $P=X(X^{T}X)^{-1}X^{T}$.

$$
y\sim N_{n}(X\beta,\;\sigma^{2}I_{n})
$$
$$
\hat{\beta}\sim N_{p}(\beta,\;\sigma^{2}(X^{T}X)^{-1})
$$
$$
\hat{y}\sim N_{n}(X\beta,\;\sigma^{2}P)
$$
$$
\hat{\epsilon}\sim N_{n}(0_{n},\;\sigma^{2}(I_{n}-P))
$$
All four are fixed linear maps of $y$, so normality transfers; means use $\mathbb{E}[Ay]=A\mathbb{E}[y]$ and covariances use $\mathrm{Var}(Ay)=A\mathrm{Var}(y)A^{T}$ (9/9), together with $PX=X$ and the symmetry/idempotence of $P$ and $I_{n}-P$.

### Covariance Rank and Support
**Principle:** For a random vector $V$ with mean $\mu$ and covariance $\Sigma$,
$$
\mathbb{P}(V-\mu\in Col(\Sigma))=1
$$
and $Col(\Sigma)$ is the smallest such subspace, so $rank(\Sigma)$ is the number of directions in which $V$ genuinely varies.
- Why: $\gamma\in \mathcal{N}(\Sigma)\implies \mathrm{Var}(\gamma^{T}V)=\gamma^{T}\Sigma\gamma=0\implies \gamma^{T}V=\gamma^{T}\mu$ a.s. Since $\Sigma$ is symmetric, $\mathcal{N}(\Sigma)=Col(\Sigma)^{\perp}$, so ranging over a basis of $\mathcal{N}(\Sigma)$ gives $V-\mu\in Col(\Sigma)$.
- $\Sigma$ invertible $\iff$ no constrained directions $\iff$ a density exists on the full ambient space.

| Vector | $rank$ | Invertible? | Lives in |
|---|---|---|---|
| $y$ | $n$ | Yes | $\mathbb{R}^{n}$ |
| $\hat{\beta}$ | $p$ | Yes | $\mathbb{R}^{p}$ |
| $\hat{y}$ | $p$ | No | $Col(X)$ |
| $\hat{\epsilon}$ | $n-p$ | No | $Col(X)^{\perp}$ |

>Ties back to Problem 1: $\mathrm{Var}(\gamma^{T}\hat{y})=\sigma^{2}\|P\gamma\|_{2}^{2}$ and $\mathrm{Var}(\gamma^{T}\hat{\epsilon})=\sigma^{2}\|P^{\perp}\gamma\|_{2}^{2}$, so these vanish exactly for $\gamma\in Col(X)^{\perp}$ and $\gamma\in Col(X)$ respectively. Problem 1 gives the directions that are zero identically in $y$; here they are the directions that are zero with probability 1.

### Orthogonality and Independence
Covariance of two linear maps of the same vector (note which matrix gets transposed):
$$
\mathrm{Cov}(Ay,By)=A\,\mathrm{Var}(y)\,B^{T},\qquad \mathrm{Cov}(By,Ay)=\left(A\,\mathrm{Var}(y)\,B^{T}\right)^{T}
$$
$$
\mathrm{Cov}(\hat{y},\hat{\epsilon})=\sigma^{2}P(I_{n}-P)^{T}=\sigma^{2}(P-P^{2})=0_{n\times n}
$$
$$
\mathrm{Cov}(\hat{\beta},\hat{\epsilon})=\sigma^{2}(X^{T}X)^{-1}X^{T}(I_{n}-P)=0_{p\times n}\quad \text{since } X^{T}(I_{n}-P)=0_{p\times n}
$$
**Zero covariance alone gives only uncorrelatedness.** Independence needs the pair to be *jointly* normal, which is stronger than each being marginally normal. Verify it by stacking the maps:
$$
\begin{bmatrix} \hat{y} \\ \hat{\epsilon} \end{bmatrix}=\begin{bmatrix} P \\ I_{n}-P \end{bmatrix}y=Cy\implies Cy\sim N_{2n}\left(\begin{bmatrix} X\beta \\ 0_{n} \end{bmatrix},\;\sigma^{2}\begin{bmatrix} P & 0 \\ 0 & I_{n}-P \end{bmatrix}\right)
$$
Zero off-diagonal blocks plus joint normality gives $\hat{y}\perp\!\!\!\perp\hat{\epsilon}$; the same stacking with $C=\begin{bmatrix} (X^{T}X)^{-1}X^{T} \\ I_{n}-P \end{bmatrix}$ gives $\hat{\beta}\perp\!\!\!\perp\hat{\epsilon}$.

>Write-up template: (1) cross-covariance is $0$, (2) the *pair* is jointly normal as a single fixed linear map of $y$, (3) cite the fact. Step (2) is the one that is usually skipped.

### Dropping Normality
If only $\mathbb{E}[\epsilon]=0_{n}$ and $\mathrm{Var}(\epsilon)=\sigma^{2}I_{n}$ hold:
- **Survives:** all means and covariances, since the 9/9 rules are distribution-free; all ranks and support statements; $\mathrm{Cov}(\hat{y},\hat{\epsilon})=0$ and $\mathrm{Cov}(\hat{\beta},\hat{\epsilon})=0$, i.e. uncorrelatedness.
- **Does not follow:** the $N$ (normal) labels themselves (only the first two moments are known), and the independence conclusions, since joint normality was the hypothesis.
- Consequence: exact pivots and confidence intervals (9/14) are lost; you fall back on CLT approximations.

>General rule: anything derived from $\mathbb{E}[\epsilon]$ and $\mathrm{Var}(\epsilon)$ survives; anything needing the full distribution of $\epsilon$ does not.

### Collinearity and the Geometry of $\mathrm{Var}(\hat{\beta})$
Setup: two designs with the same $\beta$, $\sigma$, and $n$, built from orthonormal $u,v\in \mathbb{R}^{n}$ with $s^{2}=1-\rho^{2}$:
$$
X_{orth}=\begin{bmatrix} u & v \end{bmatrix},\qquad X_{col}=\begin{bmatrix} \dfrac{u}{s} & \dfrac{\rho u}{s}+v \end{bmatrix}
$$
The columns of $X_{col}$ have equal norms $1/s$ and cosine angle exactly $\rho$, so $\rho$ is the correlation between the columns.

**Core tool** (9/9): $\mathrm{Var}(\hat{\beta})=\sigma^{2}(X^{T}X)^{-1}$, and for fixed $\gamma$,
$$
\mathrm{Var}(\gamma^{T}\hat{\beta})=\gamma^{T}\mathrm{Var}(\hat{\beta})\gamma=\sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma
$$
The two Gram matrices and their inverses ($\sigma^{2}=1$):
$$
X_{orth}^{T}X_{orth}=I_{2}\implies \mathrm{Var}(\hat{\beta})=I_{2}
$$
$$
X_{col}^{T}X_{col}=\frac{1}{s^{2}}\begin{bmatrix} 1 & \rho \\ \rho & 1 \end{bmatrix}\implies \mathrm{Var}(\hat{\beta})=\begin{bmatrix} 1 & -\rho \\ -\rho & 1 \end{bmatrix}
$$
>The $1/s$ scaling is chosen so $s^{2}=1-\rho^{2}$ cancels in the inverse. This makes the *marginal* variances identical across designs; the designs differ only in the off-diagonal.

**Takeaway 1: collinearity does not destroy precision, it redistributes it.** Individual variances are $1$ in both designs, but the joint structure differs entirely. With $\gamma=(1,1)^{T}$ and $\gamma=(1,-1)^{T}$ in the collinear design:
$$
\mathrm{Var}(\hat{\beta}_{1}+\hat{\beta}_{2})=2(1-\rho),\qquad \mathrm{Var}(\hat{\beta}_{1}-\hat{\beta}_{2})=2(1+\rho)
$$
At $\rho=0.9$ these are $0.2$ and $3.8$, versus $2$ for both under orthogonality. Some directions become far better determined, others far worse. There is no single scalar summary of "how bad" collinearity is; precision is a property of the direction $\gamma$, not of the design alone.

**Takeaway 2: marginal distributions can hide everything.** Histograms of $\hat{\beta}_{1}$ and $\hat{\beta}_{2}$ alone are indistinguishable between the two designs here. Only the scatterplot (or the covariance matrix) reveals the difference. Always inspect the joint object $\mathrm{Var}(\hat{\beta})$, not just its diagonal.

**Takeaway 3: the sign of the covariance drives the sum.** From Problem 4(a) with $a=(1,1)^{T}$:
$$
\mathrm{Var}(\hat{\beta}_{1}+\hat{\beta}_{2})=\mathrm{Var}(\hat{\beta}_{1})+\mathrm{Var}(\hat{\beta}_{2})+2\mathrm{Cov}(\hat{\beta}_{1},\hat{\beta}_{2})
$$
Positively correlated columns give $\mathrm{Cor}(\hat{\beta}_{1},\hat{\beta}_{2})=-\rho<0$, so the cross term *subtracts*. Correlation alone is not enough to shrink the sum; the negative sign is what causes the cancellation.

**Takeaway 4: the geometric picture.** Nearly parallel columns mean the data cannot attribute the fit to one column versus the other: overshooting on $\hat{\beta}_{1}$ is compensated by undershooting on $\hat{\beta}_{2}$, yielding nearly the same $\hat{y}$. The sampling cloud is a narrow ridge whose long axis is $(1,-1)$ (the ill-determined direction) and whose short axis is $(1,1)$ (the well-determined one). Movement along the ridge barely changes the sum.
$$
\text{ill-determined direction}=\text{eigenvector of }\mathrm{Var}(\hat{\beta})\text{ with the largest eigenvalue}
$$
Here the eigenvectors are $(1,-1)/\sqrt{2}$ and $(1,1)/\sqrt{2}$ with eigenvalues $1+\rho$ and $1-\rho$.

**Takeaway 5: unbiasedness is untouched.** Both designs are full rank, so $\mathbb{E}[\hat{\beta}]=\beta$ regardless of collinearity. Both clouds center at the true $\beta$. Collinearity is a variance phenomenon, not a bias one. Relatedly, $P_{X}$ and hence $\hat{y}$ depend only on $Col(X)$, which is identical for both designs — what collinearity destabilizes is the *decomposition* of a well-determined $\hat{y}$ into per-column contributions.

9/16
## Inference Continued
$$
Z=\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}\sim N(0,1)
$$
Define event $$
C(y)=\left\{  \Phi^{-1}\left( \frac{\alpha}{2} \right)\leq Z\leq\Phi^{-1}\left( 1-\frac{\alpha}{2} \right)  \right\}
$$
$\mathbb{P}(C(y))=1-\alpha$
We are thinking about $y$ as random vector.
We are thinking about repeatedly realizing $\epsilon$'s and running this experiment over and over again. Because $Z$'s randomness comes through $\hat{\beta}$ whose randomness comes through $y$ whose randomness comes through $\epsilon$.
We will shorthand $N_{\frac{\alpha}{2}}:=\Phi^{-1}\left( \frac{\alpha}{2} \right)=-N_{1-\frac{\alpha}{2}}$
We can now rewrite $C(y)=\left\{  N_{\frac{\alpha}{2}}\leq Z\leq-N_{\frac{\alpha}{2}}  \right\}=\left\{  -N_{\frac{\alpha}{2}}\geq-Z  \geq N_{\frac{\alpha}{2}}\right\}=\left\{  -N_{\frac{\alpha}{2}}\geq \frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}\geq N_{\frac{\alpha}{2}} \right\}$
$=\left\{  -N_{\frac{\alpha}{2}}\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }+\gamma^{T}\hat{\beta}\geq\gamma^{T}\beta\geq N_{\frac{\alpha}{2}}\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }+\gamma^{T}\hat{\beta}  \right\}=1-\alpha$
We can rewrite this compactly as $\mathbb{P}(\{\gamma^{T}\beta\in\{\gamma^{T}\hat{\beta}\pm N_{\frac{\alpha}{2}}\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }\}\})=1-\alpha$
So we now have a confidence interval as the set $CI(y)=\{\gamma^{T}\hat{\beta}\pm N_{\frac{\alpha}{2}}\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }\}$

##### Testing
$H_{0}:\gamma^{T}\beta=b$
Construct $Z(b)=\frac{\gamma^{T}\hat{\beta}-b}{\sqrt{ \sigma^{2} \gamma^{T}(X^{T}X)^{-1}\gamma}}$
Under $H_{0}$ we have $\gamma^{T}\beta=b$ which gives us the same original statement as above by plugging in $b$.
Thus, $Z(b)\sim N(0,1)$.
$\mathbb{E}_{H_{0}}[\delta_{\alpha}(y)]=\alpha$ (probability of rejection is $\alpha$, thus arriving at size $\alpha$ test).

#### Inference with Unknown Variance
In $Z$ above the only thing we really don't know is $\sigma^{2}$ (unless given/known), so what do we do if we don't have it?
Estimate it!

**Primitives**
Suppose $W_{i}\overset{\text{iid}}{\sim}N(0,1)$ for $i=1,\dots,d$ then $\sum_{i=1}^{d}W_{i}^{2}\sim \chi^{2}_{d}$
Let $Z\sim N(0,1)$ and $V\sim \chi_{d}^{2}$ with $Z$ independent of $V$. Then $\frac{Z}{\sqrt{ \frac{V}{d} }}\sim t_{d}$ (t distribution with $d$ d.o.f.).

Now back to estimation of variance:
$$s^{2}=\frac{\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}}{(n-p)}$$
Note that we have $n-p$ because we have $p$ parameters/covariates.
Claim: $$\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{s\sqrt{\gamma^{T}(X^{T}X)^{-1}\gamma }}\sim t_{n-p}$$
We will do the following steps to prove it
1. Rewrite as $\frac{Z}{\sqrt{ \frac{V}{d} }}$
2. Show $Z\sim N(0,1)$
3. Show $V\sim \chi_{d}^{2}$ (arguably hardest)
4. Show $Z\perp\!\!\!\perp V$ (need to be careful here as obvious way won't work)

**Step 1** (Rewriting):
$\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{s\sqrt{ \gamma^{T}(X^{T}X)^{-1}\gamma }} \frac{\sigma}{\sigma}$ then we have the same $Z$ as before thus we can factor this into $\frac{Z\sigma}{s}$
Now examining $s$, recall we have $s^{2}=\frac{\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}}{(n-p)}$ so $\frac{\sigma}{s}=\frac{\sigma}{\sqrt{ \frac{\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}}{(n-p)} }}$. From here we take $n-p=d$ and $\frac{\sigma^{2}}{\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}}=\frac{1}{V}$
Now checking $$\frac{Z}{\sqrt{ \frac{V}{d} }}=\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }} \frac{1}{\sqrt{ \frac{\frac{1}{\sigma^{2}}\sum(\hat{y}_{i}-y_{i})^{2}}{n-p} }}$$
Note that $\frac{1}{\sigma}\sum(\hat{y}_{i}-y_{i})^{2}=\frac{1}{\sigma}||\hat{\epsilon}||_{2}^{2}$. Recall $\hat{\epsilon}=(I-P_{X})y=P_{X}^{\perp}y=Q_{2}Q_{2}^{T}y$ (from QR decomposition as $Q_{2}$ gives us a basis for orthogonal complement of $X$).
So $\frac{1}{\sigma}||\hat{\epsilon}||_{2}^{2}=\frac{1}{\sigma}||Q_{2}Q_{2}^{T}y||_{2}^{2}$. Note that $\hat{\epsilon}\sim N(Q_{2}Q_{2}^{T}X\beta,\sigma^{2}Q_{2}Q_{2}^{T}Q_{2}^{T}Q_{2})$


9/23
Recall again that $y=X\beta+\epsilon,X\in \mathbb{R}^{nxp},rank(X)=p,\epsilon \sim N_{n}(0_{n},\sigma^{2}I_{n})$.
We want to show that for any $\gamma\in \mathbb{R}^{p}$ that $\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{s\sqrt{ \gamma^{T}(X^{T}X)^{-1}\gamma }}=T\sim t_{n-p}$ where $s^{2}=\frac{\sum(y_{i}-\hat{y_{i}})^{2}}{n-p}$
We will follow the 4 steps above to do this.
Recall also that (step 1 above) $$
Z=\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}
$$
$$
V=\frac{(n-p)s^{2}}{\sigma^{2}},\;d=n-p
$$
Step 2: 
Recall that $\hat{\beta}\sim N_{p}(\beta,\sigma^{2}(X^{T}X)^{-1})$ thus $\gamma^{T}\hat{\beta}\sim N_{1}(\gamma^{T}\beta,\sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma)$
Thus, $\gamma^{T}\hat{\beta}-\gamma^{T}\beta \sim N_{1}(0,\sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma)$
Finally then, $Z=\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}\sim N_{1}(0,1)$.

Step 3:
WTS $V\sim\chi_{d}^{2}\overset{d}{=}\chi_{n-p}^{2}$
$$V=\frac{(n-p)s^{2}}{\sigma^{2}}=\frac{(n-p)\sum(y_{i}-\hat{y}_{i})^{2}}{(n-p)\sigma^{2}}=\frac{\sum(y_{i}-\hat{y}_{i})^{2}}{\sigma^{2}}$$
Note that $$
\sum(y_{i}-\hat{y}_{i})^{2}=||y-\hat{y}||_{2}^{2}=||\hat{\epsilon}||_{2}^{2}=||P_{X}^{\perp}y||_{2}^{2}=||Q_{2}Q_{2}^{T}y||_{2}^{2}=y^{T}Q_{2}Q_{2}^{T}Q_{2}Q_{2}^{T}y=y^{T}Q_{2}I_{n-p}Q_{2}^{T}y
$$$$
=||Q_{2}^{T}y||_{2}^{2}
$$
Recall that the QR decomposition gives use $Q=[Q_{1}\;Q_{2}]$ where $Col(Q_{1})=Col(X)$ and $Col(Q_{2})=Col^{\perp}(X)$. Also recall that $P_{X}^{\perp}=Q_{2}Q_{2}^{T}$ (in general can create projection matrix from an orthonormal basis, in this case $Q_{2}$).
Now we know that $y\sim N(X\beta,\sigma^{2}I_{n})\implies Q_{2}^{T}y\sim N_{n-p}(Q_{2}^{T}X\beta,\sigma^{2}Q_{2}^{T}Q_{2})=N_{n-p}(Q_{2}^{T}X\beta,\sigma^{2}I_{n-p})=N_{n-p}(0,\sigma^{2}I_{n-p})$ where the last equality comes from the fact that $X\beta\in Col(X)$ and $Q_{2}$ spans $Col^{\perp}(X)$ thus $Q_{2}^{T}X\beta=0$.
Finally, $$
V=\frac{||Q_{2}^{T}y||_{2}^{2}}{\sigma^{2}}=\frac{y^{T}Q_{2}}{\sigma} \frac{Q_{2}^{T}y}{\sigma}\overset{d}{=}\sum w_{i}^{2}\sim \chi_{n-p}^{2}
$$
Because $\frac{Q_{2}^{T}y}{\sigma}\sim N_{n-p}(0_{n-p},I_{n-p})\implies \frac{Q_{2}^{T}y}{\sigma}=[w_{i}]_{i=1,\dots,n-p}$ where $w_{i}\overset{\text{iid}}{\sim} N(0,1)$.

Step 4:
Consider QR decomposition: $X=QR$.
Then $U=Q^{T}y=[Q_{1}^{T}y\;Q_{2}^{T}y]$ stacked. And note that all of the randomness of $V$ comes from $Q_{2}^{T}y$ and similarly the randomness of $Z$ comes from $\hat{\beta}$ which comes from $Q_{1}^{T}y$.
So $Z$ is a function of $Q_{1}^{T}y$, $V$ is a function of $Q_{2}^{T}y$ and $Q_{1}^{T}y,Q_{2}^{T}y$ are both multivariate normal, so now we can check if their covariance is 0 $\implies \perp\!\!\!\perp$.
$$
\mathrm{Cov}(Q_{1}^{T}y,Q_{2}^{T}y)=Q_{1}^{T}\mathrm{Cov}(y,y)Q_{2}=Q_{1}^{T}\sigma^{2}I_{n}Q_{2}=\sigma^{2}Q_{1}^{T}Q_{2}=0_{p\times(n-p)}
$$
Last equality comes from the fact that $Q_{1}$ spans $Col(X)$ and $Q_{2}$ spans $Col(X)^{\perp}$.
Thus, $Q_{1}^{T}y\perp\!\!\!\perp Q_{2}^{T}y$ and functions preserve independence $\implies Z\perp\!\!\!\perp V$.

Now we have a t-distribution and our t statistics $$
\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ s^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}\sim t_{n-p}
$$
So construct a confidence interval where $T\sim t_{n-p}$ and we have $$
\mathbb{P}\left(\left\{  t_{n-p}^{-1}\left( \frac{\alpha}{2} \right)\leq T\leq t_{n-p}^{-1}\left( 1-\frac{\alpha}{2} \right)  \right\}\right)=1-\alpha
$$$$
\implies\gamma^{T}\beta\in\gamma^{T}\hat{\beta}\pm t_{n-p}^{-1}\left( \frac{\alpha}{2} \right)s\sqrt{ \gamma^{T}(X^{T}X)^{-1}\gamma }
$$
Which gives us a confidence interval when we don't know the variance. We can see this is very similar to when we do know variance except $\sigma\to s,\Phi^{-1}\to t_{n-p}^{-1}$ which is the "price we paid".

##### Testing at Size $\alpha$
Two sided test is check if $T(y)\geq t_{n-p}^{-1}\left( 1-\frac{\alpha}{2} \right)$ or $T(y)\leq t_{n-p}^{-1}\left( \frac{\alpha}{2} \right)$.
If we have null $H_{0}:\beta=\beta_{0}$ then under the null these probabilities would be of size $\alpha$, but if $\beta\neq\beta_{0}$ then things can go wrong and the probability would not equal $\alpha$.
Can also get p-value from this as the smallest $\alpha$ at which you reject.