
## About compatibility of the data types

- Example: network protocols often specify that a field must be exactly 32 bits or 16 bits.
    
- If your program uses a `long` that is 4 bytes on one machine and 8 bytes on another, the data sent/received will be misinterpreted.
	- long
		- 예. 32 bit linux에서는 4 bytes
		- 64 bit linux에서는 8 바이트
		- 64 bit windows에서는 4바이트
- 그래서 우리는 intN_t나 unitN를 이용해서 한다.



## INT_MIN as (-INT_ MAX -1)

- For 32-bit `int`, the **maximum value is 2,147,483,647** (`INT_MAX`).
	- So the literal `2147483648` **does not fit in a 32-bit `int`
    
- int x = -2147483648;
	- 이걸 c가 해석 방법은
		- int x= 2147483648
			- 숫자를 먼저 처리해서 
	- `2147483648` is treated as an **unsigned int literal** because it doesn’t fit in a signed 32-bit int