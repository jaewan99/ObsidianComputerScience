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
	- 