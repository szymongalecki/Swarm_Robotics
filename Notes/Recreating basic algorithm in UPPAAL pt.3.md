## Recreating basic algorithm in UPPAAL pt.3

### Robot synchronisation using channels
- Regular channels are binary which means that a single channel can only synchronise two automata at a time. After introducing a clock that triggers synchronisation after a single time interval it will only trigger one automat transition ( if the guard condition is satisfied ). All of the automata interleavings that were possible in memory based synchronisation were also available with this solution.
- Broadcast channel allow for one sender to synchronise with an arbitrary number of receivers. Single clock triggers a broadcast channel which in turn triggers simultaneous transitions of all automata. This means that robots 'move' with the same pace, taking decisions at the same time. This should be an acceptable approximation as they should operate in a similar manner which also includes pace. It greatly reduces the state space of the solution.
### Issues
Limiting integer values doesn't seem to work well

**Exact number of steps:**
```
A[] C.loop_counter == 30 imply 
(P1.conn && P2.conn) || (P1.final && P2.final)
```
This results in out of range error for loop_counter even though I am only interested in a state after 30 steps.

**Number of steps in range:**
```
A[] (C.loop_counter > 10 && C.loop_counter < 30) imply
(P1.conn && P2.conn) || (P1.final && P2.final)
```
This range is not enforced either

**Different quantifiers seem to work exactly the same**
**`A[] p`** : for all paths **p** always holds. 
**`A<> p`** : for all paths **p** will eventually hold.

Despite defining clock explicitly, the second quantifier doesn't care about it's progress.
```
A[] (P1.conn && P2.conn) || (P1.final && P2.final)
A<> (P1.conn && P2.conn) || (P1.final && P2.final)
```
Those two properties give exactly the same counter example: initial state. I don't see how the eventuality stated in second quantifier works.

**Time progresses after automata reached the final state**
Even when robots have already reached the final state, the loop_counter is still incremented because of the passing time.
Added guard for the loop_counter so that it can only be incremented 100 times.

### Results
For two robots taking a step of length 1 in one of directions N, E, W, S with distance threshold of length 2, they will reconnect or move in the same direction after taking 8 step or more.
```
A[] C.loop_counter > 7 imply 
(P1.final && P2.final) || 
(P1.y_dir == P2.y_dir) || 
(P1.x_dir == P2.x_dir)
```

Robots take decisions simultaneously as they are triggered by the same clock which broadcasts channel triggers. This doesn't go along with the assumption by Nembrini but I didn't think of any other mechanism that would satisfy asynchronous behaviour. "As no global time is implemented the robots should react asynchronously. However each robot has the same range of communication so both reactions should occur within a short time, depending on the periodicity of the calling messages."


<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
