### ARMS Feedback
- Equation problems and unclear
	- theta
	- Equation 1, why is B equal to an inequality
- The problem is too simple in R^2, and existing methods already solve this in SE(2), and they would only care about the harder case of dense stitching with UAVs in full SE(2)
- Algorithm unclear
	- generate step vector is presented but not explained
- Not multi-robot enough
	- Does not describe how UAVs might be controlled or coordinated to obtain the imge
- Experiments weak
	- No details on the sizes of data sets used, number of experimental runs (stochastic elements or deterministic)
- How is "niceness" defined, how do you know what amount of information is necessary in firefighting, or any other domain.
- Section 1.1 states: "Drones will always have a measure of error in their localization". What about using rtk-gps + imu information? Wouldn’t this help with position accuracy? Doesn't your method rely on some level of accuracy? Aren't the results also dependent on actual flight height (z) and therefore real ground area covered per pixel? This is unclear.

- Section 2 describes the method, but the details are not clear. Is $Q \in R^2$ meant to be some variable $R$ or $\Re$ ? How is $n_i$ expressed? How is $q$ expressed (equation 1)? What is theta--is this angular FOV?

- Do all UAVs have the same height (z)? This isn't practical as actually each image should have it's own z.

- The top of page 7 describes ${\cal B}(a_n)$. Is this the same $n$ as previously ($n_i$)? If so, then why not use ${\cal B}(a_{ni})$ and $\cal{B}(a_{nj}$ instead of $a_n$ and $a_m$ ? If not, then it's unclear what $n$ is denoting.

* It's unclear how time is taken into consideration in the model.

* Near the top of page 8, this sentence is found: "To improve speed, some of the feature detection and matching could be done on a central computer..." which seems to contract the statement near the top of page 4: "our method is decentralized"

* Section 2.2 defines a graph G. It is unclear whether the geographical relationship amongst vertices is represented in the graph data structure.

* Section 3.1 presents results, illustrated in Figure 7, but the method for obtaining these results is not described. What experiments were run? How many? The same comment goes for Sections 3.2 and 3.3 and the rest of Section 3. Table 1 presents "average" results -- average over what?

- [ ] What the fuck is the difference between SE(2) and SE(3)?
- [ ] NEED a metric for coverage. Something that defines the information gain. 
- [ ] Add the meaning of the step vector.
- [ ] Future work needs to include multi-robot pathing or coverage.



Addressing Problems
1. The current application in R^2 is too simple
2. Vague, empirical nature of the method
3. Intractability of having no defined region of interest, and the continuous possible placements of the cameras.
**

-   Calculating the amount of information gained as a function. 
    
-   Q is your current position but you’re allowed to go beyond the boundary?
    

**
**FORMULATION OPTION** 
We cover a convex region with a simple back and forth motion, 
Multi robot at the rotation points.
Needs to stop every step to reposition the cameras.
Builds a grid so that it can compare the edges of the robot. 
- The objectives of the monitoring coverage task is maximizing the monitored region of the AOI and minimizing the total travel length of the agents. 
- cost is how far the robots would have to move to get into that new position.
- Rotations are the cheapest. 

There is some large envrionment $Q$ that has already been decompsed into cells that can be covered by the lawnmower method. The area $Q$ is covered when every point $p$ has appeared in a camera FOV at any step. The most efficient completion of this goal is when the UAV trajectory is minimally redundant, which is simple to accomplish with a single UAV at a known altitude. This method proposes to cover $Q$ with a team of robots, where part of the stitching is achieved while the path is being planned, and the total size of the FOV is variable at every step.

You have some number of robots $N$ each equipped with a single downward facing camera. The pathing algorithm considers the entire group as a single large robot with the size of the convex hull of the FOVs. The pathing algorithm moves the robots in steps, where the next step only overlaps slightly with the previous (large, discrete steps).  
i.e. move -> stop -> stitch -> replan -> move

The placement of the cameras at each step can be reduced to a camera placement problem, where the output needs to be stitched. 

To ensure that the image can be stitched from previous path, we keep a sparse map of the previous positions, where at each time step the adjacent images are added as virtual FOVs that have a possible step size of zero. 


Cells should be mostly larger than the formation. 
* doesn't make as much as sense bc your task will largely be over before the number of features change dramatically
* why the fuck woldn't you just use a static camera array. 
	* Cameras are heavy, drones are cheap
	* You can't fly a drone with a giant camera array attached
* Why would you want to be able to have a partial panorama? 
* Seriously who the fuck asked for this
Our objective is successful when a complete panorama can be built at any time. 

**CAMERA PLACEMENT FORMULATION 1**
Continuous space, gradient proof of stability
Lasalle, Lipschitz, and Lyapunov.
Let $p_i \in \cal P$ represent the state of camera $i$
We wnat to control $n$ cameras such that their placement maximizes information gathered per step but allows for image stitching. 
 
**CAMERA PLACEMENT FORMULATION 2**
Pick and place w/ greedy algorithm. 
The movement is restricted to like 3 rotations, 3 positions. 6^n possible positions total. 

**FORMULATION OPTION**
We use some sort of fire model and more analysis on what firefighters need nto actually fight a fire. We try to maintain that. This isthe human one where you manually move aorund your position. This would be probable for inspection methods. 

FORMULATION OPTION: 
Camera placement, but the information is the amount of gorund covered by a pixel, where the quality goes down if the camera is above some $z$ , and the cameras are mostly static except that they can zoom out to capture more features,. 
- Features will change with distance, so you may fail to match features when the z axis changes. 
- 


FORMUALTION OPTION
Long term monitoring of an area, but it includes z axis and rotation. 


We expect this to be incorporated into a path planning algorithm, so it stands that there is a maximal amount of distance

We use continuous space but discrete time. In each time step, the optimization is solved for a static system. The optimization is over all possible sets of rotation and translation, however, allowing for uncontrained camera poses makes the problem ill defined. Instead, we impose a constrain based on the maximal distance d that a drone could move in timestemp t, and only allow for planar rotation of the FOV, and that the camera can only be placed along the same z axis. This gives the cameras only  3 degrees of freedom - two translational and one rotational.

Rather than using a method where each camera array will have to be checked for optimality, we use a control based method. We project an virtual space, an unlimited environment over which to optimize. 

Where to put the robots?

You cannot optimize. What else can I prove about this system? It converges? 
- You can offer a greedy suboptimal method.

** The threshold for overlap is zero if the exact positions of the cameras are known. However, as uncertainty about the position of environment grows, the amount of overlap required increases as well. What does not change it the number of features needed for successful image stitching. 


Can I do something to minimize the uncertainty? 
1. Restrict movement to four cardinal directions
2. 


SLIDES
Possible Solution: We are finding the maximal convex hull of the formation, however, this would cause most things to be a square, and would be undefined if you have a square that requires more robots than the ones just at the vertices.


the difficulty of this task lies in the infinite possibilties of the camera placements, which is different than existing camera placement literature that has pre-defined places to put cameras. 

And that the local coverage is ill-defined. 
Therefore we have proposed this gradient method that shows promising results. 

**COST FUNCTION DEFINITION**
We gave $R = R_i, i = 1, 2...N$ cameras we want to place in the envrionment.


$\argmin_R  H(R) \text{ where } R \in A \cap C$ 
H(R) is the cost function. 

$\mu(C)$ 

\mu is the utility function of the camera network. It is 


Slide 1: Definition of  problem
Slide 2: Definition of the camera the camera definit
Slide 3: Intro to the cost function (or algorithm if I can't finish this)
Slide 4: 




