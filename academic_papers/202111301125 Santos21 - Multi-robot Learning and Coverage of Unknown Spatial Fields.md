# Santos Multi-robot Learning and Coverage of Unknown Spatial Fields
tags = #Paper #IEEE-MRS #Coverage #Local-Coverage-With-Stitching


### Summary

### Main Idea
* Learning/movement tradeoff to optimally cover a space with an unknown envrionmental distribution
* TWo algorithms for this. 

### Method
* explores the space AND optimally covers it in mostly one step (two sampling strategies)
* Creates voronoi "regions of interest"
* Gaussian processes for field estimation of \phi, the density function that is learned online. 
	* Uses a linear model fot he bean and a squared-exponential kernal for covariance. Why? 
	* Thus, the unknown density function can be described with a [[202112061637]](Gaussian process),
	φ(·) ∼ GP(µ(·, ρ), k(·, ·, τ )).
* Unknown hyperparameters estimated through data using maximum likelihood estimation. 


### Links
Uses variation of Llyods Algorithm [[202112071702]]

### References
environmental features are optimally monitored [1], [2], [3], [4]
J. Cortes, S. Martinez, T. Karatas, and F. Bullo, “Coverage control for mobile sensing networks,”

F. Bullo, J. Cortes, and S. Martınez, Distributed Control of Robotic
Networks: A Mathematical Approach to Motion Coordination Algorithms. Princeton University Press, 2009.


M. Schwager, J. McLurkin, and D. [[202112061737]], “Distributed coverage control
with sensory feedback for networked robots,” in Proceedings of
Robotics: Science and Systems, 2006

L. C. A. Pimenta, V. Kumar, R. C. Mesquita, and G. A. S. Pereira,
“Sensing and coverage for a network of heterogeneous robots,” in 2008
47th IEEE Conference on Decision and Control, 2008, pp. 3947–3952.





