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
2. $A$ is invertible, $A^{-1}$ is also PD
3. $tr(A)>0$ (inherent from property 1)
4. $\exists$ non-singular $R$ s.t. $A=RR^{T}$
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
	Now going back up to $||y-\tilde{\theta}||_{2}^{2}=(y-\hat{\theta})^{T}(y-\hat{\theta})+(\hat{\theta}-\tilde{\theta})^{T}(\hat{\theta}-\tilde{\theta})=||y-\hat{\theta}||_{2}^{2}+||\hat{\theta}-\tilde{\theta}||_{2}^{2}$. Note the second term is minimized to 0 when $\hat{\theta}=\tilde{\theta}$. We can't do anything with first term since we already fixed $\hat{\theta}=P_{X}y$. Thus, we conclude that $\hat{\theta}=P_{X}y$ is the minimizer (among all $\theta\in Col(X)$ ) of $||y-\theta||_{2}^{2}$. Moreover, since $\hat{\theta}\in Col(X)$ there exists a $\hat{\beta}$ such that $\hat{\theta}=X\hat{\beta}$. And since we are assuming $X$ has full column rank there is one and only one such $\hat{\beta}$. Also since $y-\hat{\theta}\in Col^{\perp}(X)$ (from Seeber and Lee appendix first property + existence proven above) we know that $X^{T}(y-\hat{\theta})=0\implies X^{T}y=X^{T}\hat{\theta}\implies X^{T}y=X^{T}X\hat{\beta}\implies\hat{\beta}=(X^{T}X)^{-1}X^{T}y$. Can look at picture on phone (8/26 12:18) as well for visualization which essentially says that $\hat{\theta}$ is the vector in the column space of $X$ that lies directly under $y$ i.e. the projection of $y$ onto the column space. Any other $\tilde{\theta}$ would be rotated around thus meaning the distance is further (not minimal).

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
$X=QR$ where $X\in \mathbb{R}^{nxp},Q\in \mathbb{R}^{nxn},R\in \mathbb{R}^{nxp}$ and $Q$ is orthogonal, $R$ is upper triangular. Note that this $Q$ is a little too big for the $Q$ we are looking for ($P_{X}=QQ^{T}$) since we just need a $Q$ to span $p$ columns of $X$.
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
We can now rewrite $C(y)=\left\{  N_{\frac{\alpha}{2}}\leq Z\leq-N_{\frac{\alpha}{2}}  \right\}=\left\{  -N_{\frac{\alpha}{2}}\geq-Z  \geq N_{\frac{\alpha}{2}}\right\}=\left\{  -N_{\frac{\alpha}{2}}\geq \frac{\gamma^{T}\beta-\gamma^{T}\hat{\beta}}{\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}\geq N_{\frac{\alpha}{2}} \right\}$
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


## Homework 3 Takeaways

### Linear Models and Design
- **"Linear" means linear in $\beta$**, not in the covariate. The hinge model $\mu(M)=\beta_{1}+\beta_{2}\frac{M}{60}+\beta_{3}\left(\frac{M}{60}-1\right)_{+}$ is a linear model because each column of $X$ is a fixed, known function of $M$:
$$
X[i,:]=\begin{bmatrix} 1 & \dfrac{M_{i}}{60} & \left(\dfrac{M_{i}}{60}-1\right)_{+} \end{bmatrix}
$$
This requires the knot to be known. An estimated knot $\kappa$ in $\left(\frac{M}{60}-\kappa\right)_{+}$ makes the model nonlinear in its parameters.
- **Hinge function:** $\mu$ is continuous at the knot and differentiable there iff $\beta_{3}=0$. $\beta_{3}$ is the *change in slope* (right slope minus left slope), not the slope after the knot, which is $\beta_{2}+\beta_{3}$.
- **Identifiability:** if all $M_{i}\leq 60$, the third column of $X$ is $0_{n}$, so $e_{3}\in\mathcal{N}(X)$ and $\beta_{3}$ cannot be estimated.
- **The null hypothesis must match the scientific question.** "No change between 60 and 120 minutes" is $H_{0}:\beta_{2}+\beta_{3}=0$, (because we have $\mu(120)-\mu(60)=(\beta_{1}+2\beta_{2}+\beta_{3})-(\beta_{1}+\beta_{2})=\beta_{2}+\beta_{3}$) not $H_{0}:\beta_{3}=0$ (no bend) or $H_{0}:\beta_{2}=\beta_{3}=0$ (no effect anywhere, a two-constraint hypothesis).
- **Degrees of freedom:** if $n=p$ then $\hat{y}=y$, $RSS=0$, and $s^{2}=\frac{0}{0}$. Estimating $\sigma^{2}$ requires $n-p\geq 1$

### Standard Errors and Contrasts
- **The standard error is the standard deviation of an estimator** (the square root of its variance), not the variance itself. It measures how much the estimate varies across repeated datasets, while $\sigma$ measures how much individual observations vary. With $v_{\gamma}=\gamma^{T}(X^{T}X)^{-1}\gamma$:
$$
SE(\gamma^{T}\hat{\beta})=\sigma\sqrt{ v_{\gamma} },\qquad \widehat{SE}(\gamma^{T}\hat{\beta})=s\sqrt{ v_{\gamma} }
$$
- **Covariances between coefficients enter through $v_{\gamma}$:**
$$
\mathrm{Var}(\hat{\beta}_{2}+\hat{\beta}_{3})=\mathrm{Var}(\hat{\beta}_{2})+\mathrm{Var}(\hat{\beta}_{3})+2\mathrm{Cov}(\hat{\beta}_{2},\hat{\beta}_{3})
$$
Negative covariance shrinks the variance of a sum and inflates the variance of a difference.
- **Saturated designs:** with as many distinct covariate values as parameters, the fit passes through the group means. Here $\hat{\theta}=\bar{y}_{120}-\bar{y}_{60}$.

### Confidence Intervals and Tests
- **CI via a pivot.** The pivot below holds at the **true** $\beta$, with no null hypothesis involved:
$$
T=\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{s\sqrt{ v_{\gamma} }}\sim t_{n-p}
$$
Rearranging $\mathbb{P}(|T|\leq t_{n-p,1-\alpha/2})=1-\alpha$ gives the CI:
$$
\gamma^{T}\hat{\beta}\pm t_{n-p,1-\alpha/2}\,s\sqrt{ v_{\gamma} }
$$
- **Any split of $\alpha$ between the tails gives valid coverage.** Equal tails gives the shortest two-sided interval. One-sided bounds correspond to one-sided alternatives, and the direction must be chosen before looking at the data.
- **Test–CI duality:** reject $H_{0}:\theta=b$ at level $\alpha$ iff $b$ is outside the $100(1-\alpha)\%$ CI. The CI is the set of null values that are not rejected. The proof uses $|x|\leq c\iff -c\leq x\leq c$.
- **Two-sided p-value.** "Extreme" means far from what $H_{0}$ predicts, in either direction: (note that $F_{d}$ is the cdf of the $t_{d}$ distribution here)
$$
p=\mathbb{P}_{H_{0}}\left(|T|\geq|t_{obs}|\right)=2F_{n-p}(-|t_{obs}|)
$$
- **Interpretation.** 95% confidence means that about 95% of intervals from repeated experiments cover the fixed $\theta$. The interval is random and $\theta$ is fixed. A p-value is computed *assuming* $H_{0}$. It is not the probability that $H_{0}$ is true.

### Distribution Theory via QR
- With full QR $X=[Q_{1}|Q_{2}]\begin{bmatrix} R_{1} \\ 0 \end{bmatrix}$, we have $Q_{2}^{T}X=0$ and $Q_{2}^{T}Q_{2}=I_{n-p}$, so
$$
U=Q_{2}^{T}y\sim N_{n-p}(0_{n-p},\sigma^{2}I_{n-p}),\qquad RSS=||Q_{2}Q_{2}^{T}y||_{2}^{2}=||U||_{2}^{2}
$$
- **Residuals are not $n$ independent errors.** $\hat{\epsilon}\sim N_{n}(0_{n},\sigma^{2}(I-P))$: the residuals are correlated, have smaller variances than $\sigma^{2}$, and have a singular covariance of rank $n-p$ (they satisfy $X^{T}\hat{\epsilon}=0_{p}$). The QR rotation converts them into $n-p$ independent coordinates with the same sum of squares.
- **Distribution of RSS and bias of $RSS/n$:**
$$
\frac{RSS}{\sigma^{2}}\sim\chi^{2}_{n-p}\implies \mathbb{E}[s^{2}]=\sigma^{2},\qquad \mathbb{E}\left[ \frac{RSS}{n} \right]=\frac{n-p}{n}\sigma^{2}
$$
$RSS/n$ is the MLE and is biased downward.
- **The $t$ result:** $T=\frac{Z}{\sqrt{ V/d }}$ with $Z=\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sigma\sqrt{ v_{\gamma} }}\sim N(0,1)$, $V=\frac{RSS}{\sigma^{2}}\sim\chi^{2}_{d}$, and $d=n-p$. The unknown $\sigma$ cancels.
- **Independence of $Z$ and $V$.** $Q_{1}^{T}y$ and $Q_{2}^{T}y$ are **jointly normal** with zero cross-covariance, so they are independent. $Z$ and $V$ are functions of them, so $Z\perp\!\!\!\perp V$. Showing $\mathrm{Cov}(Z,V)=0$ is **not enough**: $(Z,V)$ is not jointly normal, and covariance only detects linear dependence (e.g. $\mathrm{Cov}(W,W^{2})=\mathbb{E}[W^{3}]=0$ for $W\sim N(0,1)$).
- **Without normality** (keeping $\mathbb{E}[\epsilon]=0_{n}$ and $\mathrm{Var}(\epsilon)=\sigma^{2}I_{n}$), first- and second-moment results survive and distributional results do not. The trace trick shows $s^{2}$ is still unbiased:
$$
\mathbb{E}[y^{T}Ay]=tr(A\,\mathbb{E}[yy^{T}])=\sigma^{2}tr(A)+\mathbb{E}[y]^{T}A\,\mathbb{E}[y]
$$
But $Z$ need not be normal, $V$ need not be $\chi^{2}$, and independence is no longer established, so the exact $t$ result is lost. It still holds approximately for large $n$.

### Simulation Lessons
- **Algebraic identities vs. distributional claims.** Identities such as $RSS=||U||_{2}^{2}$ and the two constructions of $T$ agree to machine precision in every dataset. Distributional claims agree only up to Monte Carlo error, about $1/\sqrt{ B }$.
- **What simulation can and can't show.** A simulation can show a lack of *correlation* and no visible dependence. It cannot prove *independence*, which requires $\mathrm{Cov}(f(Z),g(V))=0$ for all functions $f,g$. That needs the joint-normality argument.
- **$t_{n-p}$ vs. $N(0,1)$.** The $t_{n-p}$ distribution has heavier tails than $N(0,1)$, because the random $s$ is sometimes small, and $\mathrm{Var}(T)=\frac{d}{d-2}$.
- **Coverage of the three intervals.** For each interval, coverage is $\mathbb{P}(|\text{pivot}|\leq\text{cutoff})$. The denominator ($\sigma$ or $s$) determines the pivot's distribution, and the quantile determines the cutoff:
$$
A:\;2\Phi(z_{0.975})-1=0.95,\qquad B:\;2F_{n-p}(z_{0.975})-1<0.95,\qquad C:\;2F_{n-p}(t_{n-p,0.975})-1=0.95
$$
B undercovers (about 0.90 when $n-p=6$), and the gap closes as $n-p\to\infty$.
- **Width.** C is wider than A iff $\frac{s}{\sigma}>\frac{z_{0.975}}{t_{n-p,0.975}}$. This is random, so it doesn't hold in every dataset. On average, C is wider:
$$
\frac{\mathbb{E}[\text{width of }C]}{\text{width of }A}=\frac{t_{n-p,0.975}}{z_{0.975}}\cdot\frac{\mathbb{E}[s]}{\sigma}
$$
where $\mathbb{E}[s]<\sigma$ by Jensen's inequality. The extra width is the cost of estimating $\sigma$, and it shrinks as the degrees of freedom grow.
- **Calibration vs. precision.** Coverage measures calibration and width measures precision. Even with true coverage exactly $0.95$, the empirical coverage has standard error about $\sqrt{ 0.95(0.05)/B }$, so it won't be exactly $0.95$.

9/28
## Inference for Vector Targets
**Definition**: F-Distribution
Let $V_{1}\sim\chi_{d_{1}}^{2},V_{2}\sim\chi_{d_{2}}^{2}$ with $V_{1}\perp\!\!\!\perp V_{2}$. Then $\frac{\frac{V_{1}}{d_{1}}}{\frac{V_{2}}{d_{2}}}\sim F_{d_{1},d_{2}}$.

