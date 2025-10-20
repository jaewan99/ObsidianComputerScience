https://www.youtube.com/watch?v=Fy9cnP9TXUc&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=17


Virtual Machine
- Ex. disk - the controller instead presents to the kernel a view of the disk as a series of sequence of logical blocks. It presents that view by intercepting the requests from the kernel for I/O, and changing those logical block numbers that the kernel sends into the actual physical address
- ![[Pasted image 20251020131130.png]]
- Used in "simple" systems like embedded microcontroller devices like cars, elevators, digital picture frames.

- ![[Pasted image 20251020131409.png]]
- Virtualized the disk by having the disk controller intercept request. In the case of the main memory resource, the requests are actually intercepted by a piece of hardware called MMU, memory management unit.
	- CPU executes an instruction - like move instruction that generates some effective address. This is a virtual address.
	- CPU send that address to MMU - which goes through a process called 'Address Translation' 
	- and that points to actual physical address.


- [05:39](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=05:39.62) 
- ![[Pasted image 20251020131937.png]]
- Address space is a "set" of address, not of data bytes but the address of these bytes
- Typically the virtual address space is usually much larger than the physical address space.
	- Physical address space corresponds to the amount of DRAM that we have in the system
- Why Virtual Memory (VM)?
	- Uses main memory efficiently
		- Use DRAM as a cache for parts of a virtual address space
	- Simplifies memory management
		- Each process gets the same uniform linear address space
	- Isolates address spaces
		- One process can't interfere with another's memory
		- User program cannot access privileged kernel information and code
		
- [08:54](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=08:54.25)
- VM as a tool for caching
	- ![[Pasted image 20251020132918.png]]
	- So conceptually we can think virtual memory as a sequence of bytes stored in the disk. And then the contents of that virtual memory stored on disk are cached in DRAM.
	- Conceptually, virtual memory is an array of N contiguous bytes stored on disk.
	- The contents of the array on disk are cached in physical memory (DRAM cache)
		- These cache blocks are called pages (size is P = 2P bytes)
	
	- DRAM Cache Organization
		- DRAM cache organization driven by the enormous miss penalty
			- DRAM is about 10x slower than SRAM
			- Disk is about 10,000x slower than DRAM
		- Consequences
			- Large page (block) size: typically 4 KB, sometimes 4 MB
			- Fully associative
				- Remember we saw direct mapped caches that were subject to these conflict misses, if we increase the associativity of the cache, we reduce the proba
				- Any VP can be placed in any PP
				- 