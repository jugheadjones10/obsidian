#flashcards/m4ml/linear-algebra




# 2.3 Solving Systems of Linear Equations

## 2.3.1 Particular and General Solution
What mathematical object is a "particular solution" or "special solution" to a system of linear equations?::It is just a single vector that is a solution to the linear system.
<!--SR:!2026-01-06,17,303-->

Assume that we have found a particular solution to a system of linear equations. How can we generate more solutions using the particular solution?::We can check if we can non-trivially generate the 0 vector using linear combinations of the columns of the matrix such that $Az=0$, where $z$ is the vector giving the 0 vector. Then adding $z$ to the particular solution can give us more solutions.
<!--SR:!2026-01-27,27,292-->

How do we generate a 0 vector from the columns of a matrix?::Look for one column that can be expressed as a linear combination of some of the other columns. Then the 0 vector is this linear combination minus the original column that the linear combination is equal to.
<!--SR:!2026-01-04,16,299-->

Given a solution to a system of linear equations that produces the 0 vector, how do we generate more solutions resulting in the 0 vector?::Any scaling of the original solution by some $\lambda \in \mathbb{R}$ will also be a solution to the system resulting in a 0 vector.
<!--SR:!2026-01-05,17,299-->

What is a "general solution" to a system of linear equations?::It is the set of **all** solutions to the linear system.
<!--SR:!2026-01-03,15,292-->

What is a general approach we can use to find the general solution to a system of linear equations in the form $Ax=b$?
?
1. Find a particular solution to $Ax=b$.
2. Find all solutions to $Ax=0$.
3. Combine the solutions from steps 1 and 2 to form the general solution.
<!--SR:!2026-01-03,15,292-->

How should we transform a matrix so that it is in a form that is convenient for finding a particular solution and for finding solutions that will result in the 0 vector?::We can use Gaussian elimination.
<!--SR:!2026-01-06,17,300-->

## 2.3.2 Elementary Transformations
Why is it that addition of two equations (or rows) in a system of linear equations does not change the solution set?
?
Adding one equation to another is an elementary row operation that preserves the set of solutions.
Concretely, replace an equation $r_i(x)=b_i$ by
$$
r_i(x) + \lambda r_j(x) \;=\; b_i + \lambda b_j.
$$
If $x$ satisfies the original system, then $r_i(x)=b_i$ and $r_j(x)=b_j$, so it also satisfies the new equation.
Conversely, if $x$ satisfies the new equation and still satisfies $r_j(x)=b_j$, then subtracting $\lambda r_j(x)=\lambda b_j$ gives $r_i(x)=b_i$.
Thus the solution set is unchanged.
<!--SR:!2026-01-02,14,292-->

What are two criteria for a matrix to be in row-echelon form?
?
1. All rows that contain only zeros are at the bottom of the matrix; correspondingly, all rows that contain at least one nonzero element are on top of rows that contain only zeros.
2. Looking at nonzero rows only, the first nonzero number from the left (also called the pivot or the leading coefficient) is always strictly to the right of the pivot of the row above it.
<!--SR:!2026-01-06,17,300-->

For a matrix in row echelon form, is it possible for a pivot to be directly above or below another pivot? Why?::It is *not* possible. By the definition of a matrix in row echelon form, for nonzero rows, the pivot is always strictly to the right of the pivot of the row above it. So we cannot have "stacked" pivot rows where the lengths of the pivot rows are the same.
<!--SR:!2026-01-14,17,331-->

What are basic variables?::They are the variables corresponding to the pivots of the matrix in row-echelon form.
<!--SR:!2026-01-03,15,290-->

What are free variables?::They are the variables corresponding to the non-pivot columns of the matrix in row-echelon form.
<!--SR:!2026-01-04,16,300-->

Why does a matrix being in row-echelon form make it easy to find a particular solution?::Row-echelon form makes it easy to find a particular solution because once we set all free (non-pivot) variables to $0$, only the pivot variables remain. Then the echelon structure lets us solve by back-substitution: the bottom pivot equation has only one unknown so we solve it first, and each pivot equation above reduces to one unknown after substituting previously found values. Repeating upward determines all pivot variables, giving a particular solution.
<!--SR:!2025-12-31,6,276-->

What are the three criteria for a matrix to be in a reduced row-echelon form?
?
1. It is in row-echelon form.
2. Every pivot is 1.
3. The pivot is the only nonzero entry in its column.
<!--SR:!2026-01-09,17,313-->

What does Gaussian elimination do?::It is an algorithm that performs elementary operations to bring a system of linear equations into reduced row-echelon form.
<!--SR:!2026-01-10,17,305-->

Why does a matrix being in reduced row-echelon form make it easy to find the general solutions of a system of linear equations?::Starting from the leftmost column and moving right, for each non-pivot column we encounter, there will be enough pivot columns to its left for the non-pivot column to be expressed as their sums and multiples. Then we can obtain a solution by assigning the basic variables to the left of our non-pivot column the same values that are in the non-pivot column. We assign -1 to the free variable corresponding to our non-pivot column, and 0 to all other remaining variables, in this way obtaining a solution to $Ax=0$.
<!--SR:!2026-01-13,13,265-->

What two properties of matrices in reduced row-echelon form make it trivial to express a non-pivot column as a linear combination of the pivot columns to its left?::For each non-zero number in a non-pivot column, there exists a pivot column to its left where the 1 is on the same row as the non-zero number. This is guaranteed because for each row of a matrix in reduced row-echelon form (that is not a 0-row), the pivot, which is the leftmost non-zero number, is 1. Secondly, it is also trivial because in all the pivot columns, the pivot is the only nonzero element in its column; therefore, when expressing a non-pivot column j as a linear combination of pivot columns, we can simply take as coefficients the entries of column j in the pivot rows.
<!--SR:!2026-01-05,13,295-->

