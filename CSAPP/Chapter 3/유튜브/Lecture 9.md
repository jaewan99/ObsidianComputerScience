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


- [43:52](https://www.youtube.com/watch?v=V6bY22KZbRc#t=43:52.42) 
- Avoid overflow vulnerabilities