> Connect [Problem statement for research project - corrected](../Formal/Problem%20statement%20for%20research%20project%20-%20corrected.md) with implementation of Alpha algorithm using UPPAAL


### UPPAAL
**SOURCES:**
[Introduction to UPPAAL](../Notes/Introduction%20to%20UPPAAL.md)
[Time in UPPAAL](../Notes/Time%20in%20UPPAAL.md)
[Expressions in UPPAAL](../Notes/Expressions%20in%20UPPAAL.md)
[Verifying properties in UPPAAL](../Notes/Verifying%20properties%20in%20UPPAAL.md)
[Timed automaton](../Notes/Timed%20automaton.md)

>~~What is it?~~
>~~Why use it?~~
>Modelling in UPPAAL
>~~Timed automata~~
>Verifying properties in UPPAAL

"UPPAAL is an integrated tool environment for modeling, simulation and verification of real-time systems. It is appropriate for systems that can be modelled as a collection of non-deterministic processes with finite control structure and real-valued clocks, communicating through channels or shared variables. Typical application areas include real-time controllers and communication protocols in particular, those where timing aspects are critical." ( https://uppaal.org/features/ )

Swarm of robots fits within description of a system that can be modelled using UPPAAL. It is a collection of non-deterministic processes - single robots, that are defined using finite control structure - algorithm that is transformed into finite state machine. Swarm has to communicate and it can be achieved using channels or shared variables. Finally the emergent behaviour is a result of individual robot behaviour which is influenced by the passing time.

UPPAAL is based on a timed automata, which is a finite state machine extended with a finite set of real-valued clocks progressing with the same speed. Clock values can be compared to integers in order to create guards that enable or disable transition between states. Clock values can be reset individually, creating possibility to reuse defined guards and control the frequency of operation. They constitute to the state of the system in the same way as locations of all automata and variable values.




### Alpha algorithm
**SOURCES:**
[Recreating alpha algorithm in UPPAAL pt.1](../Notes/Recreating%20alpha%20algorithm%20in%20UPPAAL%20pt.1.md)
[Recreating alpha algorithm in UPPAAL pt.2](../Notes/Recreating%20alpha%20algorithm%20in%20UPPAAL%20pt.2.md)
[Publications of Alessio Lomuscio](../Notes/Publications%20of%20Alessio%20Lomuscio.md)

> ~~What is it?~~
> ~~Who created it?~~
> ~~Pseudocode~~

Alpha algorithm was introduced by Julien Nembrini in [Minimalist Coherent Swarming of Wireless Networked Autonomous Mobile Robots](../Papers/Minimalist%20Coherent%20Swarming%20of%20Wireless%20Networked%20Autonomous%20Mobile%20Robots.pdf). It was inspired by Kasper Støy's work: [Using Situated Communication in Distributed Autonomous Mobile Robotics](../Relevant%20Papers/Using%20Situated%20Communication%20in%20Distributed%20Autonomous%20Mobile%20Robotics.pdf). Støy proposed and implemented a simple control system for aggregating robots. Instead of relying on environment and localisation information, it uses physical properties of the signal used for communication. Robot behaviour is solely determined by the change in the number of robots that are in the range of its signal.

Alpha algorithm is an approach to an aggregation task within the category of spatial organisation. It is based on assumption that robots send and receive signals through omnidirectional channels like radio or infrared. Single robots make decisions about their movement based only on the number of connections to other robots. The interconnectivity of the swarm is controlled by alpha parameter which is a threshold on desired number of connections for a single robot. 

```
Create a list of neighbours for robot, Nlist
k = number of neighours in Nlist
i = 0

loop forever {
	i = i modulo cadence

	if (i = 0){
		Send ID message

		Save copy of k in LastK
		k = number of neighbours in Nlist

		if ((k < lastK) and (k < alpha)){
			turn robot through 180 degrees
		}
		else if (k > LastK) {
			make random turn
		}
	}

	Steer the robot according to state
	Listen for calls from robots in range
	Grow Nlist with neighbours IDs

	i++
}
```
Pseudocode from [Minimalist Coherent Swarming of Wireless Networked Autonomous Mobile Robots](../Papers/Minimalist%20Coherent%20Swarming%20of%20Wireless%20Networked%20Autonomous%20Mobile%20Robots.pdf)

### Movement
>UPPAAL limitations in choosing random angle
>Resolution and grid like map
>Randomness

### Connection
> Need to mimic technology
> Distance based connection
> UPPAAL limitations
> Use of global functions


### Initialisation

### Randomness

### Clocks

### Global state and global functions

### Automata
>picture of automata
>description of parts
>modelling limitations connected to timed automata and not UPPAAL
