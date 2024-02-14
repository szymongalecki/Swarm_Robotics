## Concurrency within swarm
An important variety of abstraction concerns the representation of concurrent activity within the swarm of robots. Thus, in modelling this aspect we must ask questions about whether all robots run simultaneously, whether some robots run faster than others, etc.  
Choice of concurrency model can significantly affect the results of model checking.

### Synchrony
All robots execute at the same time and with the same clock.

### Strict turn taking
Execution of the robots is essentially interleaved but the robots must execute in a certain order: 1, 2, 3, 1, 2, 3....

### Non strict turn taking
Execution of the robots is again interleaved but for m robots in every cycle of m steps each robot moves once, so we can now have a situation where a robot executes two steps consecutively: 1, 2, 3, 3, 2, 1...

### Fair asynchrony
Robots execute at the same time, yet some robots are faster than others. However the fair aspect ensures that a robot can only take a finite number of steps before all other robots have finished their step.

From: [Towards Autonomous Robotic Systems](../Books/Towards%20Autonomous%20Robotic%20Systems.pdf)
