https://www.cs.cmu.edu/afs/cs/academic/class/18213-m25/www/lectures/22-concprog.pdf
https://www.youtube.com/watch?v=jKWfQfZkQ-w&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=23
So as soon as we have multiple flow accessing shared resources all kinds of bad things can happen in your program. 

Classical problem classes of concurrent programs:
- Races: outcome depends on arbitrary scheduling decisions elsewhere in the system
	- Example: who gets the last seat on the airplane?
	- Job-list - runs and finish before the parents has chance to add the child in the list
	
- Deadlock: improper resource allocation prevents forward progress
	- Example: traffic gridlock
	- printf - interrupted by signal handler - printf
		- Printf acquires a terminal lock but the second printf won't be able to get it because the printf and the main routine has it
		- So now your signal handler the printf and the signal handler is waiting for the event that will never occur
		- ![[Pasted image 20251103101607.png]]
- Livelock / Starvation / Fairness: external events and/or system scheduling decisions can prevent sub-task progress
			- Example: people always jump in front of you in line

Iterative servers
- Iterative servers process on request at a time.
	- ![[Pasted image 20251103101819.png]]
	- ![[Pasted image 20251103101840.png]]
	- Where Does Second Client Actually Block?
		- Second client attempts to connect to iterative server
			- Due to TCP Buffering:
				- Call to connect returns
					- Even though connection not yet accepted
					- Server side TCP manager queues request
				- Call to rio_writen returns
					- Server side TCP manager buffers input data
				- Call to rio_readlineb blocks!
					- Server hasn’t written anything for it to read yet.
- Fundamental Flaw of Iterative Servers
	- ![[Pasted image 20251103102641.png]]
	- Client 1:
		- User goes out to lunch
		- Client 1 blocks waiting for user to type in data
	- Server
		- Server blocks waiting for data from Client 1
	- Client 2:
		- Client 2 blocks waiting to read from server
	
	- We are in the untenable situation - where one client has sort of totally affected all of the other clients in the system and none of the other clients can get service.
		- Solution: use concurrent servers instead
		- Concurrent servers use multiple concurrent flows to serve multiple clients at the same time
- Approaches for Writing Concurrent Servers
	- Allow server to handle multiple clients concurrently
		- 1. Process-based
			- Kernel automatically interleaves multiple logical flows
			- Each flow has its own private address space
				- each flow is independent and controlled by kernel
		- 2. Event-based
			- Programmer manually interleaves multiple logical flows
			- All flows share the same address space
			- Uses technique called I/O multiplexing
				- The user and programmer creates this flow and manually interleaves this flows.
		- 3. Thread-based
			- Kernel automatically interleaves multiple logical flows
			- Each flow shares the same address space
			- Hybrid of process-based and event-based
				- Each of these flows are implemented by thread

- Approach #1: Process-based Servers
	- Spawn separate process for each client
		- ![[Pasted image 20251103103417.png]]
	- Process-Based concurrent echo server
		- ![[Pasted image 20251103103755.png]]
		- argv  - pass in the port number that we want this server to listen on
		- sockaddr_storage - protocol independent, big enough to handle IPv4, IPv6
		- listenfd - create listening descriptor
		- 