202406251840
Meta Tags: #class
Tags: [[OS]]

# Videos - Module 10

## Optimizing the Page Table Design

- Page tables are too big

### Naive Solution

- Reduce the granularity by increasing the page size 
- Less pages → smaller page table
- This causes internal fragmentation, however

![[Pasted image 20240625184530.png]]

Better approaches:

- Linear Inverted Page Table
- Hashed Inverted Page Table
- Multi-Level Page Table

### Linear Inverted Page Table

- **Idea:** instead of keeping one page table per process, the system keeps a single page table that has an entry for each physical frame of the system
- Each entry tells which process owns the page, and VPN to PFN translation

![[Pasted image 20240625184841.png]]

- Goal: use linear search to find the index i ( which is the PFN); inverted because a traditional page table indexes by VPN
- Pros - extreme memory savings
- Cons - a linear search is expensive

### Hashed Inverted Page Table

- For large address spaces, a hashed page table can be used, with the hash value being the VPN
- **Idea:**
	- A PTE contains a chain of elements hashing to the same location (to handle collisions) within PT
	- Each element has three fields: VPN, PFN, a pointer to the next element in the linked list
	- VPNs are compared in this chain searching for a match. If a match is found, the corresponding PFN is extracted

![[Pasted image 20240625185703.png]]

**Limitations:**
- The hash table may be unbalanced
	- some virtual addresses are frequently used, others are not
- Linear search in one slot has different performance due to the position differences
	- searching the linked list at different positions
- Rehash may cause a lot of unexpected risks
	- memory copying, moving, and locking

### Multi-level Page Table

**Idea:**
- Break the page table into pages (the entire page table is paged!)
- Only have pieces with >0 valid entries
	- Don't allocate the page of page table if the entire page of page-table entries is invalid

![[Pasted image 20240625190208.png]]

### Two-level Paging

- A logical address (32-bit machine with 4KB page size) is divided into:
	- a page number consisting of 20 bits
	- a page offset consisting of 12 bits
- A page table entry is 4 bytes
- Since the page table is paged, the page number is further divided into
	- $p_1$: a 10-bit page directory index
	- $p_2$: a 10-big page table index
- The logical address is as follows:

![[Pasted image 20240625190445.png]]

![[Pasted image 20240625190555.png]]

Problem: page directory may not fit in a page
Solution: split page directories into pages, use another page directory to refer to the original page directory pages

- better balances the searching speed, memory space efficiency, and dynamic extension capability

## Swapping - Go Beyond the Memory Limit

How to avoid wasting physical pages to hold rarely used virtual pages?

"swapping in" or "paging in"

![[Pasted image 20240625191055.png]]

How do we know if a page is still on the disk or already in physical memory?

### Present Bit

With each PTE a present is associated
- 1: in-memory; 0: out in disk

![[Pasted image 20240625191241.png]]

![[Pasted image 20240625191404.png]]

![[Pasted image 20240625191420.png]]

What if physical memory is full?

![[Pasted image 20240625191432.png]]

![[Pasted image 20240625191442.png]]

Why not leave the page on disk?

![[Pasted image 20240625191520.png]]

### Beyond the Physical Memory

- **Idea:** use the disk space as an extension of main memory
- Two ways of interaction between memory and disk
	- Demand Paging
	- Swapping

### Demand Paging

- Bring a page into memory only when it is needed (demanded)
	- Less I/O needed
	- Less memory needed
	- Faster response
	- Support more processes/users
- Page is needed → use the reference to page
	- if not in memory → must bring from disk

### Swapping

- allows the OS to support the illusion of a large virtual memory for multiprogramimng
	- multiple programs can run "at once"
	- better utilization
	- ease of use
- Demand paging vs. Swapping
	- On demand vs. Page replacement under memory pressure

![[Pasted image 20240625192001.png]]

- Part of disk space reserved for moving pages back and forth
	- swap pages out of memory
	- swap pages into memory from disk
- OS reads from and writes to the swap space at page-sized unit

### Address Translation Steps

1. Extract VPN from VA
2. Check TLB for VPN
3. if TLB hit:
	1. Build PA from PFN and offset
	2. Fetch PA from memory (expensive)
4. if TLB miss:
	1. Fetch PTE (expensive)
	2. if (!valid): exception segfault (expensive)
	3. else if (!present): exception pagefault (expensive)
	4. else: extract PFN, insert in TLB, retry

### Page Fault

- The act of accessing a page that isn't in physical memory
- OS is invoked to service the page fault
	- page fault handler
- Typically, PTE contains the page address on disk

**Page-Fault Handler:**

```
PFN = FindFreePage()
if (PFN == -1)
	PFN = EvictPage()       //depends
DiskRead(PTE.DiskAddr, PFN) //expensive
PTE.present = 1
PTE.PFN = PFN
retry instruction
```


![[Pasted image 20240625192839.png]]

**Impacts:**
- each page fault affects the system performance negatively:
	- the process experiencing the page fault will not be able to continue until the missing page is brought to main memory
	- The process will be blocked (moved to the waiting state)
	- Dealing with the page fault involves disk I/O
		- increased demand for the disk drive
		- increased waiting time for process experiencing page fault

### Memory as a Cache

As we increase the degree of multiprogramming, over-allocation of memory becomes a problem. What if we are unable to find a free frame at the time of the page fault?

OS chooses to page out one or more pages to make room for new page(s) OS is about to bring in
- the process to replace page(s) is called page replacement policy

OS keeps a small portion of memory free proactively
- High watermark (HW) and low watermark (LW)

When OS notices free memory is below LW (i.e., memory pressure)
- a background thread (i.e., swap/page daemon) starts running to free memory
- it evicts pages until there are HW pages available

![[Pasted image 20240625193320.png]]




---
# *References*