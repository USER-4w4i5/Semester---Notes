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


### **Mutex (Mutual Exclusion):**

- **Definition:**
  - A mutex, short for "mutual exclusion," is a synchronization primitive used to protect critical sections in multithreaded or multiprocess systems.
  - It ensures that only one thread or process can access a shared resource or critical section at a time.
- **Usage with Semaphores:**
  - In the context of the Producer/Consumer problem and many other synchronization scenarios, mutex locks are used to protect access to shared data structures like buffers or queues.
  - Mutexes ensure that while one thread or process is working in a critical section, no other thread or process can enter that section.
- **Implementation:**
  - Mutex locks typically provide two operations:
    - **Lock (or Acquire):** A thread or process attempts to acquire the lock. If the lock is already held by another thread or process, it will block until the lock becomes available.
    - **Unlock (or Release):** A thread or process releases the lock, allowing other threads or processes to acquire it.
- **Example in Producer/Consumer Problem:**
  - In the code examples I provided for the Producer and Consumer, the `buffer_mutex` is a mutex used to protect access to the shared buffer.
  - When a thread or process wants to access the buffer (either for adding an item or removing an item), it must first acquire the `buffer_mutex`. This ensures that only one thread can access the buffer at any given time.

Here's how mutex locks are used in the provided code:

```python
Producer:
  while (true) {
    // ...
    
    // Lock the buffer.
    lock(buffer_mutex);
    
    // Add the item to the buffer.
    add_item_to_buffer(item);
    
    // Unlock the buffer.
    unlock(buffer_mutex);
    
    // ...
  }
```

```python
Consumer:
  while (true) {
    // ...
    
    // Lock the buffer.
    lock(buffer_mutex);
    
    // Remove an item from the buffer.
    item = remove_item_from_buffer();
    
    // Unlock the buffer.
    unlock(buffer_mutex);
    
    // ...
  }
```

### **Semaphores (Duplicate notes):**

- **Mutual Exclusion:**
  - Semaphores are a synchronization mechanism that can be used to enforce mutual exclusion.
  - A semaphore is a non-negative integer variable that can be accessed by two standard operations: "wait" and "signal."

- **Semaphore Operations:**
  - **Wait (P) Operation:**
    - If the semaphore value is greater than 0, it decrements the value and allows the process to continue.
    - If the semaphore value is 0, it blocks the process until another process signals (increments) the semaphore.
  - **Signal (V) Operation:**
    - Increments the semaphore value, possibly waking up a waiting process if the value was 0.

**The Producer/Consumer Problem:**

- **Scenario:**
  - The Producer/Consumer problem is a classic synchronization problem involving two types of processes: producers and consumers.
  - Producers produce items and place them in a shared buffer, while consumers remove items from the buffer.
  - The challenge is to ensure that producers don't add items to a full buffer and consumers don't remove items from an empty buffer, all while maintaining mutual exclusion.

- **Using Semaphores:**
  - Semaphores can be used to solve the Producer/Consumer problem.
  - Two semaphores, "empty" and "full," are used:
    - "empty" counts the number of empty slots in the buffer.
    - "full" counts the number of filled slots in the buffer.
  - Additional semaphores or mutex locks are used to protect access to the shared buffer.

- **Implementation Example:**
  - Let's assume we have a shared buffer with a maximum size of 10.
  - We define semaphores:
    - `empty` initialized to 10 (representing empty slots).
    - `full` initialized to 0 (initially, no items in the buffer).
  - We also use mutex locks to protect the buffer.

  ```python
  Producer:
    while (true) {
      // Produce an item.
      item = produce_item();
      
      // Wait if the buffer is full.
      wait(empty);
      
      // Lock the buffer.
      lock(buffer_mutex);
      
      // Add the item to the buffer.
      add_item_to_buffer(item);
      
      // Unlock the buffer.
      unlock(buffer_mutex);
      
      // Signal that the buffer is no longer empty.
      signal(full);
    }
  ```

  ```python
  Consumer:
    while (true) {
      // Wait if the buffer is empty.
      wait(full);
      
      // Lock the buffer.
      lock(buffer_mutex);
      
      // Remove an item from the buffer.
      item = remove_item_from_buffer();
      
      // Unlock the buffer.
      unlock(buffer_mutex);
      
      // Signal that an empty slot is available.
      signal(empty);
      
      // Consume the item.
      consume_item(item);
    }
  ```

  - The "wait" and "signal" operations, along with mutex locks, ensure that producers and consumers can work without violating mutual exclusion or buffer overflows/underflows.

This solution using semaphores and mutex locks is a common approach to the Producer/Consumer problem. It ensures that producers and consumers operate safely and efficiently. If you have more specific questions or need further clarification, please let me know.
## Message Passing
- **Synchronization:**
  - Message passing is a mechanism for inter-process communication (IPC) in which processes exchange data through messages.
  - Synchronization in message passing is achieved by sending and receiving messages between processes.
  - Message passing ensures that processes coordinate their actions and can be used for both cooperation and synchronization.

- **Addressing:**
  - In message passing, processes are identified by their process IDs (PIDs).
  - When a process sends a message, it specifies the target process by its PID.
  - This addressing mechanism ensures that the message reaches the intended recipient.

- **Message Format:**
  - Messages typically have a format that includes a header and a body.
  - The header contains control information, such as the sender's PID and the message type.
  - The body contains the actual data being transmitted.

- **Queueing Discipline:**
  - In message passing systems, messages are often placed in message queues.
  - The order in which messages are retrieved from the queue can follow different queueing disciplines.
  - Common queueing disciplines include first-come, first-served (FCFS), priority-based, and round-robin.

- **Mutual Exclusion:**
  - Message passing can be used to implement mutual exclusion.
  - For example, when multiple processes need to access a shared resource, they can coordinate through message passing to ensure only one process accesses the resource at a time.

**Example: Implementing Mutual Exclusion with Message Passing:**

Suppose we have two processes, Process A and Process B, which need to access a shared resource using message passing for mutual exclusion:

- **Process A:**
  ```python
  while (true) {
    // Request permission to access the shared resource from Process B.
    send_request_message(ProcessB_PID);
    
    // Wait for a response message from Process B.
    receive_response_message();
    
    // Access the shared resource.
    // ...

    // Release the shared resource.
    // ...
    
    // Notify Process B that it can access the resource.
    send_release_message(ProcessB_PID);
  }
  ```

- **Process B:**
  ```python
  while (true) {
    // Wait for a request message from Process A.
    receive_request_message();

    // Grant permission to access the shared resource to Process A.
    send_response_message(ProcessA_PID);
    
    // Wait for Process A to release the resource.
    receive_release_message();
  }
  ```

In this example, the two processes, A and B, coordinate their access to the shared resource through message passing. The request and response messages help achieve mutual exclusion, ensuring that only one process accesses the resource at a time.



---



# Chapter 4: Threads
