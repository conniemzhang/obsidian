# Methods for Flyby Planning
tags = #Planning #Flyby #Convex


**State Space** ; any point that is not on a road, or in a no-fly zone. Can be continuous or discrete. 
**Time** ; Proper sequence implies time, given that the drone must travel. 
**Actions** ; What to do when it encounters a bad state.
**Initial and Goal States**; Restaurant and Customer.
**A Criterion**; currently only feasbility. Would like Optimality, where it optimizes performances in addition to arriving in a goal state.
**A Plan** ; The output plan i.e. sequence of steps to take.

- Our envrionment is largely static, which makes planning easier.

- Relevant Sections of Lavalle's Planning Book:
	- Chapter 2: Discrete Planning
	- Chapter 3: Geometric Representations and Transformations
	- Chapter 4: The Configuration Space
	- PART IV: Planning Under Differential Constraints


- Only need boundary representation for obstacles O, which is an m-sided polygon consisting of features: vertices and edges. This can be represented as the intersection of halfspaces aligned with the edges of the polygon. 
- 