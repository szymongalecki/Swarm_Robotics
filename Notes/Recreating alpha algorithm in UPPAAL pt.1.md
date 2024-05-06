## Recreating alpha algorithm in UPPAAL pt.1

### Fix implementation of the basic algorithm
Clock that was triggering transitions didn't have invariant on its state. That meant that it could remain in the initial state indefinitely and was not forced to make transition. This in turn meant that robots were not forced to make transitions either.

As a result of adding an invariant on the clock state, robots have to make transitions. This led to correctly verifying two properties. 
1.  For all paths eventually, robots will remain connected or disconnect and reconnect again: 
	- `A<> (P1.conn && P2.conn) || (P1.final && P2.final)`
2. For all paths that consist of at least 7 transitions, robots will remain connected or disconnect and reconnect again:
	- `A[] C.loop_counter > 7 imply (P1.conn && P2.conn) || (P1.final && P2.final)`

### Alpha algorithm
Pseudocode taken from [Minimalist Coherent Swarming of Wireless Networked Autonomous Mobile Robots](../Papers/Minimalist%20Coherent%20Swarming%20of%20Wireless%20Networked%20Autonomous%20Mobile%20Robots.pdf)
```
Create a list of neighbours for robot, Nlist
k = number of neighours in Nlist
i = 0

loop forever {
	i = i modulo cadence

	if (i = 0){
		Send ID message

		Save copy of k in LastK
		k = number of neighbours in Nlist

		if ((k < lastK) and (k < alpha)){
			turn robot through 180 degrees
		}
		else if (k > LastK) {
			make random turn
		}
	}

	Steer the robot according to state
	Listen for calls from robots in range
	Grow Nlist with neighbours IDs

	i++
}
```

### Implementation
Elements:
- Number of robots n
- Array for storing x and y coordinates for n robots
- Function that returns the number of robots in range given robots id
- Array that stores the number of connections for each n robots
- Step size s 
- Threshold distance t that determines whether robots are connected, it is related to step size s
- Number of neighbours k and previous number of neighbours lastK
- States for random turn and 180 turn 
- Alpha parameter that specifies desired number of connections, it is related to number of robots n

Every move forward of every robot triggers functions updating the global state:
- `update_neighbours()` updates a 1d array **N** that stores number of neighbours for each robot `N[id] = # of neighbours`
- `update_distances()` updates a 2d array **D** that stores mutual distances between each robot `D[id_a][id_b] = distance between a and b`

Transform this code:
```
if ((k < last_k) and (k < alpha)){
	turn robot through 180 degrees
}
else if (k > last_k) {
	make random turn
}
else {
	do not turn
}
```

Into a set of mutually exclusive guards based on variables: `k, last_k, alpha`