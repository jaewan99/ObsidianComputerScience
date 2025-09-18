https://www.youtube.com/watch?v=ViP6V-U4y8M&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=5

### Lecture 05 Machine Level Programming I Basics


- [01:45](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=01:45.55) 
Introduction
actual code that runs in the computer - bytes that run that the processor execute
assembly - the word form of the bytes
machine code - object code, binary code, assembly code

- [02:16](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=02:16.99) 
machine code is the intermediate form between what the program is trying to do and machine is trying to do

- [06:28](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=06:28.21) 
- Intel is complex instruction set computer

- [13:00](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=13:00.79) 
- Broadwell model
	- PCle - connection to the peripheral devices 
	- DDR - to connect to main memory
	- SATA - is connection to different types of dics
	- USB
	- Ethernet - is the connection to the network connection

- [20:03](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=20:03.72) 
- Instruction set - target of the a compiler to give you a series of instructions that tell the machine exactly what to do
- Instruction set architecture - What the target of a compiler should be and then let the hardware people figure out how best to implement it
- Microarchitecture - lower level; how it actually gets implement.
- Machine code - that incorporate both actual bytes that are operated executing as well as the assembly level version of it.


- [22:24](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=22:24.59) 
- processor
	- Some sort of program counter - what address of the next instruction that will execute next
	- Set of registers which are part of that the programmer actually make use of. Think of them as a very small number of memory locations. But rather than giving an address from 0 up to n-1 or something. You actually give them by name. 
	- Few bit worth of state that talked about what are results of some recent instructions, where they did it produce a value of 0, did it produce a negative or positive value. And those are used to implement conditional branching
- memory
	- Array of bytes
	- collaboration between the OS and the hardware - virtual memory to make it look like each program running on the processor has its own independent array of bytes that it can access even though they actually share values within the physical memory itself.
	- Cache - automatically loaded with the recent staff.  if we re-access that memory it will go faster but it's not visible in terms of there's no instructions to manipulate the cache. There's no way to directly access the cache.

- [25:02](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=25:02.77) 
- First step, take c and generate assembly code from it
- Second step, run that through assembler - which takes the text representation of instructions and turns it into the actual byte level presentation
- Third step, linker - merges together all the different files for both your individual files and their compiled version and for the library code.
- Fourth, libraries that get imported dynamically when the program first begins


- [26:28](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=26:28.36) 
- pushq - push something to a stack
- movq - move copy it from one place to another
- call - call some procedure
- popq - pop from stack
- ret - exit / return out of this particular function


- [30:18](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=30:18.38) 
- gcc -Og - S sum.c
- -S = stop
- -Og = what kind of optimization -- it's very hard to read without it
- .cft_startproc - instruction sets starting with "." they aren't actually instructions they're something else - related

