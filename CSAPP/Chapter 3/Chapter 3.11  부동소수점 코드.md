![[Pasted image 20250922143458.png]]

Each YMM register is 256 bits (32 bytes) long. When operating on scalar data, these registers only hold floating-point data, and only the low-order 32 bits (for float) or 64 bits (for double) are used.


### 3.11.1 Floating-Point Movement and Conversion Operations

![[Pasted image 20250922144104.png]]

Those that reference memory are scalar instructions, meaning that they operate on individual, rather than packed, data values. The data are held either in memory (indicated in the table as M32 and M64) or in XMM registers (shown in the table as X).
### 3.11.2 Floating-Point Code in Procedures
![[Pasted image 20250922144408.png]]

안 읽음
### 3.11.3 Floating-Point Arithmetic Operations

### 3.11.4 Defining and Using Floating-point constants

### 3.11.5 Using Bitwise Operations in Floating-Point Code

### 3.11.6 Floating-Point Comparison Operations

### 3.11.7 Observation about Floating-Point Code

We see that the general style of machine code generated for operating on floating-point data with AVX2 is similar to what we have seen for operating on integer data. Both use a collection of registers to hold and operate on values, and they use these registers for passing function arguments.

