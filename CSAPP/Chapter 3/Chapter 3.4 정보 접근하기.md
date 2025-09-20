

Those that generate 1 or 2-byte quantities leave the remaining bytes unchanged. Those that generate 4 byte quantities set the upper 4 bytes of the register to zero.

Most unique among them is the stack pointer, %rsp, used to indicate the end position in the run-time stack.

![[Pasted image 20250920164225.png]]
### 3.4.1 Operand Specifiers
Most instructions have one or more operands, specifying the source values to use in performing an operation and the destination location into which to place the result.

page 209 (pdf) for operand forms

Source values can be given as constants or read from registers or memory.

The first type, **immediate**, is for constant values.  
In AT&T format assembly code, these are written with a `$` followed by an integer using standard C notation — for example, `$-577` or `$0x1F`.

The second type, **register**, denotes the contents of a register, one of the sixteen 8-, 4-, 2-, or 1-byte low-order portions of the registers for operands having 64, 32, 16, or 8 bits, respectively.
**Memory reference**, in which we access some memory location according to a computed address, often called the **effective address**.

### 3.4.2 Data Movement Instructions

movb, movw, movl, and movq. All four of these instructions have similar effects; they differ primarily in that they operate on data of different sizes: 1, 2, 4, and 8 bytes, respectively


![[Pasted image 20250920171228.png]]

![[Pasted image 20250920171624.png]]

The only exception is that when `movl` has a register as the destination, it will also set the high-order 4 bytes of the register to 0.


![[Pasted image 20250920171956.png]]

![[Pasted image 20250920174831.png]]
![[Pasted image 20250920174847.png]]
### 3.4.3 Data Movement Example
![[Pasted image 20250920181145.png]]


- **`%rax`** → the **value stored in the RAX register** (just a number, no memory access).
    
- **`(%rax)`** → the **memory contents at the address held in RAX** (dereferences the pointer).
    
- **`0x1232`** → either an **immediate value** (if `$0x1232`) or a **memory address** (if used without `$`), depending on context.

### 3.4.4 Pushing and Popping Stack Data
pushq %rbp is equivalent to that of the pair of instructions

![[Pasted image 20250920185124.png]]

popq %rax is equivalent to the following pair of instructions:

![[Pasted image 20250920185148.png]]

The value `0x123` remains at memory location `0x104` until it is overwritten (e.g., by another push operation).


