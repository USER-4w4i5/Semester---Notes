# Chapter 5: Concurrency
## Key terms related to concurrency
- Atomic operation
	- Function/operation implemented as a sequence of one or more instructions that appears to be indivisible
	- No other process can see the intermediate state or interrupt the operation
	- Guaranteed
		- Execute as a group
		- Not execute at all
		- No visible effect on system state
	- Isolation from concurrent processes
- Critical Section
	- Section of code that must not be executed while other processes are using the shared resources it has to use
- Deadlock
	- Two or more processes are unable to proceed as each is waiting on for one of the others to do something
- Livelock
	- Two or more processes continuously change their states in response to each other without doing as useful work
- Mutual exclusion
	- Requirement, if a process accesses shared resources, no other process can use that shared resource i.e be in a critical section
- Race Condition
	- Situation, where multiple threads/processes read and write shared resources
- Starvation
	- Overlooked by scheduler, ready to run but never run
## Principles of Concurrency
- 
## Mutual Exclusion
## Semaphores
## Message Passing

sruff