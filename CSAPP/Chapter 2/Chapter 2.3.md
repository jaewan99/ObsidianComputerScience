Integer Arithmetic

2.3.1. Unsigned Addition
워드 크기 증가   “Word size inflation” means we cannot place any bound on the word size required to fully represent the results of arithmetic operations.


For example, consider a 4-bit number representation with x = 9 and y = 12, having bit representations [1001] and [1100], respectively. Their sum is 21, having a 5-bit representation [10101]. But if we discard the high-order bit, we get [0101], that is, decimal value 5. This matches the value 21mod 16 = 5.

![[Pasted image 20250912164255.png]]

> When executing C programs, overflows are not signaled as errors. At times, however, we might wish to determine whether or not overflow has occurred.


2.3.2 two's complement addition
