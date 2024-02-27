## Paper - Property-Driven Design for Swarm Robotics
Note on [Property-Driven Design for Swarm Robotics](../Relevant%20Papers/Property-Driven%20Design%20for%20Swarm%20Robotics.pdf)  
Year: **2012**

Paper focuses on the property driven design but gives a good example on how to model rules around tested properties of swarm behaviors.

### Model checker software
PRISM is a probabilistic model checker which supports DTMC and PCTL* among many other models and logics. With PRISM, it is possible not only to verify properties, but also to perform so called “experiments,” in which the model checker computes the probability of the property being true against different parameter values. In this way, it is possible to find the parameter set that scores the best probability in verifying a property.

### Property: Robots form an aggregate as fast as possible
"We would like that the aggregate is formed as fast as possible (for example, in the first 1,000 seconds) but we do not differentiate between obtaining the aggregate in area A or area B"
```PRISM
P=? [F<=1000 (a=N_total)|(b=N_total)]
```

"In less formal terms, we compute the probability  $(P=?)$ that, in the first thousand seconds $(F<=1000)$, the number of robots in area A or in area B is equal to the total number of robots in the swarm $((a=N_{total})|(b=N_{total}))$. Since we want to maximize this probability, we do not specify a value for it."

### Property: Formed aggregate is stable for a certain period
"Another property we want for the system is that the aggregate, once formed, is stable for a certain period. In this example we set such period to 10 seconds. We verify this property with probability greater or equal to 2/3."

```PRISM
(a=N_total)|(b=N_total) =>
      P>=0.67 [G>=10 (a=N_total)|(b=N_total)]
```

"In natural language, Property 2 can be expressed in this way: from the aggregate state $((a=N_total)|(b=N_total))$ is it true with probability greater or equal to 0.67 $(=> P>=0.67)$ that the system stays for at least 10 seconds $(G>=10)$ in the aggregate state?"

### Building the model
"Once the above desired properties have been specified we need to build the model. We start by setting the total number of robots in the system. In order to perform a scalability test, we selected three different group sizes: $N_t = 10, 20, 50.$ Then, we specify three states: state $S_a$, $S_b$ and $S_c$. A robot in area $A$ or $B$ is in state $S_a$ or $S_b$, respectively. Robots outside area $A$ or $B$ are in state $S_c$. Moreover, three counters $a$, $b$ and $c$ are associated to the respective states. These counters are used to keep track of the number of robots that are in state $S_a$, $S_b$ and $S_c$, respectively. Note that $a+b+c=N_t$"

### Videos of simulation and hardware test
[videos](https://iridia.ulb.ac.be/supp/IridiaSupp2011-018/)
