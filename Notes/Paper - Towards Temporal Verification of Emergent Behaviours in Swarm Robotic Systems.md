### Paper - Towards Temporal Verification of Emergent Behaviours in Swarm Robotic Systems
From: [Towards Temporal Verification of Emergent Behaviours in Swarm Robotic Systems](../Relevant%20Papers/Towards%20Temporal%20Verification%20of%20Emergent%20Behaviours%20in%20Swarm%20Robotic%20Systems.pdf) 
Referenced in: [Property-driven design for swarm robotics](../Relevant%20Papers/Property-Driven%20Design%20for%20Swarm%20Robotics.pdf)  
Year: **2011**  

This paper focuses on formal verification, particularly on [Model checking](Model%20checking.html) . Model of all possible behaviors of the system is constructed and assessed against a logical formula which in this case is temporal. [Temporal verification](Temporal%20verification.html)

The logic considered is propositional linear-time temporal logic, called PTL.
Only two temporal operators are used:
- Sometime in the future
- Always in the future

Input to the model checker is a model of the paths through a system and a formula to be checked on that model. The language of the formula to be checked is usually some form of temporal logic for example the linear-time temporal logic, PTL, or the branching-time temporal logic, CTL. A number of model checkers have been developed but we will use **NuSMV** which allows properties expressed in both CTL and PTL.

Essentially, we construct a set of finite-state transition systems, correspond- ing to each of the robots in the swarm, and then model-check a PTL formula against the concurrent composition of these transition systems. If there are execution paths of the system that do not satisfy the required temporal formula, then at least one such “failing” path will be returned as a counter-example.

The basic alpha algorithm:
- The default behaviour of a robot is forward motion.
- While moving each robot periodically sends an “Are you there?” message. It will receive “Yes, I am here” messages only from those robots that are in range, namely its neighbours.
- If the number of a robot’s neighbours should fall below the threshold alpha then it assumes it is moving out of the swarm and will execute a $180\degree$ turn
- When the number of neighbours rises above alpha (when the swarm is regained) the robot then executes a random turn. This is to avoid the swarm simply collapsing in on itself.

Model checking approach limited the state-space by using small grid (5x5 to 8x8) and small swarm sizes (2 to 3). Obviously we would like to consider larger number of robots and, even with the above observation, may need to consider larger grid sizes but we are faced by the well known [State explosion problem](State%20explosion%20problem.html). Even with the simplifications we use here, the state space explored is huge. Modelling a robot’s position on an $n × n$ grid, with 4 directions, and two motion modes for r robots requires of the order of $(n × n × 4 × 2)^r$ states to be explored.