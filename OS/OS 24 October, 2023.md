## Principals of concurrency
- Interleaving and overlapping
	- Can be viewed as examples of concurrent processing
	- both present the same problems
- Uniprocessor
	- depends on the activites of the other processes
	- the way OS handles interrupts
	- Scheduling policies of the OS

### Difficulty of concurrency 
- Sharing of global resources
- Difficult for the OS to manage the allocation of resources optimally
- Difficult to locate programming errors as results are not determinsitic and reproducible

### Race Condition
- When multiple processes or threads read and write data items
- The final result depends on the order of the execution
	- Loser of the race updates last and will determine the final value of the variable
