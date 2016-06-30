#1. Data Storage

##1.1 Bits and Their Storage
bits: binary digits

###Boolean Operations
The bit 0 represents the value false and the bit 1 represents the value true.
The basic Boolean operations: AND, OR, XOR(exclusive or) and NOT.

###Gates and Flip-Flops
*Gate*: a device that produces the output of a Boolean operation when given the operation's input values is called a gate.
Gates provide the building blocks from which conputers are constructed.
*Flip-flop*: a flip-flop is a circuit that produces an output value of 0 or 1, which remains constant until a pulse(a temporary change to a 1 that returns to 0) from another circuit causes it to shift to the other value. In other words, the output will flip or flop between two values under control of external stimuli.

###Hexadecimal Notation
Stream: a long string of bits.

##1.2 Main Memory
###Memory Organization
*Byte*: a conputer's main memory is organized in manageable units called cells, with a typical cell size being eight bits. a string of eight bits is called a byte.
high-order end/low-order end
most significant bit/least significant bit
*Address*: to identify individual cells in a computer's main memory, each cell is assigned a unique "name", called its address.
Such an addressing system not only gives us a way of uniquely identifying each cell but also associates an order to the cells, giving us phrases such as "the next cell" or "the previous cell".
An important consequence of assigning an order to both the cells in main memory and the bits within each cell is that the entire collection of bits within a computer's main memory is essentially ordered in one long row. Pieces of this long row can therefore be used to store bit patterns that may be longer than the length of a single cell.
**RAM**: Beacuse a computer's main memory is organized as individual, addressable cells, the cells can be accessed independently as required. To reflect the ability to access cells in any order, a computer's main memory is often called random access memory.
DRAM/SDRAM

###Measuring Memory Capacity

##1.3 Mass Storage

###Magnetic Systems
A disk storage system consists of many individual sectors, each of which can be accessed as an independent string of bits.
The location of tracks and sectors is not a permanent part of a disk's physical structure, they are marked magnetically through a process called formatting (or initializing) the disk. 

Evaluate a disk system's performance:
(1) seek time
(2) rotation delay or latency time
(3) access time (the sum of seek time and rotation delay)
(4) transfer rate (in the case of zone-bit recording, the amount of data passing a read/write head in a single disk rotation is greater for tracks in an outer zone than for an inner zone, and therefore the data transfer rate varies depending on the portion of the disk being used.)

