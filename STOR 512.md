### Examples of Multivariable Functions (cont.)
We can always write a quadratic function in the form $f(x) = \frac{1}{2}x^{T}Qx+q^{T}x+r$. 
**Note that $Q$ is always symmetric.**
For example: $f(x) = x_{1}^{2}+x_{2}^{2}+2x_{1}x_{2}+x_{1}+2x_{2}+x_{3}+0$.
$r=0$
$q=\vec{(1,2,1)}$
We have $\frac{1}{2}(2x_{1}^{2}+2x_{2}^{2}+2x_{3}^{2}+4x_{1}x_{2})$
$$
\implies Q = 
\begin{bmatrix}
2 & 2 & 0 \\
2 & 2 & 0 \\
0 & 0 & 2
\end{bmatrix}
$$
Think of the top left as being the coefficient of $x_{1}^{2}$ and the middle 2 being the coefficient of $x_{2}^{2}$ and then the first row/column second index is 2 because it is the coefficient of $x_{1}x_{2}$ and $x_{2}x_{1}$ then you add them together (hence we have $2x_{1}x_{2}+2x_{2}x_{1}=4x_{1}x_{2}$).
What is $\nabla f(x)$? $\nabla f(x)=Qx+q\implies H=\nabla^{2}f(x)=Q$

Whole lotta stuff, mainly NLS

2/24
# Classification
## Logistic Model
$p(x)$ is the logistic sigmoid function as seen in slides
Note that $\mu$ and $\beta$ are the unknown parameters and that the term inside exp(.) is linear.

## Convexity
If f is twice differentiable then f is convex if and only if $\nabla^{2}f(x)$ is positive semidefinite.
Example: $f(x)=x_{1}+x_{2}\implies \nabla^{2}f(x)=0m$ where 0m means the 0 matrix which is positive semidefinite which implies $f(x)$ is convex.
Example 2: $f(x)=x_{1}^{2}-x_{1}x_{2}+x_{2}^{2}+x_{1}-x_{2}\implies$
$$
\nabla^{2}f(x)=
\begin{bmatrix}
2 & -1 \\
-1  & 2
\end{bmatrix}
$$ which is positive semidefinite so f is convex.
Example 3: $f(x)=x_{1}x_{2}\implies$ $$
\nabla^{2}f(x)=
\begin{bmatrix}
0 & 1 \\
1 & 0
\end{bmatrix}
$$ which is not positive semidefinite so not convex.
Note that the logistic model is a sum of a convex function and a linear function thus its loss is convex indicating a global minimizer exists for logistic regression.

Look at practice on finding Lipschitz constant $L$ depending on $f(x)$.
Example: $f(x)=\psi(a^{T}x)$ where $\psi$ is L-smooth. $\nabla f(x)=\psi'(a^{T}x)a$
Thus, $$||\nabla f(x)-\nabla f(y)||=||\psi'(a^{T}x)a-\psi'(a^{T}y)a||=||a|| |\psi'(a^{T}x)-\psi'(a^{T}y)|$$
$$
\leq L||a|||a^{T}x-a^{T}y|=L||a|||a^{T}(y-x)|\leq L||a||||a||||y-x||\leq L||a||^{2}||y-x||
$$
So our constant $L_{p}=L||a||^{2}$ for $f(x)$. Thus, $f$ is $L_{p}$-smooth.

