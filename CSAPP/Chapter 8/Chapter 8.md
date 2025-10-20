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
- Exception handler is nothing more a piece of code in the os telling what should be done when the exception happens


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
- argv - when you run a program you specify the program name. And then arguments separated by spaces
	- list of pointers to arg strings above
- envp - environment variable strings is a set of key equal value pairs.


- [1:06:23](https://www.youtube.com/watch?v=79yH0NeoEv4#t=1:06:23.38) 
- Executes "/bin/ls -lt /usr/include" in child process using current environment:
- ls - list the files in /usr/include
- -lt - show the long form of the listing and sort them in time order. From most recent
- ![[Pasted image 20251018172306.png]]
- Summary
	- Exceptions
		- Events that require nonstandard control flow
		- Generated externally (interrupts) or internally (traps and faults)
	- Processes
		- At any given time, system has multiple active processes
		- Only one can execute at a time on a single core, though
		- Each process appears to have total control of processor + private memory space
	- Spawning processes
		- Call fork
		- One call, two returns
	- Process Completion
		- Call exit
		- One call, no return
	- Reaping and waiting for processes
		- Call wait and waitpid
	- Loading and running programs
		- Call execve (or variant)
		- One call, (normally) no return

https://www.youtube.com/watch?v=zc96AQLPrGY&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=15



- [01:10](https://www.youtube.com/watch?v=zc96AQLPrGY#t=01:10.65) 
- Linux process hierarchy
- ![[Pasted image 20251019233216.png]]
	- There is only one way to create processes on a linux system - that is using the fork call.
	- In fact, the all of the processes on the system 
		- All processes on the system actually form a hierarchy
		- So that the very first process created when you boot the system up is the init process
			- which has the process id of 1
			- all other processes on the system are descendants of that init process
			- Init process - when it starts up it creates daemons
				- daemons - which are long running programs that provides services typically, so for example, web server  or other kinds of services that you always want running on the system.
			- Login shell - which provide command line interface to users
				-  so when you login to linux system 
				- executes programs in my behalf
				-  when we types something in your shelf like "ls" - we are asking the shell to run the executable program called 'ls'
					- so it will create a child and execute ls 
- Shell program
	- Problem with Simple Shell Example
		- Our example shell correctly waits for and reaps foreground jobs
	- But what about background jobs?
		- Will become zombies when they terminate
		- Will never be reaped because shell (typically) will not terminate
		- Will create a memory leak that could run the kernel out of memory
- ECF to the Rescue!
	- Solution: Exceptional control flow
		- The kernel will interrupt regular processing to alert us when a background process completes
		- In Unix, the alert mechanism is called a signal

- [09:36](https://www.youtube.com/watch?v=zc96AQLPrGY#t=09:36.85) 
- Signals
	- A signal is a small message that notifies a process that an event of some type has occurred in the system
		- Akin to exceptions and interrupts
		- Sent from the kernel (sometimes at the request of another process) to a process
		- Signal type is identified by small integer ID's (1-30)
		- Only information in a signal is its ID and the fact that it arrived
- Signal Concepts: Sending a Signal
	- Kernel sends (delivers) a signal to a destination process by updating some state in the context of the destination process
	- Kernel sends a signal for one of the following reasons:
		- Kernel has detected a system event such as divide-by-zero (SIGFPE) or the termination of a child process (SGCHLD)
		- Another process has invoked the kil1 system call to explicitly request the kernel to send a signal to the destination process
- Signal Concepts: Receiving a Signal
	- A destination process receives a signal when it is forced by the kernel to react in some way to the delivery of the signal
	- Some possible ways to react:
		- Ignore the signal (do nothing)
		- Terminate the process (with optional core dump)
		- Catch the signal by executing a user-level function called signal handler
		- Akin to a hardware exception handler being called in response to an asynchronous interrupt:
- Signal Concepts: Pending and Blocked Signals
	- A signal is pending if sent but not yet received
		- There can be at most one pending signal of any particular type
		- Important: Signals are not queued
			- If a process has a pending signal of type k, then subsequent signals of type k that are sent to that process are discarded
		- A process can block the receipt of certain signals
			- Blocked signals can be delivered, but will not be received until the signal is unblocked
		- A pending signal is received at most once
	- Kernel maintains pending and blocked bit vectors in the context of each process
		- pending: represents the set of pending signals
			- Kernel sets bit k in pending when a signal of type k is delivered
			- Kernel clears bit k in pending when a signal of type k is receive
		- blocked: represents the set of blocked signals
			- Can be set and cleared by using the sigprocmask function
			-  Also referred to as the signal mask


- [20:12](https://www.youtube.com/watch?v=zc96AQLPrGY#t=20:12.49) 
- ![[Pasted image 20251020100448.png]]
- Sending Signals: Process Groups
	- Every process belongs to exactly one process group
		- getpgrp () - Return process group of current process
		- setpgid () - Change process group of a process
- Process group allows us to send signals to the group of processes at the same time.
- ![[Pasted image 20251020100841.png]]
- Sending Signals from the Keyboard
	- Typing ctrl-c (ctrl-z) causes the kernel to send a SIGINT (SIGTSTP) to every job in the foreground process group.
		- SIGINT - default action is to terminate each process
		- SIGTSTP - default action is to stop (suspend) each process
		- ![[Pasted image 20251020101018.png]]
		- ![[Pasted image 20251020101201.png]] 
		- [27:12](https://www.youtube.com/watch?v=zc96AQLPrGY#t=27:12.73) 
		- Sending signals with kill function


- [28:05](https://www.youtube.com/watch?v=zc96AQLPrGY#t=28:05.43) 
- Receiving Signals
	- There's a control passes into the kernel because of some exception
		- That exception can be either a timer going off, interrupt or it can be trap user calls a system call.
		- Transfer control into the kernel is always caused by some exception
		- From process A to B - kernel code
			-  Calls the scheduler function and decides to do context switch from process A to process B
			- Right before it returns from the exception and right before it's ready to pass control back to process the user code and process B
				- It checks for the any signals that any pending signals
				- Kernel computes pnb = pending & ~blocked
					- The set of pending nonblocked signals for process p
					- These are the pending system that should be received
				- If (pnb == 0)
					- Pass control to next instruction in the logical flow for p
				- Else
					- Choose least nonzero bit k in pnb and force process p to receive signal k
					- The receipt of the signal triggers some action by p
					- Repeat for all nonzero k in pnb
					- Pass control to next instruction in logical flow for p
- Default actions
	- Each signal type has a predefined default action, which is one of:
		- The process terminates
		- The process stops until restarted by a SIGCONT signal
		- The process ignores the signal
- Installing Signal Handlers
	- The signal function modifies the default action associated with the receipt of signal signum:
		- handler_t *signal(int signum, handler_t *handler)
	- Different values for handler:
		- SIG_IGN: ignore signals of type signum
		- SIG_DFL: revert to the default action on receipt of signals of type signum
		- Otherwise, handler is the address of a user-level signal handler
			- Called when process receives signal of type signum
			- Referred to as "installing" the handler
			- Executing handler is called "catching" or "handling" the signal
			- When the handler executes its return statement, control passes to the instruction in the control flow of the process that was interrupted on receipt of the signal.
	- ![[Pasted image 20251020102834.png]]


- [34:01](https://www.youtube.com/watch?v=zc96AQLPrGY#t=34:01.42) 
- 