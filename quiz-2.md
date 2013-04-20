Quiz 2
======

Mar 7, 2013
-----------

Assume that we have a data matrix $X$ with $n$ rows and $2$ columns.  

* Give the matrix formula for $J$ such that $Y=JX$ is a column-centered version of $X$ 
* Give the matrix formula for computing the sample covariance matrix `cov(X)` 
* Give the matrix formula for computing the squared distance matrix $D(X)^2$ for $X$
* Give the R function definition, i.e., for `cmdscale`
    * Input: a squared distance matrix `M` 
    * Output: 
        * a rotated version of centered version of the unknown data matrix
    * N.B.: 
        * the output `JXhat` should be such that `cov(JXhat)` is a diagonal matrix
        * i.e., the features are indepedent
    * Hint: 
        * use `eigen` function
* Give the R function definition, i.e., for `prcomp`
    * Input: a data matrix, `X` 
    * Output: 
        * as a list object that has
            * `Xrot`, a rotated version of the centered version of `X`
            * `rotmat`, the rotation matrix 
    * Hint: 
        * use `eigen` function together with `cov`
        * or use `svd`

Solution
========

### Problem 1 (5pts)
$$
J = \mathbf I - \frac{1}{n}\mathbf 1 \mathbf 1^\top,
$$
where $\mathbf I$ is the $n\times n$ identity matrix 
and $\mathbf 1$ is a column vector/maxtrix with dimension $n\times 1$.
Note that $\frac{1}{n} \neq \frac{1}{2}$. 

### Problem 2 (5pts) 
Using $J$ defined above, 
$$
\texttt{Cov}(X) = \frac{1}{n-1} (JX)^\top JX
\approx 
\texttt{Cov}(X) = \frac{1}{n} (JX)^\top JX.
$$
Note that $\frac{1}{n-1}$ and $\frac{1}{n}$ are both honored. 

### Problem 3 (5pts) 
Let $c$ denotes the diagonals of $X X^\top$, i.e., $c_k = (XX^\top)_k$
for each $k=1, \dots, n$.  Then,
$$
D^2(X) = c \mathbf 1^\top + \mathbf 1 c^\top - 2 X X^\top.
$$

### Problem 4 (10pts)

```{r, eval=FALSE}
cmdscale2 <- function(M) { 
    tmp = rep(1,nrow(M)) 
    J = diag(tmp) - 1/nrow(M) * cbind(tmp) %*% rbind(tmp) 
    M = -1/2*J %*% M %*% J  # or equivalently, -1/2 * J %*% M %*% t(J) 
    Up = eigen(M)$vectors[,1:2]
    Lp = sqrt(diag(eigen(M)$values[1:2]))
    Up %*% Lp
}
```

### Problem 5 (10pts) 
```{r, eval=FALSE}
prcomp2 <- function(X) { 
    tmp = rep(1,nrow(X)) 
    J = diag(tmp) - 1/nrow(X) * cbind(tmp) %*% rbind(tmp) 
    JX = J %*% X 
    Xrot = svd(JX)$u %*% diag(svd(JX)$d) 
    rotmat = svd(JX)$v
    list(Xrot=Xrot,rotmat=rotmat)
}
```
```{r, eval=FALSE}
prcomp2 <- function(X) { 
    rotmat = eigen(cov(X))$vectors 
    Xrot = scale(X,center=TRUE,scale=FALSE) %*% rotmat
    list(Xrot=Xrot,rotmat=rotmat)
}
```
