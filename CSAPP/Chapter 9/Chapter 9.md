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
	- Key point: waiting until the miss to copy the page to DRAM is known as demand paging
	- ![[Pasted image 20251020135935.png]]


- [21:11](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=21:11.15) 
- Allocating space (like by using sbrk) just changes this page table entry and then when page is actually touched then it'll be brought into the cache
- Allocating a new page (VP 5) of virtual memory.
- ![[Pasted image 20251020140620.png]]

- Locality to the Rescue Again!
	- Virtual memory seems terribly inefficient, but it works because of locality.
	- At any point in time, programs tend to access a set of active virtual pages called the working set
		- Programs with better temporal locality will have smaller working sets
	- If (working set size < main memory size)
		- Good performance for one process after compulsory misses
	- If ( SUM(working set sizes) > main memory size )
		- Thrashing: Performance meltdown where pages are swapped in and out continuously
 
 - [24:04](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=24:04.08) 
 - VM as a Tool for Memory Management
	 - Key idea: each process has its own virtual address space
		 - It can view memory as a simple linear array
		 - Mapping function scatters addresses through physical memory
			 - Well-chosen mappings can improve locality
 - Each process has its own virtual address space, and kernel implements this by giving each process its own separate page table. In the context of that process so it's just a data structure in the kernel, that kernel keeps for the process.
 - In this way we can present a view to the programmer and tools, that each process has a very similar address space, virtual space, same size address space, code and data start at the same place. but then the actual pages that process used can be scattered in memory. It gives us the most efficient way to use the memory
	 - ![[Pasted image 20251020142343.png]]
 - VM as a Tool for Memory Management
	 - Simplifying memory allocation
		 - Each virtual page can be mapped to any physical page
		 - A virtual page can be stored in different physical pages at different times
			 - ex. if VP1 can be mapped to PP2 and PP6 when PP2 is no longer used
	 - Sharing code and data among processes
		 - Map virtual pages to the same physical page (here: PP 6)
			 - To share certain code or data
				 - ex. lib.c just needs to be loaded into physical address, other VP just mapped to physical address.
	
- [29:22](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=29:22.22) 
- Simplifying Linking and Loading
	- Linking
		- Each program has similar virtual address space
		- Code, data, and heap always start at the same addresses.
	- Loading
		- execve allocates virtual pages for .text and data sections & creates PTEs marked as invalid
		- The . text and .data sections are copied, page by page, on demand by the virtual memory system


- [32:57](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=32:57.70) 
- VM as a Tool for Memory Protection
	- Extend PTEs with permission bits
	- MMU checks these bits on each access
	- ![[Pasted image 20251020143617.png]]


- [37:23](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=37:23.98) 

- 1. Given one virtual address - that consist of n bits; and blocks that consists of whose size can be represented with p bits.
	- Virtual page offsets are analogous to the block offsets that we saw with caches
	- Virtual page number - since VM is fully associative, there's only one set, so think of this as like a tag [[Chapter 6.4 캐시 메모리#Example Direct Mapped Cache (E = 1)]]
		- what uniquely identifies this block.
	- When CPU presents virtual address to MMU - it takes the VPN and uses that index into that page table
		- And physical page number comes out from the page table entry
	- The offsets in a virtual block is going to be the same as the offset in a physical block
		-  the same size block
	- ![[Pasted image 20251020150615.png]]
- Address Translation: Page Hit
	- 1) Processor sends virtual address to MMU
	- 2-3) MMU fetches PTE from page table in memory
	- 4) MMU sends physical address to cache/memory
	- 5) Cache/memory sends data word to processor
	- ![[Pasted image 20251020150701.png]]

- Address Translation: Page Fault
- ![[Pasted image 20251021223445.png]]

- 1) Processor sends virtual address to MMU
- 2-3) MMU fetches PTE from page table in memory
- 4) Valid bit is zero, so MMU triggers page fault exception
- 5) Handler identifies victim (and, if dirty, pages it out to disk)
- 6) Handler pages in new page and updates PTE in memory
- 7) Handler returns to original process, restarting faulting instruction



