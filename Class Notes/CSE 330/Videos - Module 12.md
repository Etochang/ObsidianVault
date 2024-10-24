202406302002
Meta Tags: #class
Tags: [[OS]]

# Videos - Module 12

## Storage System I/O Basics

### Memory-Storage Hierarchy

![[Pasted image 20240630200336.png]]

### Storage Systems

- Typically, it includes the hardware device (e.g. hard drive or solid state drive), driver (software, can be a module of OS), basic storage software layer (file system, object store).
- Traditionally, storage devices are used as "block device". The read and write must be "data blocks" which is 4KB or other fixed size.
- Usually, we use a file system. For database, simple DB usually use file system to store the data. But some advanced DB can directly write data to block device (no file system).

### Prototypical System Architecture

![[Pasted image 20240630200912.png]]

### Basic I/O Protocol

```
while (STATUS == BUSY)
	//spin
Write data to DATA register
write command to COMMAND register
while (STATUS == BUSY)
	//spin
```

![[Pasted image 20240630201153.png]]

### Programmed I/O vs. Direct Memory Access

- PIO
	- CPU directly tells device what data is
	- CPU involved in data transfer
- DMA
	- CPU leaves data in memory
	- DMA hardware does data copy

### PIO Data Flow

![[Pasted image 20240630201453.png]]

![[Pasted image 20240630201509.png]]

![[Pasted image 20240630201539.png]]

### DMA Data Flow

![[Pasted image 20240630201655.png]]

![[Pasted image 20240630201707.png]]

![[Pasted image 20240630201733.png]]

![[Pasted image 20240630201749.png]]

![[Pasted image 20240630201843.png]]

## HDD Introduction

### Basic Interface

- a magnetic disk has a sector-addressable address space
	- a disk = an array of sectors
	- each sector (logical block) is the smallest unit of transfer
- sectors are typically 512 or 4096 bytes
- Main Operations:
	- Read from sectors
	- Write to sectors

### Disk Interface

- The 1D array of logical blocks is mapped into the sectors of the disk sequentially
	- Sector 0 is the first sector of the first track on the outermost cylinder
	- Mapping proceeds in order through that track, then the rest of the tracks in that cylinder, and then through the rest of the cylinders from outermost to innermost
	- Logical to physical address should be easy
		- except for bad sectors

### HDD Internals

![[Pasted image 20240630202857.png]]

![[Pasted image 20240630202903.png]]

![[Pasted image 20240630202909.png]]

![[Pasted image 20240630202919.png]]

![[Pasted image 20240630202947.png]]

![[Pasted image 20240630203120.png]]

### Disk Performance

I/O latency:
$$L_{I/O} = L_{Seek} + L_{Rotate} + L_{Transfer}$$
at the ms level. 

### Seek, Rotate, Transfer

- Seek may take several ms, settling along can take 0.5 - 2ms, entire seek often takes 4 - 10ms: arm motion
- Rotation  - RPM
	- 7200 RPM is common
	- 15000 RPM is high end
	- worst case scenario is one rotation
- Transfer - relatively fast, depends on RPM and sector density. 

### Workloads

- Seeks and rotations are slow while transfer is relatively fast
- Sequential I/O is preferred since sectors are accessed in order, minimizing seek and rotation time
- Random workloads are typically slow on disks (e.g. QuickSort)

## HDD Scheduling Algorithms

>Given a stream of I/O requests, in what order should they be serviced?

### Disk Scheduling

- OS is responsible for using hardware efficiently – for the disk drives, this means having a fast access time and high disk bandwidth utilization
- Strategy: reorder requests to meet some goal
	- Performance (e.g., by making I/O sequential)
	- Fairness
	- Consistent latency
- Usually implemented in both OS and hardware

- Performance objective: minimize seek+rotation time
	- minimize the distance the head needs to go
- Disk bandwidth
	- the total number of bytes transferred, divided by the total time between the first request for service and the completion of the last transfer

- There are many sources of disk I/O requests:
	- OS
	- System processes
	- User processes
- I/O requests: read/write mode, disk address, memory address, number of sectors to transfer
- OS maintains queue of requests, per disk or device
- Idle disk can immediately work on I/O request, busy disk means work must queue
	- Optimization algorithms make sense only when a queue exists

- Note that drive controllers have small buffers and can manage a queue of I/O requests of varying "depth". 
- Disk scheduling algorithms:
	- algorithms that schedule the orders of disk I/O requests
	- the basic goal is to minimize the number of cylinders the head passes

### FIFO

- Idea: Serve the I/O requests in the order they arrive

