[https://www.geeksforgeeks.org/operating-systems/virtual-memory-in-operating-system/](https://www.geeksforgeeks.org/operating-systems/virtual-memory-in-operating-system/)



Virtual memory is a memory management technique used by operating systems to give the appearance of a large, continuous block of memory to applications, even if the physical memory (RAM) is limited. It allows larger applications to run on systems with less RAM.

가상메모리의 목적
- To support multiprogramming , it allows more than one program to run at the same time.
- - A program doesn’t need to be fully loaded in memory to run. Only the needed parts are loaded.
- Programs can be bigger than the physical memory available in the system.
- - Virtual memory creates the illusion of a large memory, even if the actual memory (RAM) is small.
- - It uses both RAM and disk storage to manage memory, loading only parts of programs into RAM as needed.
- - This allows the system to run more programs at once and manage memory more efficiently.!
 
![[virtual_memory-1024.webp]]
### How Virtual Memory Works

- Virtual memory uses both hardware and software to manage memory.
- When a program runs, it uses virtual addresses (not real memory locations).
- The computer system converts these virtual addresses into physical addresses (actual locations in RAM) while the program runs.

Types of virtual memory

1. Paging
2. Segmentation

****Page and Frame:**** Page is a fixed size block of data in virtual memory and a frame is a fixed size block of physical memory in RAM where these pages are loaded.

- Think of a page as a piece of a puzzle (virtual memory) While, a frame as the spot where it fits on the board (physical memory).
- When a program runs its pages are mapped to available frames so the program can run even if the program size is larger than physical memory.

Segmentation divides virtual memory into segments of different sizes. Segments that aren't currently needed can be moved to the hard drive. Here,

- The system uses a segment table to keep track of each segment's status, including whether it's in memory, if it's been modified and its physical address.
- Segments are mapped into a process's address space only when needed.