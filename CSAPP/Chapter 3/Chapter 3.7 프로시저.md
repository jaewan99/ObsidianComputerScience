


Procedures provide a way to package code that implements some functionality with a designated set of arguments and an optional return value.

For discussion purposes, suppose procedure **P** calls procedure **Q**, and **Q** then executes and returns back to **P**. These actions involve one or more of the following mechanisms:

1. **Passing control.** The program counter must be set to the starting address of the code for **Q** upon entry, and then set to the instruction in **P** following the call to **Q** upon return.
    
2. **Passing data.** **P** must be able to provide one or more parameters to **Q**, and **Q** must be able to return a value back to **P**.
    
3. **Allocating and deallocating memory.** **Q** may need to allocate space for local variables when it begins and then free that storage before it returns.


### 3.7.1 The Run-Time Stack

![[Pasted image 20250921183125.png]]

When an x86-64 procedure requires storage beyond what it can hold in reg isters, it allocates space on the stack. This region is referred to as the procedure’s stack frame


.Indeed, manyfunctionsdonotevenrequireastackframe.Thisoccurswhenallofthelocal variables canbeheldinregistersandthefunctiondoesnotcallanyotherfunctions (sometimes referred to as a leaf procedure, in reference to the tree structure of procedure calls).


### 3.7.2 Control Transfer
The **call** instruction has a target indicating the address of the instruction where the called procedure starts. Like jumps, a call can be either **direct** or **indirect**.

In assembly code, the target of a direct call is given as a **label**, while the target of an indirect call is given by `*` followed by an operand specifier.

The stack pointer **%rsp** and the program counter **%rip** are the key registers involved.

The instruction **callq** is used to call other functions.
### 3.7.3 Data Transfer
![[Pasted image 20250921185640.png]]

When a function has more than six integral arguments, the other ones are passed on the stack.

Then the code for **P** must allocate a stack frame with enough storage for arguments 7 through _n_.

When passing parameters on the stack, all data sizes are rounded up to be multiples of eight.

Procedure **Q** can access its arguments via registers and possibly from the stack.


![[Pasted image 20250921190746.png]]


### 3.7.4 Local Storage on the stack

There are not enough registers to hold all of the local data.

The address operator **‘&’** is applied to a local variable, and hence we must be able to generate an address for it.

Some of the local variables are arrays or structures and hence must be accessed by array or structure references.


![[Pasted image 20250921213846.png]]
![[Pasted image 20250921213855.png]]


### 3.7.5 Local Storage in Registers

When one procedure (the caller) calls another (the callee), the callee does not overwrite some register value that the caller planned to use later.

Registers **%rbx**, **%rbp**, and **%r12–%r15** are classified as _callee-saved registers_.

When procedure **P** calls procedure **Q**, **Q** must preserve the values of these registers, ensuring that they have the same values when **Q** returns to **P** as they did when **Q** was called.

Registers **%rbx**, **%rbp**, and **%r12–%r15** are classified as _callee-saved registers_. When procedure **P** calls procedure **Q**, **Q** must preserve the values of these registers, ensuring that they have the same values when **Q** returns to **P** as they did when **Q** was called.

All other registers, except for the stack pointer **%rsp**, are classified as _caller-saved registers_. This means that they can be modified by any function. The name “caller-saved” can be understood in the context of a procedure **P** having some local data in such a register and calling procedure **Q**.

### 3.7.6 Recursive Procedure

The conventions we have described for using the registers and the stack allow **x86-64 procedures** to call themselves recursively.