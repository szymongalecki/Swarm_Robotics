## Model checking
Model checking is an approach for verifying the temporal behavior of a system. Model is a representation of the system with the right level of granularity. Specification is a high-level desired property of the system. Model checking involves exhaustively exploring all possible states of a finite-state model of the system to check if certain properties hold.

From: [Model checking - Stanford lecture](../PDFs/Model%20checking%20-%20Stanford%20lecture.pdf)

### Modeling
Model checking typically operates over transition systems.
A transitions system is <S, I, T>
- S - a set of states
- I - a set of initial states
- T - a transition relation: T is subset or equal to  S x S
	- A transition T(s0, s1) holds when there is a transition from s0 to s1

In practice a transition system is <V, I, T>
- V - a set of state variables where V' denotes next state variables
- I - a set of initial states
- T - a transition relation defined on V and V'

### State machine vs execution
State machine describes possible states and transitions while an execution is a single path through that state machine.

### Specification
Original approaches only considered equivalence between models: "M1 implements M_2 exactly"
Duality between model and specification
- The specification is itself a model
- It can be a partially specified model
- Can have loose definitions of timing
- Specification is typically higher-level, abstract behavior

### Safety
*Something bad doesn't happen*

### Liveness
*Something good eventually happens*

### Fairness condition
- Fair traces satisfy each of the fairness conditions infinitely often 
- E.g. only fair if it doesn’t delay acknowledging a request forever
