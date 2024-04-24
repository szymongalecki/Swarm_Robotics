## Recreating basic algorithm in UPPAAL pt.1
Inspired by [Paper - Towards Temporal Verification of Emergent Behaviours in Swarm Robotic Systems](Paper%20-%20Towards%20Temporal%20Verification%20of%20Emergent%20Behaviours%20in%20Swarm%20Robotic%20Systems.md)  
Algorithms adapted from Julien's Membrini [Minimalist Coherent Swarming of Wireless Networked Autonomous Mobile Robots](../Papers/Minimalist%20Coherent%20Swarming%20of%20Wireless%20Networked%20Autonomous%20Mobile%20Robots.pdf)

### Basic algorithm
1. Assume that the robots are **initially in communication range, moving forward with random headings**.
2. Unless they have parallel or crossing trajectories, the former situation not detrimental to the connection and the latter being dealt by the avoidance behaviour, **they will eventually lose contact**. 
3. In order to check whether this is the case or not, the algorithm uses a send-listen mechanism: With a certain periodicity each robot broadcasts a message containing its ID to the other indiscriminately and then listens for possibly incoming messages. 
	**A**. If no message is received within a certain time, each robot assumes it is out of range and reacts immediately by turning 180 degrees in order to reconnect.
	**B**. Then as soon as it receives a message it chooses a new random heading.

### Minimal version
- Single robot
- Stays in the the circle of radius = threshold
- Connected when inside of the circle
- Disconnected when outside of the circle

**Variables:**
- `x, y`
- `dir_x, dir_y`
- `radius`

**Initial state:**
- ` x = 0, y = 0`
- ` dir_x = 0, dir_y = 0`
- `radius = 3`

**Random turn:**
- *Move only in multiples of 45 degrees*
- `dir_x` $\in \{-1, 0, 1\}$
- `dir_y` $\in \{-1, 0, 1\}$

**Connected:**
$$\sqrt{x^2 + y^2} <= radius$$

**Turn 180:**
```C++
dir_x = dir_x == 0 ? 0 : dir_x == -1 ? 1 : -1,
dir_y = dir_y == 0 ? 0 : dir_y == -1 ? 1 : -1,
```

### Next iteration
- Change `dir_x` and `dir_y` to `angle`
- Calculate the `x` and `y` position from `angle` and unit step of length 1
- 180 degree turn is `(angle + 180) % 360`
- Random turn is choosing an angle from range 0 to 359 degrees

**Formulas:**
$step=length(hypotenuse)$ 
$sin(\alpha) = \frac{opposite}{hypotenuse}$
$cos(\alpha)=\frac{adjacent}{hypotenuse}$
$x' = x + (step * sin(\alpha))$
$y' = y + (step * cos(\alpha))$

I cannot use type `double` for coordinates `x` and `y`:
Error: *"When using symbolic methods you cannot get state-doubles."*

**This means that I either have to cast to integer or use grid approach with either 4 or 8 directions.**

**Casting to integer doesn't work as expected** when using `fint()` 
[UPPAAL reference](https://docs.uppaal.org/language-reference/expressions/)
[StackOverflow issue](https://stackoverflow.com/questions/54460545/how-to-cast-a-double-value-to-a-integer-value-in-uppaal)

Casting $sin(\alpha)$ to integer means that we will only get movement for $\alpha \in \{0, 90, 180, 270\}$ if the `step` is equal to one. Therefore `step` must be bigger than 1 to observe any kind of movement.

**The biggest issue is that the Symbolic Simulator doesn't seem to work when values are casted to integer ( or for some other reason )**

For example let's take the property:
*All robots that left the circle of radius 'threshold' will find their way back*
`A[] R1.disconnected imply R1.connected`
It is not satisfied but the corresponding diagnostic trace is unavailable.

### Two robots moving in four directions
- Robots store their coordinates through the shared data structure
- Array `X` stores the x coordinates of the robots
- Array `Y` stores the y coordinates of the robots
- If the distance between two robots between their distance is bigger than `threshold`, it means that they are disconnected