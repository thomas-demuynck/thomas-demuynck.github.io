The Frish-Waugh-Lovell theorem
==============================
**Thomas Demuynck**
*April 5 2021*

---

### OLS and projections 

Consider an $(n\times 1)$ vector $Y$ of observations and an $(n \times k)$ matrix $X$ of explanatory variables. We look at the regression: 
$$
	Y = X b + u, 
$$
where $b$ is an $(k \times 1)$ vector of coefficients and $u$ is the error term. 

The **least squares** estimate of $b$ can be found by projecting the vector $Y$ on the linear subspace:
$$
	{\cal L}_X = \{Y = X \beta: \beta \in \mathbb{R}^k\}.
$$

Let $\hat Y = X\beta$ be this linear projection. Then we know that $(Y - \hat Y)$ should be orthogonal to ${\cal L}_X$. As such, for all $Z \in {\cal L}_X$.
$$
	(Y - \hat Y)'Z = 0.
$$
In particular as $X \in {\cal L}_X$:
$$
	(Y - \hat Y)'X = (Y - X \beta)' X = 0
$$
This gives the condition:
$$
	Y' X - \beta' X' X = 0 \to \beta = (X' X)^{-1} X' Y.
$$
The projection is then equal to:
$$
	\hat Y = X \beta = X(X'X)^{-1} X'Y \equiv P_X Y.
$$
where $P_X = X(X'X)^{-1}X'$ is the linear operator that projects a vector $Y$ into the subspace ${\cal L}_X$. 

**Properties of the projection matrix**:

1. $P_X$ is symmetric: $(P_X)' = P_X$.

   *proof*: easy.

2. $P_X$ is idempotent: $P_X P_X = P_X$.

   > *proof*: 
   >$$
   >\begin{align*}
   >P_X P_X &= (X(X'X)^{-1}X')'(X(X'X)^{-1}X'),\\ 
   >&= X'(X'X)^{-1}X'X(X'X)^{-1}X',\\
   >&= X'(X'X)^{-1}X,\\
   >&= P_X
   >\end{align*}
   >$$
   
3. The residuals of the regression are given by:

$$
\hat u = Y - \hat Y = Y - P_X Y = (I - P_X)Y \equiv M_X Y.
$$
where $M_X = (I - P_X)$. 