We want to test null hypothesis $H_{0}:\beta=0_{p}$ (all zero's).
Claim: Under $H_{0}$, $\frac{\frac{\frac{||\hat{y}||_{2}^{2}}{p}}{||\hat{\epsilon}||_{2}^{2}}}{n-p}\sim F_{p,n-p}$.
Proof: Let $V_{1}=||\hat{y}||_{2}^{2},d_{1}=p,d_{2}=n-p,V_{2}=||\hat{\epsilon}||_{2}^{2}$. But then things won't work out so we need to add division by $\sigma^{2}$ to make it work for chi-squared distributions, and this will work since they will cancel. I.e. $V_{1}=\frac{||\hat{y}||_{2}^{2}}{\sigma^{2}},V_{2}=\frac{||\hat{\epsilon}||_{2}^{2}}{\sigma^{2}}$.
Now show $V_{2}\sim\chi_{n-p}^{2}$. $||\hat{\epsilon}||_{2}^{2}=||Q_{2}Q_{2}^{T}y||_{2}^{2}=||Q_{2}^{T}y||_{2}^{2}\implies\left( \frac{Q_{2}^{T}y}{\sigma} \right)^{T}\left( \frac{Q_{2}^{T}y}{\sigma} \right)\sim \chi_{n-p}^{2}$.
Now show $V_{1}\sim \chi_{p}^{2}$. $||\hat{y}||_{2}^{2}=||Q_{1}Q_{1}^{T}y||_{2}^{2}=||Q_{1}^{T}y||_{2}^{2}=(Q_{1}^{T}y)^{T}(Q_{1}^{T}y)$. Note that $Q_{1}^{T}y\sim N_{p}(Q_{1}^{T}X\beta,\sigma^{2}I_{p})=N_{p}(0_{p},\sigma^{2}I_{p})$ under $H_{0}$ because $\beta=0_{p}$. Thus, $\frac{(Q_{1}^{T}y)^{T}}{\sigma} \frac{Q_{1}^{T}y}{\sigma}\sim\chi_{p}^{2}$.
$V_{1}$ is a function of $\hat{y}$, $V_{2}$ is a function of $\hat{\epsilon}$ and we can show that $\mathrm{Cov}(\hat{y},\hat{\epsilon})=0_{n\times n}\implies V_{1}\perp\!\!\!\perp V_{2}$ since covariance is 0 between joint normal.

Now to test our null we check if $F\geq$ to the $1-\alpha$ quantile of $F_{p,n-p}$. If so, reject. 

Note that this is a one-sided test, but we can't really think of $H_{0}:\beta=0_{p}$ as a "two-sided" hypothesis anymore because after 1D we lose this ordered sense of sidedness. For example, in 2D $H_{0}:\beta_{1}=\beta_{2}=0$, both could be positive, or both negative, or one positive and one negative so there is nice sense of sidedness now like in 1D.

Note we can easily go from $t_{n-p}$ distribution to $t_{n-p}^{2}\overset{d}{=}F_{1,n-p}$ distribution.


Suppose we have an intercept and design matrix $\tilde{X}=[1_{n}\;X]$ and model $y=\tilde{X}\tilde{\beta}+\epsilon$ where $\tilde{\beta}=[\delta\;\beta]^{T}$. Thus, $y=\delta 1_{n}+X\beta+\epsilon$. I.e. we can split up the model with and without an intercept.
Then we have null $H_{0}:\beta=0_{p-1}$ which is just seeing if any of our actual predictors are nonzero, but we don't care about the intercept.
Claim: Under $H_{0}$ we can construct quadratic form, $$\frac{\frac{y^{T}(P_{\tilde{X}}-P_{1_{n}})y}{(p-1)}} {\frac{y^{T}P_{\tilde{X}}^{\perp}y}{n-p}}\sim F_{p-1,n-p}$$We will now check whether $P_{\tilde{X}}-P_{1_{n}}$ is a projection matrix.$$
(P_{\tilde{X}}-P_{1_{n}})^{2}=P_{\tilde{X}}^{2}-P_{\tilde{X}}P_{1_{n}}-P_{1_{n}}P_{\tilde{X}}+P_{1_{n}}^{2}=P_{\tilde{X}}-P_{1_{n}}-P_{1_{n}}+P_{1_{n}}=P_{\tilde{X}}-P_{1_{n}}
$$
Where the second to last equality comes from the fact that $Col(1_{n})\subseteq Col(\tilde{X})$ and note that nested projections project you into the smallest space (which is $1_{n}$ in this case).

9/30
Continuing F-statistic above.
Task: Suppose $U,V$ both subspaces of $\mathbb{R}^{n}$ and they satisfy $V\subset U$ ($V$ is strict subset of $U$). Which of the following are projection matrices?
For each of the following, is it a projection matrix? What space does it project onto?
1. $P_{U}P_{V}$ - Yes, because $P_{U}P_{V}=P_{V}$ since $V\subset U$ (see note above). Projects onto $V$ 
2. $P_{V}P_{U}$ - Yes, $P_{V}P_{U}=P_{V}$ so projects onto $V$
3. $P_{U}-P_{V}$ - Yes, follows same argument as above for idempotence and projects onto $U \cap V^{\perp}$.
4. $P_{V}-P_{U}$ - No, it is not idempotent: $(P_{V}-P_{U})^{2}=P_{U}-P_{V}$

To show these more rigorously we can choose any orthonormal basis for $V$ as $Q_{V}$ and build an orthonormal basis for $U$ where the first columns are $Q_{V}$: $Q_{U}=[Q_{V}\;\tilde{Q}_{U}]$. Thus we have $P_{U}=Q_{U}Q_{U}^{T}$ and $P_{V}=Q_{V}Q_{V}^{T}$ so $P_{U}P_{V}=Q_{U}Q_{U}^{T}Q_{V}Q_{V}^{T}=Q_{V}Q_{V}^{T}$. Note that $\tilde{Q}_{U}$ is an orthonormal basis for $U \cap V^{\perp}$.

Note that $\lim_{ k \to \infty }(P_{U}P_{V})^{k}=0$ for two subspaces that aren't nested. Intuitively, we bounce back and forth between the two spaces slowly compressing and getting closer to 0 with every iteration. In general it converges to the projection onto $P_{U\cap V}$.


For null $H_{0}:\beta_{M}=0$ where $M$ is an index set its the same idea: $$
\frac{\frac{y^{T}(P_{X}-P_{X_{-M}})y}{|M|}} {\frac{y^{T}P_{X}^{\perp}y}{n-p}}\sim F_{|M|,n-p}
$$Where $P_{X_{-M}}$ is the projection onto the $X$ with the $M$ columns removed.
>Note: $P_{X}-P_{X_{_{-M}}}$ is not the same as $P_{X_{M}}$ because they live in different spaces, but if we have an orthogonal design they would be the same. The first lives in $Col(X)\cap X_{-M}^{\perp}$. We can think about the difference between $P_{X}-P_{X_{_{-M}}}$ and $P_{X_{M}}$ as the first is describing the effect of the $M$ columns after accounting for the other columns whereas $P_{X_{M}}$ is just directly the effect of the $M$ columns without taking other columns into consideration.

Generalizing further, $H_{0}:C\beta=0_{q}$ for $C\in \mathbb{R}^{q\times p}$
Consider a medical study where participants get one of four distinct drugs, or placebo, and also are assigned to exercise $W$ minutes per day, and we measure blood pressure. Goal: test if **any** drugs influence blood pressure.
Look at pic on phone for matrix: $X=[1_{n}\;\mathbb{I}\{ A \}\;\mathbb{I}\{ B \}\;\mathbb{I}\{ C \}\;\mathbb{I}\{ D \}\;W_{i}]$ where $\mathbb{I}\{ \cdot \}$ is an indicator for if that patient received that drug. Thus, $X\in \mathbb{R}^{n\times6}$
So our $C$ matrix should be $C=[0_{4}\;I_{4}\;0_{4}]$ because then $C\beta=[\beta_{2}\;\beta_{3}\;\beta_{4}\;\beta_{5}]$.
We can also have a design matrix $X$ where the intercept column can be an indicator of if people got placebo. Then our $C$ must be different: $C=[1_{4}\;-I_{4}]$ because now we are doing getting $\beta_{1}-\beta_{2},\beta_{1}-\beta_{3}$,etc. because now our $\beta_{i}$'s measure the mean response of each drug group (including placebo) at 0 minutes of exercise. So to test if any drugs influence blood pressure we need to check the difference between baseline ($\beta_{1}$) and any drug group ($\beta_{i},i=2,3,4,5$).

Think of this as saying drugs A and $B$ are in drug class 1 and $C$ and $D$ are in drug class 2. So we want to test if drug class 1 is equivalent to drug class 2.
The $C$'s for this can bake in different assumptions. For example a $C$ with pairwise differences between drugs in class 1 and 2 essentially just tests if all the drugs are equivalent.

When we have a null hypothesis $H_{0}:C\beta=0$ this is the same as asking if $\beta\in \mathcal{N}(C)$.

10/5
Missed beginning of class; going over quiz 3
**Review 3b (which best describes relationship between $||W||_{2}^{2}$ and $V$?) as it will show back up on midterm**

### Inference for Vector Targets (continued)
Usual model $y=X\beta+\epsilon$ with $\epsilon \sim N_{n}(0_{n},\sigma^{2}I_{n})$
Testing null hypothesis $H_{0}:C\beta=0_{q}\equiv\beta \in \mathcal{N}(C)\subseteq \mathbb{R}^{p}$ (note that $C\in \mathbb{R}^{q\times p},\beta\in \mathbb{R}^{p\times1}$)
Recall that $\mathbb{E}y\in Col(X)$ (since $y\sim N_{n}(X\beta,\sigma^{2}I_{n})$)
So take $K$ to be a matrix satisfying $Col(K)=\mathcal{N}(C)$ and $K^{T}K=I$. I.e. $K$ gives us an orthonormal basis for the null-space of $C$. Note $K\in \mathbb{R}^{p\times r}$.
Suppose $dim(\mathcal{N}(C))=r$. Under $H_{0}$ any "legal" $\beta$ must be in $\mathcal{N}(C)$ which can be written as $\beta=K\gamma$ for some $\gamma\in \mathbb{R}^{r}$.
Replace $X$ by $XK\implies \tilde{X}=XK$.
We can construct the $F$ statistic $$
\frac{\frac{y^{T}(P_{X}-P_{XK})y}{p-r}}{\frac{y^{T}(I-P_{X})y}{n-p}}
$$
	Examining $P_{XK}$, note that $K:\mathbb{R}^{r}\to \mathbb{R}^{p}$ (maps from r subspace to p subspace) and $X:\mathbb{R}^{p}\to \mathbb{R}^{n}$. Thus, $\mathrm{Im}(K)=Col(K)$ and $\mathrm{Im}(X)=Col(X)$. So we are composing $X$ and $K$ meaning $XK:\mathbb{R}^{r}\to \mathbb{R}^{n}$. ($XK\in \mathbb{R}^{n\times r}$). Look at picture on phone 10/5 11:54 for drawing of this mapping. Recall image is all points that the domain maps too e.g. $f(x)=x^{2}\implies \mathrm{Im}(f)=[0,\infty)$.

Getting back to the point "Replace $X$ by $XK\implies \tilde{X}=XK$.", any legal $\beta$ has a corresponding $\gamma\in \mathbb{R}^{r}$ such that $\beta=K\gamma$. This effectively restricts $\beta$ from $p$ points to $r$ points. Hence, the idea is that we are working in $\mathbb{R}^{r}$ without any restrictions by using $XK$ since having the $K$ bakes in this restriction to $\mathbb{R}^{r}$ from $\mathbb{R}^{p}$.
Recall that $C\in \mathbb{R}^{q\times p}$ and $dim(\mathcal{N}(C))=r$. Assume $C$ has full row rank ($rank(C)=q$). Thus, $rank(C)+dim(\mathcal{N}(C))=q+r=p\implies q=p-r$ so in the formula above we can use $q$ or $p-r$ as degrees of freedom (denominator in numerator of $F$ statistic above).
So under $H_{0}:\beta\in Col(K)$ we have that $F\sim F_{q,n-p}$.

#### Slightly More General
Suppose $H_{0}:C\beta=d$ for $C\in \mathbb{R}^{q\times p},\beta\in \mathbb{R}^{p\times1},d\in \mathbb{R}^{q\times1}$ so we have an affine constraint now instead of linear.
Find a $\beta_{0}$ satisfying $C\beta_{0}=d$. Then shift $y$ as $\tilde{y}=y-X\beta_{0}$. Then proceed as though $H_{0}:C\beta=0_{q}$ but using $\tilde{y}$ instead of $y$.
The upshot is that we will arrive at a form for our $F$ statistic: $$
\frac{\frac{\frac{\tilde{y}^{T}(P_{X}-P_{XK})\tilde{y}}{q}}{y^{T}(I-P_{X})y}}{n-p}
$$So under $H_{0}:C\beta=d$ and $F\sim F_{q,n-p}$.
Note that we keep $y$ in the denominator because we still want accurate estimation of variance. And the variance does still potentially change (even though we are just shifting) because each data point is shifting by a potentially different amount ($X\beta$ instead of some constant $\lambda1_{n}$).

**Activity**
Consider $\beta_{0}$ satisfying $C\beta_{0}=d$ and a different $\beta_{0}'$ also satisfying $C\beta_{0}'=d$.
1. Does $\tilde{y}$ change?
	In general yes, $\tilde{y}$ can change because just because $C\beta_{0}=d=C\beta_{0}'$ does not mean that $X\beta_{0}=X\beta_{0}'$.
2. Does $F$ change?
	No. Think about the set $\{ b:Cb=d \}$. Suppose $\beta_{0}$ satisfies $C\beta_{0}=d$. Consider $\beta_{0}'=\beta_{0}+\gamma$ where $\gamma \in \mathcal{N}(C)\implies C\beta_{0}'=C\beta_{0}+C\gamma=C\beta_{0}=d$. If one thinks through it, we can could see that all $\beta_{0}$'s can be related through shifts in the $\mathcal{N}(C)$. Additionally, we can explain it through the projection matrix in the numerator ($P_{X}-P_{XK}$) (which is a projection matrix since $Col(XK)\subseteq Col(X)$). This projection matrix projects onto $Col(X)\cap Col(XK)^{\perp}$. And as we just said, $\beta_{0}$'s vary only through shifts in $\mathcal{N}(C)$ and $Col(K)=\mathcal{N}(C)$. Hence, if $\tilde{y}=X\beta_{0}'=X\beta_{0}+X\gamma$ then the $X\gamma$ portion gets killed by the projection since we are projecting onto $Col(XK)^{\perp}$ (since $X\gamma$ lives in $Col(XK)$).

10/7
Midterm will be more open ended (rather than style of quizzes)
Can look at slides that go with today's lecture
We will be looking at a Drug experiment where each patient gets randomized to placebo (PBO), drug A, $B$, or $C$.
Recall another parameterization (than the one in slides) is to have first column be an indicator for PBO instead of an intercept.
To answer the question on the slide "How could we use orthogonal_complement() to find a null-space basis?" For a matrix $C$ we use orthogonal_complement(t(C)) i.e. getting the complement of $C^{T}$ from the fact that $\mathcal{N}(C^{T})=Col(C)^{\perp}\implies \mathcal{N}(C)=Col(C^{T})^{\perp}$. **Make sure you fully understand this**
All of the entries in covariance matrix are relative to the placebo group. I.e. if the intercept moved up (healthier patients) then the relative effect of all of the drugs will go down (hence negative covariance with intercept and positive covariance with each other).
Q1: Is drug A effective? How effective is drug A?
- Natural guess for how effective is just $\hat{\beta}_{A}$, but we want to do inference and determine what kind of effects are plausible.
- For is drug A effective the confidence interval is more useful (i.e. is 0 in it).
Can we test Q1 using an $F$ test?
- $$F=\frac{ \frac{y^{T}(P_{X}-P_{X_{-2}})y}{1}}{\frac{y^{T}(I-P_{X})y}{n-p}}$$where $P_{X_{-2}}$ is projecting onto $X$ with the second column removed. Under null $H_{0}:F\sim F_{1,n-p}$.
- In the slides note that $t^{2}=F$ that is if we square our t statistic it is equal to our $F$ statistic. So not every $F$ has a corresponding t, but if we have a t distribution/statistic we can always get an $F$ and that goes back to the fact that t = standard normal / sqrt(chi-squared  d.o.f). Thus, $t^{2}$=chi-squared 1 d.o.f. / chi-squared n d.o.f. = $F_{1,n}$.

Q2: Are any of the drugs effective?
- Our null is $H_{0}:\beta_{A}=\beta_{B}=\beta_{C}=0$
- We cannot test with t test, but can with $F$ test $$
F=\frac{ \frac{y^{T}(P_{X}-P_{1_{n}})y}{p-1}}{\frac{y^{T}(I-P_{X})y}{n-p}}
$$
- Think of $P_{X}-P_{1_{n}}$ is what you gain by releasing the null. That is the projection we are subtracting is the model under the null. So if we just had $P_{X}$ we would be evaluating under our full model, but by evaluating under $P_{X}-P_{1_{n}}$ we are testing the model with the null released. I.e. we are going from $P_{restricted}$ to $P_{X}=P_{full}$ and this gap is represented as $P_{full}-P_{restricted}$,. **Look into a little more with AI**. Note that by expanding it out we also get $y^{T}P_{full}y-y^{T}P_{restricted}y=SS_{full}-SS_{restricted}$ so we are evaluating how much $SS$ is accounted for by the full after accounting for our null model.

Q3: How does Drug A compare to Drug $B$?
- Want to look at target of inference $\beta_{A}-\beta_{B}$.
- So lets look at $\gamma^{T}\beta$ with $\gamma=[0\;1\;-1\;0]$. Note that we could also use $\gamma=[0\;-1\;1\;0]$ to test if $\beta_{A}-\beta_{B}=0$, so the sign doesn't matter for equaling 0, but it does matter for constructing confidence intervals. For example, if our CI has a lot of positive values then it may indicate that one drug is much stronger than the other and which is stronger depends on the sign of $\gamma$.
- $$
t=\frac{\gamma^{T}\hat{\beta}}{\sqrt{ s^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}
$$will give us our t statistic and if we wanted a pivot for a confidence interval we can use $$
\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ s^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}
$$
- So for our CI we have $\gamma^{T}\hat{\beta}\pm t_{n-p}^{-1}\left( 1-\frac{\alpha}{2} \right)\sqrt{ s^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }$.

Q4: Are the drugs all equivalent?
- $H_{0}:\beta_{A}=\beta_{B}=\beta_{C}$ (note this is different than Q2)
- So to do this with $F$ test we first want to write $H_{0}:C\beta=0_{q}$ where $C\in \mathbb{R}^{q\times p}$. $C$ will represent the pairwise differences between drugs A,$B$, and $C$. Hence $C = [0\;-1\;1\;0;0\;1\;0\;-1]$ which tests if drug A = $B$ and drug A = drug $C$ (hence if drug $B$ = $C$ as well).
- Thus, $H_{0}:C\beta=0_{q}\equiv\beta\in \mathcal{N}(C)$.
- As we said above, we now create a basis for $\mathcal{N}(C)$ by orthogonal_complement(t(C)).
- So let matrix $K$ have column space as null space of $C$: $Col(K)=\mathcal{N}(C)$. Thus, $XK$ is now our restricted $X$. Now we find $\hat{\phi}$ which is our coordinates (simplified betas i.e. $\beta_{B}-\beta_{A}$ and $\beta_{A}-\beta_{C}$) through standard normal equation $\hat{\phi}=(\tilde{X}^{T}\tilde{X})^{-1}\tilde{X}^{T}y$ where $\tilde{X}=XK$. Then to get the original $\hat{\beta}$ we unwrap $\hat{\phi}$ by $\hat{\beta}_{restricted}=K\hat{\phi}$. Note that $\hat{\beta}_{restricted}$ just means it is the optimal $\beta$ such that $C\beta=0$ (restriction). **Worth looking at more to solidify understanding**

Q5: $B$ claims the same mean effect as A; $C$ claims ten units more than B
- So we want to test $\beta_{A}=\beta_{B}$ and $\beta_{C}=\beta_{B}+10$.
- Hence to get affine representation $C\beta=d$ we have $H_{0}:C\beta=d$ with $C=[0\;1\;-1\;0;\;0\;0\;-1\;1]$ and $d=[0;10]$.
- Then the approach we can take is find a $\beta_{0}$ that satisfies the constraint $C\beta_{0}=d$ then shift y by $X\beta_{0}$.
10/12
Questions from slides continued
Q5 continued
- Note that an equivalent $C=[0\;1\;-1\;0;0\;-1\;0\;1]$ since in our null we assume that A and $B$ are the same. Mathematically, the null space of both $C$'s are the same.
- If we have $C(\beta_{0}+\tilde{\beta})=d$ choose $\beta_{0}$ that satisfies $C\beta_{0}=d$ then we have $C\tilde{\beta}=0_{2}$.
- We can then think of $\tilde{\beta}=K\hat{\phi}$ where $K$ is a basis for the null space of $C$ hence $\hat{\phi}$ is the regressed coefficients on $XK$ instead of $X$ after shifting $y-X\beta_{0}$. **Look into more**
Q7:
- Given a new data point with $X=[1\;0\;0\;1]$ we want a confidence interval for an expectation i.e. an interval for an observation (a prediction interval).
- In this case with $X=[1\;0\;0\;1]$ we are giving them drug $C$, hence $y_{new}\sim N(\beta_{1}+\beta_{C},\sigma^{2})$ (new observation with this design) note that we have the mean as $X\beta=\beta_{1}+\beta_{C}$ (first and fourth betas). Hence, $\hat{y}_{new}=\hat{\beta}_{1}+\hat{\beta}_{4}$.
- So our prediction interval is $\gamma^{T}\hat{\beta}\pm t_{n-p}^{-1}\left( 1-\frac{\alpha}{2} \right)\sqrt{ s^{2}\gamma^{T}(X^{T}X)^{-1}\gamma+s^{2}}$ where $\gamma^{T}$ is our new observation where $s^{2}\gamma^{T}(X^{T}X)^{-1}\gamma$ in square root comes from uncertainty of $\beta$ and $s^{2}$ term comes from uncertainty of $\epsilon$.
9c Midterm practice
- Intuition of the identity is that $RSS_{F}$ is the error from the full model and the sum term is the additional error from imposing the restriction.
- For deriving the identity, we have $RSS_{F}=y^{T}(I-P_{X})y$. Let $z:=y-X\beta_{0}$ then $RSS_{R}=z^{T}(I-P_{XK})z$. 

# Midterm Review
- $Col(A)^{\perp}=\mathcal{N}(A^{T})$
- Check if $P_{A}$ is a the projection matrix for $A$ (projection matrices are unique)
	- Idempotence & Symmetry (projection matrix)
	- $Col(P_{A})=Col(A)$ (valid for $A$)
- $Col(AB)\subseteq Col(A)$
- $Col(A)=\mathbb{R}^{n}\implies n\leq p$
- For $A\in \mathbb{R}^{n\times p}$, $Col(A)=\{ Ax:x\in \mathbb{R}^{p} \}\subseteq \mathbb{R}^{n}$ and $Col(A)^{\perp}=\{ u\in \mathbb{R}^{n}:u^{T}Ax=0,\forall x\in \mathbb{R}^{p} \}\subseteq \mathbb{R}^{n}$
- $rank(A)=p\iff A^{T}A\text{ is PD}\iff A^{T}A\text{ invertible}\iff \mathcal{N}(A)=\{ 0 \}$
- $\mathcal{N}(A^{T}A)=\mathcal{N}(A)\implies rank(A^{T}A)=rank(A)$
- Let $A$'s columns be a basis for $Col(X)$ then $P_{X}:=P_{Col(X)}=A(A^{T}A)^{-1}A^{T}$. (Note $A$ has full column rank)
- $P_{X}^{\perp}=I-P_{X}=P_{\mathbb{R}^{n}}-P_{X}$
- $y=P_{X}y+P_{X}^{\perp}y=\hat{y}+\hat{\epsilon}$
- If $Q$ forms an orthogonal basis for subspace $\Omega$ then $P_{\Omega}=QQ^{T}$.
- If $U\subseteq V$ then $P_{V}-P_{U}=P_{U^{\perp}\cap V}$ (projecting onto part of $V$ that is orthogonal to $U$).
- If $U\subseteq V$ then $P_{U}P_{V}=P_{V}P_{U}=P_{U}$.
- QR Decomposition: $Q\in \mathbb{R}^{n\times n},R\in \mathbb{R}^{n\times p}$
	- $R_{1}\hat{\beta}=Q_{1}^{T}y$ i.e. given $Q^{T}y$ and $R$ we can find $\hat{\beta}$.
	- $X=Q_{1}R_{1}$ where $Q=[Q_{1}|Q_{2}],R=[R_{1}|0_{n-p,p}]$ ($Q_{1}\in \mathbb{R}^{n\times p},R_{1}\in \mathbb{R}^{p\times p}$)
	- $Q_{1}^{T}Q_{1}=I_{p},Q_{1}Q_{1}^{T}=P_{X},Q_{2}^{T}Q_{2}=I_{n-p},Q_{2}Q_{2}^{T}=P_{X}^{\perp}$
	- $H_{k}=I_{n}-2P_{v_{k}}=I_{n}-\frac{2v_{k}v_{k}^{T}}{v_{k}^{T}v_{k}}$
	- $Q^{T}y=\begin{bmatrix} z \\ d \end{bmatrix},\qquad z=Q_{1}^{T}y\in \mathbb{R}^{p},\quad d=Q_{2}^{T}y\in \mathbb{R}^{n-p}\implies||\hat{y}||_{2}^{2}=||z||_{2}^{2},||\hat{\epsilon}||_{2}^{2}=||d||_{2}^{2}$ i.e. Given just $Q^{T}y$ we can find $||\hat{y}||_{2}^{2}$ and $||\hat{\epsilon}||_{2}^{2}=RSS$.
	- $Q_{2}^{T}y\sim N_{n-p}(0_{n-p},\sigma^{2}I_{n-p})$ and $Q_{1}^{T}y\sim N_{p}(R_{1}\beta,\sigma^{2}I_{p})$
- Covariance
	- $\mathrm{Cov}(U,W)=\mathbb{E}[UW^{T}]-\mathbb{E}[U]\mathbb{E}[W]^{T}$
	- $\mathrm{Var}(AU)=A\mathrm{Var}(U)A^{T},\mathrm{Cov}(AU,BU)=A\mathrm{Var}(U)B^{T}$
	- $\mathrm{Var}(\hat{\beta}_{1}-\hat{\beta}_{2})=\mathrm{Var}(\gamma^{T}\hat{\beta})=\gamma^{T}\mathrm{Var}(\hat{\beta})\gamma$.
	- $\mathrm{Var}(a^{T}U)=a^{T}\Sigma a=\sum_{i} \sum_{j} a_{i}a_{j}\Sigma_{ij}$ where $\Sigma$ is covariance matrix of random variables in random vector $U$
	- $\mathrm{Var}(\hat{\beta}_{2}+\hat{\beta}_{3})=\mathrm{Var}(\hat{\beta}_{2})+\mathrm{Var}(\hat{\beta}_{3})+2\mathrm{Cov}(\hat{\beta}_{2},\hat{\beta}_{3})$ hence negative covariance shrinks the variance of a sum and inflates the variance of a difference.
- Lemma for following: $v^{T}y=0,\forall y\in \mathbb{R}^{n}\iff v=0_{n}$:
	- $\gamma^{T}\hat{y}=\gamma^{T}P_{X}y=0\;\;\forall y\iff X^{T}\gamma=0_{p}\iff \gamma\in Col(X)^{\perp}$
	- $\gamma^{T}\hat{\epsilon}=0\;\;\forall y\iff \gamma\in Col(X)$
	- Recipes if time
- Distributional Facts:
	- $y\sim N_{n}(X\beta,\sigma^{2}I_{n})$, $rank(\Sigma)=n$ (full rank so invertible), lives in $\mathbb{R}^{n}$
	- $\hat{\beta}\sim N_{p}(\beta,\sigma^{2}(X^{T}X)^{-1})$, $rank(\Sigma)=p$ (full rank so invertible), lives in $\mathbb{R}^{p}$
	- $\hat{y}\sim N_{n}(X\beta,\sigma^{2}P_{X})$, $rank(\Sigma)=p$ (not full rank), lives in $Col(X)$
	- $\hat{\epsilon}\sim N_{n}(0,\sigma^{2}P_{X}^{\perp})$, $rank(\Sigma)=n-p$ (not full rank), lives in $Col(X)^{\perp}$ (note residuals not n independent normals, but rather are correlated hence $\Sigma=\sigma^{2}(I-P_{X})$)
	- $\mathcal{N}(\Sigma)$ describes the directions in which distribution $V$ does not vary. The general principle is $V-\mu\in Col(\Sigma)\implies V\in Col(\Sigma)+\mu$.
- Stack parameters to get joint normality and 0 covariance to prove independence between $\hat{y}\perp\!\!\!\perp\hat{\epsilon},\hat{\beta}\perp\!\!\!\perp\hat{\epsilon}$. For example: $\begin{bmatrix} \hat{y} \\ \hat{\epsilon} \end{bmatrix}=\begin{bmatrix} P \\ I_{n}-P \end{bmatrix}y=Cy\implies Cy\sim N_{2n}\left(\begin{bmatrix} X\beta \\ 0_{n} \end{bmatrix},\;\sigma^{2}\begin{bmatrix} P & 0 \\ 0 & I_{n}-P \end{bmatrix}\right)$
- If $\mathrm{Var}(\hat{\beta})$ has negative terms in off-diagonals, then $\mathrm{Var}(\hat{\beta}_{1}+\hat{\beta}_{2})$ observes a reduction in variance and an increase in variance for positive terms. This is the idea the collinearity is a variance phenomenon.
- Confidence Intervals:
	- Recall $Z=\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }}\sim N(0,1)$ hence we have $CI(y)=\{\gamma^{T}\hat{\beta}\pm N_{\frac{\alpha}{2}}\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }\}$ giving $\mathbb{P}(\gamma^{T}\beta\in CI(y))=1-\alpha$. Note this is a confidence interval that we hope contains our true parameter $\gamma^{T}\beta$ with $1-\alpha$ confidence. Hypothesis testing on the other hand checks if $\gamma^{T}\hat{\beta}\in \{b\pm N_{\frac{\alpha}{2}}\sqrt{ \sigma^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }\}$ under our null $H_{0}:\gamma^{T}\beta=b$.
	- For unknown variance: $\gamma^{T}\beta\in \{ \gamma^{T}\hat{\beta}\pm t_{n-p}^{-1}\left( \frac{\alpha}{2} \right)s\sqrt{ \gamma^{T}(X^{T}X)^{-1}\gamma }\}$
