### PROBLEM 1a
a) First prove that $\forall P, Q.$ $D_{KL}(P||Q) \geq 0$

From the question we know that $$D_{KL}(P||Q) = \sum_{X\in\chi}P(X)\log\frac{P(X)}{Q(X)}$$
Jensen's inequality is defined as  $f(\mathbb{E}[X])\geq \mathbb{E}[f(X)]$ , if $f(X)$ is a convex function. 
However, $\log(X)$ is a concave function, so we set $f(X) = -\log(X)$, which is a convex function. 

$$
\begin{aligned}
D_{KL}(P \parallel Q) &= \sum_{X \in \chi} P(X) \log \frac{P(X)}{Q(X)} \\
           &= - \sum_{X \in \chi} P(X) \log \frac{Q(X)}{P(X)} \\
           &\geq - \log\sum_{X \in \chi} P(X) \frac{Q(X)}{P(X)} \quad \text{(by Jensen's inequality)} \\
           &= - \log \sum_{X \in \chi} Q(X) \\
           &= - \log(1) \\
           &= 0
\end{aligned}
$$

Which implies that KL divergence is always non-negative.
$$D_{KL}(P \| Q) \geq 0.$$
Since $\log(X)$is a strictly concave function, equality holds if and onlY if $\frac{P(X)}{Q(X)}$ is constant, which only occurs when $P = Q$.


<div style="page-break-after: always;"></div>



### PROBLEM 1b
b) 
Given the definition, we can prove the following chain rule:
$$ D(P(X, Y) \parallel Q(X, Y)) = D(P(X) \parallel Q(X)) + D(P(Y|X) \parallel Q(Y|X)) $$
**Proof** $$ \begin{aligned} D(P(X, Y) \parallel Q(X, Y)) &= \sum_{X \in \mathcal{X}} \sum_{Y \in \mathcal{Y}} P(X, Y) \log \frac{P(X, Y)}{Q(X, Y)} \\ &= \sum_{X \in \mathcal{X}} \sum_{Y \in \mathcal{Y}} P(X, Y) \log \frac{P(X)P(Y|X)}{Q(X)Q(Y|X)} \\ &= \sum_{X \in \mathcal{X}} \sum_{Y \in \mathcal{Y}} P(X, Y) \log \frac{P(X)}{Q(X)} + \sum_{X \in \mathcal{X}} \sum_{Y \in \mathcal{Y}} P(X, Y) \log \frac{P(Y|X)}{Q(Y|X)} \\ &= D(P(X) \parallel Q(X)) + \sum_{X \in \mathcal{X}} P(X) \sum_{Y \in \mathcal{Y}} P(Y|X) \log \frac{P(Y|X)}{Q(Y|X)} \\ &= D(P(X) \parallel Q(X)) + D(P(Y|X) \parallel Q(Y|X)) \end{aligned} $$

<div style="page-break-after: always;"></div>


### PROBLEM 1c
We start with
$$ \arg \min_\theta D_{KL}(\hat{P} \parallel P_\theta) = \arg \max_\theta \sum_{i=1}^{n} \log P_\theta(x^{(i)}) $$

The KL divergence definition between $\hat{P}$ and the model distribution $P_\theta$ is given by:
$$ D_{KL}(\hat{P} \parallel P_\theta) = \sum_{x} \hat{P}(x) \log \frac{\hat{P}(x)}{P_\theta(x)} $$

Substitute $\hat{P}(x)$:
$$ D_{KL}(\hat{P} \parallel P_\theta) = \sum_{x} \left( \frac{1}{n} \sum_{i=1}^{n} 1\{x^{(i)} = x\} \right) \log \frac{\frac{1}{n} \sum_{i=1}^{n} 1\{x^{(i)} = x\}}{P_\theta(x)} $$

When we sum over $x$, it is equivalent to to summing over the data points $x^{(i)}$ in the training set:
$$ D_{KL}(\hat{P} \parallel P_\theta) = \frac{1}{n} \sum_{i=1}^{n} \log \frac{\frac{1}{n}}{P_\theta(x^{(i)})} $$

Simplifying the $\log$ and breaking up the components gives us:
$$ D_{KL}(\hat{P} \parallel P_\theta) = \log \frac{1}{n} - \frac{1}{n} \sum_{i=1}^{n} \log P_\theta(x^{(i)}) $$
To find the parameter $\theta$ that minimizes the KL divergence, we plug back in:
$$ \arg \min_\theta D_{KL}(\hat{P} \parallel P_\theta) = \arg \min_\theta \left( \log \frac{1}{n} - \frac{1}{n} \sum_{i=1}^{n} \log P_\theta(x^{(i)}) \right) $$

Since $\log \frac{1}{n}$ is a constant with respect to $\theta$, minimizing $D_{KL}(\hat{P} \parallel P_\theta)$ is equivalent to maximizing:
$$ \arg \max_\theta \frac{1}{n} \sum_{i=1}^{n} \log P_\theta(x^{(i)}) $$

The $\frac{1}{n}$ does not impact the max function since it is a scaling factor, so we can drop the term giving us:
$$ \arg \max_\theta \sum_{i=1}^{n} \log P_\theta(x^{(i)}) $$

Which is the right hand side. Therefore, we have shown that:
$$ \arg \min_\theta D_{KL}(\hat{P} \parallel P_\theta) = \arg \max_\theta \sum_{i=1}^{n} \log P_\theta(x^{(i)}) $$


<div style="page-break-after: always;"></div>


### PROBLEM 4a
a) Given the regularized linear regression with cost function 
$$ J_\lambda(\beta) = \frac{1}{2} \|X \beta - \mathbf{y}\|^2_2 + \frac{\lambda}{2} \|\beta\|^2_2$$
Which is equivalent to the following when the Euclidean norms are expanded:

