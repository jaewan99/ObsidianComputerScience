
## About compatibility of the data types

- Example: network protocols often specify that a field must be exactly 32 bits or 16 bits.
    
- If your program uses a `long` that is 4 bytes on one machine and 8 bytes on another, the data sent/received will be misinterpreted.
	- long
		- 예. 32 bit linux에서는 4 bytes
		- 64 bit linux에서는 8 바이트
		- 64 bit windows에서는 4바이트
- 그래서 우리는 intN_t나 unitN를 이용해서 한다.