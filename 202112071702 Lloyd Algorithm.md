# Lloyd Algorithm
tags = #notes #robotics 

Voronoi iteration, evently spaced sets of points in subsets of Euclidean spaces into well-shaped and uniformly sized convex cells. 

Related to k-means clustering [[202112071709]]

_Algorithm_
Lloyd's algorithm starts by an initial placement of some number k of point sites in the input domain. In mesh-smoothing applications, these would be the vertices of the mesh to be smoothed; in other applications they may be placed at random or by intersecting a uniform triangular mesh of the appropriate size with the input domain.

It then repeatedly executes the following relaxation step:
	1. The Voronoi diagram of the k sites is computed.
	2. Each cell of the Voronoi diagram is integrated, and the centroid is computed.
	3. Each site is then moved to the centroid of its Voronoi cell.

_Difficulties_
1. It may be hard to find the centroid of a Voronoi cell, esp. in inputs dimension higher than two.
	a. Can approximate: 
		* like averaging the positions of all the "pixels" in a region
		* Monte Carlo methods can be used.
	b. Exact computation:
		* Takes advantage of convex shapes, see wikipedia for more detail [link](en.wikipedia.org/wiki/Lloyd%27s_algorithm)

### Used in
[[202112061737]] Cortes - Coverage control for mobile sensing networks
[[202111301125]] Santos - multi-robot learning and coverage of unknown spatial fields.

[img](img/lloyds_algorithm.png)


