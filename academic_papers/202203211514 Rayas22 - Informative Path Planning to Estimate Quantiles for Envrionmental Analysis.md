# Rayas22 - Informative Path Planning to Estimate Quantiles for Envrionmental Analysis
tags = #IPP




### Main Idea
- Robot planning using objective function to improve estimates of quantile values
- Baseline: 
	- Spreading out. 
	- Entropy Optimization
	- Sequential Bayesian Optimization
- Them: perform adaptive robotic survey to find locations for scientific analysis. 

### Contribution
1. A planner with custom objective functions for adaptively increasing the quality of estimated quantiles
2. A method to select spatial locations which have the values estimated for the quantiles
3. Quantitative evaluation of our method on point and cmaera sensors with previously collected aquatic datasets
4. A demonstration of our method on a robot in real-world crop health estimation task.


### Methods
_Online IPP_ - alternate between planning and taking an action. The plan is made up of steps, until the cost exceeds some predefined budget. 

_Estimation of Quantiles and Quantile Standard Error_ - They use Gaussian Kernel density estimator to estimate the standard error when planning. Other methods include Maritz-Jarrett. Bootstrap, jacknife  calculate quantiles over repeatedly sampled subsets of data, but the these are slow. 

_Formulation_
1. Grid-based
2. Two steps; survey and selection



### References
[11] IPP as POMPDP: 
[5] IPP as POMDP for finding maxima: 
[2]Adapt parameters of a rollout-based POMPDP solver online: 
[17] Statistical techniques: 
[19] Cross-entropy method for Continuous Non-Convex Gradient-Free Optimization: 
[20] Simulated Annealing:
[21] [5] [23] [22] Bayesian optimization: 





what the the metric of success? What advantage does maximizing quantiles offer over other estimations?