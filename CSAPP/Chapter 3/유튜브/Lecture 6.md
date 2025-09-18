https://www.youtube.com/watch?v=LqSN8OOdLQw&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=6

### Lecture 06 Machine Level Programming II Controls

Is register part of memory - No,  // part of cache? - No


- [05:39](https://www.youtube.com/watch?v=LqSN8OOdLQw#t=05:39.02) 
![[Pasted image 20250918200314.png]]
- Condition Codes (Implicit settings) - there are actually 8 condition codes
	- CF - Carry Flag (for unsigned) - carry bit 
	- SF - Sign Flag (for signed) - sets the negative value
	- ZF -Zero Flag - Set if the value is zero
	- OF-Overflow Flag (for signed) - Two's complement version of overflow
		- Positive and Negative Overflow
	- Most of the time these flags are ignored

- Condition Codes (Explicit settings)
	- cmpq b,a like computing a-b without setting destination
	- ex. ZF set if a=b
	- testq b,a like computing a&b without setting destination
- 
- [11:34](https://www.youtube.com/watch?v=LqSN8OOdLQw#t=11:34.79) 
- How to read the condition codes
	- read and set 1 bit flag based on the result in the a read some other register
	- OR try conditional branch
		- SetX instruction
			- sets a single byte of a single register to either 1 or 0
			- based on the most recent instruction before hand
- We can directly set the lowest order byte of it to either 0 or 1 - and doesn't affect any of the other 7 bytes of the register (%cl) "L" - means low


- [21:21](https://www.youtube.com/watch?v=LqSN8OOdLQw#t=21:21.58) 
- Jumping / Jump Instructions
- conditional and unconditional jump


- [26:59](https://www.youtube.com/watch?v=LqSN8OOdLQw#t=26:59.85)  
- Goto Code // conditional code
- if, then statement
- 

- [35:29](https://www.youtube.com/watch?v=LqSN8OOdLQw#t=35:29.65) 
- gcc -Og -S -fno-if-conversion control.c
- Bad cases for conditional move
	- expensive computations
		- val = Test(x) ? Hard1(x) : Hard(x);
			- both values get computed
			- only makes sense when computations are very simple
	- Risky Computations
		- val = p ? (pointer) P : 0 ;
		- May have undesirable effects
	- Computations with side effects
		- val = x > 0 ? x = x times 7 : x = x + 3
		- Both values get computed
		- Must be side-effect free


- [38:35](https://www.youtube.com/watch?v=LqSN8OOdLQw#t=38:35.11) 
- Do-While loop example
-  