- t-distribution:
	- Let $Z\sim N(0,1)$ and $V\sim \chi_{d}^{2}$ with $Z$ independent of $V$. Then $\frac{Z}{\sqrt{ \frac{V}{d} }}\sim t_{d}$ (t distribution with $d$ d.o.f.).
	- $\frac{\gamma^{T}\hat{\beta}-\gamma^{T}\beta}{s\sqrt{\gamma^{T}(X^{T}X)^{-1}\gamma }}\sim t_{n-p}$ where $s^{2}=\frac{\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}}{(n-p)}$
- Coverage
	- $\mathbb{E}[s]<\sigma$ because ($\mathbb{E}[s]=\mathbb{E}[\sqrt{ s^{2} }]<\sqrt{ \mathbb{E}[s^{2}] }=\sigma$)
	- $t_{d}(\alpha)$ quantile will always be larger than equivalent normal quantile $z_{\alpha}$
	- Width only smaller with probability 1 if the randomness cancels (i.e. no $s$ in the comparison $\frac{L_{1}}{L_{2}}$)
- Linear Models and Designs
	- $n-p\geq1$ in order to estimate $\sigma^{2}$ (i.e. we must have at least 1 degree of freedom to estimate variance)
	- When formulating null hypothesis evaluate in terms of vectors rather than intuitive explanation (remember "No change from 60 to 120" example in HW3 takeaways)
	- $SE(\gamma^{T}\hat{\beta})=\sigma\sqrt{ v_{\gamma} }$ is standard error if $\sigma^{2}$ is known and $\widehat{SE}(\gamma^{T}\hat{\beta})=s\sqrt{ v_{\gamma} }$ is estimated standard error (if $\sigma^{2}$ is unknown). We use this for determining our CI as $\gamma^{T}\hat{\beta}\pm z*SE$ for known variance and $\gamma^{T}\hat{\beta}\pm t*\widehat{SE}$ for unknown variance
	- Test–CI duality: reject $H_{0}:\theta=b$ at level $\alpha$ iff $b$ is outside the $100(1-\alpha)\%$ CI
	- **General rule of thumb: If $\sigma$ is known use all things $Z$ if unknown use all things $t$**
	- For two sided p value of $H_{0}:\gamma^{T}\beta=b$ we have $p=\mathbb{P}_{H_{0}}(|T|\geq|t_{obs}|)=2F(-|t_{obs}|)$ where $T=\frac{\gamma^{T}\hat{\beta}-b}{s\sqrt{ v_{\gamma} }}$ and $t_{obs}$ is just plugging in everything for actual data.
	- $RSS=\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}\implies s^{2}=\frac{RSS}{n-p}$. Since $||Q_{2}^{T}y||_{2}^{2}=||\hat{\epsilon}||_{2}^{2}=RSS$ and $Q_{2}^{T}y\sim N_{n-p}(0_{n-p},\sigma^{2}I_{n-p})\implies \frac{RSS}{\sigma^{2}}\sim \chi^{2}_{n-p}\implies \mathbb{E}\left[ \frac{RSS}{\sigma^{2}} \right]=n-p\implies \mathbb{E}[RSS]=\sigma^{2}(n-p)$. Thus, $\mathbb{E}[s^{2}]=\mathbb{E}\left[ \frac{RSS}{n-p} \right]=\sigma^{2}$ and $\mathbb{E}\left[ \frac{RSS}{n} \right]=\frac{\sigma^{2}(n-p)}{n}$.
