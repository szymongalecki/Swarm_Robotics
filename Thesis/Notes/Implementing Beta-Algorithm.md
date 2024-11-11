```
Create list of neighbours for robot, Nlist
k = number of neighbours in Nlist
i = 0

loop forever {
	i = i modulo cadence

	if (i = 0) {
		Send ID message

		Save copy of k in LastK
		Set reaction indicator Back to FALSE
		k = number of neighbours in Nlist
		Create LostList comparing Nlist and OldList

		for (each robot in LostList) {
			Find nShared, number of shared neighbours
			if (nShared <= beta) {
				Set reaction indicator Back to TRUE
			}
		}

		if (Back = TRUE) {
			turn robot through 180 degrees
		}
		else if (k > LastK) {
			make random turn
		}
		
		Save copy of Nlist in Oldlist
	}
	Steer the robot according to state
	Listen for calls from robots in range
	Grow Nlist with neighbours IDs and connection info

	i++
}

```


### Next time
Inspect `turn180(id)`, there is something wrong with counting shared neighbours.

Check that all the states are reachable. Check that they are not only reachable as the next states after initial state.

I wrongly interpreted this part of the pseudocode:
```
for (each robot in LostList) {
			Find nShared, number of shared neighbours
			if (nShared <= beta) {
				Set reaction indicator Back to TRUE
			}
		}
```

**Previously:**
`If LostList is empty then nShared=0 and Back=True`

**Now:**
`If LostList is empty we do not execute this part of code as there are no elements to iterate over`
`We do not care about nShared`
`Back=False`

- ~~Add clock and invariant on not committed states.~~
- ~~Verify implementation in a similar way to alpha algorithm.~~
- Model scenarios described in the paper.

### Verification
```
const int N = 2;
const int R = 2;
const int STEP = 1;
const int BETA = 1;
const int G = 3;
const int T_MAX = 1;
clock C;
```

`E<> forall(i : int[0, N-1]) x[i] == G && y[i] == G` - FALSE
There is no path for any robot that leads to the corner of the grid.

`A[] forall(i : int[0, N-1]) abs(x[i]) <= G && abs(y[i]) <= G` - TRUE
For all the paths, all robots stay within grid boundaries

`E<> C > 0 && P0.turn_random` - TRUE
There exists a path for robot P0 to reach location turn_random after initialisation.

`E<> forall(i : int[0, N-1]) C > T_MAX && k[i] == 0 && last_k[i] == 0` - TRUE
Two robots can get disconnected after initialisation for more than two steps each.

`E<> P0.turn_180 && abs(x[0]) != G && abs(y[0]) != G` - TRUE
There exist a path for robot P0 to reach location turn_180 without reaching the boundary of the grid

`E<> P0.turn_180 && (abs(x[0]) == G || abs(y[0]) == G)` - TRUE
There exists a path for robot P0 to reach location turn_180 by reaching the boundary of the grid

`E<> P0.forward && k[0] <= last_k[0]` - TRUE
There exist a path where robot moves forward without changing direction

`A[] not deadlock` - TRUE
There is no path which results in deadlock

`A[] forall(i : int[0, N-1]) C > 0 imply x_dir[i] != 0 or y_dir[i] != 0` - TRUE
All robots have set direction after initialisation


### Properties for the algorithm

1. Three robots after initialisation can be disconnected for at least two steps each.
```
const int N = 3;        // Number of robots
const int R = 2;        // Signal radius
const int STEP = 1;     // Step size
const int BETA = 2;     // Beta parameter
const int G = 3;        // Grid boundary => Grid : 2G x 2G
const int T_MAX = 1;    // Time threshold on invariant
```

```
E<> forall(i : int[0, N-1]) C > T_MAX && k[i] == 0 && last_k[i] == 0
```


"The $\beta$-algorithm also prevents the formation of cutvertices as long as $\beta$ is greater or equal to 2. Indeed in the situation depicted in figure 4.14 a cutvertex is about to be formed. But the presence of a cutvertex implies that there can only be one shared neighbour. Hence a reaction to prevent a cutvertex providing $\beta \geq 2$."


#### 3 robots
```
const int N = 3;        // Number of robots
const int R = 1;        // Signal radius
const int STEP = 1;     // Step size
const int BETA = 2;     // Beta parameter
const int G = 3;        // Grid boundary => Grid : 2G x 2G
const int T_MAX = 1;    // Time threshold on invariant
clock C;                // Global clock 
```

