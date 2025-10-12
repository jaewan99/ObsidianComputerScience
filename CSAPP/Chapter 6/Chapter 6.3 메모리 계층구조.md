https://www.youtube.com/watch?v=FDBqMES--TY&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=11


- [53:55](https://www.youtube.com/watch?v=FDBqMES--TY#t=53:55.82) 
- Cache: A smaller, faster storage device that acts as a staging area for a subset of the data in a larger, slower device. 
- Fundamental idea of a memory hierarchy: For each k, the faster, smaller device at level k serves as a cache for the larger, slower device at level k+1.
- Why do memory hierarchies work?
	- Because of locality, programs tend to access the data at level k more often than they access the data at level k+1.
	- Thus, the storage at level k+1 can be slower, and thus larger and cheaper per bit.
- Big Idea: The memory hierarchy creates a large pool storage that costs as much as the cheap storage near bottom, but that serves data to programs at the rate of fast storage near the top.

- [1:02:08](https://www.youtube.com/watch?v=FDBqMES--TY#t=1:02:08.49) 
- Caching Concept example

- General Caching Concepts: Types of Cache Misses
	- Cold (compulsory) miss
		- Cold misses occur because the cache is empty.
	- Conflict miss
		- Most caches limit blocks at level k+1 to a small subset (sometimes a singleton) of the block positions at level k.
			- E.g. Block i at level k+1 must be placed in block (i mod 4) at level k.
		- Conflict misses occur when the level k cache is large enough, but multiple data objects all map to the same level k block.
			- E.g. Referencing blocks 0, 8, 0, 8, 0, 8, ... would miss every time.
	- Capacity miss
		- Occurs when the set of active cache blocks (working set) is larger than the cache.

Book

### 6.3 Memory Hierarchy

In general, the storage devices get slower, cheaper, and larger as we move from higher to lower levels. 
- At the highest level (L0) are a small number of fast CPU registers that the CPU can access in a single clock cycle. 
- Next are one or more small to moderate-size SRAM-based cache memories that can be accessed in a few CPU clock cycles. 
- These are followed by a large DRAM-based main memory that can be accessed in tens to hundreds of clock cycles. Next are slow but enormous local disks. 
- Finally, some systems even include an additional level of disks on remote servers that can be accessed over a network.

### 6.3.1. Caching in Memory Hierarchy

- Cache Hit
	- Ifd happens to be cached at level k, then we have what is called a cache hit.
- Cache Misses
	- If, on the other hand, the data object d is not cached at level k, then we have what is called a cache miss.
- Kinds of Cache Misses
	- 