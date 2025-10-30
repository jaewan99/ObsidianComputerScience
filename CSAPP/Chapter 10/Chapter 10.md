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
			- it actually does have an interpretation that entries in that file describe the location and attributes of other files
		- Socket: For communicating with a process on another machine
			- Connection to next, send and receiving the message
			
	- Other file types beyond our scope
		- Named pipes (FIFOs)
		- Symbolic links
		- Character and block devices
	
-  Regular Files
	- A regular file contains arbitrary data
	- Applications often distinguish between text files and binary files
		- Text files are regular files with only ASCII or Unicode characters
		- Binary files are everything else
			- e.g., object files, JPEG images
		- Kernel doesn’t know the difference! - doesn't happen in the low level
	- Text file is sequence of text lines
		- Text line is sequence of chars terminated by newline char (‘\n’)
			- Newline is 0xa, same as ASCII line feed character (LF)
	- End of line (EOL) indicators in other systems
		- Linux and Mac OS: ‘\n’ (0xa)
			- line feed (LF)
		- Windows and Internet protocols: ‘\r\n’ (0xd 0xa)
			- Carriage return (CR) followed by line feed (LF)
		- Two classes of systems have different ways of interpreting of encoding when is the end of a line.
			- linux or MAC file it's just this character code 0xa
			- In windows files with two characters.
- Directories
	- Directory consists of an array of links
		- Each link maps a filename to a file
	- Each directory contains at least two entries
		- . (dot) is a link to itself
		- .. (dot dot) is a link to the parent directory in the directory hierarchy (next slide)
	- Commands for manipulating directories
		- mkdir: create empty directory
		- ls: view directory contents
		- rmdir: delete empty directory
	- Directory is stored as a file but it's a file that the file system part of operating system interprets in very specific ways.
- Directory Hierarchy
	- All files are organized as a hierarchy anchored by root directory named / (slash)
	- ![[Pasted image 20251030195826.png]]
	- Kernel maintains current working directory (cwd) for each process
		- Modified using the cd command
	- There's a hierarchical organizations that's maintained as a series of files each being the directory and the directory then is a pointer to its subdirectory which again are files
- Pathnames
	- Is a way to navigate through the hierarchy of file and identify the particular file 
	- Locations of files in the hierarchy denoted by pathnames
		- Absolute pathname starts with ‘/’ and denotes path from root
			- /home/droh/hello.c
	- Relative pathname denotes path from current working directory
		- ../home/droh/hello.c
- Opening Files
	- Opening a file informs the kernel that you are getting ready to access that file