Successfully verified properties for `C > {T_MAX, 2*T_MAX, 3*T_MAX, 4*T_MAX}`

`E<> C > T_MAX and forall(i : int[0, N-1]) k[i] == 0 and last_k[i] == 0`
`E<> C > 2 * T_MAX and forall(i : int[0, N-1]) k[i] == 0 and last_k[i] == 0`
`E<> C > 3 * T_MAX and forall(i : int[0, N-1]) k[i] == 0 and last_k[i] == 0`
`E<> C > 4 * T_MAX and forall(i : int[0, N-1]) k[i] == 0 and last_k[i] == 0`

#### 4 robots
```
const int N = 4;        // Number of robots
const int R = 1;        // Signal radius
const int STEP = 1;     // Step size
const int BETA = 2;     // Beta parameter
const int G = 3;        // Grid boundary => Grid : 2G x 2G
const int T_MAX = 1;    // Time threshold on invariant
clock C;                // Global clock
```

Successfully verified properties for....


### 3 robots synchronous
```
const int N = 3;        // Number of robots
const int R = 1/2/3;    // Signal radius
const int STEP = 1;     // Step size
const int BETA = 2;     // Beta parameter
const int G = 3;        // Grid boundary => Grid : 2G x 2G
```

`E<> forall(i : int[0, N-1]) k[i] == 0 and last_k[i] == 0` - Robots can become fully disconnected for at least two steps.

### Error in the synchronised implementation
After the collective move forward of all four robots, there are inconsistencies in the connection state of the robot.

- First robot is connected to all of three other robots.
- Second robot is connected to all three other robots.
- Third robot is connected only to the fourth robot.
- Fourth robot is connected only to the third robot. 

First of all, the connections should be mutual, so if a robot A is connected to robot B then robot B is also connected to robot A. Which is not the case in this situation.

Second of all, the radius of the signal is equal to 1 which means that first and second robot should only be connected to each other and no other robot as the distance to the third and fourth robot is bigger than radius of their signal. 

The issue is probably the race condition caused by multiple robots calling the same three functions upon transitioning from the **forward** state to the grid state.

Functions causing the race condition:
`moveForward(id)`
`updateNeighbours(id)`
`updateConnections(id)`

![](../../error.png)

Solution:
Functions `updateNeighbours` and `updateConnections` were removed from transition **forward** $\rightarrow$ **grid** and added to two subsequent transitions. In this way they will be called on the system of robots with fixed positions. Order of robots calling them has no influence on the state of connections. Race condition was eliminated.
![](../Images/implementation_synchronised.png)

### Verification on the synchronised version of the implementation
```
// System specification
const int N = 4;        // Number of robots
const int R = 1;        // Signal radius
const int STEP = 1;     // Step size
const int BETA = 2;     // Beta parameter
const int G = 3;        // Grid boundary => Grid : 2G x 2G
broadcast chan step;    // Clock tells robots to transition from forward state
chan done;              // Robots tell clock that it reached forward state
```

Verified as true:
`A[] forall(i : int[0, N-1]) k[i] != 0 or last_k[i] != 0`


### Check the implementation of counting shared neighbours as this is a crucial element of the algorithm!

This part of `sharedNeighbours` seems wrong because.
Robot `id` has lost robot `i` and then we are accessing the neighbours list of robot `i` which should not be possible as we are no longer connected to it: `neighbours[i][j]`.

```c++
for (i = 0; i < N; i++){
        if (lost_neighbours[id][i] == 1){
            for (j = 0; j < N; j++){
                if (
		                neighbours[id][j] == 1 
		                && neighbours[i][j] == 1
	                )
	            {
                    shared_neighbours[id][j] = 1;
                } else {
                    shared_neighbours[id][j] = 0;
                }
            }
        }
    }
```


**Fixed**
Data structures should be cleared for all scenarios.
```C++
// Clear entries for this robot
for (i = 0; i < N; i++){
	shared_neighbours[id][i] = 0;
	shared[id] = 0;
}
```

