## Publications of Alessio Lomuscio

[A Counter Abstraction Technique for the Verification of Robot Swarms](../Alessio%20Lomuscio%20Papers/A%20Counter%20Abstraction%20Technique%20for%20the%20Verification%20of%20Robot%20Swarms.pdf)
- Year: 2022
- Testing: No
- Abstract: 
	- We study **parameterised verification** of robot swarms against **temporal-epistemic specifications**. We relax some of the significant restrictions assumed in the literature and present a counter abstraction approach that enable us to verify a potentially much smaller abstract model when checking a formula on a swarm of any size. We present an implementation and discuss experimental results obtained for the alpha algorithm for robot swarms.
- Behaviour: 
	- **Alpha algorithm** - swarm aggregation algorithm, where the robots have to form a cluster in an area of the environment
- Properties: 
	- Express properties of robot swarms in the temporal-epistemic logic ACTL∗K\X (Lomuscio, Penczek, and Qu 2010).
- Results: 
	- The implementation that we presented was used to show that the **Alpha algorithm for swarms is indeed not correct** with respect to its intended specifications. This was shown in the absence of a collision avoidance mechanism. Collision avoidance mechanisms cannot be investigated by our methodology as it assumes a finite environment only. We leave this for future work.


[Verifying Fault-Tolerance in Probabilistic Swarm Systems](../Alessio%20Lomuscio%20Papers/Verifying%20Fault-Tolerance%20in%20Probabilistic%20Swarm%20Systems.pdf)
- Year: 2021
- Testing: No
- Abstract:
	- We present a method for reasoning about fault tolerance in **unbounded robotic swarms**. We introduce a novel semantics that accounts for the probabilistic nature of both the swarm and possible malfunctions, as well as the unbounded nature of swarm systems. We define and interpret a **variant of probabilistic linear-time temporal logic** on the resulting executions, including those arising from faulty behaviour by some of the agents in the swarm. We specify the decision problem of parameterised fault-tolerance, which concerns determining whether a probabilistic specification holds under possibly faulty behaviour. We outline a verification procedure that we implement and use to study a foraging protocol from swarm robotics, and report the experimental results obtained.
- Behaviour:
	- To evaluate the usefulness of our tool we consider the **swarm foraging protocol** (Campo and Dorigo, 2007; Liu and Winfield, 2010) that has previously been verified in a probabilistic setting without any faults in (Lomuscio and Pirovano, 2019). We extend this analysis to introduce a fault.
- Results:
	- We have introduced a method for **injecting faults into probabilistic swarm systems** and presented an implementation built from an existing toolkit for verifying such systems. To the best of our knowledge, this gives the first method and toolkit that enables the assessment of resilience to faults of swarm systems that are unbounded in size. We used these to assess the resilience of a foraging protocol; other protocols are likely to be analysable in a similar way.


[Formal Verification of Opinion Formation in Swarms](../Alessio%20Lomuscio%20Papers/Formal%20Verification%20of%20Opinion%20Formation%20in%20Swarms.pdf)
- Year: 2016
- Testing: No
- Abstract:
	- We investigate the **formal verification of consensus protocols** in swarm systems composed of arbitrary many agents. We use templates to define the behaviour of the agents in an opinion dynamics setting and formulate their verification in terms of the associated parameterised model checking problem. We define a **finite abstract model** that we show to simulate swarms of any size, thereby precisely encoding any concrete instantiation of the swarm. We give an automatic procedure for verifying temporal-epistemic properties of consensus protocols by model checking the associated finite abstract model. We present a toolkit that can be used to generate the abstract model automatically and verify a given protocol by **symbolic model checking**. We use the toolkit to verify the correctness of majority rule protocols in arbitrary large swarms.
- Results:
	- The key aspect of this work is that it operates at protocol level and not at system level. In other words, we do not just assess a particular system instantiation; but **evaluate the whole class of swarm instances** following a consensus protocol. We are not aware of other work in the swarm systems literature that is based on parameterised model checking.


[Verifying Emergent Properties of Swarms](../Alessio%20Lomuscio%20Papers/Verifying%20Emergent%20Properties%20of%20Swarms.pdf)
- Year: 2015
- Testing: No
- Abstract:
	- **We investigate the general problem of establishing whether a swarm satisfies an emergent property**. We put forward a formal model for swarms that accounts for their nature of unbounded collections of agents following simple local protocols. We formally define the decision problem of determining whether a swarm satisfies an emergent property. We introduce a sound and complete procedure for solving the problem. We illustrate the technique by applying it to the **Beta aggregation algorithm**.
- Results:
	- We have introduced a technique for determining automatically whether a swarm will display an emergent behaviour **irrespective of the number of agents** present. The technique is provably sound and complete. While we have put forward a fully automatic methodology, our methodology can also be used to complement simulations for fast prototyping. Specifically, if early simulations on small populations show a particular behaviour to emerge, we can then use the technique here described to check whether this behaviour will still be displayed by larger systems.


### Slides
[A Counter Abstraction Technique for the Verification of Probabilistic Swarm Systems](../Alessio%20Lomuscio%20Papers/A%20Counter%20Abstraction%20Technique%20for%20the%20Verification%20of%20Probabilistic%20Swarm%20Systems.pdf)
- Year: 2019

[Verifying Emergence of Bounded Time Properties in Probabilistic Swarm Systems](../Alessio%20Lomuscio%20Papers/Verifying%20Emergence%20of%20Bounded%20Time%20Properties%20in%20Probabilistic%20Swarm%20Systems.pdf)
- Year: 2018


<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