4. $P_X X = X$

   > *proof*: $P_X X = X(X'X)^{-1}X'X = X$.

**Properties of the matrix M_X**

1. $Y = P_X Y + M_X Y$

   > *proof:* easy. 

2. $P_X$ and $M_X$ are orthogonal

   > *proof*: 
   > $P_X M_X = P_X(I - P_X) = P_X - P_X P_X = P_X - P_X = 0$.
   > consequentially: $\|Y\|^2 = \|\hat Y\|^2 + \|\hat u\|^2$.

### Frish-Waugh-Lovell theorem

Consider now the regression of $Y$ on $X_1$ and $X_2$.
$$
	Y = X_1 b_1 + X_2 b_2 + u.
$$
Assume that the OLSs estimates of $b_1$ and $b_2$ are $\beta_1$ and $\beta_2$.

Consider the following procedure:
1. regress $Y$ on $X_1$ giving residuals $M_{X_1} Y$

2. regress $X_2$ on $X_1$ giving residuals $M_{X_1} X_2$

3. regress $M_{X_1} Y$ on $M_{X_1} X_2$

The Frish-Waugh-Lovel theorem states that the estimate for the regression coeffients of the last step will equal the regression coefficient $\beta_2$ of the original regression. 

**Theorem** (Frish-Waugh-Lovell)
The regression coefficient of $\tilde Y$ on $\tilde X_2$ equals $\beta_2$.

> *proof:* Let us first focus on the original regression. The OLS estimates can be found by solving the following orthogonality conditions:
> $$
> \begin{align*}
> &X_1'(Y - X_1 \beta_1 - X_2 \beta_2) = 0,\\
> &X_2'(Y - X_1 \beta_1 - X_2 \beta_2) = 0.
> \end{align*}
> $$
> equivalently:
> $$
> \begin{align*}
> \begin{bmatrix} X_1'X_1 & X_1' X_2\\ X_2' X_1 & X_2'X_2\end{bmatrix}\begin{bmatrix} \beta_1\\\beta_2\end{bmatrix} = \begin{bmatrix}X_1'Y\\X_2'Y\end{bmatrix}
> \end{align*}
> $$
> Solving the first equation for $\beta_1$ gives:
> $$
> \beta_1 = (X_1'X_1)^{-1}X_1'Y - (X_1'X_1)^{-1}(X_1'X_2)\beta_2.
> $$
> Substituting into the second equation gives:
> $$
> \begin{align*}
> 	&X_2'X_1(X_1'X_1)^{-1}X_1Y - X_2'X_1(X_1'X_1)^{-1}(X_1'X_2)\beta_2 + X_2'X_2 \beta_2 = X_2'Y,\\
> 	\leftrightarrow& X_2' P_{X_1} Y - X_2' P_{X_1}X_2 \beta_2 + X_2'X_2 \beta_2 = X_2'Y,\\
> 	\leftrightarrow& X_2'(I - P_{X_1})X_2\beta_2 = X_2'(I - P_{X_1})Y,\\
> 	\leftrightarrow& X_2' M_{X_1} X_2 \beta_2 = X_2' M_{X_1} Y,\\
> 	\leftrightarrow& \beta_2 = (X_2' M_{X_1} X_2)^{-1} X_2' M_{X_1} M_{X_1} Y,\\
> 	\leftrightarrow& \beta_2 = ((M_{X_1} X_2)'M_{X_1}X_2)^{-1} (M_{X_1} X_2)' (M_{X_1} Y) 
> \end{align*}
> $$
> Here $M_{X_1}X_2$ is the residual of regressing $X_2$ on $X_1$ and $M_{X_1} Y$ is the residual of regressing $Y$ on $X_1$. 

### IV estimation

As before, consider the estimator:
$$
\begin{align*}
	\beta = (X'X)^{-1} X' Y = (X'X)^{-1}(Xb + u) = b + (X'X)^{-1} X' u. 
\end{align*}
$$
If $X'u$ is close to zero, then the last term disappears, so we obtain $\beta \approx b$. If $X' u \not \approx 0$ the coefficient $\beta$ can be a bad approximation of $b$. 

One solution is to use an instrumental (IV) variable $Z$ which satisfies the condition $Z'u \approx 0$. The IV steps consists in:

1.  Regress $X$ on $Z$ generating fitted values $P_Z X$. 
2. Regress $Y$ on $P_Z X$.

This gives the coefficient:
$$
\begin{align*}
\beta_{IV} &= ((P_Z X)'P_Z X)^{-1} (P_Z X)' Y = (X' P_Z X)^{-1} X' P_Z Y,\\
& = (X' P_Z X)^{-1} X'Z(Z'Z)^{-1}Z'(Xb + u),\\
& = (X' P_2 X)^{-1} (X'P_Z X) b + (X' P_Z X)^{-1} X'Z(Z'Z)^{-1} Z' u,\\
& = b + (X' P_Z X)^{-1} X'Z(Z'Z)^{-1} Z' u
\end{align*}
$$
If $Z'u \approx 0$ then the last term will be close to zero, so the estimator $\beta_{IV}$ might be closer to $b$ than the estimator $\beta$. Notice however that if $(X' P_Z X)$ is close to zero (which will be the case if $X'Z$ are close to zero (i.e. if they are only weakly correlated).  

### Control function approach

There exists a second way to approach the same issue. This is via a control function. For this:

1. Regress $X$ on $Z$ and save the residuals $M_Z X$.
2. Regress $Y$ on $X$ and $M_Z X$.

The coefficient of the last regression for $X$ can be found using the Frish-Waugh-Lovel theorem as:

1. regress $Y$ on $M_Z X \equiv Q$ giving residuals $M_Q Y$.
2. regress $X$ on $M_Z X \equiv Q$ giving redisulas $M_Q X$.
3. regress $Y$ on $M_Q X$.

This gives the estimate:

Notice that: 
$$
\begin{align*}
	M_Q X &= (I - P_Q) X = (I - Q(Q' Q)^{-1} Q')X  = (I - M_Z X(X' M_Z M_Z X)^{-1} X' M_Z)  X,\\
	&= X - M_Z X(X' M_Z X)^{-1} X' M_Z X,\\
	&= X - M_Z X = X - (I - P_Z)X = P_Z X. 
\end{align*}
$$
As such:


$$
\begin{align*}
	\beta_{CF} &= ((M_Q X)'M_Q X)^{-1}(M_Q X)'Y = (X' M_Q X)^{-1} X' M_Q (Xb + u),\\
	& = b + (X' M_Q X)^{-1}X' M_Q u,\\
	&= b + (X'P_Z X) X P_Z u.
\end{align*}
$$
which is the same as for the IV estimator. 