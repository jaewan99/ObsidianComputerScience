



Cprovides two mechanisms for creating data types by combining objects of dif ferent types:


structures, declared using the keyword struct, aggregate multiple objects into a single unit;

unions, declared using the keyword union, allow an object to be referenced using several different types.

### 3.9.1 Structures


The expression (*rp).width dereferences the pointer and selects the width field of the resulting structure. Parentheses are required, because the compilerwouldinterprettheexpression*rp.widthas *(rp.width), which is not valid.


That is, rp->width is equivalent to the expression (*rp).width.


### 3.9.2 Unions

UnionsprovideawaytocircumventthetypesystemofC,allowingasingleobject tobereferencedaccordingtomultipletypes.


### 3.9.3 Data Alignment

Manycomputer systemsplacerestrictionsontheallowableaddresses for the primitivedatatypes,requiringthattheaddressforsomeobjectsmustbeamultiple ofsomevalue


Alignment is enforced by making sure that every data type is organized and allocated in such a way that every object within the type satisfies its alignment restrictions
