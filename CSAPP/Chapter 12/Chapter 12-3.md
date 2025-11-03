https://www.youtube.com/watch?v=xY7Y_-b9pv4&list=PL22J-I2Pi-Gf0s1CGDVtt4vuvlyjLxfem&index=25

Using Semaphores to Coordinate Access to Shared Resources
- Basic idea: Thread uses a semaphore operation to notify another thread that some condition has become true
	- Use counting semaphores to keep track of resource state
	- Use binary semaphores to notify other threads
- The Producer-Consumer Problem
	- Mediating interactions between processes that generate information and that then make use of that information
	- Producer waits for empty slot, inserts item in buffer, and notifies consumer
	- Consumer waits for item, removes it from buffer, and notifies producer
	- Examples
		- Multimedia processing:
			- Producer creates video frames (MPEG), consumer renders them
		- Event-driven graphical user interfaces
			- Producer detects mouse clicks, mouse movements, and keyboard hits and inserts corresponding events in buffer
			- Consumer retrieves events from buffer and paints the display

Producer-Consumer on an n-element Buffer
- Requires a mutex and two counting semaphores:
	- mutex: enforces mutually exclusive access to the the buffer