What is the minus-1 trick for reading out the solutions $x$ of a homogeneous system of linear equations $Ax=0$, where $A \in \mathbb{R}^{k \times n},\; x \in \mathbb{R}^{n}$?
?
Augment the matrix $A$ to an $n \times n$-matrix $\tilde{A}$ by adding $n-k$ rows of the form
$$
\begin{bmatrix}
0 & \cdots & 0 & -1 & 0 & \cdots & 0
\end{bmatrix}
$$
so that the diagonal of the augmented matrix $\tilde{A}$ contains either 1 or -1. Then the columns of $\tilde{A}$ that contain the -1 as pivots are the solutions of the homogeneous equation system $Ax=0$.
<!--SR:!2026-01-05,13,296-->

What technique can you use to calculate the inverse $A^{-1}$ of a matrix $A \in \mathbb{R}^{n \times n}$?
?
To find $A^{-1}$, we need to find $X$ that satisfies $AX=I_{n}$. Then $X=A^{-1}$. To find $X$, we use the augmented matrix notation for a compact representation of this set of systems of linear equations and obtain
$$
\bigl[A \mid I_n\bigr] \;\sim\; \cdots \;\sim\; \bigl[I_n \mid A^{-1}\bigr].
$$
Hence by bringing the augmented equation system into reduced row-echelon form, we can read out the inverse on the right-hand side of the equation system.
<!--SR:!2026-01-10,17,313-->

Why does the technique of bringing an augmented equation system into reduced row-echelon form work when finding the inverse of a matrix $A \in \mathbb{R}^{n \times n}$?::When we want to find the inverse of a matrix $A$, we are essentially finding $X$ that satisfies $AX=I_{n}$. This can be interpreted as finding the solutions $X = [x_1 \mid \cdots \mid x_n]$ to a *set* of simultaneous linear equations. Then the problem becomes equivalent to solving the following systems of linear equations: $Ax_1 = e_1$, $Ax_2 = e_2$, etc. where $e_i$ is $i$-th unit vector (a 1 in position $i$, zeros elsewhere). By bringing $A$ in $\bigl[A \mid I_n\bigr]$ to reduced row-echelon form, we are also reducing all of $\bigl[A \mid e_i\bigr]$ at the same time. Once $A$ becomes $I_n$ after Gaussian elimination, the solutions to the set of linear systems can be read out column by column from the right-hand side of the linear system, and those columns concatenated is $A^{-1}$, as given by  $X = [x_1 \mid \cdots \mid x_n]$ and  $AX=I_{n}$.
<!--SR:!2025-12-30,7,278-->

## 2.3.3 Algorithms for Solving a System of Linear Equations
Skipped.


# 2.4 Vector Spaces

## 2.4.1 Groups
Consider a set $G$ and an operation $\otimes : G \times G \to G$ defined on $G$. Then $G := (G, \otimes)$ is called a *group* if the following properties hold (just list the properties, no need to explain them)
?
1. Closure of $G$ under $\otimes$
2. Associativity
3. Neutral element
4. Inverse element
<!--SR:!2026-01-11,18,318-->

What is a *group*?::Consider a set $\mathcal{G}$ and an operation $\otimes : \mathcal{G} \times \mathcal{G} \to \mathcal{G}$ defined on $\mathcal{G}$. Then $G := (\mathcal{G}, \otimes)$ is called a *group* if the properties of "Closure of $\mathcal{G}$ under $\otimes$", "Associativity", "Neutral element", and "Inverse element" hold.
<!--SR:!2026-01-10,17,326-->

What does the property of groups “Closure of $G$ under $\otimes$” mean?::$\forall x,y \in \mathcal{G} : x \otimes y \in \mathcal{G}$.
<!--SR:!2026-01-14,18,327-->

What does the property of groups "Associativity" mean?::$\forall x,y,z \in \mathcal{G} : (x \otimes y) \otimes z = x \otimes (y \otimes z)$.
<!--SR:!2026-01-11,18,318-->

What does the property of groups "Neutral element" mean?::$\exists e \in \mathcal{G} \ \forall x \in \mathcal{G} : x \otimes e = x \ \text{and} \ e \otimes x = x$.
<!--SR:!2026-01-10,17,318-->

What does the property of groups "Inverse element" mean?::$\forall x \in \mathcal{G} \ \exists y \in \mathcal{G} : x \otimes y = e \ \text{and} \ y \otimes x = e$, where $e$ is the neutral element. We often write $x^{-1}$ to denote the inverse element of $x$.
<!--SR:!2026-01-13,17,327-->

What is an Abelian Group?::It is a group that satisfies the additional property of commutativity.
<!--SR:!2026-01-11,18,318-->

What is the commutativity property of Abelian groups?::$\forall x,y \in \mathcal{G} : x \otimes y = y \otimes x.$
<!--SR:!2026-01-11,18,318-->

What is the general linear group?::The *general linear group* $GL(n,\mathbb{R})$, is the set of regular (invertible) matrices $A \in \mathbb{R}^{n \times n}$ that is a group with respect to matrix multiplication.
<!--SR:!2026-01-01,6,278-->

What do you call the set of regular (invertible) matrices $A \in \mathbb{R}^{n \times n}$ that is a group with respect to matrix multiplication?::The *general linear group* $GL(n,\mathbb{R})$.
<!--SR:!2026-01-06,13,298-->

