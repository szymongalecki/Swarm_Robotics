## Literature review
[Problem statement for research project - corrected](../Formal/Problem%20statement%20for%20research%20project%20-%20corrected.md)
I can start writing about the research part: 
- How did I find the articles?
- What exactly did I find out?
- What kind of models were discussed?
- What tools were used?
- What experiments were conducted?"

### How did I find the articles?
[Papers - overview, w6](Papers%20-%20overview,%20w6.md)
I initially used the search term "testing swarm robotics" to find relevant articles in Google Scholar. While I managed to find multiple articles, they were not relevant to my research topic.

Word "testing" in the search term resulted in many papers which indicated that testing was performed but through the use of virtual simulators or hardware. Testing in the context of those papers most of the time meant: observation of the behaviour emerging from defined algorithms. Consequently, the effect of testing was modification of the algorithm and further observation. I wanted to find papers with more rigorous definition of what exactly is being tested that is why I changed the "testing" part of the search term to "verification".

Term "swarm robotics" resulted in general papers, often overview papers summarising previous research. They were not very specific and didn't specify any formal logical system for defining swarm behaviour. I found more relevant results after changing search term from "swarm robotics" to "swarm engineering".

### What exactly did I find out?
In the taxonomy of swarm behaviors depicted in [Swarm Robotic Behaviors and Current Applications](../Papers/Swarm%20Robotic%20Behaviors%20and%20Current%20Applications.pdf) we find four categories of swarm behaviours. Those are spatial organisation, navigation,  decision making and miscellaneous. Most of the research that I found was focused on aggregation which is classified as a spatial organisation behaviour. Desired emergent behaviours for an aggregation task is for the robots to become and stay connected. It is to be expected that the basic task of a single robot is to become part of the swarm, a collection of robots that can communicate and interact with each other. Without robots acting as a swarm we can't talk about swarm robotics or expect more complex emergent behaviours. 

### What kind of models were discussed?
- [DTMC - Discrete Time Markov Chain](https://en.wikipedia.org/wiki/Discrete-time_Markov_chain)
- [PCTL - Probabilistic Computational Tree Logic](https://en.wikipedia.org/wiki/Probabilistic_CTL)

### What tools were used?
- [UPPAAL](https://uppaal.org/)
- [PRISM](https://www.prismmodelchecker.org/)

### What experiments were conducted?

