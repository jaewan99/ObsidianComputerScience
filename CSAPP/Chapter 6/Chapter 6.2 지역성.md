https://www.youtube.com/watch?v=FDBqMES--TY&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=11

- [44:16](https://www.youtube.com/watch?v=FDBqMES--TY#t=44:16.77) 
- Principle Locality 
	- the programs tend to use data and instructions whose addresses are near or equal to those that they have used recently
- Temporal locality:
	- Recently referenced items are likely to be referenced again in the near future
- Spatial locality
	- Items with nearby addresses tend to be referenced close together in time 
- Good locality = Good performance




- [53:55](https://www.youtube.com/watch?v=FDBqMES--TY#t=53:55.82) 
- Cache: A smaller, faster storage device that acts as a staging area for a subset of the data in a larger, slower device. 
- Fundamental idea of a memory hierarchy: For each k, the faster, smaller device at level k serves as a cache for the larger, slower device at level k+1.
- Why do memory hierarchies work?
	- Because of locality, programs tend to access the data at level k more often than they access the data at level k+1.
	- Thus, the storage at level k+1 can be slower, and thus larger and cheaper per bit.
- Big Idea: The memory hierarchy creates a large pool storage that costs as much as the cheap storage near bottom, but that serves data to programs at the rate of fast storage near the top.

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