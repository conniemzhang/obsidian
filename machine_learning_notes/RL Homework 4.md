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
I ran with early termination. I was surprised by how well it performed - it did in fact jump forward and only fell over for the last few seconds. The behavior itself looks expected, it bent the knee to create force to leap forward and repeat. It skips more "on the toes" than one would maybe try manually. 

### Problem 1g
I ran with the same seed and no early termination. This Hopper barely moved, appearing to "trip" and fall on the floor and spend the rest of the video vibrating. The one with early termination is strongly preferred over this rollout.


## Problem 2
### Problem 2a
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


## Problem 3
### Problem 3d


## Problem 4
### Problem 4a
After a read through the paper in problem (4c), it seems that raters are generally minorities and young people - both generally in lower socioeconomic groups and mixed grasp of English. The selected human raters are not representative of the general population and therefore would rate based on their own biases. This would mean that bias would be introduced into the model in harmful ways. Ethically, it means selecting for candidates that fit a certain profile to balance your model which is no longer fair to all applicants. It also means data annotation is likely not paid well, and is being outsourced to those who need the work but will not benefit from the products.

### Problem 4b
There is only one correct answer for medical diagnoses, so RLHF would not be a good way to train a system to make medical diagnoses. This is because the human trainers would need to be experienced doctors, and even so, a doctor may be wrong which would skew the results. 
With medical data specifically, there are also privacy concerns which are protected with laws like HIPAA, which would make obtaining good data difficult. Medical conditions also progress over time, making it hard to quantify as a data set as it would be very difficult to capture the full context that lead to a diagnosis. 


### Problem 4c
The paper describes the logistical issues of using people including cost/quality, limitations of types of feedback, oversight costs, and human mistakes and irrationality. It also describes challenges with the reward model itself. It's difficult to represent a human's values with a reward function, because humans have a lot of context that cannot be captured in a binary choice. The difficulty of creating these reward models means they can misgeneralize to be poor reward proxies, and could lead to reward hacking. Policies also are hard to optimize effectively, and can be adversarially exploited by humans and other AI systems -- another compelling reason to not use them for medical diagnoses.
