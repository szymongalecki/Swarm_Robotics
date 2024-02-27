## Papers - overview, w6
### [Sophisticated collective foraging with minimalist agents, a swarm robotics test](../Papers/Sophisticated%20collective%20foraging%20with%20minimalist%20agents,%20a%20swarm%20robotics%20test.pdf)
Search term: "testing swarm robotics"

Paper explores how groups of cooperative forager robots can achieve efficient and robust collective foraging. Individual behaviour of the robot is represented by probabilistic finite state automaton. Overall performance of collective foraging is tested against a theoretical model representing optimal resource allocation for the given task. Simulation is performed using [ARGoS](https://www.argos-sim.info/) simulator.

### [Swarm Robotics, A Perspective on the Latest Reviewed Concepts and Applications](../Papers/Swarm%20Robotics,%20A%20Perspective%20on%20the%20Latest%20Reviewed%20Concepts%20and%20Applications.pdf)
Search term: "testing swarm robotics"

This paper is an overview and doesn't contain any specific informations on testing.

Mentions most relevant and recent robotic simulators:
1. Gazebo is a robotics simulation platform created by the player/stage project. This framework features individual and multi-robot simulation methods. 
2. UberSim is a platform originally created to validate soccer robots. This system relies on the ODE as its physics platform. 
3. USARsim is a simulation platform based on the Unreal Engine. This platform is very popular in robotics competitions, and can be combined with ROS for simulation and control. 
4. SwarmBot3D emulates the functioning of the S-Bot. The physical engine used to create this platform was Vortex. 
5. Microsoft Robotics Studio (MSRS) is a framework based in Windows to simulate robotic units. The physics simulator in this context was an external appliance created by Ageia. 
6. ARGoS is a simulator developed for multi-robot simulation. This platform allows the usage of multiple physics engines, enabling the simulation of up to 10,000 e-puck in 60% of the time taken in a real-world experiment. 
7. Kilogrid is a virtual environment created to emulate the Kilobots. It enables the experimentation with more Kilobot modules, providing a mean to experiment without the limitations of the unit’s real versions. 
8. Simbad is an autonomous robot simulation package. It enables various methods of single or multi-robot simulation using a Java-based platform. 
9. RoboNetSim is a framework for multi-robot and network simulation. This platform is based on ARGoS, with added network simulators. 
10. Webots is a mobile robotics simulation platform. The physics features are changeable inside the platform, allowing the emulation of flexible robots and environments. 
11. JBotEvolveris a platform to enhance research and education in evolutionary robotics. This platform is based in Java, with easy installation and use. 
12. CoppeliaSim, which was previously named V-Rep, is a mobile robots simulation framework. This platform allows the simulation of several aspects of multiple robots inside a defined environment.

### [Past, Present, and Future of Swarm Robotics](../Papers/Past,%20Present,%20and%20Future%20of%20Swarm%20Robotics.pdf)
Search term: "testing swarm robotics"

Overview paper which mentions using simulators as a testing approach. 

### [Collective Decision Making in Swarm Robotics with Distributed Bayesian Hypothesis Testing](../Papers/Collective%20Decision%20Making%20in%20Swarm%20Robotics%20with%20Distributed%20Bayesian%20Hypothesis%20Testing.pdf)
Search term: "testing swarm robotics"

This paper assumes that agents have distributed perception but have to reach a consensus in order to adjust the collective strategy when solving a task.

Author mentions [Collective decision making strategies](Collective%20decision%20making%20strategies.html) as a starting point for presenting his idea - Distributed Bayesian Hypothesis Testing (DBHT).

All of the indexed papers are older than 4 years and most are older than 10 years.

### [Property-driven design for swarm robotics](../Relevant%20Papers/Property-Driven%20Design%20for%20Swarm%20Robotics.pdf)
Search term: "design control and modeling swarm robotics"

Quite old: published in 2012

Swarm robotics system properties are specified using Deterministic Time Markov Chains (DTMC) and Probabilistic Computation Tree Logic (PCTL). 

"PCTL, originally developed by Hansson and Jonsson is an extension of CTL (Computation Tree Logic), a branching time logic. CTL is based on the idea that a Markov chain can be "expanded" in a computation tree. A computation tree is a potentially infinite rooted tree in which the root is the initial state of the corresponding Markov chain, and each node is a possible state of the system. The edges link a state with its next possible states."

PCTL can be used to formally verify the properties of a swarm behaviour ~ `S. Konur and C. Dixon. Formal verification of probabilistic swarm behaviours. In Swarm Intelligence, 7th International Conference, ANTS 2010, volume 6234 of Lecture Notes in Computer Science, pages 572–573. Springer, Berlin, Germany, 2010`



<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
