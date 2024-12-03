## Problem 1f
When using a WEAK current strength, the largest discount factor that prevents the agent from swimming RIGHT is ~0.6. 

When using MEDIUM, the first time it doesn't swim right is at ~0.75

When using STRONG, the first time it doesn't swim right is ~0.9

When the discount factor is low, it prioritizes more immediate outcomes. As the current increases, it requires looking further ahead to justify moving against the current. This matches with what we see - as the current increases in strength, the discount factor takes into account future rewards. 



<div style="page-break-after: always;"></div>

## Problem 2a.
Yes, it is possible to choose a value of H that results the optimal policy, if H is sufficiently large to allow the agent to reach the terminal reward of +100. If it starts out selling, it can then switch to buying until it increases the stock to reach s = 10, which is the terminal reward.

### Problem 2b
The fully stocked inventory is when s = 10. The fastest way to reach that starting from s = 3 is to execute only buys, which is 7 steps into the future. Therefore, the range of H to reach full inventory must be any time horizon greater than 7: $H\geq7$.

### Problem 2c
When $\gamma = 0$, the agent considers only immediate rewards and no future rewards. If s = 3, selling provides an immediate reward of +1, and buying provides no immediate reward +0, so the policy will sell. 

When s = 9, buying provides a reward of +100, but selling only rewards +1, so the policy will buy.

### Problem 2d
Yes, if starting at s = 3 and with a very low gamma value (closer to zero), the policy will not weigh the final +100 more than it weighs immediate reward. Therefore, it will prioritize selling until s = 0, and never switch to buying. 

<div style="page-break-after: always;"></div>


## Problem 3a.
If the red car merges into the highway, it must do so at a velocity lower than the grey cars, and the grey cars must also slow down to allow the merge. This lowers the mean velocity, which lowers the reward for merging, so that the optimal policy for the red car is to remain stationary and keep it's velocity at zero to avoid lowering the velocity of everyone else.


## Problem 3b.
One alteration may be to account for distance travelled. For instance, this could look like:
$$ R = \alpha \cdot \text{Mean Velocity} + \beta \cdot d_{\text{AI}}$$
where $d_{\text{AI}}$ is the total distance traveled by the AI car. This ensures that the AI car is incentivized to merge and make progress on the road, as remaining parked would result in zero distance traveled and a lower reward.

Other options could include measuring how many cars are using the highway, or add a penalty for idle time. Both of these options actively encourage participation in traffic, but also reward finishing the commute quickly.

