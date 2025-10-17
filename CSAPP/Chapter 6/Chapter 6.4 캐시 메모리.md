Cache Memories
https://www.youtube.com/watch?v=AauOs6vq9yI&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=12

Cache Memories
- Cache memories are small, fast SRAM-based memories managed automatically in hardware (main memory is slower)
	- Hold frequently accessed blocks of main memory
- CPU looks first for data in cache


- [07:45](https://www.youtube.com/watch?v=AauOs6vq9yI#t=07:45.38) 
- Cache Read
	- The address of the word is 64 bits in case of x86-64 bits
	- s bits is unsigned
	- all remaining bits constitutes to t bits
	- ![[Pasted image 20251017103448.png]]



- [11:51](https://www.youtube.com/watch?v=AauOs6vq9yI#t=11:51.48) 
Example: Direct Mapped Cache (E = 1)
- Direct mapped: One line per set 
- Assume: cache block size 8 bytes
- ![[Pasted image 20251017103807.png]]
- ![[Pasted image 20251017103924.png]]
- if the valid bit was false and the tag match then that would also be a miss



- [19:44](https://www.youtube.com/watch?v=AauOs6vq9yI#t=19:44.98) 
- Direct -Mapped Cache Simulation
![[Pasted image 20251017111346.png]]
![[Pasted image 20251017111459.png]]
- since the tag is the same, we replace the set0, hence having one more miss on the last "0"

- [20:57](https://www.youtube.com/watch?v=AauOs6vq9yI#t=20:57.12) 
- E- way Set Associative Cache (Here: E =2)
- E = 2: Two lines per set
- Assume: cache block size 8 bytes
- Question: what determines the block size
	- It's determined by the design of the memory system- so that's fixed parameter of the memory system
	- 
- ![[Pasted image 20251017111646.png]]
- now we can have two different block in set 0 - but it's more logically complex - in both hardware and software



- [35:32](https://www.youtube.com/watch?v=AauOs6vq9yI#t=35:32.26) 
- What about writes?
- Multiple copies of data exist:
	- L1, L2, L3, Main Memory, Disk
- What to do on a write-hit?
	- Write-through (write immediately to memory)
	- Write-back (defer write to memory until replacement of line)
		- Need a dirty bit (line different from memory or not)
- What to do on a write-miss?
	- Write-allocate (load into cache, update line in cache)
		- Good if more writes to the location follow
	- No-write-allocate (writes straight to memory, does not load into cache)
- Typical
	- Write-through + No-write-allocate
	- ***Write-back + Write-allocate**


- [39:29](https://www.youtube.com/watch?v=AauOs6vq9yI#t=39:29.54) 
- 