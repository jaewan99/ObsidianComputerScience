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