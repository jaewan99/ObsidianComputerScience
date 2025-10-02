### **1. Pointers & Memory Management**
- **Pointers:** Understand `*`, `&`, pointer arithmetic, and pointer-to-pointer concepts.
    - Example: Accessing `struct thread` fields via a pointer.
        
- **Dynamic memory:** `malloc`, `free`—used in thread stacks, buffers, and filesystem structures.
- **Memory layout:** Know the difference between **stack**, **heap**, **global/static**, and **code segments**.
### **2. Structures (`struct`)**
- **Structs** are everywhere in Pintos: `struct thread`, `struct file`, `struct inode`.
- Know how to define, access, and pass structs by **pointer** vs **value**.
- Understand **linked lists using structs** (e.g., `struct list_elem` in `threads`).
### **3. Arrays**
- Fixed-size and dynamic arrays, especially for buffers.
- Example: Reading/writing files or handling command-line arguments.
### **4. Functions & Function Pointers**
- Passing **functions as arguments** is common in thread or timer callbacks.
- Understand **return values** and **side effects** of functions.
### **5. Control Structures**
- Loops: `for`, `while`, `do-while`.
- Conditional statements: `if`, `switch`.
- Essential for scheduling loops, system call dispatching, and error handling.
### **6. Bitwise Operations**

- Flags, permissions, and masks often use `&`, `|`, `^`, `~`, `<<`, `>>`.
- Example: Handling thread status flags or page table entries.
### **7. Type Casting**

- Casting pointers and integers is common in low-level OS code.
- Example: Converting `void*` to a `struct thread*`.

### **8. Macros & Constants**

- `#define` and `const` are widely used in Pintos for **flags, sizes, and limits**.
- Example: `#define PGSIZE 4096`.

### **9. Preprocessor & Header Files**

- Know how `#include`, header guards (`#ifndef … #define …`) work.
- Helps you understand Pintos’ project structure and code dependencies.

### **10. Low-level Memory Tricks (Optional but Useful)**

- Casting structs to raw bytes for disk operations.
- Pointer arithmetic for arrays in structs.