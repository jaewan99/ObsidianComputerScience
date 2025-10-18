https://www.youtube.com/watch?v=79yH0NeoEv4&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=14


 Control Flow
 - From startup to shutdown, a CPU simply reads and executes (interprets) a sequence of instructions, one at a time.
 - This sequence is the CPU's control flow (or flow of control)
 - The actual sequence of instructions that the hardware is executing is called the physical control flow
 - ![[Pasted image 20251018150314.png]]

Altering the Control Flow
- Up to now: two mechanisms for changing control flow:
	- Jumps and branches
	- Call and return
	- React to changes in program state
- Insufficient for a useful system:
	- Difficult to react to changes in system state
		- Data arrives from a disk or a network adapter
		- Instruction divides by zero
		- User hits Ctrl-C at the keyboard
		- System timer expires
	- "Exceptional Control Flow"
Exceptional Control Flow
- Exists at all levels of a computer system
- Low level mechanisms
	- 1. Exceptions
		- Change in control flow in response to a system event (i.e., change in system state)
		- Implemented using combination of hardware and OS software
- High level mechanisms
	- 2. Process context switch
		- Implemented by OS software and hardware timer
	- 3.Signals
		- Implemented by OS software
	- 4.Nonlocal jumps: setjmp () and longjmp ()
		- Implemented by C runtime library

Exceptions
-  An exception is a transfer of control to the OS kernel in response to some event (i.e., change in processor state)
	- Kernel is the memory-resident part of the OS
		- like to list files, to change directories and list current progresses.
	- Examples of events: Divide by 0, arithmetic overflow, page fault, I/O request completes, typing Ctrl-C
	- ![[Pasted image 20251018151115.png]]


- [07:00](https://www.youtube.com/watch?v=79yH0NeoEv4#t=07:00.08) 
Exception Control
- The actual transfer of control like in change in the program counter or %rip is done by the hardware. 
- But the code that executes as a result of that exception is set up and determined by the OS kernel
- So every type of event 