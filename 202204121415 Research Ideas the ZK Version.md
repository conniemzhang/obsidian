#Research Ideas the ZK Version
tags = #Ideas #Research 

**Robustness and Resilience in Multi-Robot Systems**
	- Ties in a little better with the quals work
	- Can definitely use some sort of CNN 
	- Can I create a semantic map of a wildfire?


**Because I already know the features in each image, can I use them to do some sort of semantic mapping?**
	- [[202205052011 Robotic Semantics]]
	- Cleveland2015 - An automated system for semantic object labeling with soft object recognition and dynamic programming segmentation
		-  generates semantic maps in retail environments using point clouds to recognize and label objects - from the 3D information the system uses SIFT features to perform classification
	- Polastro10 - Semantic mapping with a probabilistic description logic
		- Characterize different areas


Right now I am moving away from multi-robot stuff, just because I haven't really been able to find an interesting problem to work on within it. Specifically, my attempts have just been singular robots over and over again rather than true multi-robot where the individuals are able to contribute uniquely or effectively to the team for real, additional benefits. It also hasn't addressed overcoming any of hte unique challenges about MRS, specifically commiunication, data sharing, viewpoints, etc. TODO: I need to look at the current MRS research from the past year and a half to see if there is actually any overlap I can utilize. 


Chris proposal is to use quantile regression and a quantile loss function instead of Gaussian regression or maximum loss value to better represent the uncertainty for certain data sets. Data sets such as location uncertainty 
Such as in a POMCP where he previously replaced the observation with a maximum likelihood value, and now he would replace that with a sample represented by the quantile values?

**When you move a team of robots around turns, how does your formation change? What's the most optimal reassignment?**
Rder

In order to offer guarantees of coverage in a an area, we need to have some sort of decomposition of the space. Schwager uses the pixel breakdown of the area, is it possible that we can use a feature breakdown of the area? We assume that each feature should not travel very far, is it possible to select which features are most likely to work, and therefore reduce the overlap such that the number of features is as low as possible?

It's almost unfair since all learning methods are nearly heuristic anyways, why can't I have a heuristic coverage method.

We consider each time step to be a camera placement problem, where the environment to be covered is the maximum scene possible for the current formation with zero overlap?

But how would you do coverage with a variable robot size?

You also want it to be fault tolerant I.e. the definition of the camera placement needs to work no matter how many cameras there are in the environment. That way you can argue that this is robust to failure of any types.

Still not getting a ton of good formulation options.
1. Define the area that you are covering
2. Definte how you plan to cover it with stitching guarantee.

ow did they prove their algorithm? (41) for continuous space.

Butler et.al they use a decoupled version that makes it easier to prove. 

### The Learning Zone

Also to investigate is the convex optimization technique that chooses a domain then checks to see if the answer is in it. That's also approximately where I got lost in class. 

What are the different types of neural networks?
Graph convolution, fully convolution, Bayesian deep learning??