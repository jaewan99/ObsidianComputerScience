https://www.youtube.com/watch?v=nLIhml8ni-A&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=8




- [03:37](https://www.youtube.com/watch?v=nLIhml8ni-A#t=03:37.60) 
- Array allocation
	- T A[L]
		- Array of data type T and length L
		- Contiguously allocated region of L * sizeof (T) bytes in memory
- Basic principle


- [22:28](https://www.youtube.com/watch?v=nLIhml8ni-A#t=22:28.34) 
- multidimensional (nested) arrays


- [1:05:56](https://www.youtube.com/watch?v=nLIhml8ni-A#t=1:05:56.16) 
- Structure and alignment
- Aligned Data
	- Primitive data type requires k bytes
	- Address must be multiple of K
	- required on some machines; advised on x86-64
- Motivations for aligning data
	- Memory accessed by (aligned) chunks of 4 or 8 bytes (system dependent)
		- Inefficient to load or store datum that spans quad word boundaries
		- Virtual memory trickier when datum spans 2 pages
- Compiler
	- Inserts gaps in structure to ensure correct alignment of fields


![[Pasted image 20250921234402.png]]
greedy algorithm will work



- [1:13:49](https://www.youtube.com/watch?v=nLIhml8ni-A#t=1:13:49.35) 
- Floating point
![[Pasted image 20250922142951.png]]

![[Pasted image 20250922143021.png]]

![[Pasted image 20250922142255.png]]

![[Pasted image 20250922143121.png]]
