![[Pasted image 20250922143458.png]]

EachYMMregister is256bits(32bytes) long.Whenoperatingonscalardata, theseregistersonly holdfloating-pointdata,andonlythelow-order32bits(forfloat)or64bits(for double)areused.


### 3.11.1 Floating-Point Movement and Conversion Operations

![[Pasted image 20250922144104.png]]

Those that reference memory are scalar instructions, meaning that they operate on individual, rather than packed, data values. The data are heldeitherinmemory(indicatedinthetableasM32 andM64)orinXMMregisters (shown in the table as X).
### 3.11.2 Floating-Point Code in Procedures
![[Pasted image 20250922144408.png]]

안 읽음
### 3.11.3 Floating-Point Arithmetic Operations

### 3.11.4 Defining and Using Floating-point constants

### 3.11.5 Using Bitwise Operations in Floating-Point Code

### 3.11.6 Floating-Point Comparison Operations

### 3.11.7 Observation about Floating-Point Code

Weseethatthegeneralstyleofmachinecodegeneratedforoperatingonfloating pointdatawithAVX2issimilartowhatwehaveseenforoperatingonintegerdata. Bothuseacollectionofregisterstoholdandoperateonvalues,andtheyusethese registersforpassingfunctionarguments.

