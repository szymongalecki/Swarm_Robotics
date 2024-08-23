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
- Verify implementation in a similar way to alpha algorithm.
- Model scenarios described in the paper.
