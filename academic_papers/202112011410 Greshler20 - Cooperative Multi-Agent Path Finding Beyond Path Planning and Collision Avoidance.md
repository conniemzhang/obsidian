# Cooperative Multi-Agent Path Finding: Beyond Path Planning and Collision Avoidance
tags = #MRS #MAPF #Paper #CBS
author: Greshler, Nir et.al
source: IEEE MRS 2021


Cooperative Conflict-Based Search
### Main Idea 
* Replaces agent goals from basic MAPF with cooperative tasks.
* Defines cooperative tasks with a set of (initiator, executor) for a pair of robots that consist of going to initialization point, meeting, handing over, and finshing the task.
* Solution is a set of path pairs, and is feasible when there are no conflicts in the paths of P.
* Uses SOC

### Contribution
* adds another level to CVS - meetings space in addition to original conflicts and paths space.
* creates a forest of conflict trees, similar to [19]

### Constraints
* Only works for "well formed" problems i.e. there are points where the agents can stay out of the way infinitely. These are endpoints, and is where the goals/start positions are.

### To-Read
[2] Makespan, Sum of Costs, commong objective functions for classical MAPF
[18] CBS



