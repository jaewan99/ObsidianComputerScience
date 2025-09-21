

Optimizing compilers are particularly good at simplifying the address computations used by array indexing.


### 3.8.1 Basic Principles

![[Pasted image 20250921223428.png]]



### 3.8.2 Pointer Arithmetic


The unary operators **‘&’** and **‘*’** allow the generation and dereferencing of pointers. That is:

- For an expression `Expr` denoting some object, `&Expr` is a pointer giving the address of the object.
    
- For an expression `AExpr` denoting an address, `*AExpr` gives the value at that address.

### 3.8.3 Nested Arrays


![[Pasted image 20250921224851.png]]



### 3.8.4 Fixed - Size Arrays


![[Pasted image 20250921225539.png]]


### 3.8.5 Variable-Size Arrays

Programmers requiring variable-size arrays had to allocate storage for these arrays using functions such as **malloc** or **calloc**, and they had to explicitly encode the mapping of multidimensional arrays into single-dimension ones via **row-major indexing**.