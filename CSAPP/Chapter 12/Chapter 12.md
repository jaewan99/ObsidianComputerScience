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
	- 