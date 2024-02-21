## Paper - On Formal Specification of Emergent Behaviours in Swarm Robotic Systems
Note on [On Formal Specification of Emergent Behaviours in Swarm Robotic Systems](../Relevant%20Papers/On%20Formal%20Specification%20of%20Emergent%20Behaviours%20in%20Swarm%20Robotic%20Systems.pdf)
Mentioned in: [Towards Temporal Verification of Emergent Behaviours in Swarm Robotic Systems](../Relevant%20Papers/Towards%20Temporal%20Verification%20of%20Emergent%20Behaviours%20in%20Swarm%20Robotic%20Systems.pdf)
Year: **2005**

"This paper explores the use of temporal logic to formally specify, and possibly also prove, the emergent behaviours of a robotic swarm. The paper makes use of a simplified wireless connected swarm as a case study with which to illustrate the approach."

### Formal method for swarm development
1. Formally specify the individual robots, including their safety and liveness properties. 
2. Formally specify the swarm by combining the specifications of individual robots. 
3. Formally specify any anticipated or desired emergent behaviours. 
4. Carry out proofs to determine if the swarm specification satisfies any of the emergent behaviours.

### Safety property
The safety property specifies the set of actions that are allowed. If the robot performs actions from within this set, it will not make the system unsafe.
If we only have the safety property, we cannot guarantee that anything will happen at all.

### Liveness property
The liveness property specifies the dynamic behaviour, the set of eventualities that will occur.
If we only have the liveness property, we cannot guarantee that what is happening is safe.

### Simplified Alpha algorithm
1. The bearing of each robot will have only one of these four values: $N, S, E$ and $W$.
2. The maximum connected distance between two robots is $r_w$ units.
3. At each time step a robot moves $a$ units $(a \ll rw )$.
4. A robot can move forward, turn $90\degree$ left before making a move, turn $90\degree$ right before making a move or turn $180\degree$ back before making a move.
5. Given a robot $i$ in position $x, y$ if another robot $j$ is in the area of circle of radius $r_w$, then robots $i$ and $j$ are 'connected'.
6. We simplify the finite state machine of robot by omitting the avoidance state.
7. We assume a value of $\alpha=1$ so that the loss of any connection triggers the coherence state.

### Desired emergent behaviours
1. "It is repeatedly the case that for each robot, we can find another robot so that they are connected."
2. "Eventually it will always be the case that every robot is connected to at least $k$ robots, where $k$ is a pre-defined constant."



