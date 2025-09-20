Thesigneddivisioninstructionidivltakesas itsdividendthe128-bitquantity inregisters%rdx(high-order64bits)and%rax(low-order64bits).Thedivisoris givenastheinstructionoperand.Theinstructionstoresthequotient inregister %raxandtheremainderinregister%rdx.

The execution order of a set of machine code instructions can be altered with a jump instruction, indicating that control should pass to some other part of the program, possibly contingent on the result of some test.

### 3.6.1 Condition Codes
the CPU maintains a set of single-bit condition code registers describing attributes of the most recent arithmetic or logical oper ation

CF: Carry flag. The most recent operation generated a carry out of the most significant bit. Used to detect overflow for unsigned operations. 

ZF: Zero flag. The most recent operation yielded zero. 

SF: Sign flag. The most recent operation yielded a negative value.

OF: Overflow flag. The most recent operation caused a two’s-complement overflow—either negative or positive

![[Pasted image 20250920201552.png]]
### 3.6.2 Accessing the condition codes
