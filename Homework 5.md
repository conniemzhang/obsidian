### Problem 1
We want to find the unit-length vector $u$ that minimizes the following expression:
$$
\arg \min_{u: u^T u = 1} \sum_{i=1}^n \left\| x^{(i)} - f_u(x^{(i)}) \right\|_2^2
$$

where $f_u(x)$ is the projection of $x$ onto the the direction of $u$.

The projection of a point $x$ onto a vector $u$ in vector format is given by:
$$
f_u(x) = (x^Tu)u
$$


To minimize the mean squared error, we need to minimize:
$$
\text{argmin}\sum_{i=1}^n \left\| x^{(i)} - f_u(x^{(i)}) \right\|_2^2
$$

Substitute the projection$f_u(x^{(i)}) = \left( x^{(i)T} u \right) u$:
$$
\text{argmin}\sum_{i=1}^n \left\| x^{(i)} - \left( x^{(i)T} u \right) u \right\|_2^2
$$
Expanding the squared norm gives us
$$
\begin{aligned}
\| x^{(i)} - (x^{(i)T} u) u \|_2^2 &= \left( x^{(i)} - (x^{(i)T} u) u \right)^T \left( x^{(i)} - (x^{(i)T} u) u \right) \\
&= x^{(i)T} x^{(i)} - x^{(i)T} (x^{(i)T} u) u - (x^{(i)T} u) u^T x^{(i)} + (x^{(i)T} u) u^T (x^{(i)T} u) u \\
&= x^{(i)T} x^{(i)} - (x^{(i)T} u) (x^{(i)T} u) - (x^{(i)T} u) (x^{(i)T} u) + (x^{(i)T} u)^2 (u^T u) \\
&= x^{(i)T} x^{(i)} - 2(x^{(i)T} u)^2 + (x^{(i)T} u)^2 \\
&= x^{(i)T} x^{(i)} - (x^{(i)T} u)^2
\end{aligned}
$$
So we have found the squared norm is equals this result:
$$
\left\| x^{(i)} - \left( x^{(i)T} u \right) u \right\|_2^2 = \left\| x^{(i)} \right\|_2^2 - \left( x^{(i)T} u \right)^2
$$
Sum this expression over all points in the MSE
$$
\text{argmin}\sum_{i=1}^n \left( \left\| x^{(i)} \right\|_2^2 - \left( x^{(i)T} u \right)^2 \right) = \sum_{i=1}^n \left\| x^{(i)} \right\|_2^2 - \sum_{i=1}^n \left( x^{(i)T} u \right)^2
$$

