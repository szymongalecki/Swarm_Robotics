## Recreating basic algorithm in UPPAAL
Inspired by [Paper - Towards Temporal Verification of Emergent Behaviours in Swarm Robotic Systems](Paper%20-%20Towards%20Temporal%20Verification%20of%20Emergent%20Behaviours%20in%20Swarm%20Robotic%20Systems.md)  
Algorithms adapted from Julien's Membrini [Minimalist Coherent Swarming of Wireless Networked Autonomous Mobile Robots](../Papers/Minimalist%20Coherent%20Swarming%20of%20Wireless%20Networked%20Autonomous%20Mobile%20Robots.pdf)

### Basic algorithm
1. Assume that the robots are **initially in communication range, moving forward with random headings**.
2. Unless they have parallel or crossing trajectories, the former situation not detrimental to the connection and the latter being dealt by the avoidance behaviour, **they will eventually lose contact**. 
3. In order to check whether this is the case or not, the algorithm uses a send-listen mechanism: With a certain periodicity each robot broadcasts a message containing its ID to the other indiscriminately and then listens for possibly incoming messages. 
	**A**. If no message is received within a certain time, each robot assumes it is out of range and reacts immediately by turning 180 degrees in order to reconnect.
	**B**. Then as soon as it receives a message it chooses a new random heading.
