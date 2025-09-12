2.2 Integer representation
![[Pasted image 20250912101412.png]]

2.2.1 Integral data type

C supports a variety of integral data types — ones that represent finite ranges of integers.

long

−2,147,483,648
−9,223,372,036,854,775,808


We also see that the data type `int` could be implemented with 2-byte numbers, although this is mostly a throwback to the days of 16-bit machines. We also see that the type `long` can be implemented with 4-byte numbers, and it typically is for 32-bit programs.


2.2.2 Unsigned Encodings
![[Pasted image 20250912103612.png]]

given this image the decimal value of 1011 would be 11 and such.


principle: Uniqueness of unsigned encoding 
Function B2Uw is a bijection.

Example of bijection would be
there is only one decimal values that 0001 can map which is 1 and also for reverse, where 1 can only map to 0001 to binary


2.2.3 two's compliment encodings
![[Pasted image 20250912104207.png]]
principle: Uniqueness of two’s-complement encoding 
Function B2Tw is a bijection


This asymmetry arises because half the bit patterns (those with the sign bit set to 1) represent negative numbers, while the other half (those with the sign bit set to 0) represent nonnegative numbers. Since 0 is nonnegative, this means that it can represent one less positive number than negative.

Second, the maximum unsigned value is just over twice the maximum two’s-complement value:

UMax=2 TMax+1U_\text{Max} = 2 \, T_\text{Max} + 1UMax​=2TMax​+1

![[Pasted image 20250912105047.png]]

It is important to have data types compatible with those specified by the protocol. We have seen that some C data types, especially `long`, have different ranges on different machines, and in fact, the C standards only specify the minimum ranges for any data type, not the exact ranges.

we can add like stdint.h. This file defines a set of data types with declarations of the form intN_t and uintN_t, specifying N-bit signed and unsigned integers, for different values of N. The exact values of N are implementation dependent, but most compilers allow values of 8, 16, 32, and 64.

[[Etc#About compatibility of the data types]]


2.2.4 Conversion Between signed and unsigned
For most implementations of C, however, the answer to this question is based on a bit-level perspective, rather than on a numeric one.