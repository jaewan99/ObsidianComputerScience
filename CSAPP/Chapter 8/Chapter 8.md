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
- 