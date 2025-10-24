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



https://www.youtube.com/watch?v=FblqVNY5N58&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=19

Dynamic memory allocation
Programmers use dynamic memory allocators (such as malloc) to acquire VM at run time.
- For data structures whose size is only known at runtime.
Dynamic memory allocators manage an area of process virtual memory known as the heap.

Allocator maintains heap as collection of variable sized blocks, which are either allocated or free
- Allocated means that they're being used by some program / application
- Free meaning that there available to be used by an application

Allocator maintains heap as collection of variable sized blocks, which are either allocated or free.
Types of allocators
- Explicit allocator: application allocates and frees space
	- E.g., malloc and free in C
	- The system wont free up any memory that you allocate unless you do it.
- Implicit allocator: application allocates, but does not free space
	- E.g. garbage collection in Java, ML, and Lisp
	- The system takes care of freeing the memory
		- The burden of freeing the memory is shifted from the application program to the system.
		- It frees this memory implicitly sort of behind the scenes using the process called garbage collection


- [03:30](https://www.youtube.com/watch?v=FblqVNY5N58#t=03:30.93) 
- The malloc Package
- #include <stdlib.h>
- void *malloc(size_t size)
	- The function is used to allocate memory and it takes as input size argument which is in bytes and then it returns a pointer to a memory block that contains at least the input size bytes.
	- Successful:
		- Returns a pointer to a memory block of at least size bytes aligned to an 8-byte (x86) or 16-byte (x86-64) boundary
	- Unsuccessful: returns NULL (0) and sets errno
- void free (void *p)
	- Returns the block pointed at by p to pool of available memory
	- p must come from a previous call to malloc or realloc
- Other functions
	- calloc: Version of malloc that initializes allocated block to zero
	- realloc: changes the size of a previously allocated block.
	- sbrk: Used internally by allocators to grow or shrink the heap
		- when allocator needs more memory, it calls sbrk to get that additional virtual memory


- [05:44](https://www.youtube.com/watch?v=FblqVNY5N58#t=05:44.82) 
- ![[Pasted image 20251024160958.png]]


- [07:29](https://www.youtube.com/watch?v=FblqVNY5N58#t=07:29.51) 
- Assumptions Made in This Lecture
	- Memory is word addressed (each word can hold a pointer) - but actually, it's byte address. And words are 4 bytes 
- And blocks are contiguous chunks of those words that can be either allocated or free. 
- (1) So here we have a portion of the heap, which consists of a 4 word allocated block followed by a 2 words free block.
- ![[Pasted image 20251024161412.png]]


- ![[Pasted image 20251024161657.png]]
- The allocator looks to see if it can find a free block that has enough room and it finds this free block free that has 5 free words and then it allocates the requested block inside that free block


- [10:11](https://www.youtube.com/watch?v=FblqVNY5N58#t=10:11.65) 
- Constraints
	- Applications
		- Can issue arbitrary sequence of malloc and free requests
		- free request must be to a malloc'd block
	- Allocators
		- Can't control number or size of allocated blocks
		- Must respond immediately to malloc requests
			- i.e., can't reorder or buffer requests
		- Must allocate blocks from free memory
			- i.e., can only place allocated blocks in free memory
		- Must align blocks so they satisfy all alignment requirements
			- 8-byte (x86) or 16-byte (x86-64) alignment on Linux boxes
		- Can manipulate and modify only free memory
		- Can't move the allocated blocks once they are malloc'd
			- i.e., compaction is not allowed


- [12:35](https://www.youtube.com/watch?v=FblqVNY5N58#t=12:35.02) 
- Performance Goal: Throughput
	- Given some sequence of malloc and free requests:
		- Ro Ry. ... , Rw ... , R(n-1)
	- Goals: maximize throughput and peak memory utilization
		- These goals are often conflicting
	- Throughput:
		- Number of completed requests per unit time
			- Example:
				- 5,000 malloc calls and 5,000 free calls in 10 seconds
				- Throughput is 1,000 operations/second
	- Measuring how efficiently are malloc can process these requests from an application.
- Performance Goal: Peak Memory Utilization
	- Measuring how efficiently the allocator uses the heap
		- How much is wasted on sort of overheads in the data structure that the allocator has to uses to in its implementation
	- Given some sequence of malloc and free requests:
		- Ro Ry ... , Rw ... , Rn.1
	
		- Def: Aggregate payload Pk
			- malloc (p) results in a block with a payload of p bytes
			- After request Rk has completed, the aggregate payload Pk is the sum of currently allocated payloads
			- When application makes a call to malloc it's requesting a certain size block. And that block is called payload. So if we call malloc with an argument of 10 bytes. We're requesting a block that has a payload that's at least size 10.
			- And the 10 bytes that we request that are called the payload.
			- Everything else in that block is overhead.
			- The perfect allocator - the aggregate payload would equal the amount of memory - to total size of all the allocated blocks because there would be no overhead
				- Every block would be pure payload.
		
		- Def: Current heap size Hk
			- Assume Hk is monotonically nondecreasing
				- i.e., heap only grows when allocator uses sbrk
			- but not true in a real malloc package.
			
		- Def: Peak memory utilization after k+1 requests
			-![[Pasted image 20251024164200.png]]
			- sum of all the payloads divided by the total size of the heap
			- The best case - each block consist of pure payload - so the utilization would be 1
			- But in practice, each block the allocator is going to place data structures and padding inside of each block - that keep it from getting a perfect utilization.
			- One obvious thing is that since block have to be aligned. To some you know if they're 16-byte aligned then blocks have to start on 16 byte boundaries, and have to be at least 16-bytes.
				- So if you were to request a payload of 2 bytes. You'd have a lot of wasted bytes right that would sort of decrease the utilization.


- [17:21](https://www.youtube.com/watch?v=FblqVNY5N58#t=17:21.77) 
- Fragmentation - 단편화
- Poor memory utilization caused by fragmentation
	- internal fragmentation
	- external fragmentation
- Internal fragmentation
	- For a given block, internal fragmentation occurs if payload is smaller than block size
	- ![[Pasted image 20251024165232.png]]
	- Caused by
		- This can be caused by either padding in the block or some kind of data structure in the block that the allocator needs.
		- Overhead of maintaining heap data structures
		- Padding for alignment purposes
		- Explicit policy decisions (e.g., to return a big block to satisfy a small request)
	- Depends only on the pattern of previous requests
		- Thus, easy to measure
		- At any point in time, we can just look at all the previous requests that we've made. And look at the size of the payload for each one of those request, so we can determine the level of internal fragmentation just by looking at the previous request.
- External fragmentation
	- Occurs when there is enough aggregate heap memory, but no single free block is large enough
		- When the application makes a request for a block but nowhere in the heap is a free block that's large enough to satisfy that request.
	- ![[Pasted image 20251024165923.png]]
	- The total number of free words in our heap is 7 words. And now we get a request for 6 words.
		- The allocator has to go and get more virtual memory and extend the heap out this way to get a large enough free block.
	- Depends on the pattern of the future request.
		-  Thus, difficult to measure.


- [21:44](https://www.youtube.com/watch?v=FblqVNY5N58#t=21:44.44) 
- Implementation Issues
	- How do we know how much memory to free given just a pointer?
	- How do we keep track of the free blocks?
	- What do we do with the extra space when allocating a structure that is smaller than the free block it is placed in?
	- How do we pick a block to use for allocation -- many might fit?
	- How do we reinsert freed block?


- [23:16](https://www.youtube.com/watch?v=FblqVNY5N58#t=23:16.26) 
- Knowing How much to free
	- Standard method
		- Keep the length of a block in the word preceding the block.
			- This word is often called the header field or header
		- requires an extra word for every allocated block
	- **![[Pasted image 20251024171537.png]]
	- If application malloc a payload of size 4, then the allocator needs to find a block of size 5.
		- Consisting of at least 4 payload words, and then a header block, a header word at the beginning that indicates the total size of that block. and it returns to the pointer p0 in this case to the beginning of the payload.

- [24:27](https://www.youtube.com/watch?v=FblqVNY5N58#t=24:27.24) 
- Keeping Track of Free Blocks
- ![[Pasted image 20251024172607.png]]
- since we know the size of the block which means that we know the start of the next block
- There's no list of free blocks - but we can traverse that all of the free block in the heap by traversing all of the blocks in the heap and just ignoring the allocated blocks.

- ![[Pasted image 20251024172748.png]]
- We could actually some of the words in the block to create a linked list of some kind either singly or doubly linked list.
	- So here we visit the first free block and then there's a pointer to the next free block and so on.
	- This might be little more efficient because if we want to 