![[Pasted image 20240630204600.png]]

### Shortest Positioning Time First (SPTF)

- Idea: select the request that will take the least seek and rotate time
- Also called Shortest Seek Time First (SSTF) if rotational positioning is not considered
- Might cause starvation

![[Pasted image 20240630204732.png]]

### SCAN

- Idea: Sweep back and forth, from one end of disk to the other, serving requests as you go
	- disk arm starts at one end of the disk, moves toward other end servicing requests until it arrives, where the head movement is reversed and servicing continues
	- aka Elevator Algorithm

### C-SCAN

- Idea: Only sweep in ONE direction
	- when it reaches the other end, head immediately returns to the beginning of the disk, without servicing any requests on the return trip
- Provides more uniform wait time than SCAN
- Treats the cylinders as a circular list that wraps around from the last cylinder to the first one

### C-LOOK

- Idea: Arm only goes as far as the last request in each direction, then reverse direction immediately, without first going all the way to the end of the disk
	- LOOK: a version of SCAN
	- C-LOOK: a version of C-SCAN

### Work Conservation

- Work conserving schedulers always try to do I/O if there's I/O to be done
- Sometimes, it's better to wait (delay) instead if you anticipate another request will appear nearby
- Such non-work-conserving schedulers are called anticipatory schedulers

### CFQ

- Completely fair queueing
- Queue for each process
- Do weighted round-robin among queues, with sliced time proportional to priority
- Optimize order within queue
- Yield slice only if idle for a given time (anticipation)

## Flash-based SSD Introduction

- Hold charge in cells - no moving mechanical parts
- Inherently parallel
- No seeking
- Smaller Capacity, Faster Accesses

- 400MB to 7000MB/s
- Read: 10-50 us
- Program: 200-500us
- Erase: 2ms

![[Pasted image 20240630211545.png]]

### SLC - Single-Level Cell

![[Pasted image 20240630211624.png]]

![[Pasted image 20240630211631.png]]

![[Pasted image 20240630211637.png]]

### MLC: Multi-Level Cell

![[Pasted image 20240630211705.png]]

![[Pasted image 20240630211721.png]]

### SLC vs. MLC

![[Pasted image 20240630211733.png]]

### Wearout

- Problem: flash cells wear out after being erased too many times
- MLC: ~10K times
- SLC: ~100K times
- Usage strategy: wear leveling
	- prevents some cells from being worn-out while others are still fresh

## SSD Internal Design

![[Pasted image 20240630211925.png]]

![[Pasted image 20240630212008.png]]

### Flash Writes

- Writing 0's: fast, fine-grained, can be per page., "Program"
- Writing 1's: slow, coarse-grained, must be per block, "Erase"
- Flash can only 'write' into clean pages (containing only 1's), doesn't support in-place overwrite

![[Pasted image 20240630212641.png]]

## Systems and FTL for SSD

### Traditional File System

![[Pasted image 20240630213002.png]]

Doesn't work with flash b/c it doesn't support in-place overwriting

### Traditional Flash APIs

![[Pasted image 20240630213109.png]]

### Write Amplification Issue

- Random writes are expensive - writing one 4KB page may cause reading, erasing, and programming a whole 256KB block

### Flash Translation Layer

- Add an address translation layer between upper-level file system and lower-level flash
	- translate logical device addresses to physical addresses
	- convert in-place write into append-write
	- essentially, a virtualization and optimization layer

![[Pasted image 20240630213439.png]]

![[Pasted image 20240630213502.png]]

![[Pasted image 20240630213529.png]]

![[Pasted image 20240630213541.png]]

![[Pasted image 20240630213555.png]]

- Usually implemented in flash device's firmware
- mapping is stored in SRAM
- physical pages can be in three states: free, valid, invalid
- Free: cleaned
- Valid: programmed
- Invalid: overwritten

### Free Space Reclaiming

- Some blocks may have partial valid data
- What if all pages in a block are obsolete?
- What if every block is partially valid? Cleaning:
	- occasionally move valid pages to the same block
	- erase the old block - now available for writing
- Which blocks to select for cleaning?
	- cleaning efficiency: fraction of obsolete pages

### Wear Leveling

- What happens if a block is erased again and again?
- Goal: Spread the erasures across all blocks uniformly
- Approach 1: Measure the wear level of each block, and avoid cleaning the most worn-out block
	- can be done periodically, when wear imbalance becomes high, or randomly
- Approach 2: Use a weighted measure for picking cleaning candidate
	- a function of cleaning efficiency and wear level




---
# *References*