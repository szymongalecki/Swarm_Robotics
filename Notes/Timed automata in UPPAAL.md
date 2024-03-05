## Timed automata in UPPAAL
 The UPPAAL modelling language extends timed automata with the following additional features.
### Templates 
Templates automata are defined with a set of parameters that can be of any type (e.g., `int`, `chan`). These parameters are substituted for a given argument in the process declaration. 
### Constants
Constants are declared as `const name value`. Constants by definition cannot be modified and must have an integer value. 
### Bounded integer variables
Bounded integer variables are declared as `int[min, max]` name, where `min` and `max` are the lower and upper bound, respectively. Guards, invariants, and assignments may contain expressions ranging over bounded integer variables. The bounds are checked upon verification and violating a bound leads to an invalid state that is discarded (at run-time). If the bounds are omitted, the default range of -32768 to 32768 is used.
### Binary synchronisation channels
Binary synchronisation channels are declared as `chan c`. An edge labelled with `c!` synchronises with another labelled `c?`. A synchronisation pair is chosen non-deterministically if several combinations are enabled. 
### Broadcast channels
Broadcast channels are declared as `broadcast chan c`. In a broadcast synchronisation one sender `c!` can synchronise with an arbitrary number of receivers `c?`. Any receiver than can synchronise in the current state must do so. If there are no receivers, then the sender can still execute the `c!` action, i.e. broadcast sending is never blocking.
### Urgent synchronisation
Urgent synchronisation channels are declared by prefixing the channel declaration with the keyword `urgent`. Delays must not occur if a synchronisation transition on an urgent channel is enabled. Edges using urgent channels for synchronisation cannot have time constraints, i.e., no clock guards. 
### Urgent locations
Urgent locations are semantically equivalent to adding an extra clock `x`, that is reset on all incoming edges, and having an invariant `x<=0` on the location. Hence, time is not allowed to pass when the system is in an urgent location. 
### Committed location
Committed locations are even more restrictive on the execution than urgent locations. A state is committed if any of the locations in the state is committed. A committed state cannot delay and the next transition must involve an outgoing edge of at least one of the committed locations. 
### Arrays
Arrays are allowed for clocks, channels, constants and integer variables. They are defined by appending a size to the variable name, e.g. `chan c[4]; clock a[2]; int[3,5] u[7];`. 
### Initialisers
Initialisers are used to initialise integer variables and arrays of integer variables. For instance, `int i = 2; or int i[3] = {1, 2, 3};`. 
### Record types
Record types are declared with the *struct* construct like in C. 
### Custom types
Custom types are defined with the C-like `typedef` construct. You can define any custom-type from other basic types such as records. 
### User functions
User functions are defined either globally or locally to templates. Template parameters are accessible from local functions. The syntax is similar to C except that there is no pointer. C++ syntax for references is supported for the arguments only.

[Timed automaton](Timed%20automaton.md)
