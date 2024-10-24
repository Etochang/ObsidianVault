202406292020
Meta Tags: #idea 
Tags:

# Videos - Module 11

## Why We Need Page Replacement Policies

### Major Steps of a Page Fault

![[Pasted image 20240629202129.png]]

### Page Replacement

- completes the separation between logical memory and physical memory
- impact on performance - if there are no free frames, two page transfers are needed at every page fault
- use modify (dirty) bit to reduce overhead of page transfers - only modified pages are written back to disk

**Formalizing the Problem:**
- Cache management: physical memory is a cache for virtual memory pages in the system
- Primary objective:
	- high performance
	- high efficiency
	- low cost
- Goal: minimize cache misses
	- to minimize number of times OS has to fetch a page from disk
	- maximize cache hits

### Average Memory Access Time

- AMAT is the metric to calculate the effective memory performance: 
$$AMAT = P_{hit} \cdot T_M + P_{miss} \cdot T_D$$
- $T_M$: cost of accessing memory
- $T_D$: cost of accessing disk
- $P_{hit}$: probability of finding data in cache
- $P_{miss}$: probability of not finding data in cache

### What To Do?

- Find a cache replacement policy that evicts the page that has the least influence on the future cache hit ratio
- Difficulty:
	- are we able to know the future?
	- how to define the least influence?
	- the cache replacement policy overhead?

## Replacement Policies

### FIFO

- Simplest page replacement algorithm
- Idea: items are evicted in the order they are inserted
- Implementation: FIFO queue holds identifiers of all the pages in memory
	- we replace the page at the head of the queue
	- when a page is brought into memory, it is inserted at the tail of the queue

Advantages:
- easy to implement, almost 0 implementation overhead
- effective for the workload that has some "cycling" or "repeating" patterns

Issue:
- the "oldest" page may be heavily used, and will be need to be brought back in the near future

Belady's Anomaly: more cache frames means more page faults for some access patterns.

### Random Replacement

Idea: picks a random page to replace
- simple to implement like FIFO
- no intelligence of preserving locality

Performance depends entirely on luck.

### Belady's Optimal

**OPT:**
- Idea: evict the page that will be accessed furthest in the future
- Assumption: we know about the future
- Impossible to implement in practice, but is extremely useful as a practical best-case baseline for comparison purposes.

### LRU

- Insight: use the recent past as an approximation of the near future (using history)
- Idea: evict the page that hasn't been used for the longest period of time

**LRU Stack Implementation**
- keep a stack of page numbers in a doubly linked list form
	- page referenced, move it to the top
	- requires quite a few pointers to be changed
	- no search required for replacement operation!

**LRU Hardware Support:**
- sophisticated hardware support may involve high overhead/cost
- some limited HW support is common:
	- Reference (or use ) bit
	- With each page associate a bit, initially set to 0. When the page is referenced, bit set to 1
	- By examining the reference bits, we can determine which pages have been used
	- we don't know the order of use, however
- Cheap approximation
	- useful for clock algorithm

### Clock Algorithm

![[Pasted image 20240629204844.png]]

![[Pasted image 20240629204900.png]]

![[Pasted image 20240629204912.png]]

![[Pasted image 20240629204925.png]]

![[Pasted image 20240629204947.png]]

![[Pasted image 20240629205020.png]]

![[Pasted image 20240629205038.png]]

![[Pasted image 20240629205054.png]]

## Workload Influence of Replacement Policies

![[Pasted image 20240629205859.png]]

![[Pasted image 20240629205912.png]]

![[Pasted image 20240629205923.png]]

### Thrashing

- High-paging activity: system spends more time paging than executing
- How can this happen?
	- OS observes low CPU utilization and increases the degree of multiprogramming
	- Global page-replacement algorithm is used and takes away frames belonging to other processes
	- But these processes need those pages, which causes page faults
	- Many processes join the waiting queue for the paging device, CPU utilization further decreases
	- OS introduces new processes, continuing the cycle

![[Pasted image 20240629210109.png]]

How to avoid?
- Earlier OSs did admission control to only run a subset of processes
- Current OSs just kill memory-intensive processes

### Demand Paging and Thrashing

- Why does demand paging work?
	- process migrates from one locality to another
	- localities may overlap
- Thrashing occurs when the size of locality or working set size is greater than total memory size
- WSS: number of unique items that are accessed

### Impact of Program Structure of Memory Performance

![[Pasted image 20240629210447.png]]





---
# *References*