Is the *general linear group* $GL(n,\mathbb{R})$ an Abelian group?::No, because matrix multiplication is not commutative.
<!--SR:!2026-01-06,13,298-->

## 2.4.2 Vector Spaces
For the set of vectors $x \in \mathcal{V}$, what is the inner operation and what is the outer operation?::The inner operation on $\mathcal{V}$ is $+$ (vector addition), which only acts on elements in $\mathcal{V}$ to give this mapping: $\mathcal{V} \times \mathcal{V} \to \mathcal{V}$. The outer operation is $\cdot$ (multiplication by a scalar), which is the multiplication of a vector $x \in \mathcal{V}$ by a scalar $\lambda \in \mathbb{R}$ and gives the mapping $\mathbb{R} \times \mathcal{V} \to \mathcal{V}$.
<!--SR:!2026-01-06,13,298-->

What is the definition of a real-valued *vector space* $V = (\mathcal{V}, +, \cdot)$?
?
It is a set a set $\mathcal{V}$ with two operations:
$$
+ : \mathcal{V} \times \mathcal{V} \to \mathcal{V}
$$
$$
\cdot : \mathbb{R} \times \mathcal{V} \to \mathcal{V}
$$
where the following are satisfied: $(\mathcal{V}, +)$ is an Abelian group, Distributivity, Associativity with respect to the outer operation, and Neutral element with respect to the outer operation.
<!--SR:!2026-01-09,9,258-->

What exactly is the "Distributivity" property satisfied by a real-valued *vector space* $\mathcal{V} = (\mathcal{V}, +, \cdot)$?
?
1. $\forall \lambda \in \mathbb{R},\; x,y \in \mathcal{V} : \lambda \cdot (x + y) = \lambda \cdot x + \lambda \cdot y$
2. $\forall \lambda,\psi \in \mathbb{R},\; x \in \mathcal{V} : (\lambda + \psi) \cdot x = \lambda \cdot x + \psi \cdot x$
<!--SR:!2026-01-05,10,288-->

What exactly is the "Associativity" property (with respect to the outer operation) satisfied by a real-valued *vector space* $\mathcal{V} = (\mathcal{V}, +, \cdot)$?::$\forall \lambda,\psi \in \mathbb{R},\; x \in \mathcal{V} : \lambda \cdot (\psi \cdot x) = (\lambda\psi) \cdot x$
<!--SR:!2026-01-10,17,318-->

What exactly is the "Neutral element" property (with respect to the outer operation) satisfied by a real-valued *vector space* $\mathcal{V} = (\mathcal{V}, +, \cdot)$?::$\forall x \in \mathcal{V} : 1 \cdot x = x$
<!--SR:!2026-01-09,13,307-->

## 2.4.3 Vector Subspaces
What is the definition of a vector subspace?::Let $\mathcal{V} = (\mathcal{V}, +, \cdot)$ be a vector space and $\mathcal{U} \subseteq \mathcal{V}$, $\mathcal{U} \neq \emptyset$. Then $\mathcal{U} = (\mathcal{U}, +, \cdot)$ is called a *vector subspace* of $\mathcal{V}$ (or *linear subspace*) if $\mathcal{U}$ is a vector space with the vector space operations $+$ and $\cdot$ restricted to $\mathcal{U} \times \mathcal{U}$ and $\mathbb{R} \times \mathcal{U}$. We write $\mathcal{U} \subseteq \mathcal{V}$ to denote a subspace $\mathcal{U}$ of $\mathcal{V}$.
<!--SR:!2026-01-05,5,247-->

Say that $\mathcal{U} \subseteq \mathcal{V}$ and $\mathcal{V}$ is a vector space. What properties need to be satisfied for $(\mathcal{U}, +, \cdot)$ to be a subspace of $\mathcal{V}$?
?
1. $\mathcal{U} \neq \emptyset$, in particular: $0 \in \mathcal{U}$
2. **Closure of $\mathcal{U}$:**
	a. With respect to the outer operation: $\forall \lambda \in \mathbb{R}\ \forall x \in \mathcal{U} : \lambda x \in \mathcal{U}.$
	b. With respect to the inner operation: $\forall x,y \in \mathcal{U} : x + y \in \mathcal{U}.$
<!--SR:!2026-01-09,12,311-->

What are the trivial subspaces of every vector space $\mathcal{V}$?::$\mathcal{V}$ itself and $\{0\}$.
<!--SR:!2026-01-13,17,328-->

Why is the solution set of a homogeneous system of linear equations $Ax = 0$ with $n$ unknowns $x = [x_1,\ldots,x_n]^T$ a subspace of $\mathbb{R}^n$?
?
It satisfies the conditions that a subset of a vector space needs to satisfy in order for it to be a subspace of that vector space. Let $S = \{\, x \in \mathbb{R}^n : Ax = 0 \,\}$:
1. The zero vector always satisfies the homogeneous system: $A0=0$, So $0 \in S$.
2. $S$ is closed with respect to the inner operation: If $x,y \in S$, then
$$
Ax = 0 \quad \text{and} \quad Ay = 0.
$$
Then,
$$
A(x+y) = Ax + Ay = 0 + 0 = 0,
$$
so $x + y \in S$.
3. $S$ is closed with respect to the outer operation: If $x \in S$ and $\lambda \in \mathbb{R}$, then
$$
Ax = 0.
$$
Then,
$$
A(\lambda x) = \lambda (Ax) = \lambda \cdot 0 = 0,
$$
so $\lambda x \in S$.
<!--SR:!2026-01-06,10,297-->

