So as soon as we have multiple flow accessing shared resources all kinds of bad things can happen in your program. 

Classical problem classes of concurrent programs:
- Races: outcome depends on arbitrary scheduling decisions elsewhere in the system
	- Example: who gets the last seat on the airplane?
	- Job-list - runs and finish before the parents has chance to add the child in the list
	
- Deadlock: improper resource allocation prevents forward progress
	- Example: traffic gridlock
	- printf - interrupted by signal handler - printf
		- Printf acquires a terminal lock but the second printf won't be able to get it because the printf and the main routine has it
		- So now your signal handler the printf and the g