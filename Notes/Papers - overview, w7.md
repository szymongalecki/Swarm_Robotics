## Papers - overview, w7

### "Towards Temporal Verification of Emergent Behaviours in Swarm Robotic Systems" - C. Dixon, A. Winfield, and M. Fisher
From: [Towards Autonomous Robotic Systems](../Books/Towards%20Autonomous%20Robotic%20Systems.pdf)
Referenced in: [Property-driven design for swarm robotics](../Papers/Property-driven%20design%20for%20swarm%20robotics.pdf)

This paper focuses on formal verification, particularly on model-checking. Model of all possible behaviors of the system is constructed and assessed against a logical formula which in this case is temporal.

The logic considered is propositional linear-time temporal logic, called PTL.
Only two temporal operators are used:
- Sometime in the future
- Always in the future

Input to the model checker is a model of the paths through a system and a formula to be checked on that model. The language of the formula to be checked is usually some form of temporal logic for example the linear-time temporal logic, PTL, or the branching-time temporal logic, CTL. A number of model checkers have been developed but we will use **NuSMV** which allows properties expressed in both CTL and PTL.

Essentially, we construct a set of finite-state transition systems, correspond- ing to each of the robots in the swarm, and then model-check a PTL formula against the concurrent composition of these transition systems. If there are execution paths of the system that do not satisfy the required temporal formula, then at least one such “failing” path will be returned as a counter-example.

The basic alpha algorithm:
- The default behaviour of a robot is forward motion.
- While moving each robot periodically sends an “Are you there?” message. It will receive “Yes, I am here” messages only from those robots that are in range, namely its neighbours.
- If the number of a robot’s neighbours should fall below the threshold alpha then it assumes it is moving out of the swarm and will execute a 180 degrees turn
- When the number of neighbours rises above alpha (when the swarm is regained) the robot then executes a random turn. This is to avoid the swarm simply collapsing in on itself.

Model checking approach limited the state-space by using small grid (5x5 to 8x8) and small swarm sizes (2 to 3).