Why is the solution set of an inhomogeneous system of linear equations $Ax = b, b\neq 0$ not  a subspace of $\mathbb{R}^n$?
?
Let
$$
T = \{\, x \in \mathbb{R}^n : Ax = b \,\}, \qquad b \neq 0.
$$
Then this subset already fails the first requirement that it needs to contain the 0 vector:
$$
A0 = 0 \neq b.
$$
So
$$
0 \notin T.
$$
It also fails the requirement that it be closed with respect to the inner operation as well as the outer operation.
<!--SR:!2026-01-07,12,308-->

>Feel like with a really deep understanding of linear algebra I will be able to answer this: ![[Pasted image 20251221212242.png]]

# 2.5 Linear Independence
1 day (23rd Dec)

Consider a vector space $\mathcal{V}$ and a finite number of vectors $x_1,\ldots,x_k \in \mathcal{V}$. What is a *linear combination* of the vectors $x_1,\ldots,x_k$?
?
Every $v \in \mathcal{V}$ of the form
$$
v = \lambda_1 x_1 + \cdots + \lambda_k x_k
  = \sum_{i=1}^k \lambda_i x_i \in \mathcal{V}
$$
with $\lambda_1,\ldots,\lambda_k \in \mathbb{R}$ is a *linear combination* of the vectors $x_1,\ldots,x_k$.
<!--SR:!2026-01-16,19,337-->

Consider a vector space $\mathcal{V}$ with $k \in \mathbb{N}$ and $x_1,\ldots,x_k \in \mathcal{V}$. When are the vectors $x_1,\ldots,x_k$ linearly dependent?::If there is a non-trivial linear combination such that $0 = \sum_{i=1}^k \lambda_i x_i$ with at least one $\lambda_i \neq 0$, the vectors $x_1,\ldots,x_k$ are *linearly dependent*.
<!--SR:!2026-01-15,18,331-->

Consider a vector space $\mathcal{V}$ with $k \in \mathbb{N}$ and $x_1,\ldots,x_k \in \mathcal{V}$. When are the vectors $x_1,\ldots,x_k$ linearly independent?::If only the trivial solution exists for $0 = \sum_{i=1}^k \lambda_i x_i$, i.e., $\lambda_1 = \cdots = \lambda_k = 0$.
<!--SR:!2026-01-08,12,307-->

The vectors $x_1, \ldots, x_k$ are linearly dependent if at least one of them has a certain value. What is the value, and why does it make the vectors linearly dependent?::It is the 0 vector. If there is at least one 0 vector, that means we can create a non-trivial solution to $0 = \sum_{i=1}^k \lambda_i x_i$ by setting the coefficient of the 0 vector to some non-zero number, and setting the rest of the coefficients to 0.
<!--SR:!2026-01-08,12,308-->

The vectors $x_1, \ldots, x_k$ are linearly dependent if two of them have some kind of relationship to each other. What is the relationship, and why does it make the vectors linearly dependent?::It is if they are equal to each other. If two vectors are equal, that means we can create a non-trivial solution to $0 = \sum_{i=1}^k \lambda_i x_i$ by setting the coefficient of one of them to 1 and the other to -1, then setting the rest of the coefficients to 0.
<!--SR:!2026-01-10,13,311-->

Given the vectors $\{x_1, \ldots, x_k : x_i \neq 0,\ i = 1, \ldots, k\}$, with $k \ge 2$, what is the required condition for them to be linearly dependent?::They are linearly dependent if and only if at least of them is a linear combination of the others. In particular, if one vector is a multiple of another vector, i.e., $x_i = \lambda x_j, \quad \lambda \in \mathbb{R}$, then the set $\{x_1, \ldots, x_k : x_i \neq 0,\ i = 1, \ldots, k\}$ is linearly dependent.
<!--SR:!2026-01-10,13,311-->

What is a practical way of checking whether vectors $x_1, \ldots, x_k \in V$ are linearly independent?
?
Use Gaussian elimination until the matrix is in row echelon form (we do not need it to be in reduced row-echelon form). Then
- The pivot columns indicate the vectors which are linearly independent of the vectors on the left.
- The non-pivot columns can be expressed as linear combinations of the pivot columns on their left.
Therefore if there are no non-pivot columns, the vectors are linearly independent. Or, if all the columns are pivot columns, the vectors are linearly independent.
<!--SR:!2026-01-11,14,314-->

Consider a matrix in row echelon form. Why are the pivot columns in the matrix linearly independent of the vectors to its left?::Think of the shape of a matrix in row echelon form, it is in an inverted staircase shape, with the "breadth" of each step on the staircase being potentially more than 1 if there exist non-pivot columns. If we take a pivot column, which is the leftmost column on one such step of the staircase, we see that there is at least one row of the pivot column for which all entries to its left are 0. Therefore, we see that there is no way for the vectors on the left to "cancel out" that non-zero entry of the pivot column, meaning that the pivot column is linearly independent of the columns to its left (but all of them as a set might still be linearly dependent due to how the columns to the left interact among one another).
<!--SR:!2026-01-05,9,299-->

Consider a matrix in row echelon form. Why can all the non-pivot columns in the matrix be expressed as linear combinations of the pivot columns to its left?::Consider a non-pivot column. Each non-zero entry in that column is part of a pivot row, where the pivot is somewhere to the left of the entry. We can start at the bottommost entry, and assign a coefficient to the pivot column associated with that entry. Then we move up row by row, substituting in the coefficient from previous rows to find the coefficients of the pivot columns one by one to obtain a linear combination that equals the original non-pivot column.
<!--SR:!2026-01-08,11,311-->

Say we have a matrix in row echelon form. Just by looking at its pivot columns, how can we tell if the column vectors of the matrix are linearly independent?::The column vectors are linearly independent if and only if all the columns are pivot columns.
<!--SR:!2026-01-14,17,331-->

