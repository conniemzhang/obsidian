## Problem 2a
The probability of any trajectory in a policy is the cumulative probability of an action taken in each state, and the probability of the state it transitioned to. So given a trajectory $\tau = (s_0, a_0, s_1, a_1, \ldots)$,  we can express the probability of this trajectory occurring under the policy $\pi$ as the product of the probabilities of choosing each action and transitioning to each subsequent state:

$$\rho^{\pi}(\tau) = \prod_{t=0}^{\infty} \pi(a_t | s_t) P(s_{t+1} | s_t, a_t)$$
Where:
- $\pi(a_t | s_t)$ is the probability of taking action $a_t$ in state $s_t$ under policy $\pi$.
- $P(s_{t+1} | s_t, a_t)$ is the transition probability of moving to state $s_{t+1}$ from state $s_t$ after taking action $a_t$.


<div style="page-break-after: always;"></div>


## Problem 2b
$d^\pi(s)$ is calculated by summing the probabilities of being in state s at each timestep, weighted by the discount factor, then normalized by $(1-\gamma)$: $$d^\pi(s) = (1-\gamma) \sum_{t=0}^\infty \gamma^t p(s_t = s)$$
The expectation can be thought of as a sum, so we expand the left hand side of the identity as the sum of the expectation of each state-action pair sampled from the distribution $\rho^\pi$, which is equivalent to the expectation of the entire trajectory.

$$\mathbb{E}_{\tau \sim \rho^\pi}\left[\sum\limits^\infty_{t=0}\gamma^tf(s_t​,a_t​)\right]=\sum\limits_{t=0}^{\infty}\gamma^t\mathbb{E}_{(s_t​,a_t​)\sim \rho^\pi}​[f(s_t​,a_t​)]$$
On the right hand side, $\sum\limits_{​s\in S}​d^\pi(s)$ can replace the $\mathbb{E}_{s \sim d^\pi}$ term, and express $\mathbb{E}_{a\sim\pi(s)}$ as its summation formulation to of the probability of each action-state pair over all actions to get:

$$\frac{1}{1−γ}\mathbb{​E}_{s∼d^\pi}​E_{a\sim \pi(s)}​[f(s,a)]=\frac{1}{1−γ}\sum\limits_{​s\in S}​d^\pi(s)\sum\limits_{a\in A} \pi(a∣s)f(s,a)$$


Using $d^\pi(s)$'s definition:

$$= \frac{1}{1-\gamma} \sum_{s \in S} \left((1-\gamma) \sum_{t=0}^\infty \gamma^t p(s_t = s)\right) \sum_{a \in A} \pi(a | s) f(s, a)$$
$$ = \sum_{s \in S} \sum_{t=0}^\infty \gamma^t p(s_t = s) \sum_{a \in A} \pi(a | s) f(s, a)$$


$p(s_t = s)$ is the probability of being in state s at time t. Hence, $\gamma^t p(s_t = s) \pi(a | s)$ gives the probability-weighted contribution of $f(s, a)$ at each time t.

So the RHS can be reinterpreted as summing over all times t, states s, and actions a, each weighted by their occurrence probability under $\pi$ and discounted by $\gamma^t$:

$$= \sum_{t=0}^\infty \gamma^t \sum_{s \in S} p(s_t = s) \sum_{a \in A} \pi(a | s) f(s, a)$$

$$= \sum_{t=0}^\infty \gamma^t \mathbb{E}_{(s_t, a_t) \sim \rho^\pi}[f(s_t, a_t)]$$
This final expression for the RHS matches the LHS exactly, proving the identity.


<div style="page-break-after: always;"></div>



## Problem 2c

We want to prove:
$$V^\pi(s_0) - V^{\pi'}(s_0) = \frac{1}{1-\gamma} \mathbb{E}_{s \sim d^\pi} \left[ \mathbb{E}_{a \sim \pi(s)} [A^{\pi'}(s, a)] \right]$$

We start by expressing the value functions using their definitions from part 2a:

$$V^\pi(s_0) = \mathbb{E}_{\tau \sim \rho^\pi} \left[ \sum_{t=0}^\infty \gamma^t R(s_t, a_t) \right]$$
$$V^{\pi'}(s_0) = \mathbb{E}_{\tau \sim \rho^{\pi'}} \left[ \sum_{t=0}^\infty \gamma^t R(s_t, a_t) \right]$$

Using the hint, we add and subtract $\sum_{t=0}^\infty \gamma^{t+1} V^{\pi'}(s_{t+1})$ to the expression for $V^\pi(s_0)$. 
Adding $\gamma^{t+1} V^{\pi'}(s_{t+1})$ adds the future value under policy $\pi'$ to align the expected rewards under $\pi$ with those under $\pi$.
Subtracting $\gamma^{t+1} V^{\pi'}(s_{t+1})$ it keeps the integrity of the original series but enables the next transformation.

$$V^\pi(s_0) = \mathbb{E}_{\tau \sim \pi} \left[ \sum_{t=0}^\infty \gamma^t R(s_t, a_t) + \gamma^{t+1} V^{\pi'}(s_{t+1}) - \gamma^{t+1} V^{\pi'}(s_{t+1}) \right]$$

We can simplify this expression. This is not an equivalence, but shows how we compute the advantage of $a_t$ at state $s_t$ under policy $\pi$ relative to following policy $\pi'$ from $s_t$. 

$$= \mathbb{E}_{\tau \sim \pi} \left[ \sum_{t=0}^\infty \gamma^t (R(s_t, a_t) + \gamma V^{\pi'}(s_{t+1}) - V^{\pi'}(s_t)) \right]$$

The advantage function $A^{\pi'}(s_t​,a_t​)=Q^{\pi'}(s_t​,a_t​)−V^{\pi'}(s_t​)$ captures the difference in expected rewards by taking action $a_t$ versus following the policy $\pi'$ from state $s_t$. The term $R(s_t, a_t) + \gamma V^{\pi'}(s_{t+1})$ is the $Q^{\pi'}(s_t​,a_t​)$ action-value from the advantage function.

$$ = \mathbb{E}_{\tau \sim \pi} \left[ \sum_{t=0}^\infty \gamma^t (Q^{\pi'}(s_t, a_t) - V^{\pi'}(s_t)) \right] $$
$$ = \mathbb{E}_{\tau \sim \pi} \left[ \sum_{t=0}^\infty \gamma^t A^{\pi'}(s_t, a_t) \right]$$

Using the definition of the stationary distribution and the tower property of expectation:

$$= \frac{1}{1-\gamma} \mathbb{E}_{s \sim d^\pi} \left[ \mathbb{E}_{a \sim \pi(s)} [A^{\pi'}(s, a)] \right]$$



<div style="page-break-after: always;"></div>


## Problem 3a
In order to adhere to Justice, the selection of the students must not be biased, and selected in such a way to do the least harm per student. The average ability of the chatbot must be considered when assigning hours, for example, with those who have chatbot hours earlier in the term when it is less effective may be given fewer hours as time goes on. This is to ensure that no one student is being unduly assigned chatbots that are worse than human CAs.

Students must be informed about the details of the study, the differences between human vs chatbot CAs, and given the opportunity to opt out.  This follows the principle of Respect for Persons, the students are be given the ability to informed decision on their participation as the experiment impacts their lives and goals.