- Inference for Vector Targets
	- Let $V_{1}\sim\chi_{d_{1}}^{2},V_{2}\sim\chi_{d_{2}}^{2}$ with $V_{1}\perp\!\!\!\perp V_{2}$. Then $\frac{\frac{V_{1}}{d_{1}}}{\frac{V_{2}}{d_{2}}}\sim F_{d_{1},d_{2}}$.
	- $\frac{||\hat{y}||_{2}^{2}}{\sigma^{2}}\sim \chi^{2}_{p}$ under $H_{0}:\beta=0_{p}$ (important for making mean 0; note d.o.f. is p here because $||\hat{y}||_{2}^{2}=||Q_{1}Q_{1}^{T}{y}||=||Q_{1}^{T}{y}||$ and $Q_{1}^{T}y$ lives in $\mathbb{R}^{p}$). $\frac{||\hat{\epsilon}||_{2}^{2}}{\sigma^{2}}\sim \chi^{2}_{n-p}$ always hence $\frac{\frac{||\hat{y}||_{2}^{2}}{p}}{\frac{||\hat{\epsilon}||_{2}^{2}}{n-p}}\sim F_{p,n-p}$ under $H_{0}:\beta=0_{p}$.
	- $t_{n-p}^{2}\overset{d}{=}F_{1,n-p}$
	- More generally to test $H_{0}:\beta_{M}=0$ we have $\frac{\frac{y^{T}(P_{X}-P_{X_{-M}})y}{|M|}} {\frac{y^{T}P_{X}^{\perp}y}{n-p}}\sim F_{|M|,n-p}$ i.e. we do $P_{full}-P_{null}$ in numerator to evaluate how much more the full model explains the null and the denominator examines what the model leaves unexplained and estimates $\sigma^{2}$ from it. Dividing by degrees of freedom is important to have each in "noise per dimension."
	- Further generalizing, we have $H_{0}:C\beta=0_{q},C\in \mathbb{R}^{q\times p}\iff\beta\in \mathcal{N}(C)$. Hence $\beta=K\gamma$ for some $\gamma\in \mathbb{R}^{r}$ thus $y=X\beta+\epsilon$ under $H_{0}\implies y=(XK)\gamma+\epsilon$. Thus, our $P_{null}=P_{XK}$ giving us $\frac{\frac{y^{T}(P_{X}-P_{XK})y}{q}} {\frac{y^{T}(I-P_{X})y}{n-p}}\sim F_{q,n-p}$  where $q=p-r$. To find $\hat{\beta}_{R}$ (restricted $\hat{\beta}$) we find the coefficients under the restriction $\hat{\phi}=(K^{T}X^{T}XK)^{-1}K^{T}X^{T}y$ and then recover $\hat{\beta}_{R}=K\hat{\phi}$.
	- Affine generalization: $H_{0}:C\beta=d$ then find $\beta_{0}$ such that $C\beta_{0}=d$ and get $\tilde{y}=y-X\beta_{0}$ then $\frac{\frac{\tilde{y}^{T}(P_{X}-P_{XK})\tilde{y}}{q}}{\frac{y^{T}(I-P_{X})y}{n-p}}\sim F_{q,n-p}$. Note that we keep $y$ in denominator because we still want to estimate true variance. $\beta_{0}$'s vary only through shifts in $\mathcal{N}(C)$. 
	- Final form general recipe: **Testing $H_{0}:C\beta=d$** ($C\in\mathbb{R}^{q\times p}$ full row rank, $Col(K)=\mathcal{N}(C)$, $K^{T}K=I_{r}$, $r=p-q$)
		1. Pick any $\beta_{0}$ with $C\beta_{0}=d$.
		2. Shift: $\tilde{y}=y-X\beta_{0}$.
		3. Fit the null model: $\hat{\phi}=\left((XK)^{T}XK\right)^{-1}(XK)^{T}\tilde{y}$.
		4. Shift back: $\hat{\beta}_{R}=\beta_{0}+K\hat{\phi}$, with fitted values $X\hat{\beta}_{R}=X\beta_{0}+P_{XK}\tilde{y}$. (Check: $C\hat{\beta}_{R}=d$; $\hat{\beta}_{R}$ does not depend on the choice of $\beta_{0}$.)
		5. Test:
		$$
		F=\frac{\tilde{y}^{T}(P_{X}-P_{XK})\tilde{y}/q}{y^{T}(I-P_{X})y/(n-p)}=\frac{(RSS_{R}-RSS)/q}{RSS/(n-p)}\overset{H_{0}}{\sim}F_{q,n-p}
		$$
		Reject if $F>F_{q,n-p,1-\alpha}$. The denominator can use $y$ or $\tilde{y}$: $(I-P_{X})X\beta_{0}=0_{n}$.

10/19
### Multiple Testing (Regression Setting)
We know how to do inference (in the sense of hypothesis tests and confidence intervals) for $\gamma^{T}\beta$ or to test $H_{0}:C\beta=d$.
What if we ask multiple inferential questions of the same dataset?
Ex: CIs for $\beta^{T}\gamma^{(1)},\beta^{T}\gamma^{(2)},\dots,\beta^{T}\gamma^{(k)}$ or we test $H_{0}^{(1)}:\beta_{1}=0,\dots,H_{0}^{(p)}:\beta_{p}=0$. Or we might explore and selectively report some subset of our findings.

We've talked about how individual tests and CIs have desirable properties, but what about the whole pipeline?
What we will cover today:
- Familywise Error Rate (FWER)
- Bonferroni Correction
- Halm-Bonferroni
- Scheffe Correction
- Later in semester
	- False Discovery
	- Selective Inference

Warmup: Coordinate-wise Inference and regression
Usual model and assumptions: $y=X\beta+\epsilon,\epsilon \sim N_{n}(0_{n},\sigma^{2}I_{n})$. Estimate $\hat{\beta}$ and construction CIs for $\beta_{1},\dots,\beta_{p}$.
Note $R$ will denote confidence regions (here they will be CIs, but they may just be regions later).
$\hat{R}_{j}:=\hat{\beta}_{j}\pm t_{n-p}^{-1}\left( 1-\frac{\alpha}{2} \right)s\sqrt{ e_{j}^{T}(X^{T}X)^{-1}e_{j} }$
Let $E_{j}$ be the event that the true $\{ y:\beta_{j}\in \hat{R}_{j}(y)\}$ (our confidence interval is a function of $y$ i.e. is y measurable). The whole point is we want to be able to talk about probabilities.
$\mathbb{P}(E_{j})=1-\alpha$ (for a fixed $E_{j}$)
What is the probability that ALL our CIs cover? It depends on the dependence of $\beta$'s. If they were independent we would have the intuitive result of $(1-\alpha)^{p}$ (since $1-\alpha$ for each $\beta\in \mathbb{R}^{p}$). 
Let $\delta$  be the probability that at least one of our CIs doesn't cover: $\delta=\mathbb{P}(\exists j:\beta_{j}\not\in \hat{R}_{j}(y))\implies1-\delta=\mathbb{P}(\forall j:\beta_{j}\in \hat{R}_{j})=\mathbb{P}\left[ \bigcap_{j=1}^{p}E_{j} \right]$ (this is where if independent then just becomes $(1-\alpha)^{p}$) $=1-\mathbb{P}\left[ \bigcup_{j=1}^{p}E_{j}^{c} \right]\geq1-\sum_{j=1}^{p}\mathbb{P}[E_{j}^{c}]$ (union bound of subadditivity) $=1-p\alpha$. Hence $1-\delta\geq1-p\alpha\implies\delta\leq p\alpha$.
For a fixed $\alpha$ and large $p$, this may be vacuously true, but remember that we get to choose $\alpha$.

**Definition (FWER)**: The Family Wise Error Rate (FWER) is the probability that at least one member of a family of statements is untrue.
What do we mean by an untrue statement? For CI it is $\beta_{j}\not\in \hat{R}_{j}$ and for hypothesis testing rejecting the null when it is in fact true.
So here our FWER is $\delta$.

#### Bonferroni Correction
Motivated by the union bound argument. Suppose we want to control $\delta$ at some level $\alpha_{0}$. Then construct $1-\frac{\alpha_{0}}{p}$ level confidence intervals. Then $1-\delta\geq1-\sum_{i=1}^{p}\mathbb{P}[E_{i}^{c}]=1-\frac{p\alpha_{0}}{p}=1-\alpha_{0}\implies\delta\leq\alpha_{0}$.

Example: Suppose we have tested $H_{0}^{(1)},\dots,H_{0}^{(k)}$ where each $H_{0}^{(j)}:C^{(j)}\beta=d^{(j)}$. From each of these tests we have a p-value $p^{(1)},\dots,p^{(k)}$.
Using the p-values, how should we make rejection decisions if our goal is to control $FWER\leq 0.05$.

When is Bonferroni conservative?
Still using $p^{(1)},\dots,p^{(k)}$. Under what dependence structure is Bonferroni maximally conservative?
All identical tests, i.e. k identical tests. Hence we don't need any correction since we are doing the same test k times we only need to do it once.
The bound is attained at extreme negative dependence (i.e. partition/nonoverlapping; it is easy to assume non-overlapping events are independent, but by them being partitioned/non-overlapping it limits the probability of other events).
#### Holm-Bonferroni
Uniformly more powerful than Bonferroni and requires no additional assumptions.
Claim: This procedure controls FWER at $\alpha_{0}$.
Procedure:
- Input: $K$ individually valid p-values (i.e. if you look at any particular p-value on its own it would be uniformly distributed under the null) and $\alpha_{0}$ target FWER control
	1. Sort the p-values $p_{(1)}\leq\dots\leq p_{(K)}$ (order statistics)
	2. Find $k^{*}=\min\left\{  j\in \{ 1,\dots,K \} :p_{(j)}\geq \frac{\alpha_{0}}{K+1-j} \right\}$
	3. Reject $H_{0}$'s corresponding to $p_{(1)},\dots,p_{(k^{*}-1)}$ and fail to reject the rest.
	>Note: If $k^{*}=1$ reject nothing. Also note that our smallest p-value is being compared to Bonferroni $\frac{\alpha_{0}}{K}$ and we progressively get weaker comparisons with the $p_{(2)}\geq \frac{\alpha_{0}}{K-1}$ all the way up to $p_{(K)}\geq\alpha_{0}$.

Proof of FWER control:
1. View it as closed testing procedure
2. Direct proof (doing this one)
Let $\mathcal{I}_{0}=\{ i\in \{ 1,\dots,K \}:H_{0}^{(i)}\text{ is true} \}$. Let $m_{0}=\#\{ \mathcal{I}_{0} \}$.
Claim: If we have falsely rejected a true null, then there exists an $l$ such that $p_{(l)}\leq \frac{\alpha_{0}}{m_{0}}$ where $p_{(l)}$ corresponds to a true null.
If we sort our nulls by same ordering of p-value order statistics: $H_{(1)},\dots,H_{(l)},H_{(l+1)},\dots,H_{(K)}$.
Since we are rejecting $H_{(l)}$ we can assume that $H_{(1)},\dots,H_{(l-1)}$ are rejected.
Since we rejected $H_{(l)}$ we know that $p_{(l)}\leq \frac{\alpha_{0}}{K+1-l}\leq \frac{\alpha_{0}}{m_{0}}$ (note the second inequality comes from the fact that $l-1\leq K-m_{0}\implies m_{0}\leq K-l+1$).

10/21
Holm-Bonferroni Proof Continued:
Sketch of proof
1. FWE $\implies \exists l:p_{(l)} \leq \frac{\alpha_{0}}{m_{0}}$ for a true null where $m_{0}$ is # of true nulls
2. $\mathbb{P}(FWE)=FWER\leq \mathbb{P}\left( \exists l:p_{(l)} \leq \frac{\alpha_{0}}{m_{0}} \right)$
3. $\mathbb{P}\left( \exists l: p_{(l)} \leq \frac{\alpha_{0}}{m_{0}} \right)\leq\alpha_{0}$
4. Chain these 3 things together to conclude FWER $\leq\alpha_{0}$
Step 1
Claim: If a family-wise error occurs, there must exist an $l$ such that $p_{(l)}\leq \frac{\alpha_{0}}{m_{0}}$ where $m_{0}$ is the # of true nulls (we don't know what $m_{0}$ is though).
Proof of claim by construction: Choose $l$ to correspond to $p_{(l)}$ for the true null with the smallest p-value (which must have been rejected since a FWE occurred).
If we sort our nulls by same ordering of p-value order statistics: $H_{(1)},\dots,H_{(l)},H_{(l+1)},\dots,H_{(K)}$.
Since we are rejecting $H_{(l)}$ we can assume that $H_{(1)},\dots,H_{(l-1)}$ are rejected.
Moreover, since $l$ is the first true null we rejected we know that $H_{(1)},\dots,H_{(l-1)}$ are also false nulls.
So we have $K$ total hypotheses, $m_{0}$ true nulls, and $K-m_{0}$ false nulls. 
Since we rejected $H_{(1)},\dots,H_{(l-1)}$ we know that we have at least $l-1$ false nulls, but we have at most $K-m_{0}$ false nulls hence $l-1\leq K-m_{0}\implies m_{0}\leq K-l+1$.
Since we rejected $H_{(l)}$ under Holm-Bonferroni that means that $p_{(l)}\leq \frac{\alpha_{0}}{K+1-l}\leq \frac{\alpha_{0}}{m_{0}}$ where the second inequality comes from $m_{0}\leq K-l+1$. Step 1 complete.

Step 2
A family-wise error implies the existence of $l$ satisfying $p_{(l)}\leq \frac{\alpha_{0}}{m_{0}}$ for a true null. Hence call "A family wise error occurs" event $A$ and call "the existence of $l$ satisfying $p_{(l)}\leq \frac{\alpha_{0}}{m_{0}}$ for a true null" event $B$. Since $A\implies B$ it follows that $\mathbb{P}(A)\leq \mathbb{P}(B)$. Step 2 complete.

