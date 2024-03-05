## Timed automata in UPPAAL
 The UPPAAL modelling language extends timed automata with the following additional features.
### Templates 
Templates automata are defined with a set of parameters that can be of any type (e.g., **int**, **chan**). These parameters are substituted for a given argument in the process declaration. 
### Constants
Constants are declared as **const name value**. Constants by definition cannot be modified and must have an integer value. 
### Bounded integer variables
Bounded integer variables are declared as **int(min, max)** name, where **min** and **max** are the lower and upper bound, respectively. Guards, invariants, and assignments may contain expressions ranging over bounded integer variables. The bounds are checked upon verification and violating a bound leads to an invalid state that is discarded (at run-time). If the bounds are omitted, the default range of -32768 to 32768 is used.

[Timed automaton](Timed%20automaton.md)
