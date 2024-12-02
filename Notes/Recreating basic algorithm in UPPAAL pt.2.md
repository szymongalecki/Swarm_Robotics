## Recreating basic algorithm in UPPAAL pt.2
### Automata should not be allowed to stay in the state indefinitely 
Try changing the types of location in the timed automata:

**Urgent locations** - Urgent locations freeze time; _i.e._ time is not allowed to pass when a process is in an urgent location.
	This is not enough as the the synchronisation is not based on time but on shared data structure. This means that automata will still be able to stay in the same state.

**Committed locations** - Like urgent locations, committed locations also freeze time. Furthermore, if any process is in a committed location, the next transition must involve an edge from one of the committed locations. Committed locations are useful for creating atomic sequences and for encoding synchronisation between more than two components. Notice that if several processes are in a committed location at the same time, then they will interleave.
	Committed locations are better than urgent ones but the hard part now is to understand the interleaving between two automatons. Especially checking if models are in the same states seem to be the worst idea. What I want to test for example is if the connection is mutual. Using the model states for that is absolutely useless. The closest that I can get is to check the global distance calculated from shared data structure. Another tricky thing is to specify property like: "All the automatons will go through that state eventually ( assuming that they cannot stay in the same state indefinitely )"

### Synchronisation without introducing time (yet)
- Robots are initially connected
- They turn randomly and move forward until disconnected
- They turn 180 degrees and become connected 
- They remain connected and this is the final state

### Issues
- Automata can stay in the states indefinitely **despite using urgent and committed locations**. This means that possibilities of verifying properties are very limited. Automata staying in the initial states is recognised as a valid trace that invalidates the verified property.
- Synchronisation based on memory seems to be more complex when it comes to the number of possible states. Each state of each automaton can be interleaved with another one. Without progress requirements imposed by the passing time the state explosion seems to be happening sooner than expected.
- **Only some properties of liveness can be verified**. Safety properties can't be checked for the following reasons:
	- Automata with initial states is a valid trace
	- Memory based synchronisation allows for interleaving creating state space explosion early on
- Can't save the trace from the Concrete Simulator, I get the following error: "The file name must have a valid file extension.". I tried:
	- `.xml`
	- `.xta`
	- `.ta`
	- `.xtr`
	- `.csv`
	- `.txt`

### Storing the state of the connection
The biggest mistake so far was to save the state of connectivity for a single automaton. This lead to robots progressing to move forward while one was disconnected and the other had invalid saved information on being connected.

Exemplary run that shows the undesired behaviour:
```ts
Threshold: 2
P1: connected
P2: connected

P1  --  --  P2
0,0         2,0
```

```ts
Threshold: 2
P1: disconnected
P2: connected

P1  --  --  --
--  --  --  P2
1,0         2,0
```

```ts
Threshold: 2
P1: disconnected
P2: disconnected

P1  --  --  --
--  --  --  --  P2
1,0             3,0
```

```ts
Threshold: 2
P1: disconnected
P2: disconnected

P1  --  --  --
--  --  --  --  P2
1,0             3,0
```

```ts
Threshold: 2
P1: disconnected
P2: disconnected

--  --  --  --
P1  --  --  --  P2
0,0             3,0
```

```ts
Threshold: 2
P1: disconnected
P2: disconnected

--  --  --  --
--  --  --  --  P2
P1  --  --  --  3,0
-1,0             
```

`P1` will continue with downward movement and `P2` will move left indefinitely. This is due to storing the state of the connection for each of the automatons instead of using a global function to determine the connectivity.
<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
