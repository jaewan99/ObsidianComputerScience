```timestamp-url 

 ```

 https://www.youtube.com/watch?v=vaOT9KeIUDk&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=16

- In unix, a file is just sequence of bytes, and unix doesn't distinguish between different classes of files unlike say Windows. The os operating system level has essentially no understanding of a more detailed structure inside of a file.
- Elegant mapping of files to devices allows kernel to export simple interface called Unix I/O:
	- Opening and closing files
		- open () and close ()
	- Reading and writing a file
		- read () and write ()
	- read () and write ()
		- we don't always start with the start, we want to read a data and continuously reading that data
		- indicates next offset into file to read or write
		- lseek ()
		- ![[Pasted image 20251030194003.png]]
		- File position as part of the data associated with the data, telling how far we have read or written
- File Types
	- Each file has a type indicating its role in the system
		- Regular file: Contains arbitrary data
			- The things that are on a disk drive
		- Directory: Index for a related group of files
		- Socket: For communicating with a process on another machine