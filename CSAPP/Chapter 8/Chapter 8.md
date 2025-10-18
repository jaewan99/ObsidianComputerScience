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
Exception Table
- The actual transfer of control like in change in the program counter or %rip is done by the hardware. 
- But the code that executes as a result of that exception is set up and determined by the OS kernel
- every type of event has a unique exception number
	- which serves as an index into a jump table called an exception table
	- when event k happens, the hardware uses k as an index into this exception table. Gets the address of the exception handler for that exception

- [07:50](https://www.youtube.com/watch?v=79yH0NeoEv4#t=07:50.06) 
Asynchronous Exceptions (Interrupts)
- Caused by events external to the processor
	- Indicated by setting the processor's interrupt pin
	- Handler returns to "next" instruction
- Examples:
	- Timer interrupt
		- Every few ms, an external timer chip triggers an interrupt
		- Used by the kernel to take back control from user programs
	- I/O interrupt from external device
		- Hitting Ctrl-C at the keyboard
		- Arrival of a packet from a network
		- Arrival of data from a disk

Synchronous Exceptions
- Caused by events that occur as a result of executing an instruction:
- Traps
	- Intentional
	- Examples: system calls, breakpoint traps, special instructions
	- Returns control to "next" instruction
	- OS kernel provides all kinds of services to a program but your program doesn't have direct access. Your program can't call functions in the kernel, can't access data directly in the kernel, because that memory is protected and unavailable to user programs. 
	- So what the kernel does is they provide a interface that allows programs to make request to effectively, call functions within the kernel and to make requests to various services. And this interface is called system call.
		- System call - looks like a function call but it's really transferring control into the kernel.
- Faults
	- Unintentional but possibly recoverable
	- Examples: page faults (recoverable), protection faults (unrecoverable), floating point exceptions
		- protection faults - accessing the portion of memory that's not allocated
	- Either re-executes faulting ("current") instruction or aborts
- Aborts
	- Unintentional and unrecoverable
	- Examples: illegal instruction, parity error, machine check
		- when the memory is corruptedm or when there are problems in machine
	- Aborts current program


- [13:33](https://www.youtube.com/watch?v=79yH0NeoEv4#t=13:33.06) 
![[Pasted image 20251018152903.png]]

System Call Example: Opening File
- User calls: open(filename, options)
- Calls __open function, which invokes system call instruction syscall
- ![[Pasted image 20251018153245.png]]

Fault Example: Page Fault
- User writes to memory location
- That portion (page) of user's memory is currently on disk
- it needs to be loaded from disk into memory
- ![[Pasted image 20251018153439.png]]

Fault Example: Invalid Memory Reference
- ![[Pasted image 20251018153548.png]]
- Sends SIGSEGV signal to user process
- User process exits with "segmentation fault"


- [18:24](https://www.youtube.com/watch?v=79yH0NeoEv4#t=18:24.94) 
Processes
- A program can exists in many different places, in can exist as text in C file, .text section of binary, bytes that have been loaded into memory. While a process is an instance of a program that's runnin