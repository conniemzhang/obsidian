### Problem 1a:
It is sometimes difficult to determine what the reward should be for a state. Specifying an incorrect reward function will optimize in undesirable ways, referred to as "reward hacking". For example, you may have a problem where you reward a dish-washing robot with +1 every time it cleans a dish, but it dispenses a gallon of soap per dish in order to clean it the fastest. In this case, only gaining credit when a dish is washed is maybe too sparse.

### Problem 1b:
The healthy reward keeps the Hopper stable, which is essential when considering the long term. This balances out the forward reward, which wants to move Hopper forward, but without the healthy term, would move forward at all costs. The control cost makes sure the reward takes small steps and avoid oscillations but is weighted less than the other two terms.
This seems like a reasonable and fairly easy reward function to achieve forward locomotion. 

### Problem 1c
Healthy for the Hopper means a height of 0.7+, which means it has not fallen over, a torso that is not too angled, and no observation (angle, velocity, angular velocity) is outside of the given range. Terminating early means you don't have to waste time exploring policies that result in unhealthy states. It also means that your reward is often lower since it has fewer interactions with the environment that episode. 

### Problem 1e
We see that early termination causes significant variability of the reward, and this is evident in the seed of 23. No early termination improves faster with fewer epochs, and therefore, less wall time. The standard error is high when terminating early - the agents performance is inconsistent. The standard error is better for No early termination. 

To better estimate the average return, we could use different starting seeds, or possibly increase the number of episodes so the variance is reduced in the estimate of the average. When we use different starting seeds, we could also cross-reference the performance to gain a more wholistic picture.

### Problem 1f
I ran with early termination. I was surprised by how often the early termination was triggered, and the robot did not go as far as I expected. It sort of completes the task, but tends to stability instead of hopping.

### Problem 1g
Compared with no early termination, the robot falls over and is a lot more "wacky". However, it did thrash further. Since our goal is to move further, I prefer this one even though it doesn't "hop" as well. 


## Problem 2
If we express the sum of estimated rewards for trajectory $\sigma$ as: $\hat{r}(\sigma) = \sum_{t} \hat{r}(o_t, a_t)$, we can rewrite the Bradley-Terry preference model as: 
$$P[\sigma_1 \succ \sigma_2] = \frac{\exp(\hat{r}(\sigma_1))}{\exp(\hat{r}(\sigma_1)) + \exp(\hat{r}(\sigma_2))}$$
The loss function used is a cross-entropy loss: $$\text{loss}(\hat{r}) = - \sum \mu(1) \log P[\sigma_1 \succ \sigma_2] + \mu(2) \log P[\sigma_2 \succ \sigma_1]$$
To calculate the derivative of this loss function with chain rule, we must calculate the partial derivative of $P[\sigma_1 \succ \sigma_2]$  w.r.t. $\hat{r}(\sigma_1)$.

Using the quotient rule, where $f = \exp(\hat{r}(\sigma_1))$ and $g = \exp(\hat{r}(\sigma_1)) + \exp(\hat{r}(\sigma_2))$ so $P[\sigma_1 \succ \sigma_2]= \frac{f}{g}$

$$\frac{d}{d \hat{r}(\sigma_1)} P_{\sigma_1 \succ \sigma_2} = \frac{f'g - fg'}{g^2} = \frac{\exp(\hat{r}(\sigma_1)) \exp(\hat{r}(\sigma_2))}{(\exp(\hat{r}(\sigma_1)) + \exp(\hat{r}(\sigma_2)))^2} = P_{\sigma_1 \succ \sigma_2} (1 - P_{\sigma_1 \succ \sigma_2})$$

We can now apply chain rule to loss function using the derivative from above
$$\begin{align*} 
\frac{\partial \text{loss}}{\partial \hat{r}(\sigma_1)} 
&= -\mu(1) \frac{1}{P_{\sigma_1 \succ \sigma_2}} \frac{\partial P_{\sigma_1 \succ \sigma_2}}{\partial \hat{r}(\sigma_1)} - \mu(2) \frac{1}{P_{\sigma_2 \succ \sigma_1}} \left(-\frac{\partial P_{\sigma_1 \succ \sigma_2}}{\partial \hat{r}(\sigma_1)}\right) \\ 
&= -\mu(1) \frac{P_{\sigma_1 \succ \sigma_2} (1 - P_{\sigma_1 \succ \sigma_2})}{P_{\sigma_1 \succ \sigma_2}} + \mu(2) \frac{P_{\sigma_1 \succ \sigma_2} (1 - P_{\sigma_1 \succ \sigma_2})}{P_{\sigma_2 \succ \sigma_1}} \\ 
&= (\mu(2) - \mu(1)) (1 - P_{\sigma_1 \succ \sigma_2}) 
\end{align*}$$


### Problem 2b
I randomly generated one (489), and I would agree with the label. It's hard to tell the difference between the two clips, but one has a milder knee bend and was labelled as preferred, which seems to align with Hopper's goal to move further more stably.

### Problem 2c
Out of the five samples (489, 3032, 3567, 5938, 5936) I agreed with four out of the five labels. However, some of the differences were extremely subtle and I could see it being labeled either way depending on the person, and the one I disagreed with I strongly disagreed with (3567). Given this small sample, I would say I trust the labeler and the reward function learned on this data. 