Say we have a matrix in row echelon form. Just by looking at its pivot columns, how can we tell if the column vectors of the matrix are linearly dependent?::If there is at least one non-pivot column, the column vectors are linearly dependent.
<!--SR:!2026-01-09,13,308-->

>Skipped a final remark for now, come back to it.

# 2.6 Basis and Rank

## 2.6.1 Generating Set and Basis
Consider a vector space $V=(\mathcal{V},+,\cdot)$. What is a *generating set* of $V$?::A set of vectors $\mathcal{A}=\{x_1,\ldots,x_k\}\subseteq \mathcal{V}$ is a *generating set* of $V$ if every vector $v\in\mathcal{V}$ can be expressed as a linear combination of $x_1,\ldots,x_k$.
<!--SR:!2026-01-08,8,299-->

Consider a vector space $V=(\mathcal{V},+,\cdot)$ and a set of vectors $\mathcal{A}=\{x_1,\ldots,x_k\}\subseteq \mathcal{V}$. If $\mathcal{A}$ is a generating set of $\mathcal{V}$, what is the set of all linear combinations of vectors in $\mathcal{A}$ called?::It is called the *span* of $\mathcal{A}$. If $\mathcal{A}$ spans the vector space $\mathcal{V}$, we write $\mathcal{V} = \operatorname{span}[\mathcal{A}]$ or $\mathcal{V} = \operatorname{span}[x_1,\ldots,x_k].$
<!--SR:!2025-12-29,4,319-->

Consider a vector space $V=(\mathcal{V},+,\cdot)$ and $\mathcal{A}\subseteq\mathcal{V}$. There exists no smaller set $\tilde{\mathcal{A}}\subsetneq \mathcal{A}\subseteq \mathcal{V}$ that spans $\mathcal{V}$. What is this property of $\mathcal{A}$ called?::It is *minimal*.
<!--SR:!2025-12-30,4,299-->

Let $V = (\mathcal{V}, +, \cdot)$ be a vector space and $\mathcal{B} \subseteq \mathcal{V}$, $\mathcal{B} \neq \varnothing$. If $\mathcal{B}$ is a basis of $V$, in what sense is $\mathcal{B}$ *minimal*?::$\mathcal{B}$ is the minimal generating set.
<!--SR:!2025-12-30,4,299-->

Let $V = (\mathcal{V}, +, \cdot)$ be a vector space and $\mathcal{B} \subseteq \mathcal{V}$, $\mathcal{B} \neq \varnothing$. If $\mathcal{B}$ is a basis of $V$, in what sense is $\mathcal{B}$ *maximal*?::$\mathcal{B}$ is a maximal linearly independent set of vectors in $V$, i.e., adding any other vector to this set will make it linearly dependent.
<!--SR:!2026-01-12,12,319-->

Let $V = (\mathcal{V}, +, \cdot)$ be a vector space and $\mathcal{B} \subseteq \mathcal{V}$, $\mathcal{B} \neq \varnothing$. If $\mathcal{B}$ is a basis of $V$, we know that every vector $x \in \mathcal{V}$ is a linear combination of vectors from $\mathcal{B}$. Is every such linear combination unique?
?
Yes. If we have
$$
x = \sum_{i=1}^k \lambda_i b_i \;=\; \sum_{i=1}^k \psi_i b_i
$$
and $\lambda_i, \psi_i \in \mathbb{R}$, $b_i \in \mathcal{B}$, it follows that $\lambda_i = \psi_i$, $i = 1, \ldots, k$.
<!--SR:!2026-01-19,19,339-->

Consider a vector space $V$. What does the *dimension* of $V$ mean?::It is the number of basis vectors of $V$, and is represented by $\dim(V)$.
<!--SR:!2025-12-29,4,319-->

Consider a vector space $V$. If $U \subseteq V$ is a subspace of $V$, what is the relationship between their dimensions?::$\dim(U) \le \dim(V)$. Also, $\dim(U) = \dim(V)$ if and only if $U = V$.
<!--SR:!2025-12-29,4,319-->

Is the dimension of a vector space always equal to the number of elements in a vector? Why or why not?::No. Intuitively, it seems like if a vector has, for example, 2 elements, then its "dimension" is 2, with a potential pair of basis vectors being $\begin{bmatrix} 0\\ 1 \end{bmatrix}$ and $\begin{bmatrix} 1\\ 0 \end{bmatrix}$. However, consider the vector space $V = \operatorname{span}\! \begin{bmatrix} 0\\ 1 \end{bmatrix}$. It is one-dimensional, although the basis vector possesses two elements.
<!--SR:!2025-12-29,4,319-->

How can we find a basis of a subspace $U = \operatorname{span}[x_1,\ldots,x_m] \subseteq \mathbb{R}^n$?
?
1. Write the spanning vectors as columns of a matrix $A$.
2. Determine the row-echelon form of $A$.
3. The spanning vectors associated with the pivot columns are a basis of $U$.
<!--SR:!2025-12-29,4,319-->

## 2.6.2 Rank
What is the number of linearly independent columns of a matrix $A \in \mathbb{R}^{m\times n}$ called?::It is the *rank* of $A$ and is denoted by $\mathrm{rk}(A)$.
<!--SR:!2025-12-29,4,319-->

What is the number of linearly independent rows of a matrix $A \in \mathbb{R}^{m\times n}$ called?::It is the *rank* of $A$ and is denoted by $\mathrm{rk}(A)$.
<!--SR:!2025-12-29,4,319-->

