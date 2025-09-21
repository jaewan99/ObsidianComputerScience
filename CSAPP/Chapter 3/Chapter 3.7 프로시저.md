



Procedures provideawaytopackagecode that implementssomefunctionalitywithadesignatedsetofargumentsandan optionalreturnvalue


For discussion purposes, suppose proce dure Pcalls procedure Q, and Q then executes and returns back to P. These actions involve one or more of the following mechanisms: 

Passing control. The program counter must be set to the starting address of the code for Q upon entry and then set to the instruction in P following the call to Q upon return. 

Passingdata. PmustbeabletoprovideoneormoreparameterstoQ,andQmust be able to return a value back to P. 

Allocating and deallocating memory. Q may need to allocate space for local variables when it begins and then free that storage before it returns.


### 3.7.1 The Run-Time Stack

![[Pasted image 20250921183125.png]]

When an x86-64 procedure requires storage beyond what it can hold in reg isters, it allocates space on the stack. This region is referred to as the procedure’s stack frame


.Indeed, manyfunctionsdonotevenrequireastackframe.Thisoccurswhenallofthelocal variables canbeheldinregistersandthefunctiondoesnotcallanyotherfunctions (sometimes referred to as a leaf procedure, in reference to the tree structure of procedure calls).


### 3.7.2 Control Transfer
call instruction has a target indicating the address of the instruction wherethecalledprocedurestarts.Likejumps,acallcanbeeitherdirectorindirect. In assembly code, the target of a direct call is given as a label, while the target of an indirect call is given by ‘*’ followed by an operand specifier


stackpointer%rspandtheprogramcounter%rip

callq is the instruction to call other functions
### 3.7.3 Data Transfer
![[Pasted image 20250921185640.png]]Whenafunctionhasmorethansixintegralarguments, theotheronesare passedonthestack


ThenthecodeforPmustallocateastackframewith enoughstorageforarguments7throughn,


Whenpassingparameters onthestack, alldatasizesareroundeduptobemultiplesofeight


ProcedureQcanaccess itsargumentsviaregistersand possiblyfromthestack.


![[Pasted image 20250921190746.png]]


### 3.7.4 Local Storage on the stack

Therearenotenoughregisterstoholdallofthelocaldata.

Theaddressoperator‘&’isappliedtoalocalvariable,andhencewemustbe abletogenerateanaddressforit.

Someofthelocalvariablesarearraysorstructuresandhencemustbeaccessed byarrayor structurereferences.


![[Pasted image 20250921213846.png]]
![[Pasted image 20250921213855.png]]


### 3.7.5 Local Storage in Registers

noneprocedure(thecaller)callsanother(thecallee), thecalleedoes not overwrite some register value that the caller planned to use later

registers %rbx, %rbp, and %r12–%r15 are classified as callee saved registers.



When procedure P calls procedure Q, Q must preserve the values of these registers, ensuring that they have the same values when Q returns to P as theydidwhenQwascalled.
