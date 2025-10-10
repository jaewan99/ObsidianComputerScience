https://www.youtube.com/watch?v=FDBqMES--TY&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=11


video
- [02:31](https://www.youtube.com/watch?v=FDBqMES--TY#t=02:31.25) 
- Random-Access Memory (RAM)
	- RAM is traditionally packaged as a chip.
	- Basic storage unit is normally a **cell** (one bit per cell).
	- Multiple RAM chips from a memory.
- RAM comes in two varieties:
	- SRAM (Static RAM) - 정적
	- DRAM (Dynamic RAM) - 동적

![[Pasted image 20251002164807.png]]




- [13:50](https://www.youtube.com/watch?v=FDBqMES--TY#t=13:50.88) 
- Disk
- 
![[Pasted image 20251002170357.png]]


- [19:08](https://www.youtube.com/watch?v=FDBqMES--TY#t=19:08.65) 
- Disk operations



- [20:41](https://www.youtube.com/watch?v=FDBqMES--TY#t=20:41.87) 
- Disk access 

![[Pasted image 20251002170806.png]]
- [22:30](https://www.youtube.com/watch?v=FDBqMES--TY#t=22:30.92) 
- Disk access time
- 물리적으로 한계가 있음

- [25:14](https://www.youtube.com/watch?v=FDBqMES--TY#t=25:14.80) 
- logical disk blocks
- command, logical block number, and memory address
![[Pasted image 20251002172249.png]]

![[Pasted image 20251002172311.png]]
- cpu is completely oblivious to the fact that this transfer is going on

![[Pasted image 20251002172417.png]]



- [32:06](https://www.youtube.com/watch?v=FDBqMES--TY#t=32:06.08) 
- solid state disk (SSDs)



- [39:21](https://www.youtube.com/watch?v=FDBqMES--TY#t=39:21.49) 
- The CPU-Memory Gap
	- to make their processors faster they would just double the clock frequency. they decreased the feature size of the chips that they were making- that would allow to put things closer together, and then increase the clock frequency by a proportional amount.
	- In 2003, they cant handled the heat generated from decreasing the size of the chip
		- So now they subdivided a CPU chip into individual processors cores
		- by running in parallel, you can more effective - the effective CPU cycle time go down
	- The only way to really get more performance, is to increase the number of independent cores



- [44:16](https://www.youtube.com/watch?v=FDBqMES--TY#t=44:16.77) 
- Principle Locality 
	- the programs tend to use data and instructions whose addresses are near or equal to those that they have used recently
- Temporal locality:
	- Recently referenced items are likely to be referenced again in the near future
- Spatial locality
	- Items with nearby addresses tend to be referenced close together in time 
- Good locality = Good performance

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