Is the column rank equal to the row rank?::Yes.
<!--SR:!2026-01-10,13,319-->

What is the dimension of the subspace $U \subseteq \mathbb{R}^m$ spanned by the columns of $A \in \mathbb{R}^{m\times n}$? And what is this subspace called?::$\dim(U)=\mathrm{rk}(A)$, and this subspace is called the *image* or *range*.
<!--SR:!2026-01-02,2,279-->

How do you find the basis of the subspace $U \subseteq \mathbb{R}^m$ spanned by the columns of $A \in \mathbb{R}^{m\times n}$?::Perform Gaussian elimination on $A$ to find the pivot columns, which will then be the basis vectors of the subspace $U$.
<!--SR:!2025-12-29,4,319-->

What is the dimension of the subspace $W \subseteq \mathbb{R}^n$ spanned by the rows of $A \in \mathbb{R}^{m\times n}$?::$\dim(W)=\mathrm{rk}(A)$.
<!--SR:!2025-12-29,4,324-->

How do you find the basis of the subspace $W \subseteq \mathbb{R}^n$ spanned by the rows of $A \in \mathbb{R}^{m\times n}$?::Perform Gaussian elimination on $A^\top$ to find the pivot columns, which will then be the basis vectors of the subspace $W$.
<!--SR:!2025-12-29,4,319-->

For all $A \in \mathbb{R}^{n\times n}$, how do we tell if it is regular (invertible) using rank?::$A$ is regular (invertible) if and only if $\mathrm{rk}(A)=n$.
<!--SR:!2026-01-06,9,299-->

For all $A \in \mathbb{R}^{m\times n}$ and all $b \in \mathbb{R}^m$ it holds that the linear equation system $Ax=b$ can be solved if and only if...(answer in terms of rank):: $\mathrm{rk}(A)=\mathrm{rk}(A \mid b),$ where $A \mid b$ denotes the augmented system.
<!--SR:!2025-12-29,4,319-->

What dimension does the subspace of solutions for $Ax=0$ possess, where $A \in \mathbb{R}^{m\times n}$?::It possesses dimension $n-\mathrm{rk}(A)$.
<!--SR:!2026-01-02,2,299-->

What is the subspace of solutions for $Ax=0$ called?::The *kernel* or the *null space*.
<!--SR:!2026-01-07,10,299-->

When does a matrix $A \in \mathbb{R}^{m\times n}$ have *full rank*?::If its rank equals the largest possible rank for a matrix of the same dimensions. In other words, the matrix has full rank if $\mathrm{rk}(A)=\min(m,n)$.
<!--SR:!2026-01-18,18,339-->

When is a matrix to be *rank deficient*?::If it does not have full rank.
<!--SR:!2025-12-29,4,319-->

>Figure out the *whys* behind all the above statements later on.

# 2.7 Linear Mappings
26th Dec - 30th Dec

Suppose we have a mapping on a vector space. What needs to be satisfied to ensure that we "preserve the structure of the vector space" over the mapping?
?
We know that a vector space is closed over the inner operation and the outer operation. A mapping $\Phi : V \to W$ preserves this structure of the vector space if
$$
\Phi(x+y) = \Phi(x) + \Phi(y)
$$
$$
\Phi(\lambda x) = \lambda \Phi(x)
$$
for all $x, y \in V$ and $\lambda \in \mathbb{R}$.
<!--SR:!2026-01-07,10,299-->

For vector spaces $V, W$, what is required for a mapping $\Phi : V \to W$ to be a *linear mapping* (or *vector space homomorphism* / *linear transformation*)?:: $\forall x,y \in V \ \forall \lambda,\psi \in \mathbb{R}:\quad \Phi(\lambda x + \psi y) = \lambda \Phi(x) + \psi \Phi(y)$.
<!--SR:!2025-12-29,4,324-->

What are two interpretations we can have about the meaning of matrices?::Matrices can represent a collection of vectors, or a linear mapping.
<!--SR:!2026-01-17,17,339-->

Consider a mapping $\Phi : \mathcal{V} \to \mathcal{W}$, where $\mathcal{V}, \mathcal{W}$ can be arbitrary sets. What does it mean for $\Phi$ to be *injective*?::$\forall x,y \in \mathcal{V}:\ \Phi(x)=\Phi(y) \Rightarrow x=y$. It means there cannot be many-to-one relationships. However, an injection might not necessarily cover every element in $\mathcal{W}$.
<!--SR:!2025-12-30,3,305-->

Consider a mapping $\Phi : \mathcal{V} \to \mathcal{W}$, where $\mathcal{V}, \mathcal{W}$ can be arbitrary sets. What does it mean for $\Phi$ to be *surjective*?::$\Phi(\mathcal{V})=\mathcal{W}$. It means that every element in $\mathcal{W}$ can be "reached" from $\mathcal{V}$ using $\Phi$.
<!--SR:!2026-01-19,19,345-->

Consider a mapping $\Phi : \mathcal{V} \to \mathcal{W}$, where $\mathcal{V}, \mathcal{W}$ can be arbitrary sets. What does it mean for $\Phi$ to be *bijective*?::It is both injective and surjective. A bijective $\Phi$ can be “undone”, i.e., there exists a mapping $\Psi : W \to V$ so that $\Psi \circ \Phi(x) = x$.
<!--SR:!2026-01-17,17,345-->

Consider vector spaces $V,W$. What is an _isomorphism_ between $V$ and $W$?::An isomorphism is a linear map $\Phi:V\to W$ that is bijective.
<!--SR:!2025-12-31,4,326-->

