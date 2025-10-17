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


- [20:57](https://www.youtube.com/watch?v=AauOs6vq9yI#t=20:57.12) 
- E- way Set Associative Cache (Here: E =2)
- E = 2: Two lines per set
- Assume: cache block size 8 bytes
- Question: what determines the block size
	- It's determined by the design of the memory system
