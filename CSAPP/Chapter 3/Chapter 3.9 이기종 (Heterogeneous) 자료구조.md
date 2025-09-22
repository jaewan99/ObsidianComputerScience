



C provides two mechanisms for creating data types by combining objects of different types:


**Structures**, declared using the keyword `struct`, aggregate multiple objects into a single unit.

**Unions**, declared using the keyword `union`, allow an object to be referenced using several different types.

### 3.9.1 Structures


The expression `(*rp).width` dereferences the pointer and selects the `width` field of the resulting structure. Parentheses are required, because the compiler would interpret the expression `*rp.width` as `*(rp.width)`, which is not valid.


That is, `rp->width` is equivalent to the expression `(*rp).width`.


### 3.9.2 Unions

Unions provide a way to circumvent the type system of C, allowing a single object to be referenced according to multiple types.


### 3.9.3 Data Alignment

Many computer systems place restrictions on the allowable addresses for primitive data types, requiring that the address for some objects must be a multiple of some value.


Alignment is enforced by making sure that every data type is organized and allocated in such a way that every object within the type satisfies its alignment restrictions.
![[Pasted image 20250921233628.png]]
If we pack this structure into 9 bytes, we can still satisfy the alignment requirements for fields `i` and `j` by making sure that the starting address of the structure satisfies a 4-byte alignment requirement.


struct S2 d[4];

These elements would have addresses `xd`, `xd + 9`, `xd + 18`, and `xd + 27`. Instead, the compiler allocates 12 bytes for `struct S2`, with the final 3 bytes being wasted space.

![[Pasted image 20250921233659.png]]
