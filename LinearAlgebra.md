## Vectors, Matrices and Tensors
- Vectors are denoted by lowercase letters as shown below
```math x = 
\begin{bmatrix}  
x_1 \\
x_2 \\
... \\ 
x_n
\end{bmatrix}
```
- Matrices are denoted by uppercase letters as shown below:

```math A =
\begin{bmatrix}
A_{1,1} & A_{1,2} \\
A_{2,1} & A_{2,2}
\end{bmatrix}
```
- Tensors are given by a single capital letter
$$A_{i,j,k}$$
## Matrices
- Matrix Multiplication
	- To multiply matrices $A$ and $B$, $A$ must have the same amount of columns as the $B$ has rows. In other words, $A$ (has the shape $m \times n$) and $B$ (has the shape $n \times p$) and the product will have the shape $m \times p$
	- The element-wise product is given by $$C_{i,j} = \sum_k A_{i,k} \cdot B_{k,j}$$
	- The dot product of two matrices with the same dimensionality is equivalent to the matrix product of $x^T y$
	- While matrix products aren't commutative, it is commutative when it is a dot product($x^Ty = (x^Ty)^T = y^Tx$)
- Inverse and Identity Matrix
	 - Identity matrix is filled with all zeros except for the diagonal which has 1's
	 - Inverse matrix is defined as: $$AA^{-1} = I_n$$
	 - For the equation $Ax = b$, both sides can be multiplied by the inverse matrix to solve as show below: $$A^{-1}Ax = A^{-1}b$$	 $$I_nx = A^{-1}b$$ $$x = A^{-1}b$$
	 - For $A^{-1}$ to exist, it must have exactly one solution for every value of b
		 - For some values of b, it is possible to have no solutions or infinitely many solutions
-Span and Linear Combinations
	- The span is all the possible combinations of a vector and a constant ($c\vec{v}$)
	- Colinear vectors are linearly dependent and the span of the vectors is a line
	- Non-colinear vectors are linear dependent and the span of the vectors is a plane
	- Linear independence is necessary to have a solution for every value of $b$
	- A square matrix is also needed to have an inverse
	- A square matrix with linear dependent columns is called a singular
## Norms
- The norm measures the size of a vector and is given by:
$$||x||_p = (\sum_i |x_i|^p)^{1/p}$$
- The most common norm is the $L^2$ norm which is known as the Euclidean norm
- The squared Euclidean norm can be calculated by $x^Tx$ 
- The $L^1$ norm is used when the difference between zero and non-zero elements is very important
- The $L^\infty$ also arises and it is the absolute value of the largest magnitude in the vector
- Measuring the size of the matrix requires the Frobenius norm given by: $||A||_F = \sqrt{\sum _{i,j}A _{i,j}^2}$
- The Frobenius norm is analogous to the $L^2$ norm
- The dot product of two vectors can be rewritten as norms as shown below:
$$x^Ty = ||x||_2||y||_2\cos\theta$$
## Special Matrices and Vectors
- Diagonal matrices have values only along the diagonal ($D_{i,j} = 0, i \neq j$)
	- Does not necessarily have to be a square matrix - it can be rectangular
- Symmetric matrices are equal to its own transpose ($A = A^T$)
- Vectors are orthogonal if $x^Ty = 0$
- If vectors are orthogonal but also have a unit norm ($||x||_2 = 1$) they are orthonormal
- In an orthogonal matrix is a matrix whose rows and columns are mutually orthonormal:
	$$A^TA = AA^T = I$$
	- This implies that $A^T = A^{-1}$
	- Orthogonal matrices are special because their inverse is very easy to compute
## Eigenvalue decomposition
- An eigenvector of a square matrix $A$ is a nonzero vector $v$ such that multiplication only affects the scale of $A$
	- $\lambda$ is the eigenvalue corresponding to this eigenvector such that
	- $Av = \lambda v$
- If a matrix has multiple linearly independent eigenvectors, the can be concatenated into a matrix $V = [v^{(1)}, v^{(2)},..., v^{(n)}]$ 
	- The same can be done with eigenvalues to form a vector $\lambda = [\lambda_1, \lambda_2, ..., \lambda_n]^T$
- Thus the eigendecomposition of $A$ is given by $A = V \text{diag}(\lambda)V^{-1}$
	- This is useful because calculating powers of $A$ become very easy ($A^2 = AA = X\Lambda X^{-1}X\Lambda X^{-1} = X \Lambda \Lambda X^{-1} = X \Lambda^2 X^{-1}$)
		- Thus, the generalized formula is $A^n = X \Lambda ^n X^{-1}$
- For the purposes of machine learning, the only matrices that require an eigendecomposition will be matrices in the form
$$A = Q\Lambda Q^T$$
	- Where $Q$ is an orthogonal matrix composed of eigenvectors and $\Lambda$ is a diagonal matrix with the associated eigenvalues on the diagonal
- Eigendecomposition can elucidate many useful facts about a matrix
	- If any eigenvalue is singular, the matrix is singular
	- Eigendecomposition can optimize expressions in the form $f(x) = x^TAx$ subject to $||x||_2 = 1$ 
		- Whenever $x$ is an eigenvector of $A$, $f$ is the corresponding eigenvalue
		- The maximum and minimum of $f$ is the maximum and minimum eigenvalue
	- If the eigenvalues ($\Lambda$) are:
		- $\Lambda > 0$ -> Positive definite
		-  $\Lambda \geq 0$ -> Positive semidefinite
		-  $\Lambda \leq 0$ -> Negative semidefinite
		-  $\Lambda < 0$ -> Negative definite
## Singular Value Decomposition
- Not every matrix will have a eigenvalue decomposition but every matrix will have a singular value decomposition (SVD)
- While eigenvalue decompositions are in the form $A = V\Lambda V^{-1}$ , SVDs are in the form $A = UDV^T$ where $U$ is an $m \times m$ matrix, $D$ is a $m \times n$ matrix and $V$ is an $n \times n$ matrix
	- $U$ and $V$ are orthogonal matrices while $D$ is a diagonal matrix
	- $U$ is known as the left-singular vectors and $V$ is known as the right-singular vectors
## Moore-Penrose Pseudoinverse
- For non-square matrices, matrix inversion cannot be done
	- If $A$ is taller than it is wide, then $A^{-1}$ will have no solution
		- The pseudoinverse yields $x$ for which $Ax - y$ is minimized in terms of Euclidean norm
	- If $A$ is wider than it is tall, then $A^{-1}$ will have multiple solutions
		- The pseudoinverse provides the solution to $x = A^+y$ with minimized Euclidean norm across all solutions
- The pseudoinverse is defined as 
$$A^{+} = \lim_{\alpha \rightarrow 0}(A^{T}A+ \alpha I)^{-1}A^T$$
- In practice, pseudoinverse matrices are calculated as
$$A^+ = VD^+U^T$$
## Trace Operator
- The trace operator sums all the values on the diagonal of a matrix
- The Frobenius norm can also be written using the trace operator
$$||A||_F = \sqrt{\text{Tr}(AA^T)}$$
- The trace operator is invariant to the transpose operator, swapping matrices that are being multiplied within the trace operator and cyclic permutation even if the resulting matrix shape is different
- Scalars also have their own trace equal to the scalar value themselves