Step 3
$\mathbb{P}\left( \exists l:p_{(l)}\leq \frac{\alpha_{0}}{m_{0}} \right)= \mathbb{P}\left( \exists l:p_{l}\leq \frac{\alpha_{0}}{m_{0}} \right)= \mathbb{P}\left( \bigcup_{\text{true nulls}}p_{l}\leq \frac{\alpha_{0}}{m_{0}} \right)$ $\leq \sum_{\text{true nulls}}\mathbb{P}\left( p_{l}\leq \frac{\alpha_{0}}{m_{0}} \right)=\sum_{\text{true null}} \frac{\alpha_{0}}{m_{0}}=m_{0} \frac{\alpha_{0}}{m_{0}}=\alpha_{0}$
Note in the third to last equality we are implicitly assuming our p-values follow a uniform distribution, but this comes from the fact that any valid p-value must be stochastically dominated by a uniform (don't need to know this, just nice to know) hence if it wasn't uniform, but was still a valid p-value it would be a $\leq$ instead of =.

Step 4
Putting it all together $FWER=\mathbb{P}(FWE)\leq \mathbb{P}(\exists l: p_{(l)}\leq \frac{\alpha_{0}}{m_{0}})\leq\alpha_{0}$. Hence we have proved that under Holm-Bonferroni $FWER\leq\alpha_{0}$.

One downside of Holm-Bonferroni is that there is no obvious prescription for confidence intervals

### Confidence Intervals (Revisited) and Simultaneous Inference
CI Options:
1. $\gamma^{T}\beta$ : $\gamma^{T}\hat{\beta}\pm t_{n-p}^{-1}\left( 1-\frac{\alpha}{2} \right)s\sqrt{ \gamma^{T}(X^{T}X)^{-1}\gamma }$
2. Now suppose we have $\gamma_{1},\dots,\gamma_{K}$ and we want CI for $\{ \gamma^{T}_{k}\beta \}_{k=1,\dots,K}$ that hold simultaneously with prob ability $1-\alpha_{0}$ : $\gamma^{T}_{k}\hat{\beta}\pm t_{n-p}^{-1}\left( 1-\frac{\alpha_{0}}{2K} \right)s\sqrt{ \gamma^{T}_{k}(X^{T}X)^{-1}\gamma_{k} }$ (Bonferroni-Corrected Confidence Intervals). Note that as $K\to \infty$ our confidence intervals become meaningless as they cover everything.

#### Scheffe Corrected CIs
Consider a set $\Gamma$ of vectors in $\mathbb{R}^{p}$ (could be infinite set, hence handling our growing $K$ concern for Bonferroni-Corrected CIs above).
For a particular $\gamma\in\Gamma$ the Scheffe corrected CI for $\gamma^{T}\beta$ is $\gamma^{T}\hat{\beta}\pm \sqrt{ pF_{p,n-p}^{-1}(1-\alpha)s^{2}\gamma^{T}(X^{T}X)^{-1}\gamma }$ .

The key idea about CI that we will exploit is that $\mathbb{P}_{\theta}(\theta\in R(y))\geq1-\alpha$ where $\theta$ is our parameter, $R$ is a confidence region, and $y$ is our random vector. So let $g:\Theta\to\Omega$ where $\Theta$ is our parameter space and $\Omega$ is a different parameter space and define $g(R)=\{ g(t): t\in R \}$. Then if $\theta\in R\implies g(\theta)\in g(R)$ and moreover this will hold $\forall g:\Theta\to\Omega$.
Consider $\Theta=\mathbb{R}^{2}$ and two functions $g_{1}(\theta)=e_{1}^{T}\theta$ and $g_{2}(\theta)=e_{2}^{T}\theta$ (pulling out the two coordinates of theta). 
Claim: Whenever $\theta\in R$ $g_{1}(\theta)\in g_{1}(R)$ and $g_{2}(\theta)\in g_{2}(R)$. Note the converse does not hold though; consider when $R$ is an ellipse in $\mathbb{R}^{2}$ then our $g_{1}$ and $g_{2}$ form lines for the boundaries of $R$ but if reconstructed would make a rectangle not an ellipse. The extra gap near the corners of this rectangle are where $g_{1}(\theta)\in g_{1}(R)$ but $\theta\not\in R$. Look at picture on phone for help (10/21 12:24). So when we are doing Bonferroni Correction we are in essence forming a rectangle/hyperrectangle that contains the confidence regions (but have a little bit of extra coverage; think of the corners).

For Scheffe we want to:
1. Build a confidence region for $\mu=\mathbb{E}[y]$
2. Push this forward to get a confidence region for $\beta$
3. Push forward to get a confidence interval for $\gamma^{T}\beta$

Step 1
$\frac{||\hat{\mu}-\mu||_{2}^{2}}{\sigma^{2}}\sim \chi_{p}^{2}$ since $||\hat{\mu}-\mu||^{2}_{2}=y^{T}P_{X}y$ and we can follow typical argument for showing chi squared.
We also know that $\frac{(n-p)s^{2}}{\sigma^{2}}\sim \chi_{n-p}^{2}$. Hence $\frac{||\hat{\mu}-\mu||_{2}^{2}/p}{s^{2}}\sim F_{p,n-p}$. Hence $\{ \mu: \frac{||\hat{\mu}-\mu||_{2}^{2}/p}{s^{2}}\leq F^{-1}_{p,n-p}(1-\alpha)\}$ which will be a ball in the $Col(X)$.

10/26
Side notes (before getting back to lecture material):
Valid p-values are super uniform under the null i.e. they satisfy $\mathbb{P}_{H_{0}}(p\leq t)\leq t$. Uniform is super uniform, and with mass shifted to the right it is super uniform (like right triangle with hypotenuse coming out from origin). 
Going back, householder reflectors are generally not rotation matrices. (minor correction)

### Power of Our Tests
What happens if $H_{0}$ isn't true?
**Definition (Power)**: The probability that our test rejects $H_{0}$ when $H_{0}$ is false.
>Note: Since the alternative hypothesis is often composite (e.g. $\exists$ many $\beta$ satisfying $\beta\neq0$) power is often considered a function of a specific alternative and the design (which includes $n$)

Why should we care about power?
- Lets us consider type 2 errors (power = 1 - $\mathbb{P}$(type 2 error))
- Lets you rule out silly, but otherwise valid testing regimes e.g. size $\alpha$ test where we always take $p\sim U(0,1)$ independent of our data. In this example it has size and power $\alpha$.
- Helps us plan studies

**Power Analysis**
Justification using literature, rhetoric, and calculations that a study is worth doing. For example, you want to test a drug on mice with null that your drug has no effect. A power analysis can help you determine the number of mice you need to achieve your desired power.

#### Noncentral t,$\chi^{2}$, and $F$ distributions
**Noncentral t**
Let $W\sim N_{1}(\delta,1)$. Let $V\sim \chi^{2}_{m}$ with $W\perp\!\!\!\perp V$. Then $\frac{W}{\sqrt{ \frac{V}{m} }}\sim t_{m}(\delta)$ (follows t distribution with $m$ d.o.f. and non-centrality parameter $\delta$). 

**Noncentral $\chi^{2}$**
Let $w_{1},\dots,w_{m}{\sim}N_{1}(\xi_{i},1)$ with $w_{i}$'s independent. Hence $W\sim N_{m}(\xi,I_{m})$. Let $\lambda=\sum_{i=1}^{m}\xi_{i}^{2}=||\xi||_{2}^{2}$. Then if we take $V = \sum_{i=1}^{m}w_{i}^{2}=||W||_{2}^{2}$ then $V\sim \chi^{2}_{m}(\lambda)$ where $\lambda$ is our non-centrality parameter.

**Noncentral $F$**
Suppose that $V_{1}\sim \chi^{2}_{q}(\lambda),V_{2}\sim \chi^{2}_{m}(0)\equiv \chi^{2}_{m}$ with $V_{1}\perp\!\!\!\perp V_{2}$. Then $\frac{\frac{V_{1}}{q}}{\frac{V_{2}}{m}}\sim F_{q,m}(\lambda)$.
Note that there is such a thing as a doubly non-central $F$ distribution when $V_{2}$ is non-central. However, this does not normally come up since the denominator is typically noise which is centered at 0. It can come up in model misspecification though because we compare against a model with some covariates left out which makes it noncentral. (Not super important, but nice to know).

**Distribution Under Alternatives**
$y=X\beta+\epsilon$ and $\epsilon \sim N_{n}(0_{n},\sigma^{2}I_{n})$ with $X\in \mathbb{R}^{n\times p}$ with $rank(X)=p<n$ and $\beta,\sigma^{2}$ both unknown.
We plan to test $H_{0}:\beta_{2}=0$ at level $\alpha$. What is the power of our test if $\beta_{2}=b$?
Q1) Warmup: what is the power when $b=0$? Answer: $\alpha$
Q2) How will we test? Answer: Our test statistic is $t:=\frac{e_{2}^{T}\hat{\beta}-0}{s\sqrt{ e_{2}^{T}(X^{T}X)^{-1}e_{2} }}$. Now reject if $|t|\geq$ critical value $t_{n-p}^{-1}\left( 1-\frac{\alpha}{2} \right)$.
Q3) What is the probability of rejection if $\beta_{2}=b$?
- When $\beta_{2}=b$ what is the distribution of t? We have $\frac{\hat{\beta}_{2}}{s\sqrt{ e^{T}_{2}(X^{T}X)^{-1}e_{2} }}$ as our test statistic and we know $\hat{\beta}_{2}\sim N_{1}(b,\sigma^{2}e_{2}^{T}(X^{T}X)^{-1}e_{2})$. Hence $\frac{\hat{\beta}_{2}}{\sigma \sqrt{ e_{2}^{T}(X^{T}X)^{-1}e_{2} }}\sim N_{1}\left( \frac{b}{\sigma \sqrt{ e_{2}^{T}(X^{T}X)^{-1}e_{2} }},1 \right)$. Also $(n-p)s^{2}\sim\sigma^{2}\chi^{2}_{n-p}\implies \frac{(n-p)s^{2}}{\sigma^{2}}\sim \chi_{n-p}^{2}$. Hence $t:=\frac{\hat{\beta}_{2}}{s\sqrt{ e^{T}_{2}(X^{T}X)^{-1}e_{2} }}\sim t_{n-p}\left(\frac{b}{\sigma \sqrt{ e_{2}^{T}(X^{T}X)^{-1}e_{2} }}\right)=t_{n-p}(\delta)$.
- Now using this gives the probability of rejection as $\mathbb{P}\left( t\geq t_{n-p}^{-1}\left( 1-\frac{\alpha}{2} \right) \right)+\mathbb{P}\left( t\leq t_{n-p}^{-1}\left( \frac{\alpha}{2} \right) \right)$ where $t\sim t_{n-p}(\delta)$.

How does power change with $b$? If $b$ gets larger in magnitude (difference from zero) then power increases.
What about $\beta_{-2}$ (i.e. the other coefficients)? They don't affect power since they don't show up in non-centrality parameter.
How does sample size enter? Through $X^{T}X$ whose entries get larger as $n$ increases hence entries of $(X^{T}X)^{-1}$ decrease which causes our non-centrality parameter $\delta$ to increase. Hence, power increases as $n$ increases since power increases the more non-central we are (i.e. larger the non-centrality parameter is).

10/28
### Power of t-tests for $\gamma^{T}\beta$
$t:=\frac{\hat{\beta}_{2}}{\sqrt{ s^{2}e_{2}^{T}(X^{T}X)^{-1}e_{2} }}$
Suppose $\beta_{2}=b$ then what distribution does $t$ follow? $t\sim t_{n-p}\left( \frac{b}{\sqrt{ \sigma^{2}e_{2}^{T}(X^{T}X)^{-1}e_{2} }} \right)$
In order to arrive at this we needed to look at the $\frac{\hat{\beta}_{2}}{\sqrt{ e_{2}^{T}(X^{T}X)^{-1}e_{2} }}$ term since $\hat{\beta}_{2}\sim N(b,\sigma^{2}e_{2}^{T}(X^{T}X)^{-1}e_{2})$ so dividing by $\sqrt{ \sigma^{2}e_{2}^{T}(X^{T}X)^{-1}e_{2} }$ shifts our means and gives us variance 1 in the normal i.e. $\frac{\hat{\beta}_{2}}{\sqrt{ \sigma^{2}e_{2}^{T}(X^{T}X)^{-1}e_{2} }}\sim N\left(\frac{b}{\sqrt{ \sigma^{2}e_{2}^{T}(X^{T}X)^{-1}e_{2} }},1\right)$ .
Recall $\frac{W}{\sqrt{ \frac{V}{q} }}\sim t_{q}(\delta)$ if $W\sim N(\delta,1)$ and $V\sim \chi^{2}_{q}$ with $W\perp\!\!\!\perp V$.
Remember $s^{2}=\frac{y^{T}(I-P_{X})y}{n-p}$ and $y^{T}P_{X}^{\perp}y\sim \sigma^{2}\chi^{2}_{n-p}\implies \frac{y^{T}P_{X}^{\perp}y}{\sigma^{2}}\sim \chi^{2}_{n-p}$. Hence $\frac{s^{2}}{\sigma^{2}}=\frac{V}{q}$ in our form above. 
Hence we have all components to conclude $t\sim t_{n-p}\left( \frac{b}{\sqrt{ \sigma^{2}e_{2}^{T}(X^{T}X)^{-1}e_{2} }} \right)$.

Generally, we have $$T=\frac{\gamma^{T}\hat{\beta}}{s\sqrt{ v_{\gamma} }}\sim t_{n-p}(\delta), \qquad\delta=\frac{\gamma^{T}\beta}{\sigma \sqrt{ v_{\gamma} }}$$
Look at slides on Power in canvas.

### Non-central $F$ tests
Suppose we want to test $H_{0}:C\beta=0_{q}$ (note if affine test the logic all goes through, just more tedious book keeping).
Let $K$ be a matrix that satisfies $Col(K)=\mathcal{N}(C)$. Assume $C\in \mathbb{R}^{q\times p}$ and $K\in \mathbb{R}^{p\times p-q}$.
Also let $P=P_{X}-P_{XK}$ be a projection matrix and let $P_{0}=(I-P_{X})$.
So our $F$ statistic is $$
f:=\frac{y^{T}Py/q}{y^{T}P_{0}y/(n-p)}
$$
We reject when $f\geq F^{-1}_{q,n-p}(1-\alpha)$.
We want the distribution under the alternative.
Let $\mu=X\beta$. Then $V_{1}=\frac{y^{T}Py}{\sigma^{2}}\sim \chi^{2}_{q}\left( \frac{\mu^{T}P\mu}{\sigma^{2}} \right)$ (non-centrality parameter $\lambda=\frac{\mu^{T}P\mu}{\sigma^{2}}$)
Then $V_{2}=\frac{y^{T}P_{0}y}{\sigma^{2}}\sim \chi^{2}_{n-p}$.
Suppose we want power when $C\beta=d$. Find any $\tilde{\beta}$ satisfying $C\tilde{\beta}=d$ and let $\tilde{\mu}=X\tilde{\beta}$. Then compute $\lambda$ using $\mu=\tilde{\mu}$.
Upshot is that the parts of $\beta$ that are left free will get killed when taking quadratic form $\lambda$.

11/4
### Model Selection
In section 7 of ESL (Elements of Statistical Learning) or slightly more classical treatment Section 12 of S+L (Seeber and Lee)

Why select a model? Standard model and noise
- We are unsure of model structure (so we can have many models that could potentially model this; considering including interactions, transformations on variables, etc. we need to be able to pick models)
- Depends on what we want to do downstream

Motivations
1. Learn the true $\beta$'s
2. Predict new Observations
There can often be conflict between these two goals which can sometimes be formulated as the Bias-Variance tradeoff