$\sum_{i=1}^n \left\| x^{(i)} \right\|_2^2$ is constant with respect to $u$ (I had trouble formatting the correct $argmin$ but it's wrt $u:u^Tu=1$). Thus, minimizing the total expression is equivalent to maximizing:
$$
\sum_{i=1}^n \left( x^{(i)T} u \right)^2
$$

We expand the square again to use the equation of the covariance matrix
$$
\frac{1}{n} \sum_{i=1}^n (u^T x^{(i)})^2 = \frac{1}{n} \sum_{i=1}^n u^T (x^{(i)} x^{(i)T}) u = u^T \left( \frac{1}{n} \sum_{i=1}^n x^{(i)} x^{(i)T} \right) u = u^T \Sigma u
$$
Where $\Sigma$ is the covariance matrix.

This means we can express the variance of the projections of the data points by maximizing $u^T \Sigma u$ subject to the constraint $u^T u = 1$ which is in the format of the standard eigenvalue problem.

The maximum is achieved when $u$ is the eigenvector corresponding to the largest eigenvalue of $S$. This eigenvector is the first principal component.

Thus, the unit-length vector $u$ that minimizes the mean squared error corresponds corresponds to the first principal component of the data.


<div style="page-break-after: always;"></div>





#### PROBLEM 2a
The supervised portion does not change during the E-step since it involves known labels$\tilde{z}^{(i)}$, so the supervised part$\ell_{\text{sup}}(\theta)$remains as it is:
$$
\ell_{\text{sup}}(\theta) = \sum_{i=1}^{\tilde{n}} \log p(\tilde{x}^{(i)}, \tilde{z}^{(i)}; \theta)
$$
Which means at time$\theta^{(t+1)}$we have:

$$
\ell_{\text{sup}}(\theta^{(t+1)}) = \sum_{i=1}^{\tilde{n}} \log p(\tilde{x}^{(i)}, \tilde{z}^{(i)}; \theta^{(t+1)})
$$

Combining the supervised parts with the Jensen's inequality for$\ell_{unsup}(\theta^{(t+1)})$.
$$
\ell_{\text{semi-sup}}(\theta^{(t+1)}) \geq \alpha \sum_{i=1}^{n'} \log p(\tilde{x}^{(i)}, \tilde{z}^{(i)}; \theta^{(t+1)}) + \sum_{i=1}^{n} \sum_{z^{(i)}} Q^{(t)}_i(z^{(i)}) \log \frac{p(x^{(i)}, z^{(i)}; \theta^{(t+1)})}{Q^{(t)}_i(z^{(i)})}
$$

This is the form that is used in the M-step, when we update the parameters to maximize this objective. This maximizes the log-likelihood given the current parameters$\theta^t$, so each next step will be larger than the previous:
$$
\theta^{(t+1)} = \arg \max_{\theta} \left( \alpha \sum_{i=1}^{n'} \log p(\tilde{x}^{(i)}, \tilde{z}^{(i)}; \theta) + \sum_{i=1}^{n} \sum_{z^{(i)}} Q^{(t)}_i(z^{(i)}) \log \frac{p(x^{(i)}, z^{(i)}; \theta)}{Q^{(t)}_i(z^{(i)})} \right)
$$

Therefore, by updating$\theta$to$\theta^{(t+1)}$, we ensure that the objective function increases:
$$
\ell_{\text{semi-sup}}(\theta^{(t+1)}) \geq \ell_{\text{semi-sup}}(\theta^{(t)})
$$


<div style="page-break-after: always;"></div>


#### PROBLEM 2b
In the E-step we try to guess the latent variables by calculating the posterior probability of our parameters. We represent those$z^{(i)}$'s as:
$$w^{(i)}_j := p(z^{(i)} = j|x^{(i)}; \phi, \mu, \Sigma)$$
for each {i, j} set. 
From the notes we can use Bayes rule to obtain:
$$
p(z^{(i)} = j | x^{(i)}; \phi, \mu, \Sigma) = \frac{p(x^{(i)} | z^{(i)} = j, \mu_j, \Sigma_j) p(z^{(i)} = j ; \phi)}{\sum_{l=1}^k P(x^{(i)} | z^{(i)} = l, \mu_l, \Sigma_l) P(z^{(i)} = l ; \phi)}
$$

When we replace$p(x^{(i)} | z^{(i)} = j, \mu_j, \Sigma_j)$with the density of the Gaussian and$p(z^{(i)} = j ; \phi)$with$\phi_j$, we get:
$$
p(z^{(i)} = j | x^{(i)}; \phi, \mu, \Sigma) = \frac{\mathcal{N}(x^{(i)} | \mu_j, \Sigma_j)\phi_j }{\sum_{l=1}^k \mathcal{N}(x^{(i)} | \mu_l, \Sigma_l)\phi_l }
$$
When the data is labeled, we already have the$\tilde{z}^{(i)}$, so our posterior probabilities are just:
$$
\delta(\tilde{z}^{(i)}, j) = \begin{cases}
1 & \text{if } \tilde{z}^{(i)} = j \\
0 & \text{otherwise}
\end{cases}
$$
Combining these two and including the usage of steps$t$, we get our E step to be:
$$
Q_i^{(t)}(z^{(i)}) = \begin{cases}
\frac{\mathcal{N}(x^{(i)} | \mu_j^{(t)}, \Sigma_j^{(t)}){\phi_j^{(t)}}}{\sum_{l=1}^k \mathcal{N}(x^{(i)} | \mu_l^{(t)}, \Sigma_l^{(t)})\phi_l^{(t)}} & \text{for } x^{(i)} \text{ (unlabeled)} \\
1 & \text{if } \tilde{z}^{(i)} = j \\
0 & \text{otherwise}
\end{cases}
$$
