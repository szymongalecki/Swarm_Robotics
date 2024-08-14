[Minimalist Coherent Swarming of Wireless Networked Autonomous Mobile Robots](../Relevant%20Papers/Minimalist%20Coherent%20Swarming%20of%20Wireless%20Networked%20Autonomous%20Mobile%20Robots.pdf)

Paper roadmap:
![](../Images/paper_roadmap.png)

### Major Hypothesis
That it is possible, given the constraint of limited-range wireless communication, to achieve a stable connected swarm in an unbounded environment. We shall call this property *coherence*.

### Contribution
2. An algorithm (the $\beta$-algorithm) is developed that is able using second order information (neighbour's' list of neighbours) to guarantee the coherence of the swarm (see the $\beta$-algorithm section **4.12**). This algorithm has the capacity to tune through a single parameter the connectivity of the swarm (see section **4.3**). This connectivity measure represents the resilience of the dynamical network to loss of connections and failure of the nodes. This means that the algorithm is able to tune the robustness of the connected network (see section **3.5.1**). Furthermore the same parameter has the power to control the area covered by the swarm (see section **4.4**). It is also shown that the behaviour presented show good scalability with increasing swarm size and good resilience to increasing noise (see section **4.3.2**).
4. The $\beta$-algorithm is implemented on real robots and the capacity of the algorithm to achieve coherence is confirmed, despite strong compromises on the requirements assumed by the simulation experiments. Also a thorough investigation of the possible reasons for differences noted in robot performance is conducted.
5. It is shown by the localisation-$\beta$-algorithm that the exchange of information required by the $\beta$-algorithm is sufficient for a robot to approximate its global relative position (see section **4.5**).

### Methods
**In the young field of robotics the way to assert a scientific discovery is not yet commonly agreed.** The difficulty of mathematically formalising the notion of emergence and the cost of real robot experiments in terms of time and money has led researchers in the field to state experimental guidelines that remain far from a solid scientific proof [Bisset, 2003].

It is now widely agreed that real robot experiments are needed to confirm results from simulations, however accurate they may be, because of the obvious impossibility of representing all of the interactions that can have an influence on the problem considered. The idea coming from the the new roboticists such as Brooks [Brooks, 1991] is that the **complexity of the real world is best represented by itself.**

### Robot Architecture
- The robots that will be used in the real robot experiments are the Linuxbots developed in the IAS lab in Bristol.
- In the simulation, it is assumed the robots are able to move forward and turn on-the-spot with a precision ranging from perfect to errors of 10% on the distance or angle travelled, that they have infra-red avoidance sensors, are equipped with a limited-range radio device and they carry an omni-directional light sensor able to detect whether a robot is illuminated or not.
- **The robots' control system is designed as a finite state automaton.** A robot will be in one of several mutually exclusive states and switch between them according to environmental cues.

### Coherence
In the real world, unbounded environment seem as ubiquitous as bounded ones. If it is sometimes possible to restrict the environment or assume it is bounded, this is certainly not true in general. Consider only fluid environments such as the atmosphere or the oceans. In trying to keep a group of robots together in such an environment there are two approaches: **either give the robots an ability to come back towards the group or design a swarming algorithm that will not allow any robot to lose the group.** [...] Following the desire for minimalism presented in chapter 2, the second approach will therefore be pursued: throughout this chapter the aim is to show the capacity of the algorithm developed to achieve stable swarming of the robots. It will be referred to as *coherence*. 

### Shared neighbour algorithm: $\beta$-algorithm
![](../Images/bridges.png)
To avoid the extreme configuration of figure 4.10, we make use of the graph theory concept of *clustering*: instead of considering only its own degree of connection to trigger a reaction, **each robot will receive from its neighbours their adjacency table - their neighbours' list** - in order to check whether a particular neighbour is *shared* by the other ones, that is whether a particular neighbour is the neighbour of other robots.

**The algorithm works as follows: for each lost connection a robot checks how many of its remaining neighbours still have the lost robot in their neighbourhood.** If this number is less than or equal to the fixed threshold $\beta$, the robot turns around and comes back. In parallel if its degree of connections is rising the robot chooses a random heading.

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

		Save copy of Nlist in OldList
	}

	Steer the robot according to state
	Listen for calls from robots in range
	Grow Nlist with neighbours IDs and connection info

	i++
}

```

"The following section will show that the upgrade to the $\beta$-algorithm is itself able in (possibly noisy) simulations and to a certain extent in real robot experiments, to guarantee this coherence."


### Verification ideas for $\beta$-algorithm
There are two descriptions of unwanted scenarios which the algorithm is supposed to prevent from.

![](../Images/shared_neighbour.png)
In the situation of figure 4.12, robot A, wen losing the connection with robot B will check its other neighbours and finds that robots C and D share B as neighbour. Hence A will react and turn back only if the threshold $\beta$ is set equal ot greater than two. The algorithm thus makes the robot try to maintain the triangulation observable in the figure, therefore avoiding critical states. 

![](../Images/cutvertex.png)
The $\beta$-algorithm also prevents the formation of cutvertices as long as $\beta$ is greater or equal to 2. Indeed in the situation depicted in figure 4.14 a cutvertex is about to be formed. But the presence of a cutvertex implies that there can only be one shared neighbour. Hence a reaction to prevent a cutvertex providing $\beta \geq$ 2.

###  Lower performance in hardware aka ways of optimising the model 
- Two successive 180 degrees turns without straight movement has been shown to be crucial for disconnection. However, the lack of positive increase in the length of the runs with increasing cadence, raises doubts about the unique influence of this factor.

There are so many possible hardware reasons that could be causing the lower performance in real robots but at the same time the algorithm was not verified to be correct.

### Conclusions
The main $\beta$-algorithm achieved long term coherence, tuning of the network connectivity, area coverage control and the exchange of information needed by this algorithm was demonstrated to be sufficient for crude relative positioning within the swarm (localisation-$\beta$-algorithm). **Real robot experiments and simulations presented sufficient similarities to support the correctness of the implementation.** 
(DID THEY?)

### Further research direction
........




