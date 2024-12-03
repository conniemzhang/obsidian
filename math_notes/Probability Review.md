#notes #math
Conditional Probability and Bayes' Rule
For any events A, B such that $P(B)\neq 0$ , we define:
$$ P(Ab | B) := \frac{P(A \cap B)}{P(B)}$$
You can apply conditional probabilty to obtain Bayes'Rule

$$ P(Ab | B) := \frac{P(A \cap B)}{P(B)} = \frac{P(A \cap B)}{P(A)} = \frac{P(B)P(A | B)}{P(A)}$$

## Random Variables
**Random Variable**: variable that probabilistically takes on a different values. Maps outcomes to real values. Automatically assumes there is some probability distribution on it.

**Probability Mass Function** (PMF): Given a **discrete** RV $X$, a PMF maps the values of X to probabilities (so it must all sum to 1).
$$p_X(x) := p(x) := P(X = x)$$
Probability that $X$ is equal to some value $x$.
**Cumulative Distribution Function** (CDF): maps a continuous RV to a probability (i.e. $\mathbb{R} \rightarrow [0,1]$, )
$$ F_X(a) := F(a) := P(X \leq a)$$
So now instead of mapping to a specific value, it's the probability that X is less than some range.
Must fulfill the following
* $lim_{x \rightarrow -\infty} F_X(x) = 0$
*  $lim_{\rightarrow \infty} F_X(x) = 1$
* if $a \leq b$ then $F_X(a) \leq F_X(b)$ (i.e. CDF must be nondecreasing)
* Also note: you can find the range by subtracting the larger value from the smaller.

**Probability Density Function** (PDF): PDF of a continous RV is the derivative of the CDF (so you're interested in the area under the curve)..
$$f_X(x) := f(x) := \frac{dF_X(x))}{dx}$$
Thus $$P( a \leq X \leq b) = F_X(b) - F_X(a) = \int_{b}^{a} f_X(x)dx$$
Thus a valid PDF must be such that
* for all real numbers $x$, $f_X(x) \geq 0$
* $\int_{-\infty}^{\infty} f_X(x)dx = 1$

The **Expectation** of a random variable is the average outcome over a large number of trials or observations. The probability-weighted average of all possible values that random variables can take on. **it's the weighted mean**
Discrete: $$E(X) = \sum_{i} x_i p_i$$
Continuous: $$E(X) = \int_{-\infty}^\infty x f(x) \, dx$$
**Variance**: the variance of RV X measure show concentrated the distribution of X is around it's mean. Measures the spread of the distribution i.e. find the mean and then see how far each of them is from your data points.
$$Var(x) := \mathbb{E}[(X - \mathbb{E}[X])^2] \\ = \mathbb{E}[X^2] - \mathbb{E}[X]^2$$
Some distributions are common, and have standard means, and variances. Try to identify which belong to the exponential family and which do not. 

### Joint Distributions
You now have multiple random variables that you are considering. You have formed a combined (joint) probability distribution to become univariate again. However it might be useful to know which variable part of the joint comes from.
#### **Joint PMF for discrete RV's X, Y:**
$$p_{XY}(x, y) = P(X = x, Y = y)$$
Note that it still must sum to one:  $$\sum_{x \in \text{Val}(X)} \sum_{y \in \text{Val}(Y)} p_{XY}(x, y) = 1$$
**Conditional**: you only examine a subset where one of the random variables a subset of its sample space.
**Marginal**: Combine a subset into a single variable.
Why? The joint probability distribution $P(X, Y)$, you can describe how two or more random variables interact with each other. Its a complete picture of the probabilistic relationship between the variables, and can infer how changes to one can affect the other.
Use in: Bayes theorem, Gaussian Discriminant Analysis. 


## Covariance
Measures how much one RV's value tends to move with another RV's value. 
$$\text{Cov}[X, Y] := \mathbb{E}([XY] - \mathbb{E}[X]\mathbb{E}[Y])$$
* If $\text{Cov}[X, Y] < 0$ then X and Y are negatively correlated
*  If $\text{Cov}[X, Y] \gt 0$ then X and Y are positively correlated
*  If $\text{Cov}[X, Y] = 0$ then X and Y are  uncorrelated

### Conditional Distributions to RVs
Similar as for events, but you use the distributions instead.

## Random Vectors : Expanding to Linear Alg.
Given n RV's $X_1, ... X_n$, we can define a random vector X s.t. $$X = \begin{bmatrix} X_1 \\ X_2 \\ \vdots \\ X_n \end{bmatrix}$$
Note: all notions of Joint PDF/CDF will apply to x. 
given $g : \mathbb{R}^n \rightarrow \mathbb{R}^m$ (any function that creates a vector as an output), the expectation is the element-wise expectation of your vector.
$$ g(x) = \begin{bmatrix} g_1(x) \\ g_2(x) \\ \vdots \\ g_m(x) \end{bmatrix}, \mathbb{E}[g(x)] = \begin{bmatrix} \mathbb{E}[g_1(x)] \\ \mathbb{E}[g_2(x)] \\ \vdots \\ \mathbb{E}[g_m(x)] \end{bmatrix}$$
This enables you to do vector operations of all of them. 



## Marginalization





