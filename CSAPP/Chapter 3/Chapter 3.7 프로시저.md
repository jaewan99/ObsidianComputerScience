



Procedures provideawaytopackagecode that implementssomefunctionalitywithadesignatedsetofargumentsandan optionalreturnvalue


For discussion purposes, suppose proce dure Pcalls procedure Q, and Q then executes and returns back to P. These actions involve one or more of the following mechanisms: 

Passing control. The program counter must be set to the starting address of the code for Q upon entry and then set to the instruction in P following the call to Q upon return. 

Passingdata. PmustbeabletoprovideoneormoreparameterstoQ,andQmust be able to return a value back to P. 

Allocating and deallocating memory. Q may need to allocate space for local variables when it begins and then free that storage before it returns.


### 3.7.1 The Run-Time Stack
When an x86-64 procedure requires storage beyond what it can hold in reg isters, it allocates space on the stack. This region is referred to as the procedure’s stack frame