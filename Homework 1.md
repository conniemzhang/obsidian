### Problem 1

**(a)** We know that the integral over any pdf is equal to one, so from the definition of an exponential family distribution we have

$$\int p(y;\eta)dy = \int b(y)exp(\eta y-a(\eta))dy = 1$$

we can solve this for $a(n)$ by factoring out $exp(-a\eta)$ and multiplying by both sides. $$\int b(y)exp(\eta y)dy = exp(a(\eta))$$ $$log \left( \int b(y)exp(\eta y)dy \right) = a(\eta)$$ $$\frac{\partial }{\partial \eta} a(\eta) = \frac{\partial }{\partial \eta} \left( \log \left( \int b(y) \exp(\eta y) \, dy \right) \right)$$ applying chain rule to the right hand side and using the hint given: $$\frac{\partial }{\partial \eta} a(\eta) = \frac{\int b(y)\frac{\partial }{\partial \eta}\exp(\eta y)dy}{\int b(y) \exp(\eta y)dy} = \frac{\int b(y)y\exp(\eta y)dy}{\int b(y) \exp(\eta y)dy} \tag{1}$$

So we have half of what we are trying to prove, now to calculate the Expectation, which is given as $$\mathbb{E}[Y;\eta] = \int b(y) * y * exp(\eta y - a(\eta))dy$$

We know what $\exp(a(\eta))$ is in terms of $y$ from the above, so we can substitute into our Expectation. 
$$\mathbb{E}[Y;\eta] = \frac{\int b(y)y\exp(\eta y)dy}{\int b(y)\exp(\eta y)dy}$$
and since this results is the same as (1), we have proven
$$\mathbb{E}[Y;\eta] = \frac{\partial }{\partial \eta}a(\eta)$$
__________________

**(b)** We know that the Variance of a distribution with random variable X is defined as $$Var[X] := \mathbb{E}[X^2] - \mathbb{X}[X]^2$$We know from the previous question that the $\mathbb{E}[Y;\eta] = \frac{\partial }{\partial \eta}a(\eta)$ so we are trying to show that $Var[Y;\eta] = \frac{\partial }{\partial \eta}\mathbb{E}[Y;\eta]$.

We substitute the definition of the Expectation and get the following
$$\frac{\partial}{\partial\eta}\mathbb{E}[Y;\eta] = \frac{\partial}{\partial \eta}\int y p(y;\eta)dy = \int y\frac{\partial }{\partial \eta}(p(y;\eta))dy \tag{2}$$

Calculating $\frac{\partial }{\partial \eta}p(y;\eta)$ with chain rule $$\frac{\partial }{\partial \eta}p(y;\eta) = \frac{\partial }{\partial \eta}b(y)\exp(\eta y - a(\eta)) = b(y)(y-\frac{\partial }{\partial \eta}a(\eta))\exp(\eta y-a(\eta))$$

we know $\frac{\partial }{\partial \eta}a(\eta) = \mathbb{E}[Y;\eta]$ from the previous question, and the $b(y)\exp(\eta y-a(\eta)) = p( y ; \eta)$. $$\frac{\partial }{\partial \eta}p(y;\eta) = p(y;n)(y-\mathbb{E}[Y;\eta])$$
Plugging back into (2), we have

$$\frac{\partial }{\partial \eta}\mathbb{E}[Y;\eta] = \int y p(y;\eta)(y-\mathbb{E}(Y;\eta])dy$$
When you multiply this all out and use the fact that $\mathbb{E}[Y;n] = \int yp(y;n)dy$ you get 
$$\frac{\partial }{\partial \eta}\mathbb{E}[Y;\eta] = \mathbb{E}[Y^2] - \mathbb{E}[Y]^2$$ 
This is the equation for the variance, so we have shown $Var(Y;\eta)=\frac{\partial ^2}{\partial \eta^2}a(\eta)$$\frac{\partial }{\partial \theta}$

___________________

**(c)** First we find the Negative Log Likelihood. The log-likelihood is the summation of the log of the the probabilities for $n$ inputs. $$\ell(\theta) = \sum_{i=1}^n \left( \log b(y_i) + \eta y_i - a(\eta^T) \right)$$

We substitute $\eta = \theta^T x$, and take the negative to find the NLL.$$ \text{NLL}(\theta) = -\sum_{i=1}^n \left( \log b(y_i) + (\theta^T x_i) y_i - a(\theta^T x_i) \right) $$and simplify, dropping the $log(b(y))$ term since it's a constant wrt to $\theta$$$ \text{NLL}(\theta) = \sum_{i=1}^n \left( - (\theta^T x_i) y_i + a(\theta^T x_i) \right) $$$$ l(\theta) = \text{NLL}(\theta) = \sum_{i=1}^n \left( a(\theta^T x_i) - (\theta^T x_i) y_i \right)$$
Now we take the second derivative of $l(\theta)$, and show it is PSD by using the the fact that the Variance of a probability distribution is non-negative.$$\frac{\partial }{\partial \theta}l(\theta) = \sum_{i=1}^n \left( \frac{\partial }{\partial \theta}a(\theta^T x_i) - \frac{\partial }{\partial \theta}(\theta^T x_i) y_i \right)$$
Then apply chain rule and substituting for $\theta^Tx$ for the first term
$$ \frac{\partial}{\partial \theta}a(\theta^T x_i) = x_i \frac{\partial}{\partial \eta}a(\eta) = \mathbb{E}[Y;\eta] x_i$$
Second term:
$$\frac{\partial}{\partial \theta}(\theta^T x_i) y_i = y_i x_i$$
Substituting, the gradient is then
$$ \frac{\partial l(\theta)}{\partial \theta} = \sum_{i=1}^n \left(  \mathbb{E}[Y;\eta] x_i - y_i x_i \right)$$

