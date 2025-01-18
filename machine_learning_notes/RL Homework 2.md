## Problem 1b
The max function is convex, so we use Jensen's inequality, which states that for a convex function f, $\mathbb{E}[f(X)] \geq f(\mathbb{E}[X])$, we have:

$$\mathbb{E}[\max_a Q(s, a)] \geq \max_a \mathbb{E}[Q(s, a)]$$

Since $\mathbb{E}[Q(s, a)] = Q^*(s, a)$ by the unbiasedness assumption:

$$\max_a \mathbb{E}[Q(s, a)] = \max_a Q^*(s, a) = Q^*_{\text{max}}(s)$$

Thus:

$$\mathbb{E}[\max_a Q(s, a)] \geq Q^*_{\text{max}}(s)$$

Which shows that even with unbiased estimators, the expectation of the maximum $Q_{\text{max}}(s)$ overestimates the true maximum $Q^*_{\text{max}}(s)$ due to the non-linearity of the maximum operation. Hence:

$$\mathbb{E}[\max_a Q(s, a)] \geq \max_a Q^*(s, a)$$



<div style="page-break-after: always;"></div>


## Question 2a
$Q_\theta(s,a) = \theta^T\delta(s,a)$ where $\delta(s,a)$ is a one-hot encoding of the features and $Q_\theta$ is linear in $\theta$. Taking the gradient $\nabla_\theta Q_\theta(s,a)$ gives us
$$\nabla_\theta Q_\theta(s,a) = \delta(s,a)$$
Substituting this into the parameterized update function:
$$\theta \leftarrow \theta + \alpha\left( r + \gamma \underset{a'}{\max}Q_\theta(s', a') - Q_\theta(s,a) \right) \delta(s,a)$$
This version updates $\theta$, but since $\delta(s,a)$ is one-hot, only the component of $\theta$ corresponding to the $Q(s,a)$ is updated. Therefore, the update for $\theta$ modifies $\theta_{s,a}$ exactly as the tabular rule directly modifies $Q(s,a)$:

$$Q(s, a) \leftarrow Q(s, a) + \alpha \left( r + \gamma \max_{a'} Q(s', a') - Q(s, a) \right)$$

This equivalence shows that the parameterized form is a direct linear approximation of the tabular form.


<div style="page-break-after: always;"></div>


## Question 3c
The DQN is much slower, and also seems to return a worse result. Looking at the graph, it looks like the reward drops off sharply at around 7 epochs. This seems to be a result of basic RL being somewhat unstable, and is an indication that DQN is an overcomplication of the problem.
DQN: Average reward: 3.40 +/- 0.00
Linear: Average reward: 6.20 +/- 0.00

<div style="page-break-after: always;"></div>


### Question 4a
It appears that the linear approximation is very poor. In my plot, I see it starting at -20.96 and only reaching -20.84 at peak, which is no improvement at all. This is possibly because Pong has complex non-linear relationships between game states and a sparse reward signal of +1/-1, both of which linear models handle poorly. 


### Question 4c
The DQN performs significantly better than the linear Q value approximator.
The DQN uses neural networks to capture the non-linear relationships between the game elements like the paddle position or ball position and the final resulting score. By stacking multiple frames together, the DQN incorporates state history that encodes the ball velocity and future position over time into the policy. It also overcomes the sparse rewards by using the target network, which helps stabilize weights.

### Question 4d
No, the overall trend shows improvement but it is not monotonic. There are fluctuations in performance during training due to exploration, such as early on when the agent takes random actions which may not always be better than the previous. It is also a stochastic process, which can introduce noise and is not guaranteed to always be improving.

