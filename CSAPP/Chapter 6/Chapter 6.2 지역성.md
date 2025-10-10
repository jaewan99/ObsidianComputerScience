https://www.youtube.com/watch?v=FDBqMES--TY&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=11

- [44:16](https://www.youtube.com/watch?v=FDBqMES--TY#t=44:16.77) 
- Principle Locality 
	- the programs tend to use data and instructions whose addresses are near or equal to those that they have used recently
- Temporal locality:
	- Recently referenced items are likely to be referenced again in the near future
- Spatial locality
	- Items with nearby addresses tend to be referenced close together in time 
- Good locality = Good performance

book

### 6.2 Locality

At the hardware level, the principle of locality allows computer designers to speed upmainmemoryaccesses by introducing small fast memories known as cache memories that hold blocks of the most recently referenced instructions and data items. At the operating system level, the principle of locality allows the system tousethemainmemoryasacache of the most recently referenced chunks of the virtual address space. Similarly, the operatingsystemusesmainmemorytocachethemostrecentlyuseddiskblocksin the disk file system

### 6.2.1 Locality of References to Program Data

Sincethefunctionhaseithergoodspatialortemporal localitywithrespecttoeachvariableintheloopbody,wecanconcludethatthe sumvecfunctionenjoysgoodlocality

Stride-1referencepatternsareacommonandimportantsource ofspatiallocalityinprograms.Ingeneral,asthestrideincreases,thespatiallocality decreases.


### 6.2.2 Locality of Instruction Fetches

Sinceprograminstructionsarestoredinmemoryandmustbefetched(read) bytheCPU,wecanalsoevaluatethelocalityofaprogramwithrespect toits instructionfetches.
- . Instruction references
. Reference instructions in sequence. - Spatial locality
. Cycle through loop repeatedly. - temporal locality