#### Variable Selection
$y=X\beta+\epsilon$ with $X\in \mathbb{R}^{n\times p}$ consider $p$ large but still $n>p$.
Task is to choose a subset of predictors to use in our model
Note there are $2^{p}$ possible models (different subsets of predictors)

Challenges
1. Can't realistically consider $2^{p}$ models
2. What makes one model better than another and how can we tell using our data?

Compute $SSE_{m}$ where m denotes a particular model $m\in$ the power set of indices e.g. $m_{1}=\{ 1,3,7,10 \}$ the indices of predictors or $m_{2}=\{ 1,3,7,10,15 \}$ in which case we would say $m_{1}$ is nested in $m_{2}$. 
$$
SSE_{m}=||y-X_{m}\hat{\beta}_{m}||_{2}^{2}
$$
I.e. we restrict our data to just the $m$ columns which is $X_{m}$ then find our predicted betas $\hat{\beta}_{m}$ on $X_{m}$.

Question: Which model will we choose if we use $m^{*}=\arg\min_{m}||y-X_{m}\hat{\beta}_{m}||_{2}^{2}$? The model with all the predictors (the full model). 

Instead of this brute force approach (checking all subsets) we can do best subset regression.
$\hat{\beta}_{s}:=\arg\min_{||b||_{0}\leq s}||y-Xb||_{2}^{2}$. Recall $||b||_{0}=\#\{ i:b_{i}\neq0 \}$. (number of nonzero elements). Again if we let $s=p$ then we will find the whole model. Otherwise we are essentially limiting how many predictors we can have.

**Definition (Coefficient of Multiple Determination)**: $R^{2}=1-\frac{SSE}{SSTO}$ (SSE/Sum Squared Total) $=1 - \frac{y^{T}(I-P_{X})y}{y^{T}(I-P_{1_{n}})y}$.
Choosing the model that maximizes $R^{2}$ will just minimize $SSE$ which will always choose the largest possible model. 

Instead we will use a correction:
**Definition (Adjusted $R^{2}$)**: $R^{2}_{adj}=1- \frac{SSE/(n-p)}{SSTO/(n-1)}=1-\frac{MSE}{MSTO}$. Intuitively this adds a penalizer for adding predictors that aren't needed. This helps, but in practice it tends to over select (so doesn't penalize enough).

11/9 (no lecture — reading S+L 12.1–12.3.3)
## S+L Ch. 12: Prediction and Model Selection (12.1–12.3.3)

> Notation bridge: S+L write $\text{RSS}$ for what we call $SSE$ in lecture, $\mathbf{P}$ for $P_{X}$, and use $p$ = number of columns of the design (so $p-1$ variables + intercept). $K$ = total number of candidate explanatory variables, so the full model has $K+1$ columns.

### 12.1 Setup and Roadmap

We now assume a large pool of $K$ candidate variables $x_{1},\dots,x_{K}$ and must decide which ones to use. Two (sometimes conflicting) framings:

1. **"Pure" model selection:** the truth really is $$ Y=\beta_{0}+\beta_{1}x_{1}+\dots+\beta_{K}x_{K}+\varepsilon \tag{12.1} $$ and the job is to find which $\beta_{j}=0$.
2. **Predictive framing (more realistic):** the truth is not that simple; use the $x_{j}$'s as raw material to build the model of form (12.1) with the best predictive accuracy.

Counterintuitive point: even if the goal is pure prediction, using _every_ variable is often worse than throwing some away (especially when $K$ is large relative to $n$).

Map of the chapter (the four strategies):

- **All possible regressions (APR):** define a criterion, evaluate it on all $2^{K}$ subsets, pick the optimizer (Section 12.3 — this reading).
- **Sequential testing:** forward selection, backward elimination, stepwise (12.4). Cheap, but assumes (12.1) is true and no guarantee of optimality for any 12.3 criterion.
- **Shrinkage:** keep all variables but use biased estimators (ridge, garrote, lasso) (12.5).
- **Bayesian / model averaging** (12.6).

> Warning (12.7): if the same data are used to _select_ the model and then to _fit/infer_, the usual inference from earlier chapters is invalid — it overstates precision of estimates and accuracy of predictions.

---

### 12.2 Why Select?

#### Motivating example (Linhart & Zucchini)

True model: $Y_{i}=\exp(ax_{i}^{2}+b)+\varepsilon_{i}$, $\varepsilon_{i}\overset{iid}{\sim}N(0,\sigma^{2})$, with $a=0.02$, $b=0.1$, $\sigma=1.5$, $n=100$, $x_{i}$ equally spaced on $[1,10]$. Target: $f(5)=e^{0.6}\approx1.822$.

The analyst fits polynomials of degree $1,\dots,7$. A degree-7 polynomial can approximate $f$ almost perfectly (Fig 12.1b), so in principle it _could_ predict well. Simulating repeated data sets (Fig 12.1d):

- Degree 1: stable (low variance) but big bias — can't capture the curvature.
- Degree 7: essentially unbiased but highly variable — it is flexible enough to chase the noise.
- Minimum MSE: **cubic**. The best predictor uses 3 of the 7 available power terms.

So both too few and too many variables hurt. Now the theory.

#### Prediction Error and Model Error

Training set $(x_{i},Y_{i})$, $i=1,\dots,n$, $X\in\mathbb{R}^{n\times p}$. New design points $X_{0}\in\mathbb{R}^{m\times p}$ with new responses $Y_{0}$, $\mu_{0}=E[Y_{0}]$. Assume $\mathrm{Var}(Y)=\sigma^{2}I_{n}$, $\mathrm{Var}(Y_{0})=\sigma^{2}I_{m}$, $Y\perp!!!\perp Y_{0}$, same mean structure. Predictor: $X_{0}\hat{\beta}$ with $\hat{\beta}=(X^{T}X)^{-1}X^{T}Y$ from the training set.

Add and subtract $\mu_{0}$: $$ |Y_{0}-X_{0}\hat{\beta}|_{2}^{2}=|Y_{0}-\mu_{0}|_{2}^{2}+|\mu_{0}-X_{0}\hat{\beta}|_{2}^{2}+2(Y_{0}-\mu_{0})^{T}(\mu_{0}-X_{0}\hat{\beta}) \tag{12.4} $$ **Definition (Prediction Error)**: take expectation over the _new_ data only (so $\hat{\beta}$ is held fixed): $$ \text{PE}=E_{Y_{0}}\left[|Y_{0}-X_{0}\hat{\beta}|_{2}^{2}\right]=m\sigma^{2}+|\mu_{0}-X_{0}\hat{\beta}|_{2}^{2} \tag{12.5} $$ The cross term dies because $Y_{0}\perp!!!\perp\hat{\beta}$ and $E_{Y_{0}}[Y_{0}-\mu_{0}]=0$.

**Definition (Model Error)**: $$ \text{ME}=|\mu_{0}-X_{0}\hat{\beta}|_{2}^{2},\qquad \text{PE}=m\sigma^{2}+\text{ME} \tag{12.6–12.7} $$ $m\sigma^{2}$ is irreducible noise; ME is the only part the model controls. Minimizing PE $\iff$ minimizing ME. Note PE and ME are still random (functions of the training $Y$ through $\hat{\beta}$).

#### Expected ME when predicting at the training design ($X_{0}=X$)

Then $m=n$, $\mu_{0}=\mu=E[Y]$. Write $\varepsilon=Y-\mu$ and $P=P_{X}=X(X^{T}X)^{-1}X^{T}$. Since $X\hat{\beta}=PY=P\mu+P\varepsilon$: $$ \text{ME}=|\mu-PY|_{2}^{2}=|(I_{n}-P)\mu-P\varepsilon|_{2}^{2}=\mu^{T}(I_{n}-P)\mu+\varepsilon^{T}P\varepsilon $$ The cross term $-2\mu^{T}(I-P)P\varepsilon=0$ because $(I-P)P=P-P^{2}=0$.

> [!tip] Linear algebra used here
> 
> - $P$ is symmetric idempotent, so $(I-P)$ and $P$ project onto orthogonal subspaces ($\text{Col}(X)^{\perp}$ and $\text{Col}(X)$). Pythagoras kills the cross term.
> - $E[\varepsilon^{T}A\varepsilon]=\sigma^{2}\operatorname{tr}(A)$ when $\mathrm{Var}(\varepsilon)=\sigma^{2}I$ (S+L Thm 1.5: $E[Y^{T}AY]=\operatorname{tr}(A\Sigma)+\mu^{T}A\mu$).
> - For a projection, $\operatorname{tr}(P)=\operatorname{rank}(P)=p$.

Taking expectations: $$ E[\text{ME}]=\mu^{T}(I_{n}-P)\mu+\sigma^{2}p \tag{12.8} $$ $$ E[\text{PE}]=(n+p)\sigma^{2}+\mu^{T}(I_{n}-P)\mu \tag{12.9} $$

**Bias–variance reading of (12.8).** Define

- $\text{TOTAL BIAS}=|\mu-E[X\hat{\beta}]|_{2}=|\mu-P\mu|_{2}$, so $(\text{TOTAL BIAS})^{2}=\mu^{T}(I-P)\mu$ (Exercise 12a.1). Zero iff $\mu\in\text{Col}(X)$.
- $\text{TOTAL VARIANCE}=\operatorname{tr}(\mathrm{Var}[X\hat{\beta}])=\operatorname{tr}(\sigma^{2}P)=\sigma^{2}p$.

$$ E[\text{ME}]=(\text{TOTAL BIAS})^{2}+\text{TOTAL VARIANCE} $$ Adding a (linearly independent) column: $\text{Col}(X)$ grows so $|(I-P)\mu|^{2}$ can only shrink (bias $\downarrow$), but $p$ goes up by 1 (variance $\uparrow$ by $\sigma^{2}$). The best model balances these.

> Connection to ESL Ch. 7: predicting at the same $x_{i}$'s is ESL's "in-sample error". The $2p\sigma^{2}$-type optimism that shows up below in $C_{p}$ is the same idea.

#### When the true model _is_ (12.1): can a wrong (smaller) model predict better?

Partition $X=(X_{1},X_{2})$, $\beta=(\beta_{1}^{T},\beta_{2}^{T})^{T}$ with $X_{1}$ having $p$ columns, $X_{2}$ the remaining $K-p+1$. Suppose $\beta_{2}\neq0$. Predict $x^{T}\beta$ at $x=(x_{1}^{T},x_{2}^{T})^{T}$ with either:

- **Biased (submodel)** predictor $x_{1}^{T}\hat{\beta}_{1}$, $\hat{\beta}_{1}=(X_{1}^{T}X_{1})^{-1}X_{1}^{T}Y$, or
- **Unbiased (full)** predictor $x^{T}\hat{\beta}$.

Let $L=(X_{1}^{T}X_{1})^{-1}X_{1}^{T}X_{2}$ (the "alias matrix" — regress each column of $X_{2}$ on $X_{1}$). From Section 9.2, omitted variables give $E[\hat{\beta}_{1}]=\beta_{1}+L\beta_{2}$. Define $$ h=L^{T}x_{1}-x_{2},\qquad M=\left[X_{2}^{T}(I_{n}-P_{1})X_{2}\right]^{-1},\qquad P_{1}=X_{1}(X_{1}^{T}X_{1})^{-1}X_{1}^{T} $$ Bias of submodel predictor: $x_{1}^{T}E[\hat{\beta}_{1}]-x^{T}\beta=x_{1}^{T}L\beta_{2}-x_{2}^{T}\beta_{2}=h^{T}\beta_{2}$. With $m=1$ in (12.5): $$ \text{Submodel: }E[\text{PE}]=\sigma^{2}+\mathrm{var}[x_{1}^{T}\hat{\beta}_{1}]+(h^{T}\beta_{2})^{2} \tag{12.10} $$ $$ \text{Full: }E[\text{PE}]=\sigma^{2}+\mathrm{var}[x_{1}^{T}\hat{\beta}_{1}]+\sigma^{2}h^{T}Mh \tag{12.11} $$

> [!note] Why (12.11)? (fills in the Section 9.2 step) In the full fit, $\hat{\beta}_{2}=MX_{2}^{T}(I-P_{1})Y$ and $\hat{\beta}_{1}^{\text{full}}=\hat{\beta}_{1}-L\hat{\beta}_{2}$. So $x^{T}\hat{\beta}=x_{1}^{T}\hat{\beta}_{1}-h^{T}\hat{\beta}_{2}$. Also $\mathrm{Cov}(\hat{\beta}_{1},\hat{\beta}_{2})\propto X_{1}^{T}(I-P_{1})X_{2}=0$ and $\mathrm{Var}(\hat{\beta}_{2})=\sigma^{2}M$. Hence $\mathrm{var}[x^{T}\hat{\beta}]=\mathrm{var}[x_{1}^{T}\hat{\beta}_{1}]+\sigma^{2}h^{T}Mh$: **the full model always pays extra variance** $\sigma^{2}h^{T}Mh\ge0$.

So the submodel wins at $x$ iff $$ (h^{T}\beta_{2})^{2}<\sigma^{2}h^{T}Mh \tag{12.12} $$ $M$ is positive definite (Lemma, S+L 3.7), so by the generalized Cauchy–Schwarz inequality (A.4.11) $$ (h^{T}\beta_{2})^{2}\le (h^{T}Mh)(\beta_{2}^{T}M^{-1}\beta_{2})\quad\forall h $$ (Proof idea: $h^{T}\beta_{2}=(M^{1/2}h)^{T}(M^{-1/2}\beta_{2})$, then ordinary Cauchy–Schwarz.) Therefore if $$ \beta_{2}^{T}M^{-1}\beta_{2}=\beta_{2}^{T}X_{2}^{T}(I_{n}-P_{1})X_{2}\beta_{2}<\sigma^{2} $$ the **submodel predicts better at every $x$**, even though it is the wrong model.