- [45:52](https://www.youtube.com/watch?v=Fy9cnP9TXUc#t=45:52.57) 
- ![[Pasted image 20251020151653.png]]
- Speeding up Translation with a TLB
	- Page table entries (PTEs) are cached in L1 like any other memory word
		- PTEs may be evicted by other data references
		- PTE hit still requires a small L1 delay
	- Solution: Translation Lookaside Buffer (TLB)
		- TLB is a hardware cache that caches PTEs
		- Small set-associative hardware cache in MMU
		- Maps virtual page numbers to physical page numbers
		- Contains complete page table entries for small number of pages
- ![[Pasted image 20251020154028.png]]
- ![[Pasted image 20251020154116.png]]
- ![[Pasted image 20251020154225.png]]
- ![[Pasted image 20251020154842.png]]
- How does this saves space?
	- If we don't use the page level, we need a page table that would have an entry for each virtual page, even if it's used or not.
	- With this multi-level scheme, we only need to generate level two page tables, enough level two pages to cover the portion of the virtual address space that we're actually using. And that the portion of the virtual address space that you're not using at this gap right here. (the "gap" in the picture) there's no need to have the page table.

- ![[Pasted image 20251020155128.png]]
- Summary
	- Programmer's view of virtual memory
		- Each process has its own private linear address space
		- Cannot be corrupted by other processes
	- System view of virtual memory
		- Uses memory efficiently by caching virtual memory pages
			- Efficient only because of locality
		- Simplifies memory management and programming
		- Simplifies protection by providing a convenient interpositioning point to check permissions

https://www.youtube.com/watch?v=lu1B1faqpUw&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=18

![[Pasted image 20251020143830.png]]


- [00:57](https://www.youtube.com/watch?v=lu1B1faqpUw#t=00:57.25) 
- Addressing - 
	- ![[Pasted image 20251021101535.png]]
	- ![[Pasted image 20251021111443.png]]
	
	- ![[Pasted image 20251021111552.png]]
	- Each page entry consists of a physical page number, and a valid bit, if's on, the page is in the memory. This VPN column doesn't exist in the page table.

	- Simple Memory System cache
		- 16 lines, 4 byte block size
		- Physically addressed
		- Direct mapped
		- ![[Pasted image 20251021112043.png]]
		- 
- [05:51](https://www.youtube.com/watch?v=lu1B1faqpUw#t=05:51.28) 
- Address Translation Example
	- Check the actual book
- [18:04](https://www.youtube.com/watch?v=lu1B1faqpUw#t=18:04.86) 
	- Each core can execute instructions separately.
	- Each of the core has a register file.
	- Some hardware that fetches instructions.
	-  ![[Pasted image 20251021124015.png]]
	- ![[Pasted image 20251021124038.png]]
- ![[Pasted image 20251021130023.png]]
- To this point, we have been using a model where the MMU does the address translation and creates a complete physical address - and send that physical address to cache.
	- But in reality, intel does this little trick to speed up L1 cache accesses
		- We are given the virtual address
			- In this virtual address
				- The index and the offset bits in the physical addresses are identical / exactly correspond to the PPO in the physical address which is exactly identical to the VPO in the virtual address
				- That means is that when the MMU is given a virtual address.
					- It can send the VPO off to the L1 cache
					- Even though, L1 is physically addressed, we can send the VPO in the virtual address to the L1 cache because of this phenomenon that the PPO is identical to the VPO
					- So even before the MMU is doing any address translation, it can send this these VPO bits to cache.
					- And then the cache can get busy extracting the index the cache index bits
						- Looking up all of the lines, in that set. and then have everything ready for the tag check.
							- can only occur after the address translation happens - once there's a physical address with a from which we can extract the cache tag.
						- We are getting 8 possible tag - because we are having 8-way associative


- Observation
	- Bit that determine Cl identical in virtual and physical address
	- Can index into cache while address translation taking place
	- Generally we hit in TLB, so PPN bits (CT bits) available next
	- 'Virtually indexed, physically tagged"
	- Cache carefully sized to make this possible
	- From book: Aside Optimizing address translation
- [51:30](https://www.youtube.com/watch?v=lu1B1faqpUw#t=51:30.11) 
-  Memory Mapping
	- VM areas initialized by associating them with disk objects.
		- Process is known as memory mapping
		- Every are and thus page within that area is associated with some portion of a file
			- Initial contents of the pages in that area come from that file
	- Area can be backed by (i.e., get its Initial values from)
		- Regular file on dis (e.g., an executable object file)
			- Initial page bytes come from a section of a file
		- Anonymous file (e.g, nothing)
			- First fault will allocate a physical page full of 0's (demand-zero page)
			- Once the page it written to (dirtied), it is like any other page
	- Dirty pages are copied back and forth between memory and a special swap file.

	- The fork Function Revisited
		- a VM and memory mapping explain how fork provides private address space for each process.
		- To create virtual address space for new child process
			- Create exact copies of current mm_struct, vm_area_struct, and page tables.
			- Fag each page in both proceses as read-only
			- Flag each vn_area_struct in both processes as private Copy On Write
		- On return, each process has exact copy of virtual memory
		- Subsequent writes create new pages using COW mechanism.
		- So it's tries to do a write the page is flagged as read-only (in the PTE), that triggers fault
			- the kernel looks at that looks up the flags for that particular page sees that it's COW, so it makes a copy of that target page and maps it to a new region of the physical address space. 
			- Fault handler returns and it restarts that instruction. And now the write is writing to the copy

- [1:05:26](https://www.youtube.com/watch?v=lu1B1faqpUw#t=1:05:26.80) 
- Execve - running a new program in a new virtual address space within the current process. So it frees all the area_struct and page tables for the current process, then it creates new area_structs and page tables for the new areas.
- The program (i think it's .text) and initialized data (.data) - those areas are backed by the file in this case the executable binary.
	- And their program is backed by the portion of the executable that contains code
	- data segment is backed by the portion of the executable file that contains the initialized data
		- These two are private - shouldn't being shared with anything else. 
		- file-backed - these portion is backed with file
- .bss - demand zero - the system initialize this to zero
- Once the loader sets the %RIP to the entry point - the first instruction in this text segment
	- Then linux will fault in all the code and data that's needed on demand
	- Therefore, the loading of the page of code or data is deferred, until that code or data page is actually referenced and accessed.
- ![[Pasted image 20251021152849.png]]

- [1:11:40](https://www.youtube.com/watch?v=lu1B1faqpUw#t=1:11:40.93) 
- ![[Pasted image 20251021154419.png]]
- *start = some pointer to virtual address space
- length = tries to map that portion of the virtual address space to the object with 'offset'
- fd = to some objects specified in this file descriptor
- prot = PROT_READ, PROT_WRITE
- flags = MAP_ANON, MAP_PRIVATE, MAP_SHARED
- return a pointer to the start of the mapped area (may not be start)
- ![[Pasted image 20251021155436.png]]
- not gets copied, it's just mapping.
- ![[Pasted image 20251021155737.png]]
- 