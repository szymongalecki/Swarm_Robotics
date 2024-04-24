## Recreating alpha algorithm in UPPAAL pt.1

### Fix implementation of the basic algorithm
Clock that was triggering transitions didn't have invariant on its state. That meant that it could remain in the initial state indefinitely and was not forced to make transition. This in turn meant that robots were not forced to make transitions either.

As a result of adding an invariant on the clock state, robots have to make transitions. This led to correctly verifying two properties. 
1.  For all paths eventually, robots will remain connected or disconnect and reconnect again: 
	- `A<> (P1.conn && P2.conn) || (P1.final && P2.final)`
2. For all paths that consist of at least 7 transitions, robots will remain connected or disconnect and reconnect again:
	- `A[] C.loop_counter > 7 imply (P1.conn && P2.conn) || (P1.final && P2.final)`

