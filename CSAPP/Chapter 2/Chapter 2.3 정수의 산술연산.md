Integer Arithmetic

### 2.3.1. Unsigned Addition
워드 크기 증가   “Word size inflation” means we cannot place any bound on the word size required to fully represent the results of arithmetic operations.

![[Pasted image 20250914195352.png]]

For example, consider a 4-bit number representation with x = 9 and y = 12, having bit representations [1001] and [1100], respectively. Their sum is 21, having a 5-bit representation [10101]. But if we discard the high-order bit, we get [0101], that is, decimal value 5. This matches the value 21mod 16 = 5.

![[Pasted image 20250912164255.png]]


When executing C programs, overflows are not signaled as errors. At times, however, we might wish to determine whether or not overflow has occurred.

### 2.3.2 two's complement addition
![[Pasted image 20250912172155.png]]


![[Pasted image 20250912172605.png]]


### 2.3.3 2의 보수에서의 비트반전 (negation)

![[Pasted image 20250912173508.png]]

That is, for w-bit two’s-complement addition, TMinw is its own additive in verse, while any other value x has −x as its additive inverse. Since TMinw doesn't have its own additive in the given data type.

### 2.3.4 unsigned multiplication

![[Pasted image 20250914201011.png]]
![[Pasted image 20250914201100.png]] 

Overflow is not generating random, they have patterns to be interpreted.

2.3.5 two's complement multiplication


2.3.6 Multiplying by constants

So, for example, 11 can be represented for w = 4 as [1011]. Shifting this left by k =2 yields the 6-bit vector [101100], which encodes the unsigned number 11. 4 =44.


14 = 23 + 22 +21, the compiler can rewrite the multiplication as (x<<3) + (x<<2) + (x<<1)

Even better, the compiler can also use the property 14 = 24 − 21 to rewrite the multiplication as (x<<4)- (x<<1), requiring only two shifts and a subtraction.


https://pages.cs.wisc.edu/~markhill/cs354/Fall2008/beyond354/int.mult.html

2.3.7


 %%