https://www.youtube.com/watch?v=zVcE3Opyk-o&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=24 
Question: which variables in a threaded c program are shared?
- The answer is not as simple as "global variables are shared" and "stack variables are private".

Threads Memory Model
- Conceptual model:
	- Multiple threads run within the context of a single process
	- Each thread has its own separate thread context
		- Thread ID, stack, stack pointer, PC, condition codes, and GP registers
	- All threads share the remaining process context
		- Code, data, heap, and shared library segments of the process virtual address space
		- Open files and installed handlers
	- Operationally, this model is not strictly enforced:
		- Register values are truly separate and protected, but ...
		- Any thread can read and write the stack of any other thread
		- ![[Pasted image 20251103134557.png]]
		- ![[Pasted image 20251103134147.png]]
	- Mapping Variable Instances to Memory
		- Global variables
			- Def: Variable declared outside of a function
				- Virtual memory contains exactly one instance of any global variable
		- Local variables
			- Def: Variable declared inside function without static attribute
				- Each thread stack contains one instance of each local variable
		- Local static variables
			- Def: Variable declared inside function with the static attribute
				- Virtual memory contains exactly one instance of any local static variable.
	- Answer: A variable x is shared iff multiple threads reference at least one instance of x. Thus:
		- ptr, cnt, and msgs are shared
		- i and myid are not shared
- badcnt.c : Improper Synchronization
	- ![[Pasted image 20251103140929.png]]
	- ![[Pasted image 20251103141148.png]]
- Concurrent Execution
	- Key idea: In general, any sequentially consistent interleaving is possible, but some give an unexpected result!
		- I i denotes that thread i executes instruction I
		- %rdxi is the content of %rdx in thread i’s context