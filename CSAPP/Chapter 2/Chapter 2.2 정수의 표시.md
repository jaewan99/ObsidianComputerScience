p2.2 Integer representation
![[Pasted image 20250912101412.png]]

### 2.2.1 Integral data type

C supports a variety of integral data types — ones that represent finite ranges of integers.

long
![[Pasted image 20250912114012.png]]

−2,147,483,648
−9,223,372,036,854,775,808


We also see that the data type `int` could be implemented with 2-byte numbers, although this is mostly a throwback to the days of 16-bit machines. We also see that the type `long` can be implemented with 4-byte numbers, and it typically is for 32-bit programs.


### 2.2.2 Unsigned Encodings
![[Pasted image 20250912103612.png]]

given this image the decimal value of 1011 would be 11 and such.


principle: Uniqueness of unsigned encoding 
Function B2Uw is a bijection.

Example of bijection would be
there is only one decimal values that 0001 can map which is 1 and also for reverse, where 1 can only map to 0001 to binary.


### 2.2.3 two's compliment encodings
![[Pasted image 20250912104207.png]]
principle: Uniqueness of two’s-complement encoding 
Function B2Tw is a bijection


This asymmetry arises because half the bit patterns (those with the sign bit set to 1) represent negative numbers, while the other half (those with the sign bit set to 0) represent nonnegative numbers. Since 0 is nonnegative, this means that it can represent one less positive number than negative.

Second, the maximum unsigned value is just over twice the maximum two’s-complement value:

UMax=2 TMax+1U_\text{Max} = 2 \, T_\text{Max} + 1UMax​=2TMax​+1

![[Pasted image 20250912105047.png]]

It is important to have data types compatible with those specified by the protocol. We have seen that some C data types, especially `long`, have different ranges on different machines, and in fact, the C standards only specify the minimum ranges for any data type, not the exact ranges.

we can add like stdint.h. This file defines a set of data types with declarations of the form intN_t and uintN_t, specifying N-bit signed and unsigned integers, for different values of N. The exact values of N are implementation dependent, but most compilers allow values of 8, 16, 32, and 64.

[[CSAPP/Chapter 2/Etc#About compatibility of the data types]]

![[Pasted image 20250914211715.png]]
### 2.2.4 Conversion Between signed and unsigned
For most implementations of C, however, the answer to this question is based on a bit-level perspective, rather than on a numeric one.

The bit values are identical but change how these bits are interpreted.

![[Pasted image 20250912125957.png]]

principle: Conversion from two’s complement to unsigned 
For x such that TMinw ≤x ≤TMaxw

For example, we saw thatT2U16(−12,345)=−12,345+216 =53,191,andalso that T2Uw(−1) =−1+2w =UMaxw.


![[Pasted image 20250912115847.png]]

### 2.2.5 Signed versus unsigned in C


all machines use two’s complement. Generally, most numbers are signed by default

`%d`, `%u`, and `%x` are used to print a number as a signed decimal, an unsigned decimal, and in hexadecimal format, respectively.

We can see the conversion routines in action: `T2U32(-1) = UMax32 = 2^32 - 1` and `U2T32(2^31) = 2^31 - 2^32 = -2^31 = TMin32`.

When an operation is performed where one operand is signed and the other is unsigned, C implicitly casts the signed argument to unsigned and performs the operation assuming the numbers are nonnegative.

![[Pasted image 20250912131314.png]]

[[CSAPP/Chapter 2/Etc#INT_MIN as (-INT_ MAX -1)]]


### 2.2.6 Expanding the Bit representation of a number

Expansion of an unsigned number by zero extension uses zero extension for the unsigned number.

Expansion of a two’s-complement number by sign extension uses sign extension for the signed number.

Figure 2.20 shows the result of expanding from word size w=3w = 3w=3 to w=4w = 4w=4 by sign extension. The bit vector `[101]` represents the value −4+1=−3-4 + 1 = -3−4+1=−3.  
Applying sign extension gives the bit vector `[1101]`, representing the value −8+4+1=−3-8 + 4 + 1 = -3−8+4+1=−3.  
We can see that, for w=4w = 4w=4, the combined value of the two most significant bits, −8+4=−4-8 + 4 = -4−8+4=−4, matches the value of the sign bit for w=3w = 3w=3. Similarly, the bit vectors `[111]` and `[1111]` both represent the value −1-1−1.

![[Pasted image 20250912134351.png]]


![[Pasted image 20250912155745.png]]

this shows that, when converting from short to unsigned 
This shows that, when converting from `short` to `unsigned`, the program first changes the size and then the type. That is, `(unsigned) sx` is equivalent to `(unsigned)(int) sx`, evaluating to 4,294,954,951, not `(unsigned)(unsigned short) sx`, which evaluates to 53,191. Indeed, this convention is required by the C standards.


![[Pasted image 20250914195205.png]]


![[Pasted image 20250914195220.png]]

### 2.2.7 Truncating Numbers

![[Pasted image 20250912160116.png]]
Truncating numbers may create some problems as we cast from higher bit to lower bit data type like int -> short


### 2.2.8 Advice on Signed versus Unsigned  

Since the casting takes place without any clear indication in the code, programmers often overlook its effects.