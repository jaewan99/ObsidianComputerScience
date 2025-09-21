The signed division instruction `idiv` takes as its dividend the 128-bit quantity in registers `%rdx` (high-order 64 bits) and `%rax` (low-order 64 bits). The divisor is given as the instruction operand. The instruction stores the quotient in register `%rax` and the remainder in register `%rdx`.

The execution order of a set of machine code instructions can be altered with a jump instruction, indicating that control should pass to some other part of the program, possibly contingent on the result of some test.

### 3.6.1 Condition Codes
the CPU maintains a set of single-bit condition code registers describing attributes of the most recent arithmetic or logical oper ation

CF: Carry flag. The most recent operation generated a carry out of the most significant bit. Used to detect overflow for unsigned operations. 

ZF: Zero flag. The most recent operation yielded zero. 

SF: Sign flag. The most recent operation yielded a negative value.

OF: Overflow flag. The most recent operation caused a two’s-complement overflow—either negative or positive

![[Pasted image 20250920201552.png]]
### 3.6.2 Accessing the condition codes
![[Pasted image 20250920203959.png]]

### 3.6.3 Jump Instructions
![[Pasted image 20250920204144.png]]In generating the object-code file, the assembler determines the addresses of all labeled instructions and encodes the jump targets.
![[Pasted image 20250920204448.png]]

### 3.6.4 Jump Instruction Encodings



### 3.6.5 Implementing Conditional Branches with Conditional Control


Usinggotostatementsisgenerallyconsideredabadprogramming style,sincetheirusecanmakecodeverydifficulttoreadanddebug.


### 3.6.6 Implementing Conditional Branches with Conditional Moves

processors achieve high performance through pipelining, where an instruc tion is processed via a sequence of stages, each performing one small portion of the required operations (e.g., fetching the instruction from memory, determining the instruction type, reading from memory, performing an arithmetic operation, writing to memory, and updating the program counter).

