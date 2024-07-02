**SOURCES:**
[Recreating basic algorithm in UPPAAL pt.1](../Notes/Recreating%20basic%20algorithm%20in%20UPPAAL%20pt.1.md)
[Recreating basic algorithm in UPPAAL pt.2](../Notes/Recreating%20basic%20algorithm%20in%20UPPAAL%20pt.2.md)
[Recreating basic algorithm in UPPAAL pt.3](../Notes/Recreating%20basic%20algorithm%20in%20UPPAAL%20pt.3.md)
[Recreating alpha algorithm in UPPAAL pt.1](../Notes/Recreating%20alpha%20algorithm%20in%20UPPAAL%20pt.1.md)
[Recreating alpha algorithm in UPPAAL pt.2](../Notes/Recreating%20alpha%20algorithm%20in%20UPPAAL%20pt.2.md)


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
> What is it?
> Who created it?
> Pseudocode

### Movement
>UPPAAL limitations in choosing random angle
>Resolution and grid like map
>Randomness

### Connection
> Need to mimic technology
> Distance based connection
> UPPAAL limitations
> Use of global functions
> 


