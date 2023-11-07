# Differential Architecture

- ## Microkernel Architecture
	- A kernel usually has a few essential functions
		- Address Spaces
		- Inter Process communication
		- Basic Scheduling
	- Microkernel vs Monolithic Kernel
	- Allows 
		- Simplifies implementation
		- Provides flexibility
		- Well suited to a distributed environment
	- `NOTE:: Filesystem types are deployed within the kernel`
	- `Add in differences from monolilthic kernel`
- ## Multithreading
	- A process is which executes an application is divided into threads that can run concurrently
	- Most beneficial to an SMP (Symmetric Multiprocessor)
	- Thread
		- Dispatchable unit of work 
		- Includes a process context and its own data area to enable subroutine branching
		- Executes sequentially and is interruptible
	- Process
		- A collection of one or more thread and associated system resources
		- Consists of at least a single thread
		- Programmer has greater control over the modularity of the application and the timing of application related events
- ## OS Design
	- Distributed OS
		- Provides the illusion of 
			- a single main/secondary memory space
			- a unified access facilities
		- State of the art for distributed OS lags that of uniprocessor and SMP OS.
	- Object-Oriented Design
		- Used for adding modular extensions to a small kernel
		- Enables programmers to customize an OS without disrupting system integrity
		- Eases the development of distributed tools and full-blown distributed operating systems
- ## Fault Tolerance
	- Refers to the ability of a system or component
	- Fundamental Concepts
		- Basic measures are
			- Reliability: R(t)
				- Probability of its correct operation up to time t given that the system was operating correctly at time=0
			- Mean time to failure (MTTF)
				- Time it takes to fail (Uptime)
			- Mean time to repair (MTTR)
				- Time it takes to get the system back up and running
				- The avg time it takes to repair/replace a faulty element
			- Availability
				- Classes
					- Continuous
						- `Fill in later`
					- Fault Tolerant
					- Fault Resilient
					- High Availability
					- Normal Availability
			- Fault Types
				- Permanent
				- Temporary
			- Fault Categories of redundancy
				- Physical(Spatial)
					- `Fil in later`
				- Temporal
				- Data
			- Operating System Mechanisms
				- Process isolation
				- Concurrency
				- Virtual Machines
				- Checkpoints and rollbacks
					- Saved state at a certain point in time to rollback to that state
## Multiprocessor OS Considerations
- Design Issues
	- Simultaneous concur`Fill in later` 
## MultiCore OS Considerations

## Grand Central Dispatch
- Usually Dev specifies what pieces can or should be executed simultaneously or in 
- GCD helps a dev by identifying a task that can be split off into a separate task
- Thread pool mechanism
- allows anon functions as a way of specifying tasks

## Virtual Machine Approach

## Windows Architecture

## Client/Server model