Consider a vector space $V$. What is an _endomorphism_ of $V$?::An endomorphism is a linear map $\Phi:V\to V$.
<!--SR:!2026-01-03,3,265-->

Consider a vector space $V$. What is an _automorphism_ of $V$?::An automorphism is a linear map $\Phi:V\to V$ that is bijective.
<!--SR:!2026-01-03,3,265-->

Consider a vector space $V$. What is the _identity mapping_ on $V$?::It is $\mathrm{id}_V:V\to V$ defined by $\mathrm{id}_V(x)=x$ for all $x\in V$.
<!--SR:!2025-12-30,3,306-->

If we have finite-dimensional vector spaces $V$ and $W$ and they are isomorphic, what can we say about the relationship between their dimensions?::$\dim(V) = \dim(W)$.
<!--SR:!2026-01-02,2,305-->

If we have finite-dimensional vector spaces $V$ and $W$ and $\dim(V) = \dim(W)$, what can we say about the type of linear mapping between them?::They are isomorphic.
<!--SR:!2026-01-02,2,286-->

>Not sure if I want to Ankify these, don't see the conceptual importance:
• For linear mappings $\Phi : V \to W$ and $\Psi : W \to X$, the mapping $\Psi \circ \Phi : V \to X$ is also linear.
• If $\Phi : V \to W$ is an isomorphism, then $\Phi^{-1} : W \to V$ is an isomorphism, too.
• If $\Phi : V \to W$, $\Psi : V \to W$ are linear, then $\Phi + \Psi$ and $\lambda \Phi$, $\lambda \in \mathbb{R}$, are linear, too.

## 2.7.1 Matrix Representation of Linear Mappings
Consider a vector space $V$ and an ordered basis $B = (b_1,\ldots,b_n)$ of $V$. For any $x \in V$, what is the coordinate vector / coordinate representation of $x$ with respect to the ordered basis $B$?
?
For any $x \in V$ we obtain a unique representation (linear combination)
$$
x = \alpha_1 b_1 + \cdots + \alpha_n b_n
$$
of $x$ with respect to $B$. Then $\alpha_1,\ldots,\alpha_n$ are the coordinates of $x$ with respect to $B$, and the vector
$$
\alpha =
\begin{bmatrix}
\alpha_1\\
\vdots\\
\alpha_n
\end{bmatrix}
\in \mathbb{R}^n
$$
is the coordinate vector/coordinate representation of $x$ with respect to the ordered basis $B$.
<!--SR:!2026-01-18,18,346-->

>Skipped this too:
>Remark. For an $n$-dimensional vector space $V$ and an ordered basis $B$ of $V$, the mapping $\Phi : \mathbb{R}^n \to V$, $\Phi(e_i)=b_i$, $i=1,\ldots,n$, is linear (and because of Theorem 2.17 an isomorphism), where $(e_1,\ldots,e_n)$ is the standard basis of $\mathbb{R}^n$.

Consider vector spaces $V, W$ with corresponding (ordered) bases $B=(b_1,\ldots,b_n)$ and $C=(c_1,\ldots,c_m)$. Moreover, we consider a linear mapping $\Phi: V \to W$. What is the transformation matrix of $\Phi$?
?
For $j \in \{1,\ldots,n\}$,
$$
\Phi(b_j) = \alpha_{1j}c_1 + \cdots + \alpha_{mj}c_m
= \sum_{i=1}^{m} \alpha_{ij}c_i
$$
is the unique representation of $\Phi(b_j)$ with respect to $C$. Then, we call the $m \times n$-matrix $A_{\Phi}$, whose elements are given by
$$
A_{\Phi}(i,j) = \alpha_{ij},
$$
the transformation matrix of $\Phi$ (with respect to the ordered bases $B$ of $V$ and $C$ of $W$).
<!--SR:!2025-12-31,3,306-->

Consider vector spaces $V, W$ with corresponding (ordered) bases $B=(b_1,\ldots,b_n)$ and $C=(c_1,\ldots,c_m)$. If $A_{\Phi}$ is the transformation matrix of $\Phi$, where in $A_{\Phi}$ can you find the coordinates of $\Phi(b_j)$ with respect to the ordered basis $C$ of $W$?::It is the $j$-th column of $A_{\Phi}$.
<!--SR:!2026-01-01,4,326-->

Consider (finite-dimensional) vector spaces $V, W$ with ordered bases $B, C$ and a linear mapping $\Phi : V \to W$ with transformation matrix $A_\Phi$. If $\hat{x}$ is the coordinate vector of $x \in V$ with respect to $B$, how do we obtain $\hat{y}$, the coordinate vector of $y = \Phi(x) \in W$ with respect to $C$?::$\hat{y} = A_\Phi \hat{x}$. The transformation matrix can be used to map coordinates with respect to an ordered basis in $V$ to coordinates with respect to an ordered basis in $W$.
<!--SR:!2026-01-01,4,326-->

## 2.7.2 Basis Change
For a linear mapping $\Phi : V \to W$, ordered bases
$$
B = (b_1,\ldots,b_n), \qquad \tilde{B} = (\tilde{b}_1,\ldots,\tilde{b}_n)
$$
of $V$ and
$$
C = (c_1,\ldots,c_m), \qquad \tilde{C} = (\tilde{c}_1,\ldots,\tilde{c}_m)
$$
of $W$, and a transformation matrix $A_\Phi$ of $\Phi$ with respect to $B$ and $C$, what is the equation for the corresponding transformation matrix $\tilde{A}_\Phi$ with respect to the bases $\tilde{B}$ and $\tilde{C}$?
?
$$
\tilde{A}_\Phi = T^{-1} A_\Phi S.
$$
Here, $S \in \mathbb{R}^{n \times n}$ is the transformation matrix of $\mathrm{id}_V$ that maps coordinates with respect to $\tilde{B}$ onto coordinates with respect to $B$, and $T \in \mathbb{R}^{m \times m}$ is the transformation matrix of $\mathrm{id}_W$ that maps coordinates with respect to $\tilde{C}$ onto coordinates with respect to $C$.

