# Chapter 5: Concurrency
## Key terms related to concurrency
- **Atomic operation**
	- Function/operation implemented as a sequence of one or more instructions that appears to be indivisible
	- No other process can see the intermediate state or interrupt the operation
	- Guaranteed
		- Execute as a group
		- Not execute at all
		- No visible effect on system state
	- Isolation from concurrent processes
- **Critical Section**
	- Section of code that must not be executed while other processes are using the shared resources it has to use
- **Deadlock**
	- Two or more processes are unable to proceed as each is waiting on for one of the others to do something
- **Livelock**
	- Two or more processes continuously change their states in response to each other without doing as useful work
- **Mutual exclusion**
	- Requirement, if a process accesses shared resources, no other process can use that shared resource i.e be in a critical section
- **Race Condition**
	- Situation, where multiple threads/processes read and write shared resources
- **Starvation**
	- Overlooked by scheduler, ready to run but never run
## Principles of Concurrency
-
## Mutual Exclusion

**Interrupt Disabling:**

- **Interrupts and Mutual Exclusion:**
  - In a multitasking operating system, various processes or threads run concurrently.
  - Interrupts are essential mechanisms to handle events such as I/O, timer expiration, or hardware faults.
  - Achieving mutual exclusion in such an environment is critical to prevent data corruption and maintain the integrity of shared resources.

**Interrupt Disabling Approach:**

  - To ensure mutual exclusion, a process can disable interrupts before entering a critical section and re-enable them when leaving the section.
  - Disabling interrupts blocks the CPU from responding to incoming interrupt requests.
  - This approach guarantees that no interrupt will occur during the execution of the critical section.

**Advantages and Considerations:**

  - Interrupt disabling is a straightforward way to implement mutual exclusion.
  - It is generally efficient and guarantees mutual exclusion as long as all processes adhere to the same protocol.
  - However, it has some drawbacks:
    - Disabling interrupts globally may have a significant impact on system responsiveness.
    - It should be used with caution, especially in real-time systems or systems with strict timing requirements.

**Special Machine Instructions:**

- **Atomic Instructions:**
  - Some modern CPUs provide atomic instructions that are executed in a single step without interruption.
  - These instructions are designed for mutual exclusion and work as follows:
    - **Test-And-Set:** This instruction reads a memory location and sets it to a particular value, all in one atomic step. It returns the previous value of the memory location.
    - **Swap:** This instruction swaps the content of a memory location with a specified value atomically.
- **Usage for Mutual Exclusion:**
  - Processes or threads can use these atomic instructions to protect their critical sections without disabling interrupts.
  - Here's an example of using "Test-And-Set":
    1. Process A reads a shared memory location using "Test-And-Set" and gets the previous value.
    2. If the previous value is 0 (indicating no other process is in the critical section), process A enters the critical section.
    3. If the previous value is 1, process A knows that another process is in the critical section and must wait.

- **Advantages and Limitations:**
  - Using atomic instructions is highly efficient and does not disable interrupts.
  - It is particularly useful in high-performance systems.
  - However, it may not be available on all hardware platforms, and its usage should be carefully designed to avoid race conditions.

## Semaphores
## Message Passing

