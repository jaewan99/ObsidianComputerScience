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

At the hardware level, the principle of locality allows computer designers to speed up main memory accesses by introducing small, fast memories known as **cache memories** that hold blocks of the most recently referenced instructions and data items.

At the operating system level, the principle of locality allows the system to use the main memory as a cache of the most recently referenced chunks of the virtual address space. Similarly, the operating system uses main memory to cache the most recently used disk blocks in the disk file system.
### 6.2.1 Locality of References to Program Data

Since the function has either good spatial or temporal locality with respect to each variable in the loop body, we can conclude that the **`sumvec`** function enjoys good locality.

**Stride-1 reference patterns** are a common and important source of spatial locality in programs. In general, as the stride increases, spatial locality decreases.

### 6.2.2 Locality of Instruction Fetches

Since program instructions are stored in memory and must be fetched (read) by the CPU, we can also evaluate the locality of a program with respect to its instruction fetches.

- **Instruction references:** 
- Reference instructions in sequence → _spatial locality_
- **Loop cycles:** Cycle through the loop repeatedly → _temporal locality_