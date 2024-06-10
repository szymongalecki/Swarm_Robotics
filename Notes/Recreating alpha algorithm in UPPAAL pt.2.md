## Recreating alpha algorithm in UPPAAL pt.2

### Transform the direct implementation of alpha algorithm into a version that can be verified
- Added a clock with a step counter.
- Added broadcasting channel for synchronisation. It triggers transitions every time unit. Unfortunately can't apply it to edge going out of initial state. `Non deterministic input is not supported by SMC on line 1 of Project/Robot/initial -> turn_random/synchronisation: bc?`

### Using global state incorrectly for `last_k`
Value assigned to `last_k` is not necessarily the last number of observed robots by specific robot. This causes incorrect behaviour, 'forward motion' instead of '180 degree turn'.
While neighbours can and should be updated globally, the last number of neighbours for the robot should be updated by the specified robot only.
`last_k` was removed altogether in favour of using global array `L[id]`

### Robot should move forward before edge reaches the 'forward' state
While it doesn't matter when robot moves forward whether at beginning or end of the alpha algorithm's loop, it should be consistent to avoid double updates of global state.
If robot performs a random turn and moves forward it should not move forward again after reaching the 'forward' state.

### Non-deterministic state is not supported
Triggering transitions with explicit clock, breaks down sooner or later.

### Remove the clock from the alpha algorithm
I removed the clock and tried to add the invariant to the states of the robot. Unfortunately I do not know how to specify the invariant with the modulo operator. As the time is passing forward, once set invariant to 5 time units will not make sense after 15 time units. As the invariant will not be able to be satisfied, transition to this state will not be possible. This will create the deadlock. 
Now the question is how to specify the invariant so that the robot can stay in the state for x time units with continues time. We don't want to reset the clock.

### Each robot has its own clock
- Declared array of clocks `clock C[n]`, where `n` is the number of robots.
- Robots have invariants on states that are connected to their own clocks.
- Once the robot leaves the state with defined invariant, it resets its own clock.
- The main loop has only invariant on the 'forward' state.
- Rest of the states are 'committed', which means that time doesn't pass in them.
- Passing time is associated with the forward motion and decision about direction: 'random turn', '180 degree turn', is instantaneous.

Problem:
- With `n` declared and instantiated robots there are only `n-1` clocks used.
- Robots reset wrong clocks for some reason
- Example:
	- Robot P4 with `id = 3` makes transition that resets its clock
	- Transition triggers an update `C[id] = 0`
	- Instead of resetting clock for `id = 3` it resets clock for `id = 2`
	- Clock for `id = 3` is empty: `{}`
	- **It looks like a simple off by one error but it is not**

Remove the array altogether to exclude an off by one error:
- Declare a `clock c` in the 'Robots' declarations
- Each robot now has its own `clock c`
- It is used to define invariant on states `initial` and `forward`
- After leaving those states, the local clock gets reset `c = 0`
- Still, out of `n` declared robots only first `n-1` clocks get updated
- Clock `n` is empty - `{}`