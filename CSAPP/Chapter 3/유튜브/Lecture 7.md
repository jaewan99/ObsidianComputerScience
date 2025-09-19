https://www.youtube.com/watch?v=A2JFx93ANHs&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=7

Function, procedure or a method - they are roughly the same thing

Combination of the actual x86 hardware and how it supports it, but also in some ways more importantly a set of conventions that were developed that basically everyone agreed to and it's known as an ABI (Application Binary Interface)


- [04:30](https://www.youtube.com/watch?v=A2JFx93ANHs#t=04:30.48) 
Mechanism in procedures
 - passing control
	 - to beginning of procedure code
	 - back to return point
 - Passing data
	 - procedure arguments
	 - return value
 - memory management
	 - allocate during procedure execution
	 - deallocate upon return
 - Mechanisms all implemented with machine instructions


- [07:26](https://www.youtube.com/watch?v=A2JFx93ANHs#t=07:26.35) 
- x86-64 stack
- stack - is not a region of special memory, it's a region of normal memory
- stack is where it passes all these potential information, the control information, data and allocate local data.
- Why stack? - because of the nature of the whole idea of procedure calls and return. 
	- call - need some information
	- return from a call - all that information is discard
- [09:16](https://www.youtube.com/watch?v=A2JFx93ANHs#t=09:16.72) 
	- x86-64 stack starts with a very high numbered address, and when they grow when more data are allocated for the stack. It's done by decrementing the stack pointer
- [10:42](https://www.youtube.com/watch?v=A2JFx93ANHs#t=10:42.01) 
	- pushq Src
		- fetch operand at Src
		- Decrement %rsp(pointer stack) by 8
			- decrement before you write, because when you first started out, the stack pointer is pointing to whatever was the top element of the stack. We wanna create a new top element so we're going to decrement first and then do the write
		- Write operand at address give by %rsp
	- popq Dest
		- read value at adress given by %rsp
		- increment %rsp by 8
			- sort of deallocating the stack
				- just moving the stack pointer - whatever it was there at the top of the stack is still in memory but it's not just considered a part of the stack
		- store value at Dest (must be register)



- [15:37](https://www.youtube.com/watch?v=A2JFx93ANHs#t=15:37.06) 
- Control flow example 1


- [20:36](https://www.youtube.com/watch?v=A2JFx93ANHs#t=20:36.11) 
- Procedure data flow
	- 