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