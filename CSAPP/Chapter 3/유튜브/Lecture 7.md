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
- ![[Pasted image 20250919112910.png]]
- Procedure data flow
	- This is all for arguments that are either integers or pointers (data)
	- What happens if you have more than 6 arguments to a function
		- rule on this is that those get put in memory on the stack - pass to a function and then the function has to retrieve those values off the stack 
- function in multstore has three argument
	- in this code - we can see we are using %rdi, %rsi and dest in %rbx
	- but in mult2 function - we also use %rdi, %rsi
		- the code is generated under the assumption that whatever arguments is being passed to it will be passed in that particular set of registers in the the particular order they're listed

- [26:02](https://www.youtube.com/watch?v=A2JFx93ANHs#t=26:02.06) 
- Managing local data
	- stack frame
		- particular allocation pattern that's used in memory and as I mentioned earlier. one of the feature of calling and returning is you can imagine when you have a nested series of calls to a function. 
		- When a particular function is executing, it only needs to reference the data within that function or values that have passed to it. So rest of the functions are sort of frozen.
		- Stack frame - it's a frame for a particular instance of a procedure and a particular call to a procedure. 
		- Contents
			- Return information
			- Local Storage (if needed)
			- Temporary space (if needed)
		- Management
			- Space allocated when enter procedure
				- "set-up" code
				- Includes push by call instruction
			- Deallocated when return
				- "Finish" code
				- includes pop by ret function

- [31:06](https://www.youtube.com/watch?v=A2JFx93ANHs#t=31:06.74) 
- Example of the stack frame


- [34:46](https://www.youtube.com/watch?v=A2JFx93ANHs#t=34:46.64) 
- x86-64 / linux stack frame
	- Caller Frame - if we have pass more than 6 arguments
		- Caller will actually use its own stack frame to store those arguments
		- When we do a call, it will push the return address onto the stack
	- Saved Registers
		- Some registers need to be saved and we'll see examples of that
		- Or an array that needs to be allocated locally

- [36:41](https://www.youtube.com/watch?v=A2JFx93ANHs#t=36:41.39) 
- so by default - %rsi == val
- but in line long y = x + val // %rsi == y (since it's val + x)