We take the derivative of the gradient to find the Hessian. 

$$\frac{\partial^2}{\partial \theta^2}l(\theta) = \frac{\partial}{\partial \theta}\sum_{i=1}^n \mathbb{E}[Y;\eta] x_i - \frac{\partial}{\partial \theta}\sum_{i=1}^n y_i x_i$$

We use the other form of $\mathbb{E}[Y;\eta]$ to use chain rule again on the first term
$$ \frac{\partial}{\partial \theta} \left( \sum_{i=1}^n a'(\theta^T x_i) x_i \right) = a''(\theta^T x_i) x_i^2$$

The second term does not depend on $\theta$:

$$\frac{\partial}{\partial \theta} \left( \sum_{i=1}^n y_i x_i \right) = 0$$
Combining the second derivatives of the two terms to find the Hessian:

$$\frac{\partial^2}{\partial \theta^2}l(\theta) = \sum_{i=1}^n Var[Y;\eta] x_i^2$$


The Variance is always non negative, and the $x$ term is also always non-negative. Therefore, the Hessian is positive semi-definite.
<div style="page-break-after: always;"></div>

### Problem 2

(a) Replacing the $x$ in the general form with $\hat{x}$, the transformed input of the data set gives you the following objective function.
$$J(\theta) = \frac{1}{2} \sum_{i=1}^n(h_{\theta}(\hat{x}^{(i)} - y^{(i)})^2$$
So then taking the partial derivative of $J(\theta)$ and replacing $h_\theta(x) = \theta^T\hat{x}$ as given in the problem, and applying chain rule gives us:
$$\nabla_{\theta} J(\theta) = \sum_{i=1}^{n}(\theta^T\hat{x}-y^{(i)})\frac{d}{d\theta_j}(\theta^T\hat{x}-y^{(i)}) = \sum_{i=1}^{n}(\theta^T\hat{x}^{(i)}-y^{(i)})\hat{x}^{(i)}$$

which makes the gradient descent update rule
$$\theta := \theta - \lambda\sum_{i=1}^n(\theta^T\hat{x}^{(i)}-y^{(i)})\hat{x}^{(i)}$$
(b) See Coding

(c) As the k increases, we see a closer fit to the data. We start from a single line fit at k = 1, then adding curve inflections up to a very fitted function that follows the curves of the data at k = 20. 

(d) See Coding

(e) The models from 2d fit the data better at lower k. In 2d, even at k = 1 we see a good fit compared to the single line from 2b due to the inclusion of sine transformation.

(f) not graded

(g) We see the middle k's be the most reasonable in Figure 3, and lower k's in Figure 4. At lower k's, it is not a good estimation of the training data, but is mostly within the range of the training values. At higher k's, we see the model wildly overshoot the training data, and would provide very bad answers for test examples, particularly at the extremes past the training data. 

<div style="page-break-after: always;"></div>

### Problem 3
(a) Dataset A converges in ~30000 iterations. Dataset B never converges.

(b) When testing several theories, the one that helped dataset B to converge is adding a regularization term to the loss function. This because dataset B is perfectly separated (see Fig 1 below) - infinitely large thetas will infinitely reduce the loss function so it never converges. Adding the regularization penalizes large coefficients, so the loss function is able to converge even though it's perfectly separated. Dataset A was not perfectly separated, so when the magnitudes were large the loss function would also get worse due to the crossover data points. We see the difference the regularization term makes in Fig 2, that compares the coefficients before and after regularization.

Mathematically 
$$ \text{Log Loss} = \sum_{(x, y) \in D} \left[ -y \log (\theta^T\mathbf{x}) + (1 - y \log (1 - ( \theta^T\mathbf{x})) \right] $$
Since there is a perfect boundary, the linear combination $θ^Tx$ will be pushed towards positive or negative infinity achieve probabilities close to 1 or 0.

![[Pasted image 20240531231753.png |[800]]
Fig 1. Plotting the data

![[Pasted image 20240531234010.png |500]]
Fig 2. Comparing the coefficients before and after regularization for Dataset B.



(c) 
i. No, a different learning rate would not help. The problem is that the coefficients are infinitely large, and a different learning rate would just change how fast you approach infinity.

ii. No, for the same reason as above. No learning rate changes would help.

iii. No, scaling the features would not help. Scaling helps standardize the mean, variance, or restrict the input to a range, and the range is just 0, 1 since it's a classifier. It would still have perfect separation.

iv: Yes. Regularization adds a penalty to the loss function, as described in 3b.

v. Yes, since it shakes up data points near the boundaries breaking the perfect separation.