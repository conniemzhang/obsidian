# Paper-Cortes-Coverage control for mobile sensing networks
tags = #Paper #Seminal #Coverage #Networks #Communication

-incomplete. Complex paper that i barely understand the math for-

### Summary


### Main Idea
* Lloyd descent algorithms [[202112071702]] that take consider constraints of mobile sensing network.
* Distributed, Adaptive, Asynchronous, Verifiably asymptotically correct
* 

### Method 
* minimizing the locational optimization function subject to a density function
* A proof that due to the parallel axis theorm, the centroids of the Voronoi partitions is the local minimum point for the cost function.
1. Discrete time lloyd algorithm
	* Maps to T over the space, such that for the distance from T(all sensors) to the centroid is less than distance from position to the centroid.  
	* If P is not centroidal, then there's a better position _j_ that will create the inequality.
	* So then H_v is a descent function for the algorithm T
.


### References
[10] Q. Du, V. Faber, and M. Gunzburger, “Centroidal Voronoi tessellations: applications and algorithms,” SIAM Review, vol. 41, no. 4, pp. 637–676, 1999.


### Referenced By
[[202111301125]] Santos - multi-robot learning and coverage of unknown spatial fields.

