https://www.youtube.com/watch?v=xY7Y_-b9pv4&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=25

Using Semaphores to Coordinate Access to Shared Resources
- Basic idea: Thread uses a semaphore operation to notify another thread that some condition has become true
	- Use counting semaphores to keep track of resource state
	- Use binary semaphores to notify other threads
- The Producer-Consumer Problem
	- Mediating interactions between processes that generate information and that then make use of that information
	- Producer waits for empty slot, inserts item in buffer, and notifies consumer
	- Consumer waits for item, removes it from buffer, and notifies producer
	- Examples
		- Multimedia processing:
			- Producer creates video frames (MPEG), consumer renders them
		- Event-driven graphical user interfaces
			- Producer detects mouse clicks, mouse movements, and keyboard hits and inserts corresponding events in buffer
			- Consumer retrieves events from buffer and paints the display

Producer-Consumer on an n-element Buffer
- Requires a mutex and two counting semaphores:
	- mutex: enforces mutually exclusive access to the the buffer
	- slots: counts the available slots in the buffer
	- items: counts the available items in the buffer
- Implemented using a shared buffer package called sbuf.
- ![[Pasted image 20251103150548.png]]
- ![[Pasted image 20251103150717.png]]
- ![[Pasted image 20251103150857.png]]
- ![[Pasted image 20251103151225.png]]
- ![[Pasted image 20251103151237.png]]
- Readers-Writers Problem
	- Generalization of the mutual exclusion problem
	- Problem statement:
		- Reader threads only read the object
		- Writer threads modify the object
		- Writers must have exclusive access to the object
		- Unlimited number of readers can access the object
	- Occurs frequently in real systems, e.g.,
		- Online airline reservation system
			- can be reading at the same
			- writing like reservation
				- should happen on the mutual exclusive way.
		- Multithreaded caching Web proxy
- Variants of Readers-Writers
	- First readers-writers problem (favors readers)
		- No reader should be kept waiting unless a writer has already been granted permission to use the object
		- A reader that arrives after a waiting writer gets priority over the writer
		- The writer could starved out
	- Second readers-writers problem (favors writers)
		- Once a writer is ready to write, it performs its write as soon as possible
		- A reader that arrives after a writer must wait, even if the writer is also waiting
		- The readers could starved out
	- Starvation (where a thread waits indefinitely) is possible both cases

- Solution to First Readers-Writers Problem
	- ![[Pasted image 20251103154135.png]]

````C

P(&mutex);          // lock to safely update readcnt
readcnt++;
if (readcnt == 1)   // if I'm the first reader
    P(&w);           // block writers - when it's writing, it will wait until the 
					//writer releases 
V(&mutex);          // done updating readcnt

````


![[Pasted image 20251103155508.png]]
	- before the created new created new thread, whenever new connection request arrive. When leaves, it kills the thread- creates overhead - creating on-demand
	- Create a pool worker thread - pre-threaded or pre-pork processes
	- 1. Accept connection
	- 2. Insert descriptors - they are shared from thread to thread.
	- 3. remove descriptors - when item appears, one of the worker thread will remove that item. And use that descriptor to interact with the client.
		- When that interaction finishes, it goes back and checks for the next file descriptor in the buffer.
		- Instead of killing the thread, replace the thread.
	- ![[Pasted image 20251103160624.png]]
	- ![[Pasted image 20251103161532.png]]
	- echo_cnt = pthread_once will the checked everytime but only called once.
- Crucial concept: Thread Safety
	- Functions called from a thread must be thread-safe
	- Def: A function is thread-safe iff it will always produce correct results when called repeatedly from multiple concurrent threads.
	- Classes of thread-unsafe functions:
		- Class 1: Functions that do not protect shared variables
		- Class 2: Functions that keep state across multiple invocations
		- Class 3: Functions that return a pointer to a static variable
		- Class 4: Functions that call thread-unsafe functions
- Thread-Unsafe Functions (Class 1)
	- Failing to protect shared variables
		- Fix: Use P and V semaphore operations (or mutex)
		- Example: goodcnt.c
		- Issue: Synchronization operations will slow down code
- Thread-Unsafe Functions (Class 2)
	- Relying on persistent state across multiple function invocations
		- Example: Random number generator that relies on static state
		- ![[Pasted image 20251103162536.png]]
		- the random numbers that each thread gets back, are not only a function of the previous seed from the previous time that thread called the function. But also a function of other threads that are calling it
		- ![[Pasted image 20251103162907.png]]
		- Pass state as part of argument
			- and, thereby, eliminate static state
			- *nextp is now local variable on the thread stack
			- each caller will keep its own local copy of next and it will pass in a p pointer to rand
- Thread-Unsafe Functions (Class 3)
	- Returning a pointer to a static variable
	- Fix 1. Rewrite function so caller passes address of variable to store result
		- Requires changes in caller and callee
	- Fix 2. Lock-and-copy
		- Requires simple changes in caller (and none in callee)
		- However, caller must free memory.
	- ![[Pasted image 20251103163307.png]]
		- make a wrapper
		- P - so only one thread at a time we'll have this mutex
		- ctime = normale ctime
		- copy = strcpy - creating this local string array
- Thread-Unsafe Function (class 4)
	- Calling thread-unsafe functions
		- Calling one thread-unsafe function makes the entire function that calls it thread-unsafe
		- Fix: Modify the function so it calls only thread-safe functions ☺
- Reentrant Functions
	- Def: A function is reentrant iff it accesses no shared variables when called by multiple threads.
		- Important subset of thread-safe functions
			- Require no synchronization operations
			- Only way to make a Class 2 function thread-safe is to make it reentrant (e.g., rand_r )
			- ![[Pasted image 20251103164548.png]]
- Thread-Safe Library Functions
	- All functions in the Standard C Library (at the back of your K&R text) are thread-safe
		- Examples: malloc, free, printf, scanf
	- Most Unix system calls are thread-safe, with a few exceptions:
		- ![[Pasted image 20251103164643.png]]
- Race condition
	- Could this race occur?
	- ![[Pasted image 20251103165702.png]]
	- ![[Pasted image 20251103165528.png]]
	- 
	- Race Test
		- If no race, then each thread would get different value of i
		- Set of saved values would consist of one copy each of 0 through 99
	- ![[Pasted image 20251103165547.png]]
	- ![[Pasted image 20251103165739.png]]
- Another worry: Deadlock
	- Def: A process is deadlocked iff it is waiting for a condition that will never be true.
	- Typical Scenario
		- Processes 1 and 2 needs two resources (A and B) to proceed
		- Process 1 acquires A, waits for B
		- Process 2 acquires B, waits for A
		- Both will wait forever!
		- ![[Pasted image 20251103170429.png]]
		- Locking introduces the potential for deadlock: waiting for a condition that will never be true
		- Any trajectory that enters the deadlock region will eventually reach the deadlock state, waiting for either s0 or s1 to become nonzero
		- Other trajectories luck out and skirt the deadlock region
		- Unfortunate fact: deadlock is often nondeterministic (race)
		- ![[Pasted image 20251103170647.png]]
	- ![[Pasted image 20251103170819.png]]
	- Avoided Deadlock in Progress Graph
		- No way for trajectory to get stuck
		- Processes acquire locks in same order
		- Order in which locks released is immaterial                   
		- ![[Pasted image 20251103170851.png]]