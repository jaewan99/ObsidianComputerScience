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
- .cft_startproc - instruction sets starting with "." they aren't actually instructions they're something else - related to what the information that needs to be fed to a debugger for it to be able to locate various parts of the program. Some information for the linker to tell it that this is a globally defined function. and various other things.

- [34:39](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=34:39.78) 
- Assembly code - number of different sort of integer data types


- [42:32](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=42:32.94) 
- objdump -d sum > sum.d
- object code to assembly code
- figured this out by the bytes in the actual object code file
- Another way to do it
- gdb - powerful debugging examine step through and operate on programs in.


- [47:59](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=47:59.34) 
- Registers
	- For each register "%r.." -you get 64 bits of it. "%e.." version of it you get 32 bits 
	- ex. long ints - "%r.." - if it's ints (32bits) - "%e.."
	- Now, names doesn't have nothing to do with the purpose
	- One special register - "%rsp" - stack pointer

- [53:37](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=53:37.07) 
- Moving Data 
- movq source, dest
- Operand types:
	- immediate - constant integer data
		- example, $0x400
		- Like C constant, but prefixed with "$"
		- Encoded with 1,2, or 4 bytes
	- Register - one of 16 integer registers
		- example, %rax, %r13
		- But %rsp reserved for special use
		- other have special use for particular instructions
	- Memory - 8 consecutive bytes of memory at address given by register
		- simple example (%rax)
		- various "address mode"

- [54:24](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=54:24.61) 

![[Pasted image 20250918174433.png]]
 ![[Pasted image 20250918175746.png]]


- [1:01:14](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=1:01:14.57) 
- Continuation on the understanding the Swap()
![[Pasted image 20250918180622.png]] 
- [1:06:08](https://www.youtube.com/watch?v=ViP6V-U4y8M#t=1:06:08.18) 
- Address computation example

- Address computation instruction
	- leaq Src, Dst
		- Src is address mode expression - from the memory references
		- Set Dst to address denoted by expression - it has to be register
	- Example
		- & - give me the address of some place / that designated some location
		- p = 