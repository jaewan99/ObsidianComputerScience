![[Pasted image 20250920192908.png]]

### 3.5.1 Load Effective Address

Its first operand appears to be a memory reference, but instead of reading from the designated location, the instruction copies the effective address to the destination.

### 3.5.2 Unary and Binary Operations
unary operations, with the single operand serving as both source and destination


binary operations, where the second operand is used as both a source and a destination

![[Pasted image 20250920192619.png]]

### 3.5.3 Shift operations

![[Pasted image 20250920192811.png]]

### 3.5.4 Discussion

Only right shifting requires instructions that differentiate between signed versus unsigned data.
### 3.5.5 Special Arithmetic Operations

For both of these instructions, one argument must be in register %rax, and the other is given as the instruction source operand. The product is then stored in registers %rdx (high-order 64 bits) and %rax (low-order 64 bits).


