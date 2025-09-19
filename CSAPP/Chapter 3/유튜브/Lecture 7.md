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
	- 