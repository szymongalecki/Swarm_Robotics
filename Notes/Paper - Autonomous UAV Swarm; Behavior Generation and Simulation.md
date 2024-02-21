## Paper - Autonomous UAV Swarm: Behavior Generation and Simulation
Note on: [Autonomous UAV Swarm; Behavior Generation and Simulation](../Papers/Autonomous%20UAV%20Swarm;%20Behavior%20Generation%20and%20Simulation.pdf)

This paper presents a software framework to produce and simulate autonomous behaviors of UAV swarm tasked with search and reconnaissance missions.  The main challenge is the **generation of the desired autonomous behaviors** of the UAV swarm, with minimum centralised control and human intervention.

### High-level rule specification with linear temporal logic
- **Collision policy for agent** $i$: All other UAVs must be separated by the minimum of safety distance.
- **Fuel policy**: Fuel must be sufficient to return.
- **Spread-out search policy**: avoid the area if there is another agent that is closer, until under direct command.
- **Joint tracking policy**: if there is a nearby agent in tracking mode, join as a new tracking member.