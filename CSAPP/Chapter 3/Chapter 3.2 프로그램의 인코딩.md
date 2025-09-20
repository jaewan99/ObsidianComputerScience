
![[Pasted image 20250920153638.png]]
gcc compiler을 이용한 c 코드 인코딩
-Og
- O - optimization
- debug - g
- O1 - higer level of optimization
- O2 
- Invoking higher levels of optimizationcangeneratecodethatissoheavilytransformedthattherelationship between the generated machine code and the original source code is difficult to understand


### 3.2.1 Machine-level code
Two different forms of abstraction.
First, the format and behavior of a machine-level program is defined by the instruction set architecture, or ISA, defining the processor state, the format of the instructions, and the effect each of these instructions will have on the state.
Second, thememoryaddressesused byamachine-level programarevirtual addresses.


Parts of the processor state are visible that normally are hidden from the C programmer:
- program counter
- register file
- condition code
- a set of vector registers (to hold one more integer, float)

### 3.2.2 Code Examples
