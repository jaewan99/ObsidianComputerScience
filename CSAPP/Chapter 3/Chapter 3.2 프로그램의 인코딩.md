
![[Pasted image 20250920153638.png]]
gcc compiler을 이용한 c 코드 인코딩
-Og
- O - optimization
- debug - g
- O1 - higer level of optimization
- O2 
- Invoking higher levels of optimization can generate code that is so heavily transformed that the relationship between the generated machine code and the original source code is difficult to understand.


### 3.2.1 Machine-level code
Two different forms of abstraction.

First, the format and behavior of a machine-level program is defined by the instruction set architecture, or ISA, defining the processor state, the format of the instructions, and the effect each of these instructions will have on the state.

Second, the memory addresses used by a machine-level program are virtual addresses.

Parts of the processor state are visible that normally are hidden from the C programmer:
- program counter
- register file
- condition code
- a set of vector registers (to hold one more integer, float)

### 3.2.2 Code Examples
All information about local variable names or data types has been stripped away in the assembly code.

Embedded within the 1,368 bytes of the file `mstore.o` is a 14-byte sequence with the hexadecimal representation.

- **Machine instructions** (your actual code).
- **Symbol table**
	- Keeps track of function names, global variables, and where they will be in memory.
- **Relocation information**
	- like printf
- **Section headers and metadata**


Several features about machine code and its disassembled representation are worth noting:
- x86-64 instructions can range in length from 1 to 15 bytes.
- There is a unique decoding of the bytes into machine instructions.

The things are done in linker
- The linker has shifted the location of this code to a different range of addresses.
- One task for the linker is to match function calls with the locations of the executable code for those functions.
- Growth of the code for the function to 16 bytes enables a better placement of the next block of code in terms of memory system performance.



### 3.2.3 Notes of formatting
`.` are directives to guide the assembler and linker. We can generally ignore these.