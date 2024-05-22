## Recreating alpha algorithm in UPPAAL pt.2

### Transform the direct implementation of alpha algorithm into a version that can be verified
- Added a clock with a step counter.
- Added broadcasting channel for synchronisation. It triggers transitions every time unit. Unfortunately can't apply it to edge going out of initial state. `Non deterministic input is not supported by SMC on line 1 of Project/Robot/initial -> turn_random/synchronisation: bc?`