For midterm look at summary of topics covered on canvas.
For free response it will be 1 big question with 2 or 3 subquestions (parts a-c).
Have calculator for matrix inverse and vector multiplication (won't be bigger than 3x3 for computation).
Not going to be any questions on topic 4 (Basic machine learning concepts). Wants us to know the concepts, but will not be on exam as it is primarily terminology.
May need to show orthogonal matrices/vectors (every pair of vectors is orthogonal).
No matrix norm or trace operator.
Inner products yes, but not between matrices.
Eigenvalue decomposition is also important (usually 2x2 matrix).
Convex vs nonconvex functions: convexity of one-variable is simple with second derivative. For 2 or 3 variable functions we need to check that $\nabla^{2}f(x)$ is positive semidefinite or you can express $f(x)=\psi(a^{T}x)$. Note that there **will** definitely be a question if not multiple involving this.
For gradient, hessian, and jacobian it will be on there but just computational.
For coding you will be given a piece/snippet of code and need to evaluate what it is doing. Probably solving linear least squares or Newton-Gauss method. May also be a question of if the code has an error or fill in the blank line for multiple choice.
The last question (free response) will be on Linear regression or nonlinear regression (**logistic regression will not be on this exam**). The free response may be on one or both of these topics.
So in summary the true/false and multiple choice questions will cover topics 1-3, 5-6, 10 on study guide and the free response will be on topics 7-8. Topics 4 and 9 will not be covered.
Examples are posted online with the summary.
May need to compute $R_{2}$-score which I need to review: $$
R_{2}=1-\frac{\sum|\hat{y_{i}}-y_{pi}|^{2}}{\sum(y_{l}-\bar{y})^{2}}
$$

If all principle minors are non-negative then you know the matrix is PSD. Look into principle minors. Essentially determinants of each square submatrix is positive. So in the 2x2 case you just need to check the top left entry and the determinant of the whole matrix. For 3x3 case you check top left, then determinant of top left 2x2, then determinant of whole matrix. There are tricks for 3x3 (with triangles?) you can learn to be quick.


# Feedforward NNs
If you want to capture more non-linearities add more layers because the more layers we add the more compositions that occur (of ReLu's, sigmoids, etc.). If you want to capture more linear behavior increase the size of layers. This makes sense mathematically as the larger the layer the more parameters $w,\mu$ we have for $w^{T}x+\mu$ per layer, and for more layers we have more compositions allowing more flexibility to nonlinear problems.

# Stuff For Final
Goal is to take 2 hours for final. But obviously have all 3 hours.
Going to focus on topics not covered in midterms and quizzes. So more focused on new content.
NN, back propagation, gradient descent, etc.
Topics 1-6 will only be in T/F or MC, even then won't be a heavy focus on these.
For topics 1-3 focus on stationary points, global and local minima/maxima, and saddle points
Topic 4 is removed, will not be covered at all.
For linear algebra need to know most of it (don't need to know matrix norms).
Probably a few questions on convexity.
No nonlinear regression (no topic 8) or logistic regression (topic 9).
One free response question will probably be on linear regression or SVM (topics 7 or 10).
One free response question will be on Matrix Factorization or Gradient Descent (topics 11 or 12).
There will also be MC and T/F from topics 7-12 (excluding topics 8 and 9).
One free response question will be from topics 14-16 (potentially more heavy/longer free response since it is newer content). Perhaps mathematically representing a simple 2 or 3 layer NN.
For any question about SGD he will give a concrete function like $x^{2}$ then compute the values at certain iterations (would be MC or T/F). For NN would need to be able to find number of parameters.
For gradient evaluation given concrete function, need to be able to find gradient at a certain point. Decompose a function into basic functions, going forward and backward?
For code will be given piece of code in Pytorch or Sklearn (general basic Python code) and question is going to ask you to correct the errors or missing line. 1 or 2 questions at most MC on python code stuff.
Could potentially give code and need to determine the neural network from the code for free response.
Build optimization models for NNs.
Tips: Go over homework solutions to study and see methodology. Take time to work on practice questions posted. Review scanned slides.
Last office hours is next Tuesday; not available after that.
Seats shuffled.
Can bring 2 pages of cheat sheet, front and back. Can be printed.
Look at worked through example below of AutoDiff.

Example:
Compute $f'(x)$ at $x=2$ of $f(x)=\sin(\cos(x))+\log(x)$ using the reverse (or backward) mode of AutoDiff.
Solution
Step 1: Decompose $f$ into basic functions:
$$
\begin{cases}
w_{1}=x \\
w_{2}=\cos(w_{1}) \\
w_{3}=\log(w_{1}) \\
w_{4}=\sin(w_{2}) \\
w_{5}=w_{3}+w_{4}
\end{cases}
$$
Step 2: Construct a computational graph
Input node is $x$ ($w_{1}$).
Then we have nodes for $\cos$, $\sin$, $\log$, and $+$.
The directed graph looks like $x\to \log$, $x\to \cos$, $\cos\to \sin$, $\sin\to +$, $\log\to +$.
So now we do forwards propagation to compute the diff. Start with $w_{1}=2$.

Step 3: Forward step to compute values and the derivatives of basic operations $w_{i}$
$$
\begin{cases}
w_{1}=2 \\
w_{2}=\cos(2) \\
w_{4}=\sin(w_{2})=\sin(\cos(2)) \\
w_{3}=\log(2) \\
w_{5}=w_{2}+w_{4}=\log(2)+\sin(\cos(2))
\end{cases}
$$
Also need to compute derivatives

Step 4: Reverse step to compute the derivatives
Formula: $\bar{w}_{i}:=\bar{w}_{i}+\bar{w}_{j}\frac{\partial w_{j}}{\partial w_{i}}$ where $j$ is a child of $i$
Thus we initialize $$
\begin{cases}
\bar{w}_{1}=0 \\
\bar{w}_{2}=0 \\
\bar{w}_{3}=0 \\
\bar{w}_{4}=0 \\
\bar{w}_{5}=1
\end{cases}
$$
We have derivatives:
$$
\begin{cases}
\frac{dw_{2}}{dw_{1}}=-\sin(w_{1}) \\
\frac{dw_{3}}{dw_{1}}=\frac{1}{w_{1}} \\
\frac{dw_{4}}{dw_{2}}=\cos(w_{2}) \\
\frac{dw_{5}}{dw_{4}}=1 \\
\frac{dw_{5}}{dw_{3}}=1
\end{cases}
$$
We can then use the formula to get $$
\begin{cases}
\bar{w}_{5}=1 \\
\bar{w}_{4}=0+\bar{w}_{5}\cdot \frac{dw_{5}}{dw_{4}}=0+\bar{w}_{5}\cdot1=\bar{w}_{5}=1 \\
\bar{w}_{3}=0+\bar{w}_{5}\cdot \frac{dw_{5}}{dw_{3}}=1 \\
\bar{w}_{2}=0+\bar{w}_{4}\cdot \frac{dw_{4}}{dw_{2}}=0+1\cdot \cos(w_{2})=\cos(w_{2})=\cos(\cos(2)) \\
\bar{w_{1}}=0+\bar{w}_{3}\cdot \frac{dw_{3}}{dw_{1}}+\bar{w}_{2}\cdot \frac{dw_{2}}{dw_{1}}=0+1\cdot\frac{1}{w_{1}}+\cos(w_{2})\cdot \sin(w_{1})=\frac{1}{2}+\cos(\cos(2))\cdot \sin(2)
\end{cases}
$$
Note that it is typically useful to already have all $\frac{dw_{j}}{dw_{i}}$'s computed (derivative of parent with respect to child).
Thus, we have $\bar{w}_{1}=f'(2)$.

Example from Practice Final NN code
$y=f(w,x)$ where $y$ is the output, $w$ is the weights/biases, and $x$ is the input data
$$
loss:=\frac{1}{N}\sum_{i=0}^{N} l(y_{i},f(w,x_{i}))
$$
And our optimization problem is to minimize the loss where $l$ is the loss function (could be squared error, absolute loss, etc.)
