# Skills found in industry job postings
tags = #career 


## Divergent3D: 
### Robotic printing and modular manufacturing of automobiles.

Role: The lead AI planning development engineer is to develop the advanced AI system to plan robot assembly sequence with temporal, resource and geometric constraints program where this role will be responsible for the following to progress work related to:

• Encode the assembly problem planning optimization either as OR, HTN, or PDDL, or other open standard formats that enable performance scaling via HPC
• Evaluate the existing technology frameworks for sequence planning with capabilities to satisfy constraints from motion planning and design optimization
• Develop the high performance planner that encodes the problem and solve it using an anytime algorithm.
• Develop multi-objective optimization (assembly time and robot utilization) in the planner
• Decode the output and integrate the planner into the cloud platform


OR: Combinatorial #Optimization
[developers.google.com/optimization](Google OR-Toolkit)
OR-Tools is an open source software suite for optimization, tuned for tackling the world's toughest problems in vehicle routing, flows, integer and linear programming, and constraint programming.

After modeling your problem in the programming language of your choice, you can use any of a half dozen solvers to solve it; commercial solvers such as Gurobi or CPLEX, or open-source solvers such as SCIP, GLPK, or Google's GLOP and award-winning CP-SAT



HTN: Hierarchical Task Network
[en.wikipedia.org/wiki/Hierarchical_task_network](Wikipedia)
Hierarchical task network (HTN) planning is an approach to automated planning in which the dependency among actions can be given in the form of hierarchically structured networks.

Planning problems are specified in the hierarchical task network approach by providing a set of tasks, which can be;

1. primitive (initial state) tasks, which roughly correspond to the actions of STRIPS;
2. compound tasks (intermediate state), which can be seen as composed of a set of simpler tasks;
3. goal tasks (goal state), which roughly corresponds to the goals of STRIPS, but are more general.


PDDL: 
[en.wikipedia.org/wiki/Planning_Domain_Definition_Language](Wikipedia)
[[202203221456]](MAPL)
- Language defined in 2000
- Modeled planning problems in two major parts
	1. Domain descriptoin
	2. Problem description
- Domain and problem form a **input** of a planner, which aims to solve the given planning-problem via some appropriate planning algorithm
- Output is not specified with PDDL, but is usually a plan i.e. a sequence of actions

**domain description**
- domain-name description
- definition of requirements
- definition of object-type hierarchy
- definition of constant objects
etc, see wiki for details. Same for problem description. 


