## Timed automaton
A timed automaton is a tuple $(L, l_0, C, A, E, I)$ where 
- $L$ is a set of locations, 
- $l_0 \in L$ is the initial location, 
- $C$ is the set of clocks, 
- $A$ is a set of actions, co-actions and the internal $\tau$ - action, 
- $E \subseteq L \times A \times B(C) \times 2^C \times L$ is a set of edges between locations with an action, a guard and a set of clocks to be reset,
- $I : L \rightarrow B(C)$ assigns invariants to locations.


In automata theory, a timed automaton is a [Finite-state machine](Finite-state%20machine.md) extended with a finite set of real-valued clocks. During a run of a timed automaton, clock values increase all with the same speed. Along the transitions of the automaton, clock values can be compared to integers. These comparisons form guards that may enable or disable transitions and by doing so constrain the possible behaviors of the automaton. Further, clocks can be reset.

In UPPAAL, a system is modelled as a network of several such timed automata in parallel. The model is further extended with bounded discrete variables that are part of the state. These variables are used as in programming languages: They are read, written, and are subject to common arithmetic operations. 

A **state of the system** is defined by the locations of all automata, the clock values, and the values of the discrete variables. Every automaton may fire an edge (sometimes misleadingly called a transition) separately or synchronise with another automaton, which leads to a new state.