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