$$ J_\lambda(\beta) = \frac{1}{2} (X \beta - \mathbf{y})^\top (X \beta - \mathbf{y}) + \frac{\lambda}{2} \beta^\top \beta $$

We want to find the value of $\beta$ that minimizes this cost function by computing the gradient of $J_\lambda(\beta)$ wrt $\beta$ and set it to zero.

Taking the gradient of $J_\lambda(\beta)$ with respect to $\beta$, we get:

$$ \nabla_\beta J_\lambda(\beta) = \nabla_\beta \left( \frac{1}{2} (X \beta - \mathbf{y})^\top (X \beta - \mathbf{y}) + \frac{\lambda}{2} \beta^\top \beta \right) $$

We first look at the first part of the the expression and expand:

$$ \nabla_\beta \left( \frac{1}{2} (X \beta - \mathbf{y})^\top (X \beta - \mathbf{y}) \right) = \frac{1}{2}\nabla_\beta \left(\beta^\top X^\top X \beta - 2 \mathbf{y}^\top X \beta + \mathbf{y}^\top \mathbf{y} \right)$$

Differentiating each term with respect to $\beta$:
   -  $\beta^\top X^\top X \beta = 2 X^\top X \beta$
   -  $-2 \mathbf{y}^\top X \beta = -2 X^\top \mathbf{y}$
   -  $\mathbf{y}^\top \mathbf{y}= 0$
Combine terms and we get for the first part:
$$ \nabla_\beta \left( \frac{1}{2} (X \beta - \mathbf{y})^\top (X \beta - \mathbf{y}) \right) = X^\top X \beta - X^\top \mathbf{y} $$

And for the regularization term:

$$ \nabla_\beta \left( \frac{\lambda}{2} \beta^\top \beta \right) = \lambda \beta $$

Combining these results, we get:

$$ \nabla_\beta J_\lambda(\beta) = X^\top X \beta - X^\top \mathbf{y} + \lambda \beta $$

Setting the gradient to zero for minimization, we get:

$$X^\top X \beta - X^\top \mathbf{y} + \lambda \beta = 0 $$
Adding a identity matrix  $I_{d \times d}$ so that the dimensions match and we can factor out the $\beta$, rearranging the terms:
$$ (X^\top X + \lambda I_{d\times d}) \beta = X^\top \mathbf{y} $$
Rearranging for $\beta$ gives us the closed form solution.
$$ \beta = (X^\top X + \lambda I)^{-1} X^\top \mathbf{y} $$