> [!tip] Tie-back to our 10/28 notes (non-central $F$) $\lambda=\beta_{2}^{T}X_{2}^{T}(I-P_{1})X_{2}\beta_{2}/\sigma^{2}$ is exactly the non-centrality parameter of the $F$-test of $H_{0}:\beta_{2}=0$ (it's $\mu^{T}(P_{X}-P_{1})\mu/\sigma^{2}$ with $\mu=X\beta$). So: **if $\lambda<1$, drop $X_{2}$ for prediction.** Small signal relative to noise $\Rightarrow$ the bias you incur is cheaper than the variance you'd pay to remove it.

Same trade-off as the polynomial example: more variables $\Rightarrow$ less bias, more variance.

---

### 12.3 Choosing the Best Subset

Strategy: least squares on a chosen subset; pick the subset by optimizing a criterion. Four families of criteria:

1. Goodness of fit (12.3.1)
2. Estimates of prediction error / model error (12.3.2)
3. Estimates of distributional discrepancy, i.e. KL (12.3.3)
4. Approximations to posterior probabilities (12.3.4 — not in this reading)

#### 12.3.1 Goodness-of-Fit Criteria

RSS alone is useless for comparing models of different size: if $S_{1}\subset S_{2}$ then $\text{RSS}(S_{2})\le\text{RSS}(S_{1})$ (adding even pure-noise columns lowers RSS, since you project onto a bigger subspace). It _is_ fine for comparing models with the same number of variables. Need a size correction.

**Option 1:** $S_{p}^{2}=\text{RSS}_{p}/(n-p)$ — choose the smallest.

**Option 2 — Adjusted $R^{2}$**: $$ \bar{R}_{p}^{2}=1-(1-R_{p}^{2})\frac{n-1}{n-p} \tag{12.14} $$ Choose the largest.

_Motivation via the $F$-test against the full model._ With $K$ variables available and the current model using $p-1<K$ of them, the $F$-statistic for testing the submodel against the full model (Exercises 4c.3) is $$ F_{p}=\frac{R_{K+1}^{2}-R_{p}^{2}}{1-R_{K+1}^{2}}\cdot\frac{n-K-1}{K-p+1} \tag{12.15} $$ Solving for $1-R_{p}^{2}$: $$ 1-R_{p}^{2}=(1-R_{K+1}^{2}),\frac{(K-p+1)F_{p}+n-K-1}{n-K-1} \tag{12.16} $$ Plug into (12.14): $$ 1-\bar{R}_{p}^{2}=\underbrace{(1-R_{K+1}^{2})\frac{n-1}{n-K-1}}_{=,1-\bar{R}_{K+1}^{2}}\cdot\frac{(K-p+1)F_{p}+n-K-1}{n-p} $$ If $F_{p}>1$, the numerator of the last fraction exceeds $(K-p+1)+n-K-1=n-p$, so the fraction is $>1$ and $$ \bar{R}_{p}^{2}<\bar{R}_{K+1}^{2} $$ So **adjusted $R^{2}$ prefers the bigger model exactly when $F_{p}>1$** — and large $F_{p}$ is evidence for the bigger model. (Note the threshold is $1$, far more lenient than an $F$ critical value — foreshadows $\bar{R}^{2}$ including too many variables.)

**Equivalence with $S^{2}$.** With $SSY=\sum_{i}(Y_{i}-\bar{Y})^{2}$ (our $SSTO$) and $1-R_{p}^{2}=\text{RSS}_{p}/SSY$: $$ \bar{R}_{p}^{2}=1-\frac{\text{RSS}_{p}/(n-p)}{SSY/(n-1)}=1-\frac{S_{p}^{2}}{SSY/(n-1)} $$ $SSY$ doesn't depend on the model, so max $\bar{R}^{2}\iff$ min $S_{p}^{2}$. Options 1 and 2 are the same criterion.

#### 12.3.2 Criteria Based on Prediction Error

$E[\text{ME}]$ in (12.8) involves the unknown $\mu$, so we need to _estimate_ it.

##### Mallows' $C_{p}$

Fit a $p$-parameter model with $X_{p}$, $P_{p}=X_{p}(X_{p}^{T}X_{p})^{-1}X_{p}^{T}$. By Thm 1.5 (with $\mathrm{Var}(Y)=\sigma^{2}I$, $\operatorname{tr}(I-P_{p})=n-p$): $$ E[\text{RSS}_{p}]=E[Y^{T}(I_{n}-P_{p})Y]=\mu^{T}(I_{n}-P_{p})\mu+(n-p)\sigma^{2}=E[\text{ME}]+(n-2p)\sigma^{2} \tag{12.17} $$ using (12.8). Rearranging, $\dfrac{E[\text{ME}]}{\sigma^{2}}=\dfrac{E[\text{RSS}_{p}]}{\sigma^{2}}+2p-n$. So given an estimate $\hat{\sigma}^{2}$: $$ C_{p}=\frac{\text{RSS}_{p}}{\hat{\sigma}^{2}}+2p-n \tag{12.18} $$ estimates the **scaled expected model error** $E[\text{ME}]/\sigma^{2}$.

If the model fits well ($\mu$ nearly in $\text{Col}(X_{p})$, so $\mu^{T}(I-P_{p})\mu\approx0$): $$ E[C_{p}]\approx\frac{\mu^{T}(I-P_{p})\mu}{\sigma^{2}}+(n-p)+2p-n\approx p \tag{12.19} $$ **$C_{p}$ plot:** plot $C_{p}$ vs. $p$ for all subsets; models near the line $C_{p}=p$ fit well; models well above it are biased. Use it to see which variables matter.

_Usual choice of $\hat{\sigma}^{2}$:_ from the full model, $\hat{\sigma}^{2}=\text{RSS}_{K+1}/(n-K-1)$. Then automatically $C_{K+1}=K+1$.

_Relation to $\bar{R}^{2}$:_ $\text{RSS}_{p}/\text{RSS}_{K+1}=(1-R_{p}^{2})/(1-R_{K+1}^{2})$, so $$ C_{p}=\frac{(1-R_{p}^{2})(n-K-1)}{1-R_{K+1}^{2}}-n+2p $$ and after substituting $1-R_{p}^{2}=(1-\bar{R}_{p}^{2})\frac{n-p}{n-1}$, $$ C_{p}-p=(n-p),\frac{\bar{R}_{K+1}^{2}-\bar{R}_{p}^{2}}{1-\bar{R}_{K+1}^{2}} $$ If $n\gg p$, $(n-p)$ is roughly constant across models, so **min $(C_{p}-p)\approx$ max $\bar{R}_{p}^{2}$**.

> Caveat: Mallows himself _discouraged_ picking the model with smallest $C_{p}$ (same for $\bar{R}^{2}$/$S^{2}$). The formula $E[C_{p}]\approx p$ is for a model fixed in advance; minimizing over models introduces selection bias (Example 12.1 below; more in 12.9).

##### Cross-Validation

Ideal: a fresh test set $(x_{0i},Y_{0i})$, $i=1,\dots,m$, and $$ \frac{1}{m}\sum_{i=1}^{m}(Y_{0i}-x_{0i}^{T}\hat{\beta})^{2} \tag{12.20} $$ No new data? Split the training set: hold out a set $D$ of $d$ cases, fit on the other $n-d$, compute (12.20) on $D$ to get $\widehat{\text{PE}}(D)$; repeat over many $D_{1},D_{2},\dots$ and average. Tension: too few fitting cases $\Rightarrow$ poor predictor; too few test cases $\Rightarrow$ noisy PE estimate.

**Leave-one-out, CV(1)** ($d=1$): let $\hat{\beta}_{(i)}$ be the fit without case $i$. $$ \text{CV}(1)=\frac{1}{n}\sum_{i=1}^{n}\left(Y_{i}-x_{i}^{T}\hat{\beta}_{(i)}\right)^{2} \tag{12.21} $$ No need to refit $n$ times. Using the deletion formula (10.5), $\hat{\beta}_{(i)}=\hat{\beta}-\dfrac{(X^{T}X)^{-1}x_{i}e_{i}}{1-h_{i}}$ with $e_{i}=Y_{i}-x_{i}^{T}\hat{\beta}$, $h_{i}=x_{i}^{T}(X^{T}X)^{-1}x_{i}$: $$ Y_{i}-x_{i}^{T}\hat{\beta}_{(i)}=e_{i}+\frac{h_{i}e_{i}}{1-h_{i}}=\frac{e_{i}}{1-h_{i}} \tag{12.22} $$ $$ \text{CV}(1)=\frac{1}{n}\sum_{i=1}^{n}\left(\frac{e_{i}}{1-h_{i}}\right)^{2} \tag{12.23} $$ (This is the PRESS statistic / $n$.)

> [!tip] Linear algebra used here (10.5) comes from the Sherman–Morrison rank-one update: $(X^{T}X-x_{i}x_{i}^{T})^{-1}=(X^{T}X)^{-1}+\dfrac{(X^{T}X)^{-1}x_{i}x_{i}^{T}(X^{T}X)^{-1}}{1-h_{i}}$. Removing a row of $X$ is a rank-one downdate of $X^{T}X$.

**CV(1) overestimates PE.** Let $\eta=(I-P)\mu$ (bias vector), $\eta_{i}$ its $i$-th entry. Since $e=(I-P)Y=\eta+(I-P)\varepsilon$: $$ E[e_{i}^{2}]=\eta_{i}^{2}+E[{(I-P)\varepsilon}_{i}^{2}] \tag{12.24} $$ With $D_{i}=u_{i}u_{i}^{T}$ ($u_{i}$ the $i$-th standard basis vector, so $D_{i}$ is diagonal with a single 1 in position $i$), ${(I-P)\varepsilon}_{i}^{2}=\varepsilon^{T}(I-P)D_{i}(I-P)\varepsilon$, so $$ E[{(I-P)\varepsilon}_{i}^{2}]=\sigma^{2}\operatorname{tr}[(I-P)D_{i}(I-P)]=\sigma^{2}\operatorname{tr}[D_{i}(I-P)]=\sigma^{2}(1-h_{i}) $$ (cyclic trace + idempotence). Hence $E[e_{i}^{2}]=\eta_{i}^{2}+\sigma^{2}(1-h_{i})$ and $$ E[\text{CV}(1)]=\frac{1}{n}\sum_{i=1}^{n}\left[\frac{\sigma^{2}}{1-h_{i}}+\frac{\eta_{i}^{2}}{(1-h_{i})^{2}}\right] \tag{12.25} $$ Meanwhile from (12.9) and $\sum_{i}h_{i}=\operatorname{tr}(P)=p$ (10.13): $$ E[\text{PE}]=(n+p)\sigma^{2}+|\eta|^{2}=\sum_{i=1}^{n}\left[\sigma^{2}(1+h_{i})+\eta_{i}^{2}\right] \tag{12.26} $$ Subtracting term by term: $$ E[n,\text{CV}(1)-\text{PE}]=\sum_{i=1}^{n}\left[\sigma^{2}\frac{h_{i}^{2}}{1-h_{i}}+\eta_{i}^{2}\frac{h_{i}(2-h_{i})}{(1-h_{i})^{2}}\right]\ge0 $$ since $0\le h_{i}<1$. So $n,\text{CV}(1)$ is biased **upward** for PE (worse for high-leverage points and for biased models).

**Leave-$d$-out, CV($d$).** For a deleted set $D$, let $Y_{D}$, $X_{D}$ be the corresponding rows and $H_{D}=X_{D}(X^{T}X)^{-1}X_{D}^{T}$ (the $d\times d$ block of the hat matrix). Generalizing (12.22) (Exercises 10e.2): $$ Y_{D}-X_{D}\hat{\beta}_{(D)}=(I_{d}-H_{D})^{-1}(Y_{D}-X_{D}\hat{\beta}) $$ $$ \text{CV}(d)=\binom{n}{d}^{-1}\sum_{D}(Y_{D}-X_{D}\hat{\beta})^{T}(I_{d}-H_{D})^{-2}(Y_{D}-X_{D}\hat{\beta}) $$ summing over all $d$-subsets. Infeasible for $d$ beyond 2–3 $\Rightarrow$ use random subsets or balanced incomplete block designs. **Shao (1993), Zhang (1993): CV($d$) with $d$ an appreciable fraction of $n$ gives better selection and prediction than CV(1).** (Contrast with ESL, where $K$-fold with $K=5,10$ is the practical version of this.)

##### The key caveat: selection bias

(12.19) and (12.25) hold **only if the model is specified in advance**. If you pick the model _because_ it minimizes $C_{p}$ or CV, the minimized value is optimistic.

**Example 12.1.** Known $\sigma^{2}$, no intercept, $K$ orthonormal columns ($X^{T}X=I_{K}$). Then $\hat{\beta}=X^{T}Y$ and the coefficients don't change as variables are added/dropped (S+L 3.10). For a submodel $S$ with $p$ variables, $$ \text{RSS}_{p}=Y^{T}Y-\hat{\beta}_{p}^{T}X_{p}^{T}X_{p}\hat{\beta}_{p}=Y^{T}Y-\sum_{j\in S}\hat{\beta}_{j}^{2} $$ $$ C_{p}=\frac{Y^{T}Y}{\sigma^{2}}-\sum_{j\in S}\left(\frac{\hat{\beta}_{j}^{2}}{\sigma^{2}}-2\right)-n \tag{12.28} $$ Each variable contributes independently, so **min $C_{p}$ = include exactly the $j$ with $\hat{\beta}_{j}^{2}/\sigma^{2}>2$**, i.e. $|\hat{\beta}_{j}|>\sqrt{2},\sigma$ (a hard threshold). Order $\hat{\beta}_{(1)}^{2}\ge\hat{\beta}_{(2)}^{2}\ge\dots$ and let $\hat{p}$ = number passing.

Now suppose the truth is $E[Y]=0$, so $\hat{\beta}_{j}\overset{iid}{\sim}N(0,\sigma^{2})$. For any fixed model, $E[C_{p}]=p\ge0$ (here bias is 0 for every model). But for the selected one, $$ C_{\hat{p}}=\frac{Y^{T}Y}{\sigma^{2}}-\sum_{j=1}^{\hat{p}}\left(\frac{\hat{\beta}_{(j)}^{2}}{\sigma^{2}}-2\right)-n,\qquad E\left[\frac{Y^{T}Y}{\sigma^{2}}\right]=n $$ $$ \Rightarrow\quad E[C_{\hat{p}}]=-E\left[\sum_{j=1}^{\hat{p}}\left(\frac{\hat{\beta}_{(j)}^{2}}{\sigma^{2}}-2\right)\right]\le0 $$ because every included term is positive by construction. The true scaled ME of the selected model is $\sum_{j\le\hat{p}}\hat{\beta}_{(j)}^{2}/\sigma^{2}\ge0$, so **$C_{p}$ of the chosen model underestimates its model error.** (Winner's curse: you selected the models that got lucky on this data.)

##### The Little Bootstrap (preview)

Breiman's residual-resampling method gives a nearly unbiased estimate of the PE of a _data-selected_ model (and of shrinkage predictors). Deferred to 12.5.

#### 12.3.3 Estimating Distributional Discrepancies (AIC)

**Definition (Kullback–Leibler discrepancy)**: true density $f$, model density $g$: $$ KL(f,g)=\int\log\left(\frac{f(y)}{g(y)}\right)f(y),dy $$

- Not a metric: $KL(f,g)\neq KL(g,f)$ in general. Think of it as "how far is each candidate $g$ from the fixed truth $f$".
- $KL(f,g)\ge KL(f,f)=0$ (Exercise 12b.3). Quick proof via Jensen ($\log$ concave): $-KL=E_{f}[\log(g/f)]\le\log E_{f}[g/f]=\log\int g=0$.

For a parametric family $g(y;\theta)$, write $KL(f,g;\theta)$. Since $KL=\int f\log f-\int f\log g$ and the first piece doesn't involve $g$, minimizing KL $\iff$ minimizing $$ -\int\log g(y;\theta)f(y),dy=-E_{f}[\log g(Y;\theta)] \tag{12.29} $$ Two unknowns: $\theta$ and $f$. Plug in the MLE $\hat{\theta}(Y)$ from the sample, and evaluate on an independent copy: $$ \Delta=-\int\log g(x;\hat{\theta}(Y))f(x),dx \tag{12.30} $$ $$ E[\Delta]=-\iint\log g(x;\hat{\theta}(y))f(x)f(y),dx,dy $$ $\Delta$ = (up to a constant depending only on $f$) the discrepancy between truth and the _fitted_ model. Still depends on $f$, so estimate it:

**Definition (AIC)** — estimates $2\Delta$ (more precisely $E[2\Delta]$): $$ \text{AIC}=-2\log g(Y;\hat{\theta}(Y))+2r \tag{12.31} $$ where $r=\dim(\theta)$. Applies to any likelihood model. Intuition: $-2\log g(Y;\hat{\theta})$ evaluates the fit on the same data used to fit it (optimistic); $+2r$ corrects the optimism — same spirit as the $+2p$ in $C_{p}$.

##### AIC for the normal linear model

Truth: $f=N_{n}(\mu,\sigma_{0}^{2}I_{n})$. Candidate: $g=N_{n}(X\beta,\sigma^{2}I_{n})$, $X\in\mathbb{R}^{n\times p}$ rank $p$, $\theta=(\beta^{T},\sigma^{2})^{T}$, so $r=p+1$. $$ -\log g(y;\theta)=\frac{n}{2}\log(2\pi\sigma^{2})+\frac{1}{2\sigma^{2}}(y-X\beta)^{T}(y-X\beta) $$ MLEs: $\hat{\beta}=(X^{T}X)^{-1}X^{T}Y$, $\hat{\sigma}^{2}=\text{RSS}/n$ (note: divide by $n$, not $n-p$).

Let $Y_{0}$ be an independent copy of $Y$. By Thm 1.5, $E_{Y_{0}}|Y_{0}-X\hat{\beta}|^{2}=n\sigma_{0}^{2}+|\mu-X\hat{\beta}|^{2}$ (same as (12.5)), so $$ \Delta=E_{Y_{0}}[-\log g(Y_{0};\hat{\theta}(Y))]=\frac{n}{2}\log(2\pi\hat{\sigma}^{2})+\frac{1}{2\hat{\sigma}^{2}}\left(n\sigma_{0}^{2}+|\mu-X\hat{\beta}|^{2}\right) $$ Use $\hat{\beta}\perp!!!\perp\hat{\sigma}^{2}$ (S+L Thm 3.5(iii)) to split the expectation of the product, and (12.8) for $E|\mu-X\hat{\beta}|^{2}=\sigma_{0}^{2}(p+\lambda)$ where $\lambda=\mu^{T}(I_{n}-P)\mu/\sigma_{0}^{2}$: $$ E[2\Delta]=n,E[\log(2\pi\hat{\sigma}^{2})]+(n+p+\lambda),E\left[\frac{\sigma_{0}^{2}}{\hat{\sigma}^{2}}\right] $$ And AIC simplifies because $(Y-X\hat{\beta})^{T}(Y-X\hat{\beta})/\hat{\sigma}^{2}=n$: $$ \text{AIC}=n\log(2\pi\hat{\sigma}^{2})+n+2(p+1) $$ Using $E[\sigma_{0}^{2}/\hat{\sigma}^{2}]=1+O(n^{-1})$, both $E[\text{AIC}]$ and $E[2\Delta]$ equal $nE[\log(2\pi\hat{\sigma}^{2})]+n+O(1)$. They agree up to $O(1)$, so AIC is a reasonable estimate of $E[2\Delta]$.

##### Exact bias when the model is correct ($\lambda=0$) and AIC$_{c}$

$\lambda=0\iff\mu\in\text{Col}(X)\iff f$ is in the model family. Then $n\hat{\sigma}^{2}/\sigma_{0}^{2}\sim\chi_{n-p}^{2}$, and for $W\sim\chi_{\nu}^{2}$, $E[1/W]=1/(\nu-2)$, giving $$ E\left[\frac{\sigma_{0}^{2}}{\hat{\sigma}^{2}}\right]=\frac{n}{n-p-2} \tag{12.32} $$ $$ E[2\Delta]=n,E[\log(2\pi\hat{\sigma}^{2})]+\frac{n(n+p)}{n-p-2} $$ Bias of AIC: $$ E[\text{AIC}-2\Delta]=n+2(p+1)-\frac{n(n+p)}{n-p-2}=2(p+1)-\frac{2n(p+1)}{n-p-2}=-\frac{2(p+1)(p+2)}{n-p-2} $$ $O(1)$, negative (AIC is too optimistic, worse when $p$ is large relative to $n$). Fix it exactly:

**Definition (Corrected AIC, Hurvich & Tsai 1991)**: $$ \text{AIC}_{c}=n\log(2\pi\hat{\sigma}^{2})+\frac{n(n+p)}{n-p-2} $$ which is exactly unbiased for $E[2\Delta]$ when $\lambda=0$. Equivalent common form: $\text{AIC}_{c}=\text{AIC}+\dfrac{2(p+1)(p+2)}{n-p-2}$.

##### Bias when the model is wrong ($\lambda>0$)

From (12.17), $nE[\hat{\sigma}^{2}]=\sigma_{0}^{2}(\lambda+n-p)$, so approximate $E[\sigma_{0}^{2}/\hat{\sigma}^{2}]\approx n/(\lambda+n-p)$: $$ E[\text{AIC}-2\Delta]\approx n+2(p+1)-\frac{(n+p+\lambda),n}{\lambda+n-p}=2\left(p+1-\frac{pn}{\lambda+n-p}\right) $$ which is $\approx2$ for large $n$ (the last term $\approx p$). Exact series: Hurvich & Tsai (1991).

##### Known $\sigma^{2}$: AIC $\approx C_{p}$

Now $r=p$ and $-2\log g(y;\hat{\theta})=n\log(2\pi\sigma^{2})+\text{RSS}_{p}/\sigma^{2}$. Dropping the model-free constant: $$ \text{AIC}=\frac{\text{RSS}_{p}}{\sigma^{2}}+2p \tag{12.33} $$ Compare $C_{p}=\text{RSS}_{p}/\sigma^{2}+2p-n$: **they differ only by the constant $n$, so they pick the same model.**

General penalty family: $$ \frac{\text{RSS}_{p}}{\sigma^{2}}+a_{n}p \tag{12.34} $$

- $a_{n}=2$: AIC / $C_{p}$.
- $a_{n}=\log n$: **BIC** (motivated in 12.3.4).
- Others: Hannan & Quinn (1979), Zhang (1992).

In the orthonormal, known-$\sigma^{2}$ setting of Example 12.1, minimizing (12.34) $\iff$ include variable $j$ iff $\hat{\beta}_{j}^{2}/\sigma^{2}>a_{n}$. So the penalty is literally a threshold on each coefficient's squared $z$-score.

**$a_{n}=2$ over-includes.** If all $\beta_{j}=0$, then $\hat{\beta}_{j}^{2}/\sigma^{2}\overset{iid}{\sim}\chi_{1}^{2}$ and $$ \mathbb{P}(\text{choose correct (empty) model})=\left(\mathbb{P}(\chi_{1}^{2}<2)\right)^{K}=0.8427^{K} $$ $K=10$: $0.181$. $K=20$: $0.033$. Fix: raise $a_{n}$ (choosing $a_{n}$ optimally: 12.9).

> My own comparison (not in the book): with BIC, $a_{n}=\log n$. For $n=100$, $\mathbb{P}(\chi_{1}^{2}<\log 100)\approx0.968$, so $\mathbb{P}(\text{correct})\approx0.72$ for $K=10$ and $\approx0.52$ for $K=20$. BIC is far more conservative, which is the classic AIC (prediction-oriented) vs. BIC (consistent selection) trade-off.

---

### Big Picture Summary (12.1–12.3.3)

|Criterion|Formula|Choose|What it targets|
|---|---|---|---|
|$S_{p}^{2}$ / $\bar{R}_{p}^{2}$|$\frac{\text{RSS}_{p}}{n-p}$ / $1-(1-R_{p}^{2})\frac{n-1}{n-p}$|min / max|Goodness of fit; prefers bigger model iff $F_{p}>1$|
|Mallows $C_{p}$|$\frac{\text{RSS}_{p}}{\hat{\sigma}^{2}}+2p-n$|near $p$ (plot)|$E[\text{ME}]/\sigma^{2}$|
|CV(1)|$\frac{1}{n}\sum\left(\frac{e_{i}}{1-h_{i}}\right)^{2}$|min|PE (biased upward)|
|CV($d$)|leave-$d$-out average|min|PE; better with $d$ a sizable fraction of $n$|
|AIC|$n\log(2\pi\hat{\sigma}^{2})+n+2(p+1)$|min|$E[2\Delta]$ (KL to truth)|
|AIC$_{c}$|$n\log(2\pi\hat{\sigma}^{2})+\frac{n(n+p)}{n-p-2}$|min|$E[2\Delta]$, exactly unbiased if model correct|
|$\frac{\text{RSS}_{p}}{\sigma^{2}}+a_{n}p$|$a_{n}=2$ (AIC), $\log n$ (BIC)|min|penalty $\leftrightarrow$ threshold on $\hat{\beta}_{j}^{2}/\sigma^{2}$|

Recurring themes:

1. Every criterion = (fit on training data) + (penalty for optimism). The penalty is $\approx 2p\sigma^{2}$ because $E[\text{RSS}]$ undershoots $E[\text{PE}]$ by $2p\sigma^{2}$ (compare (12.9) and (12.17)).
2. Bias–variance: $E[\text{ME}]=|(I-P)\mu|^{2}+p\sigma^{2}$.
3. All the "unbiasedness" results are for a model fixed in advance. After selecting by minimizing the criterion, the minimized value is optimistic (Example 12.1).

### Self-Check Questions

> [!question]- Why can't we just pick the model with the smallest RSS? 
> Nested models: the bigger column space always gives a projection at least as close to $Y$, so RSS always picks the full model (same issue as max $R^{2}$ from 11/4 lecture).

> [!question]- In (12.8), what happens to each term when you add a column that's already in $\text{Col}(X)$? 
> Nothing: $P$ is unchanged (same column space), so the bias is unchanged, and $\operatorname{tr}(P)=\operatorname{rank}$ doesn't increase either. (Strictly, $X^{T}X$ becomes singular, but the projection is the same.)

> [!question]- Show $(\text{TOTAL BIAS})^{2}=\mu^{T}(I-P)\mu$ (Exercise 12a.1).
>  $E[X\hat{\beta}]=PE[Y]=P\mu$, so $|\mu-P\mu|^{2}=\mu^{T}(I-P)^{T}(I-P)\mu=\mu^{T}(I-P)\mu$ using symmetry and idempotence.

> [!question]- Why is the CV(1) overestimate worst at high-leverage points? 
> Both bias terms carry factors that blow up as $h_{i}\to1$: $h_{i}^{2}/(1-h_{i})$ and $h_{i}(2-h_{i})/(1-h_{i})^{2}$.

> [!question]- Exercise 12a.2 (hint only) Model $Y_{i}=\alpha+\gamma_{1}x_{i}+\gamma_{2}z_{i}+\varepsilon_{i}$ with centered, unit-length $x,z$ and $r=\sum x_{i}z_{i}$. 
> Predictor $\bar{Y}+\hat{\gamma}_{1}x$ ignores $z$. Use $E[\hat{\gamma}_{1}]=\gamma_{1}+r\gamma_{2}$ (that's $L$ from 12.2) and $\mathrm{var}(\bar{Y}+\hat{\gamma}_{1}x)=\sigma^{2}(n^{-1}+x^{2})$. For part (b), compare with (12.12): the answer should look like a condition on $\gamma_{2}^{2}(1-r^{2})$ vs. $\sigma^{2}$.


11/11
### Bias-Variance Tradeoff
Parameter estimation: can decompose into bias/variance
Prediction (of new data):
- Correctness of predictors
- Variability of predictors

Following ESL (Elements of Statistical Learning 7.3)
Suppose we observe $y_{1},\dots,y_{n}$ along with $x_{1},\dots,x_{n}$ (i.e. training data with responses and predictors). Lets assume that each $y_{i}=f(x_{i})+\epsilon_{i}$ (can be represented as some function of $x_{i}$ + error term). Assume $\epsilon_{i}$ iid and $\mathbb{E}[\epsilon_{i}]=0,\mathrm{Var}(\epsilon_{i})=\sigma^{2}$ (more general than normal because not assuming normality of errors or linearity of predictors).
Consider some new observation at $x_{*}$ associated (but also unknown) response $y_{*}$. $y_{*}=f(x_{*})+\epsilon_{*}$.
We fit a model $\hat{f}$ using our training data, but our model class isn't necessarily correct (i.e. it may be cubic or log and we could be fitting linear model; we will see where we pay this price).
We want to reason about our **Mean Squared Prediction Error (MSPE)** (at particular $x_{*}$).
We will show that $MSPE=(Bias)^{2}+\mathrm{Var}+\text{Irreducible Error}$.
So to start $MSPE=\mathbb{E}[(y_{*}-\hat{f}(x_{*}))^{2}]=\mathbb{E}[(f(x_{*})+\epsilon_{*}-\hat{f}(x_{*}))^{2}]=\mathbb{E}[f(x_{*})^{2}+\epsilon_{*}^{2}+\hat{f}(x_{*})^{2}+2f(x_{*})\epsilon_{*}-2f(x_{*})\hat{f}(x_{*})-2\epsilon_{*}\hat{f}(x_{*})]=\mathbb{E}[f(x_{*})^{2}+\sigma^{2}+\hat{f}(x_{*})^{2}-2f(x_{*})\hat{f}(x_{*})]$ (drop the cross terms involving $\epsilon_{*}$ due to $\mathbb{E}[\epsilon_{*}]=0$ and $f(x_{*})$; also can turn $\epsilon_{*}^{2}=\sigma^{2}$ since $E[\epsilon]=0$) is constant for first term and $\epsilon_{*}\perp\!\!\!\perp \hat{f}(x_{*})$ for second term) = $\sigma^{2}+f(x_{*})^{2}]+\mathbb{E}[\hat{f}(x_{*})^{2}]-2f(x_{*})\mathbb{E}[\hat{f}(x_{*})]=\sigma^{2}+f(x_{*})^{2}]+\mathbb{E}[\hat{f}(x_{*})^{2}]-2f(x_{*})\mathbb{E}[\hat{f}(x_{*})]+\mathbb{E}[\hat{f}(x_{*})]^{2}-\mathbb{E}[\hat{f}(x_{*})]^{2}=\sigma^{2}+[f(x_{*})-\mathbb{E}[\hat{f}(x_{*})]]^{2}+[\mathbb{E}(\hat{f}(x_{*})^{2}-\mathbb{E}[\hat{f}(x_{*})]^{2})]=\sigma^{2}+Bias^{2}+\mathrm{Var}(\hat{f}(x_{*}))$

