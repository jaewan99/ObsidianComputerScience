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
				- Remember we saw direct mapped caches that were subject to these conflict misses, if we increase the associativity of the cache, we reduce the probability of those conflict misses. But we can never eliminate them until we have fully associative cache with just one set.
				- Any VP can be placed in any PP
					- It's fully associative, there's only one set, and each virtual page can go anywhere in the cache.
				- Requires a "large" mapping function - different from cache memories
			- Highly sophisticated, expensive replacement algorithms
				- Too complicated and open-ended to be implemented in hardware
					- Cache memory, the hardware did a search within the set, a parallel search try to find a cache line
					- But software cache, like VM, it's not feasible
			- Write-back rather than write-through
				- They try to defer writing anything back to the disk as long as possible
- [15:37](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=15:37.44) 
- Enabling Data Structure: Page Table
- A page table is an array of page table entries (PTEs) that maps virtual pages to physical pages.
	- Per-process kernel data structure in DRAM
	-  A data structure in memory that the kernel maintains for as part of each process context, so every process has its own page table.
	- PTE K - contains the physical address of the physical page k in DRAM
	- Page tables keeps track of where those are storred.
		- This PTE 1 corresponds to VP 1, and VP 1 is mapped to PP 0
		- VP2 is mapped to PP1
		- Some of these pages aren't in memory are stored on disks the allocated pages, for those pages, the page tables entry contains a pointer to the location of that page on disk.
		- null is not allocated
	- ![[Pasted image 20251020134944.png]]
	
	- Page Hit
	- Page hit: reference to VM word that is in physical memory (DRAM cache hit)
	- ![[Pasted image 20251020135415.png]]
	- Ex. movl instruction that generates the virtual address from CPU, the MMU looks up in the page table and let's say this Virtual address is somewhere within virtual page  (PTE2), it extracts the physical address of that virtual page 2. So in this case, the page is in memory, it's cached in memory, so it's a hit. And now the memory can return the physical memory to MMU
	
	- Page Fault
	- Page fault: reference to VM word that is not in physical memory (DRAM cache miss)
	- ![[Pasted image 20251020135541.png]]
	- the hardware triggers the exception - causes the transfer of control to the chunk of code in the kernel called the page fault handler, which then select a victim to be evicted, in this case VP4
	- ![[Pasted image 20251020135753.png]]
	
	- It fetches virtual page 3 from the disk, loads it up in the physical memory.  and then update this page table entry to reflect the fact that VP4 is now stored on disk.
	- If Virtual Page 4 had been modified at any time it would have to write the contents of it that to disk as well.
	- Once the handler copies virtual page 3 into memory, the instruction that called the page fault now can be re-executed. Now when MMU checks the PTE corresponding to that page, and it finds.
	- Key point: waiting uni
	- ![[Pasted image 20251020135935.png]]
	
	- 