### Automata should not be allowed to stay in the state indefinitely 
Try changing the types of location in the timed automata:

**Urgent locations** - Urgent locations freeze time; _i.e._ time is not allowed to pass when a process is in an urgent location.
	This is not enough as the the synchronisation is not based on time but on shared data structure. This means that automata will still be able to stay in the same state.

**Committed locations** - Like urgent locations, committed locations also freeze time. Furthermore, if any process is in a committed location, the next transition must involve an edge from one of the committed locations. Committed locations are useful for creating atomic sequences and for encoding synchronisation between more than two components. Notice that if several processes are in a committed location at the same time, then they will interleave.
	Committed locations are better than urgent ones but the hard part now is to understand the interleaving between two automatons. Especially checking if models are in the same states seem to be the worst idea. What I want to test for example is if the connection is mutual. Using the model states for that is absolutely useless. The closest that I can get is to check the global distance calculated from shared data structure. Another tricky thing is to specify property like: "All the automatons will go through that state eventually ( assuming that they cannot stay in the same state indefinitely )"
