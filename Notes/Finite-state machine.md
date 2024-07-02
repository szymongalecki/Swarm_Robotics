## Finite-state machine
A finite-state machine/automaton, or simply a state machine, is a mathematical model of computation. It is an abstract machine that can be in exactly **one** of a finite number of states at any given time. The FSM can change from one state to another in response to some inputs. The change from one state to another is called a transition. An FSM is defined by a list of its states, its initial state, and the inputs that trigger each transition. 

### Types of FSM and their differences
Deterministic finite-state machine - **DFSM**
Non-deterministic finite-state machine - **NDFSM**

**Determinism**: DFSMs have a deterministic transition function, while NDFSMs have a non-deterministic one.

**Number of Next States**: DFSMs always have exactly one next state for each state-input pair, whereas NDFSMs may have zero, one, or multiple next states for a given state and input.

For any non-deterministic finite-state machine, an equivalent deterministic one can be constructed.
<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
