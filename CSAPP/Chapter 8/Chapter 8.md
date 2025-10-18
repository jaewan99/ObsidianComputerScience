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
![[Pasted image 20251018162157.png]]


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
- A program can exists in many different places, in can exist as text in C file, .text section of binary, bytes that have been loaded into memory. While a process is an instance of a program that's running in execution

Process provides each program with two key abstractions:
- Logical control flow
	- Each program seems to have exclusive use of the CPU
	- Provided by kernel mechanism called context switching
	- it gives the illusion that that you gave exclusive access/use to CPU and registers.
	- When you're running program in a process. you never have to worry about any other programs modifying your registers and you can't even tell that there's even other processes running on the system. 
- Private address space
	- Each program seems to have exclusive use of main memory.
	- Provided by kernel mechanism called virtual memory
	- another, illusion that we have our own address space, and this is provided by mechanism called virtual memory. So each running program has its own code, data, heap, stack.

![[Pasted image 20251018155116.png]]![[Pasted image 20251018155154.png]]


- [21:39](https://www.youtube.com/watch?v=79yH0NeoEv4#t=21:39.11) 
- In reality, for example if we are having single core, we are actually sharing the system and OS is the one that manages the system.
- Single processor executes multiple processes concurrently
	- Process executions interleaved (multitasking)
	- Address spaces managed by virtual memory system
	- Register values for nonexecuting processes saved in memory

- ![[Pasted image 20251018155515.png]]
- It copies the current register values into memory and saves them

- ![[Pasted image 20251018155646.png]]

- ![[Pasted image 20251018155720.png]]

- ![[Pasted image 20251018155812.png]]
- So it switches the address space for this process - address space and register values are the context. So context switch is the change in the address space and the register values.

-  Multicore processors
	- Multiple CPUs on single chip
	- Share main memory (and some of the caches)
	- Each can execute a separate process
		- Scheduling of processors done by kernel


- [23:41](https://www.youtube.com/watch?v=79yH0NeoEv4#t=23:41.36) 
Concurrent Processes
- Each process is a logical control flow.
- Two processes run concurrently (are concurrent) if their flows overlap in time
- Otherwise, they are sequential
- Examples (running on single core):
	- Concurrent: A&B, A&C
	- ![[Pasted image 20251018161014.png]]

	- User View of Concurrent Processes
		- Control flows for concurrent processes are physically disjoint in time
		- However, we can think of concurrent processes as running in parallel with each other
		
	- ![[Pasted image 20251018161046.png]]


- [26:38](https://www.youtube.com/watch?v=79yH0NeoEv4#t=26:38.36) 
Context Switching
- Processes are managed by a shared chunk of memory-resident OS code called the kernel
	- Important: the kernel is not a separate process, but rather runs as part of some existing process.
- Control flow passes from one process to another via a context switch
- Process A - Exception
	- Transfer control to kernel - kernel invokes its scheduler which decides whether to let A continue to run or to do context switch and run a new another process.
		- This case, the scheduler decided to run process B
		- Repoints the address space and registers for process B.
		- ![[Pasted image 20251018161752.png]]


- [28:20](https://www.youtube.com/watch?v=79yH0NeoEv4#t=28:20.22) 
System Call Error Handling
- On error, Linux system-level functions typically return -1 and set global variable errno to indicate cause.
- Hard and fast rule:
	- You must check the return status of every system-level function
	- Only exception is the handful of functions that return void - such as exit or free
	- ![[Pasted image 20251018161958.png]]
	- if -1, error
	- ![[Pasted image 20251018162353.png]]


- [33:14](https://www.youtube.com/watch?v=79yH0NeoEv4#t=33:14.72) 
Creating and Terminating Processes
- From a programmer's perspective, we can think of a process as being in one of three states
- Running
	- Process is either executing, or waiting to be executed and will eventually be scheduled (i.e., chosen to execute) by the kernel
- Stopped
	- Process execution is suspended and will not be scheduled until further notice (next lecture when we study signals)
- Terminated
	- Process is stopped permanently

Terminating Processes
- Process becomes terminated for one of three reasons:
	- Receiving a signal whose default action is to terminate (next lecture)
	- Returning from the main routine
	- Calling the exit function
- void exit (int status)
	- Terminates with an exit status of status
	- Convention: normal return status is 0, nonzero on error
	- Another way to explicitly set the exit status is to return an integer value from the main routine
- exit is called once but never returns.

Creating Processes
- Parent process creates a new running child process by calling fork
- int fork (void)
	- Returns 0 to the child process, child's PID to parent process
	- Child is almost identical to parent:
		- Child get an identical (but separate) copy of the parent's virtual address space.
			- All the global var, stack and code are exactly the same as the parents.
		- Child gets identical copies of the parent's open file descriptors
			- like stdio
		- Child has a different PID than the parent
- fork is interesting (and often confusing) because it is called once but returns twice
- Fork example
- ![[Pasted image 20251018163444.png]] 

- Modeling fork with Process Graphs
	- A process graph is a useful tool for capturing the partial ordering of statements in a concurrent program:
		- Each vertex is the execution of a statement
		- a -> b means a happens before b
		- Edges can be labeled with current value of variables
		- printf vertices can be labeled with output
		- Each graph begins with a vertex with no inedges
	- Any topological sort of the graph corresponds to a feasible total ordering.
		- Total ordering of vertices where all edges point from left to right
		- The logical flow represented this child have to occur in order, first 'e' and 'f'
		- ![[Pasted image 20251018164529.png]]
		- ![[Pasted image 20251018164709.png]]
		- ![[Pasted image 20251018165005.png]]
		- ![[Pasted image 20251018165024.png]]


- [48:18](https://www.youtube.com/watch?v=79yH0NeoEv4#t=48:18.50) 
Reaping Child Processes
- Idea
	- When process terminates, it still consumes system resources
		- Examples: Exit status, various OS tables
	- Called a "zombie"
		- Living corpse, half alive and half dead
- Reaping
	- Performed by parent on terminated child (using wait or waitpid)
	- Parent is given exit status information
	- Kernel then deletes zombie child process
- What if parent doesn't reap?
	- If any parent terminates without reaping a child, then the orphanage child will be reaped by init process (pid == 1)
	- So, only need explicit reaping in long-running processes
		- e.g., shells and servers
		- ![[Pasted image 20251018165817.png]]
		- Child was zombie
		
		- ![[Pasted image 20251018165958.png]]

- [54:22](https://www.youtube.com/watch?v=79yH0NeoEv4#t=54:22.09) 
- wait: Synchronizing with Children
	- Parent reaps a child by calling the wait function
	- int wait(int *child_status)
		- Suspends current process until one of its children terminates
		- Return value is the pid of the child process that terminated
		- If child_status != NULL, then the integer it points to will be set to a value that indicates reason the child terminated and the exit status:
			- Checked using macros defined in wait.h
			- WIFEXITED, WEXITSTATIS, WIFSIGNALED, WTERMSIG, WIFSTOPPED, WSTOPSIG, WIFCONTINUED
			- See textbook for details
- ![[Pasted image 20251018170238.png]]


- [1:00:22](https://www.youtube.com/watch?v=79yH0NeoEv4#t=1:00:22.25) 
- To run a different program inside of a process we use function called execve
- int execve (char *filename, char *argv[], char *envp[])
- Loads and runs in the current process:
	- Executable file filename
		- Can be object file or script file beginning with # ! interpreter (e.g., #!/bin/bash)
	- ... with argument list argv
		- By convention argv [0] == filename
	- ... and environment variable list envp
		- "name=value" strings (e.g., USER=droh)
		- getenv, putenv, printenv
	- Overwrites code, data, and stack
		- Retains PID, open files and signal context
	- Called once and never returns
		- ...except if there is an error

- [1:03:27](https://www.youtube.com/watch?v=79yH0NeoEv4#t=1:03:27.69) 
- After execve finishes its work, it creates new stack, new code and data, new empty heap, everything is new. 
- argv[0] - when you run a program you specify the program name. And then arguments seperated by spaces