For linear models, suppose we have $p$ candidate predictors, but only those with indices $M\subset \{ 1,2,\dots,p \}$ matter. Our true model is $y=X_{M}\beta_{M}+\epsilon$ (select the $M$ relevant predictors).
Lets compare three scenarios.
1. Fit full model $y=X\beta+\epsilon$
	1. Bias: 0 because our true model is nested within 
	2. Variance: Highest variance
2. Oracle version (couldn't do in practice): Fit true model $y=X_{M}\beta_{M}+\epsilon$
	1. Bias also 0 because our true model is nested within itself
	2. Variance: Medium variance
3. Fit wrong model (in particular too small): $M'\subset M$ and we fit $y=X_{M'}\beta_{M'}+\epsilon$
	1. Bias: Nonzero because there are relevant predictors that aren't being considered
	2. Variance: Generally lowest variance (but depends) because smaller numbers of predictors

Departure from Assumptions and Remedies (See Seeber and Lee Chapters 9+10)
Diagnostics for Influential Observations
- "Unusual" $y$'s (large $\epsilon$'s) <- Outliers
- Extreme $X'$s <- High-leverage
Look at picture on phone, 11/11 12:28 (figure 9.7? in S+L) which shows that points can be both outliers and high-leverage. Will continue more on Monday.
Recall: Hat matrix $H:=P_{X}=X(X^{T}X)^{-1}X^{T}$


