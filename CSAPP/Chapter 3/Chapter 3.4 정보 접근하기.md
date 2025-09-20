

Those that generate 1 or 2-byte quantities leave the remaining bytes unchanged. Those that generate 4 byte quantities set the upper 4 bytes of the register to zero.

Most unique among them is the stack pointer, %rsp, used to indicate the end position in the run-time stack.

![[Pasted image 20250920164225.png]]
### 3.4.1 Operand Specifiers
Mostinstructionshaveoneormoreoperandsspecifyingthesourcevaluestouse inperforminganoperationandthedestinationlocationintowhichtoplacethe result

page 209 (pdf) for operand forms

.Sourcevalues canbegivenasconstantsorreadfromregistersormemory.


Thefirsttype,immediate,isforconstantvalues.InATT formatassemblycode, thesearewrittenwitha‘$’ followedbyanintegerusing standardCnotation—forexample,$-577or$0x1F.


Thesecondtype, register,denotes the contentsofaregister,oneofthesixteen8-,4-,2-,or1-bytelow-orderportionsof theregistersforoperandshaving64,32,16,or8bits,respectively

memoryreference, inwhichweaccesssome memorylocationaccordingtoacomputedaddress,oftencalledtheeffectivead dress.

### 3.4.2 Data Movement Instructions

movb, movw, movl, and movq. All four of these instructions have similar effects; they differ primarily in that they operate on data of different sizes: 1, 2, 4, and 8 bytes, respectively


![[Pasted image 20250920171228.png]]

![[Pasted image 20250920171624.png]]

Theonlyexceptionis thatwhenmovlhasaregisterasthedestination, itwillalsosetthehigh-order4 bytesoftheregisterto0


![[Pasted image 20250920171956.png]]