Connection information of the lost robot are no longer accessed.
Additionally, shared neighbours are counted correctly.
```C++
for (i = 0; i < N; i++){
	if (lost_neighbours[id][i] == 1){
		for (j = 0; j < N; j++){
			if (
				neighbours[id][j] == 1 
				&& neighbours[j][i] == 1
			){
				shared_neighbours[id][i] += 1;
			}
		}
	}
}
```

We want to come up with nShared value that will satisfy this condition without modifying the robots behaviour.
```
if (nShared <= beta) {
	Set reaction indicator Back to TRUE
}
```

This is achieved by the following code and can be phrased in this way -> determine the maximum number of neighbours that are still connected to any of the lost connections.
```C++
    // Maximum number of shared neighbours for any lost robot i
    for (i = 0; i < N; i++){
        if(shared_neighbours[id][i] > shared[id]){
            shared[id] = shared_neighbours[id][i];
        }
    }
}
```

### Results
```
// System specification
const int N = 2;        // Number of robots
const int R = 1;        // Signal radius
const int STEP = 1;     // Step size
const int BETA = 1;     // Beta parameter
const int G = 3;        // Grid boundary => Grid : 2G x 2G
const int T_MAX = 1;    // Time threshold on invariant
clock C;                // Global clock 
```

**Verification of implementation** 
1. `A[] forall(i : int[0, N-1]) x[i] != G or y[i] != G` 
	1. TRUE 
	2. For all the paths, all robots will never have their x coordinate and y coordinate equal to grid boundary at the same time.
	3. There is no path for any robot that leads to the corner of the grid.
2. `A[] forall(i : int[0, N-1]) abs(x[i]) <= G && abs(y[i]) <= G` 
	1. TRUE 
	2. For all the paths, all robots stay within grid boundaries
3. `E<> C > 0 && P0.turn_random` 
	1. TRUE
	2. There exists a path for robot P0 to reach location turn_random after initialisation.
	3. Reachable locations: 
		1. forward
		2. grid 
		3. if
		4. else_if
	4. Reachable transitions:
		1. turn_random -> forward
		2. forward -> grid
		3. grid -> if
		4. if -> else_if
		5. else_if -> turn_random
4. `E<> C > 0 && P0.turn_180` 
	1. TRUE
	2. There exists a path for robot P0 to reach location turn_180 after initialisation.
5. `A[] P0.forward imply P0.t <= T_MAX`
	1. TRUE
	2. For all the paths, robot P0 will obey the invariant on location forward.
6. `E<> P0.turn_180 && abs(x[0]) != G && abs(y[0]) != G` 
	1. TRUE
	2. There exist a path for robot P0 to reach location turn_180 without reaching the boundary of the grid.
	3. Reachable transition:
		1. if -> turn_180
7. `E<> P0.turn_180 && (abs(x[0]) == G || abs(y[0]) == G)`
	1. TRUE
	2. There exists a path for robot P0 to reach location turn_180 as a result of reaching the boundary of the grid.
	3. Reachable transition:
		1. grid -> turn_180
8. `E<> P0.forward && k[0] <= last_k[0]`
	1. TRUE
	2. There exist a path for robot P0 where it moves forward without changing direction.
	3. Reachable transition:
		1. else_if -> forward
9. `A[] P0.t != 0 imply P0.forward`
	1. TRUE
	2. For all the paths, robot P0 will have its clock value different than zero only in the forward location.
	3. For the robot, time is only allowed to pass in the forward state.
10. `A[] (P0.turn_random or P0.turn_180 or P0.grid or P0.grid or P0.if or P0.else_if) imply P0.t == 0`
	1. TRUE
	2. For all the paths, robot P0 will have its clock value equal to zero in the listed locations.
	3. For the robot, time will not pass in any other location than forward.
11. `A[] forall(i : int[0, N-1]) shared_neighbours[i][0] == 0 and shared_neighbours[i][1] == 0`
	1. TRUE
	2. For all the paths, all robots have no shared neighbours.
	3. Two robots cannot have a neighbour in common.
12. `A[] forall(i : int[0, N-1]) C < 0 imply k[i] == N-1`
	1. TRUE
	2. For all paths, all robots are fully connected prior to system initialisation.
13. `A[] forall(i : int[0, N-1]) C > 0 imply x_dir[i] != 0 or y_dir[i] != 0`
	1. TRUE
	2. For all paths, all robots have set direction after system initialisation.
14. `A[] not deadlock`
	1. TRUE
	2. There is no path which results in deadlock



