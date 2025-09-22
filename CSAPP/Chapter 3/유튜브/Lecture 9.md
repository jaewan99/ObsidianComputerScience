https://www.youtube.com/watch?v=V6bY22KZbRc&list=PLcQU3vbfgCc9sVAiHf5761UUApjZ3ZD3x&index=9


- [02:02](https://www.youtube.com/watch?v=V6bY22KZbRc#t=02:02.02) 
- Memory is just big array of bits
- Memory Layout


- [16:30](https://www.youtube.com/watch?v=V6bY22KZbRc#t=16:30.53) 
- Buffer overflow

![[Pasted image 20250922102320.png]]

- Such problems are a big deal
	- Generally called a "buffer overflow"
		- when exceeding the memory size allocated for an array
	- Why a big deal?
		- It's the no1. technical cause of security vulnerabilities
			- no 1. overall cause is social engineering / user ignorance
	- Most common form
		- Unchecked lengths on string inputs
		- Particularly for bounded character arrays on the stack
			- sometimes referred to as stack smashing


- [29:25](https://www.youtube.com/watch?v=V6bY22KZbRc#t=29:25.33) 
- Buffer example

![[Pasted image 20250922103139.png]]

![[Pasted image 20250922103328.png]]
![[Pasted image 20250922103528.png]]


- [33:32](https://www.youtube.com/watch?v=V6bY22KZbRc#t=33:32.64) 
- Code injection Attack


![[Pasted image 20250922104705.png]]
- P calls q
	- q should return back to p
	- But now i've overwritten that return address with this buffer position
	- So what will happens is the program counter will happily jump to this spot
	- and start executing whatever it encounters which are the instructions that you've inserted
	- And by that means then you can inject code into a machine potentially somewhere else in the internet 
	- Example, i just made sure that the length of my exploit code plus the padding is 24 bytes, then right after that comes the return address


- [43:52](https://www.youtube.com/watch?v=V6bY22KZbRc#t=43:52.42) 
- Avoid overflow vulnerabilities
 ![[Pasted image 20250922105848.png]]

- fgets - has a parameter which is the maximum value of bytes that the program should read, if there's more bytes it will just truncate

![[Pasted image 20250922110119.png]]

ASLR - Address space layout randomization
- every time the program runs the addresses change a little bit or a lot
	- so that you can't reliably know where things are going to be in the code
	- before in the sort of run-up of your program when it first starts up, it will just do a allocation on the stack of some random number of bytes of storage. A fair amount like maybe a megabyte roughly of storage where the exact number is randomly chosen.  

![[Pasted image 20250922110602.png]]


![[Pasted image 20250922110740.png]]

- why the local and heap addresses change?
	- Code injection vulnerability - 