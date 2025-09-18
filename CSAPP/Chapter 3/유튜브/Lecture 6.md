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
	- read and set 1 bit flag based on the result in the a read so