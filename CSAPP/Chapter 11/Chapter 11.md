https://www.youtube.com/watch?v=OynSMXfNtiM&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=21

A Client-Server Transaction
- Most network applications are based on the client-server model:
	- A server process and one or more client processes
	- Server manages some resource
	- Server provides service by manipulating resource for clients
	- Server activated by request from client (vending machine analogy
	- ![[Pasted image 20251031165649.png]]
- ![[Pasted image 20251031165735.png]]
	- From the hardware perspective, the interface to a between the network and your computer is called NIC, or network interface card
		- ![[Pasted image 20251031170714.png]]
		- Network interface card
		- The interesting thing is that it looks to your computer like an I/O device
		- And unix API dealing with networks, make it looks like a file.
- Computer Networks
	- A network is a hierarchical system of boxes and wires organized by geographical proximity
		- SAN (System Area Network) spans cluster or machine room
			- Switched Ethernet, Quadrics QSW, ...
		- LAN (Local Area Network) spans a building or campus
			- Ethernet is most prominent example
		- WAN (Wide Area Network) spans country or world
			- Typically high-speed point-to-point phone lines
	- An internetwork (internet) is an interconnected set of networks
		- The Global IP Internet (uppercase "I") is the most famous example of an internet (lowercase "i")
- Lowest Level: Ethernet Segment
	- 