For a linear mapping $\Phi : V \to W$, ordered bases
$$
B = (b_1,\ldots,b_n), \qquad \tilde{B} = (\tilde{b}_1,\ldots,\tilde{b}_n)
$$
of $V$ and
$$
C = (c_1,\ldots,c_m), \qquad \tilde{C} = (\tilde{c}_1,\ldots,\tilde{c}_m)
$$
of $W$, and a transformation matrix $A_\Phi$ of $\Phi$ with respect to $B$ and $C$, we have that the  corresponding transformation matrix $\tilde{A}_\Phi$ with respect to the bases $\tilde{B}$ and $\tilde{C}$ is $\tilde{A}_\Phi = T^{-1} A_\Phi S$. What is $S$? What does the $j$-th column of $S$ represent?
?
$S = ((s_{ij})) \in \mathbb{R}^{n\times n}$ is the transformation matrix that maps coordinates with respect to $\tilde{B}$ onto coordinates with respect to $B$. The $j$-th column of $S$ is the coordinate representation of $\tilde{b}_j$
with respect to $B$.

For a linear mapping $\Phi : V \to W$, ordered bases
$$
B = (b_1,\ldots,b_n), \qquad \tilde{B} = (\tilde{b}_1,\ldots,\tilde{b}_n)
$$
of $V$ and
$$
C = (c_1,\ldots,c_m), \qquad \tilde{C} = (\tilde{c}_1,\ldots,\tilde{c}_m)
$$
of $W$, and a transformation matrix $A_\Phi$ of $\Phi$ with respect to $B$ and $C$, we have that the  corresponding transformation matrix $\tilde{A}_\Phi$ with respect to the bases $\tilde{B}$ and $\tilde{C}$ is $\tilde{A}_\Phi = T^{-1} A_\Phi S$. What is $T$? What does the $k$-th column of $T$ represent?
?
$T = ((t_{lk})) \in \mathbb{R}^{m\times m}$ is the transformation matrix that maps coordinates with respect to $\tilde{C}$ onto coordinates with respect to $C$. The $k$-th column of $T$ is the coordinate representation of $\tilde{c}_k$
with respect to $C$.

>Skipped the proof of Theorem 2.20 (Basis Change) because the intuitive explanation is much clearer and more straightforward.

For a linear mapping $\Phi : V \to W$, ordered bases
$$
B = (b_1,\ldots,b_n), \qquad \tilde{B} = (\tilde{b}_1,\ldots,\tilde{b}_n)
$$
of $V$ and
$$
C = (c_1,\ldots,c_m), \qquad \tilde{C} = (\tilde{c}_1,\ldots,\tilde{c}_m)
$$
of $W$, and a transformation matrix $A_\Phi$ of $\Phi$ with respect to $B$ and $C$, we have that the  corresponding transformation matrix $\tilde{A}_\Phi$ with respect to the bases $\tilde{B}$ and $\tilde{C}$ is $\tilde{A}_\Phi = T^{-1} A_\Phi S$. What is the equivalent form of this equation using compositions of linear mappings? Imagine the cycle diagram.
?
![[Pasted image 20251231153804.png]]
We can determine the transformation matrix $\tilde{A}_{\Phi}$ as follows: First, we find the matrix representation of the linear mapping $\Psi_{B\tilde{B}} : V \to V$ that maps coordinates with respect to the new basis $\tilde{B}$ onto the (unique) coordinates with respect to the “old” basis $B$ (in $V$). Then, we use the transformation matrix $A_{\Phi}$ of $\Phi_{CB} : V \to W$ to map these coordinates onto the coordinates with respect to $C$ in $W$. Finally, we use a linear mapping $\Xi_{\tilde{C}C} : W \to W$ to map the coordinates with respect to $C$ onto coordinates with respect to $\tilde{C}$. Therefore, we can express the linear mapping $\Phi_{\tilde{C}\tilde{B}}$ as a composition of linear mappings that involve the “old” basis:
$$
\Phi_{\tilde{C}\tilde{B}} \;=\; \Xi_{\tilde{C}C} \circ \Phi_{CB} \circ \Psi_{B\tilde{B}}
\;=\; \Xi_{C\tilde{C}}^{-1} \circ \Phi_{CB} \circ \Psi_{\tilde{B}B}.
$$
Concretely, we use $\Psi_{\tilde{B}B} = \mathrm{id}_V$ and $\Xi_{\tilde{C}C} = \mathrm{id}_W$, i.e., the identity mappings that map vectors onto themselves, but with respect to a different basis. Replacing each linear mapping with its corresponding transformation matrix gives us the original equation $\tilde{A}_\Phi = T^{-1} A_\Phi S$.

When are two matrices $A, \tilde{A} \in \mathbb{R}^{m \times n}$ _equivalent_?::If there exist regular matrices $S \in \mathbb{R}^{n \times n}$ and $T \in \mathbb{R}^{m \times m}$, such that $\tilde{A} = T^{-1}AS$.

When are two matrices $A, \tilde{A} \in \mathbb{R}^{n \times n}$ _similar_?::If there exists a regular matrix $S \in \mathbb{R}^{n \times n}$ with  
$\tilde{A} = S^{-1}AS$.



# 2.8 Affine Subspaces
31st Dec