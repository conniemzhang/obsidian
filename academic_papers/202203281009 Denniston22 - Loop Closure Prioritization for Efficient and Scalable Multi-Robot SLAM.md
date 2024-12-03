# Denniston22 - Loop Closure Prioritization for Efficient and Scalable Multi-Robot SLAM
tags = #SLAM #MRSLAM #SubT


### Main Idea
Prioritization of certain loop closure candidates to address the complexities of multi-robot SLAM. 
Centralized SLAM
Has beacons in the envrionment and uses RSSI for proximity detection.
Uses Graph Neural Network for interefence on pose graph 
Uses Simulation Annealing to maximize information-based objective function

Active SLAM
	- Others concerned about guiding robot navigation [3][10], whereas he is more concerned about minimizing computational load induced by loop closure.

_3 Modules_
1. Graph Information Prioritization
	- uses a graph neural network to determine which loop closure cnadiates would decrease the error the most if added to the graph
2. Observability Prioritization Module
	- 
3. RSSSI Priotitization Modile
	- Loop closues close to a known radio beacon

### Thoughts
- Yes, it's theoretically multi-robot but doesn't take much advantage, it's pretty much just single robot SLAM over and over again? Doesn't seem like there's much cross-referencing?


### References
[3] Max a posteriori inference in a pose graph
[4] Graph Neural Network
[5] Generalizes convolutional neural networks to graph based domains using mixture models
[6] Graph neural network for selectin submodular actions *
[17] Graduated Non-Convexity for pose graph optimization
To quantify how feature-rich or feature-poor a point
cloud scan is, we draw inspiration from the observability
metric and inverse condition number presented in [23], [24]
where the observability is described in terms of the minimum
eigenvalue of the Information matrix A of the Point-To-Plane
ICP cost for two clouds i and j.

