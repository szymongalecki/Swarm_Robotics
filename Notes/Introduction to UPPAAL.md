## Introduction to UPPAAL
UPPAAL is an integrated tool environment for modeling, simulation and verification of real-time systems. It is appropriate for systems that can be modelled as a collection of non-deterministic processes with finite control structure and real-valued clocks, communicating through channels or shared variables. Typical application areas include real-time controllers and communication protocols in particular, those where timing aspects are critical.

### Main parts of UPPAAL
- Description language
	- Non-deterministic guarded command language with data types. It serves as a modeling or design language to describe system behavior as networks of automata extended with clock and data variables.
	- [Guarded commands](Guarded%20commands.md)
- Simulator
	- The simulator is a validation tool which enables examination of possible dynamic executions of a system during early design stages and thus provides an inexpensive mean of fault detection prior to verification by the model-checker which covers the exhaustive dynamic behavior of the system.
- Model-checker
	- The model-checker can check invariant and reachability properties by exploring the state-space of a system, i.e. reachability analysis in terms of symbolic states represented by constraints.
	- To facilitate modeling and debugging, the UPPAAL model-checker may automatically generate a diagnostic trace that explains why a property is (or is not) satisfied by a system description.
	- [Model checking](Model%20checking.md)
