

### 3.10.1 Understanding Pointers
Pointers can also point to functions

int fun(int x, int *p);

### 3.10.2 Life in Real World: Using the GDB debugger

GDB (GNU Debugger) allows you to analyze and control the execution of machine-level programs. Instead of inferring a program’s behavior by reading code alone, GDB lets you **observe it in action**, inspect registers and memory, and control execution step by step.


### 3.10.3 Out-of-Bounds Memory References and Buffer Overflow


sbufferoverflow. Typically, some character array is allocated on the stack to hold a string, but the size of the string exceeds the space allocated for the array.


![[Pasted image 20250922131708.png]]


### 3.10.4 Thwarting buffer overflow attacks

Stack Randomization
Stack Corruption Detection
Limiting Executable Code Regions
[[Lecture 9]]


### 3.10.5 Supporting Variable-Size Stack Frames

 
 To manage a variable-size stack frame, x86-64 code uses register `%rbp` to serve as a frame pointer.