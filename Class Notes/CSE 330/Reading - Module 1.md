202405211913
Meta Tags: #class
Tags: [[OS]]

# Reading - Module 1

## 1-1 What operating systems do

>[!info] operating system
>Acts as an intermediary between the user of a computer and the computer hardware. The **purpose** of an operating system is to provide an environment in which a user can execute programs in a *convenient* and *efficient* manner.

**Organization/Architecture of computer hardware:**
- CPU
- memory
- I/O devices
- storage

>A fundamental responsibility of an operating system is to allocate the above resources to programs.

![[Pasted image 20240521192617.png]]
*four components of a computer system*

- **hardware:** provides basic computing resources for the system
- **application programs:** define the ways in which these computing resources are used to solve users' computing problems
- **operating system:** controls the hardware and coordinates its use among the various application programs for the various users; provides an **environment** for programs to work in

### User View

- user view varies according to the interface being used:
	- laptop
	- PC with monitor, keyboard, mouse
	- mobile phones
- OS is designed mostly for **ease of use**, some things for performance and security and none for **resource utilization**.
- Some computers have little to no user view (embedded computers in home devices/automobiles)

### System View

- OSs as a **resource allocator**, maximizing efficiency and minimizing errors. A **control program** that manages the execution of user programs and the utilization of I/O devices.

### Defining operating systems

>Operating systems exist because they offer a reasonable way to solve the problem of creating a usable computing system; they are simply a pieces of software that have the common operations that application programs need to utilize hardware and I/O devices.

The operating system is the **one program running at all times on the computer** - usually called the ***kernel***. 
- **system programs:** associated with the OS but are not necessarily part of the kernel
- **application programs:** all programs not associated with the operation of the system

Operating system is inclusive of:
- the kernel that is loaded at boot time
- middleware
- device drivers
- kernel functions loaded at run time
- system programs related to the operation of the system

Is not part of the firmware or hardware logic.

>[!info] middleware
>A set of software frameworks that provide additional services to application developers.

## 1-2 Computer-system organization

![[Pasted image 20240521194546.png]]

- **Bus:** provides access between components and shared memory
- device controller -> disk controller, USB, graphics adapter for monitor
	- maintain some local buffer storage and special-purpose registers
	- sends info to the CPU via the common bus translating through the **device driver**.

### Interrupts

1. Program tells device driver to do some action
2. device driver loads registers in the device controller
3. Controller uses these registers to determine what action to take
4. Controller starts transferring data from device to local buffer
5. **Controller informs driver when action is complete**
6. Driver than gives the wheel to the OS, and further behavior depends on the program

The controller informs the device driver using an **interrupt**.

The interrupt is a signal sent by hardware to the CPU, usually via the system bus. When this interrupt is received, the CPU stops what it is doing and immediately transfers execution to a fixed location, which usually contains the starting address of the ISR. 

- table of pointers to interrupt routines - **interrupt vector**
	- stored in low memory, used to provide speed
	- indexed by a unique number to provide the address of the ISR for the interrupting device
- interrupt architecture must also save the state information
#### Implementation

- CPU hardware has a wire called the **interrupt-request line** that the CPU senses after executing every instruction
- When signal is detected, CPU reads the interrupt number and jumps to the **interrupt-handler routine** by using the interrupt number on the interrupt vector
- interrupt handler saves the state, determines the cause of the interrupts, performs the necessary processing, performs a state restore, and instructs the CPU to return to the prior state.
- device controller **raises** an interrupt by asserting a signal on the interrupt request line
- CPU **catches** the interrupt and **dispatches** it to the handler
- handler **clears** the interrupt by servicing the device

1. Still needs the ability to disable interrupts during critical processing
2. Needs an efficient way to dispatch to the proper interrupt handler for a device
3. Needs multilevel interrupts, so that the operating system can distinguish between high- and low-priority interrupts

These are provided by the CPU and **interrupt-controller hardware**.

Most CPUs have two interrupt request lines:
- **nonmaskable interrupt:** reserved for events such as unrecoverable memory errors
- **maskable:** can be turned off by the CPU before execution of critical instruction sequences that must not be interrupted
- **interrupt chaining:** "chained dictionary" approach to more values (ISR addresses) than keys (interrupt vector slots)

### Storage Structure

- The CPU can load instructions only from memory, so any programs must first be loaded into memory to run.
- General-purpose computers run most of their programs from RAM (main memory), which is commonly implemented with DRAM.
- The first program to run on power-on is a **bootstrap program**, which loads the OS. This has to be stored in memory like EEPROM or other forms of **firmware** - storage that is infrequently written to and is nonvolatile.
- **word:** a given computer architecture's native unit of data

Typical instruction-execution cycle for von Neumann architecture:
1. fetch instruction from memory and store it in the **instruction register**.
2. Decode the instruction and fetch operands from memory/store them depending on the instruction
3. After instruction execution, result may be stored back into memory.

**Secondary storage**: hard-disk drives (HDDs) and nonvolatile memory (NVM) devices
**tertiary storage:** only used for special storing purposes

![[Pasted image 20240521201454.png]]

Volatile storage will be referred to simply as **memory**.

Nonvolatile storage will be referred to as **NVS**.
- **Mechanical**: HDDs, optical disks, holographic storage, magnetic tape
- **Electrical:** flash, FRAM, NRAM, SSD. Referred to as **NVM**.

### I/O Structure

**direct memory access:** when a device directly transfers data to main memory rather than through the CPU. Interrupt still goes to CPU though.

## 1-4 Operating-system operations

>[!note] bootstrap program
>- initializes all aspects of the system, from CPU registers to device controllers to memory contents
>- must know how to load the OS and how to start executing that system
>- must locate the operating-system kernel and load it into memory

- **system daemons:** system programs that are loaded into memory at boot time.
- Another form of interrupt is a **trap**/**exception**, which is a software-generated interrupt caused by either an error or by a specific request from a user program that an OS service be performed by executing a **system call**.

### Multiprogramming and Multitasking

Users typically want to run more than one program at a time; **multiprogramming** increases CPU utilization as well as user satisfaction by organizing programs so that the CPU always has one to execute. In a multiprogrammed system, a program in execution is termed a **process**.
- the OS keeps several processes in memory simultaneously; while one process waits for a task to finish, the CPU switches to another process, and so on and so forth

**Multitasking** is a logical extension of multiprogramming. The CPU executes multiple processes by switching among them very frequently, providing the user with a fast **response time**.

>[!info] CPU scheduling
>how the system chooses which process will run next.

**virtual memory:** a technique that allows the execution of a process that is not completely in memory. Enables users to run programs that are larger than actual **physical memory**. It also abstracts main memory into a large, uniform array of storage, separating **logical memory** as viewed by the user from physical memory.

### Dual-mode and multimode operation

>To ensure proper execution, we must be able to distinguish between executing OS code and user-defined code.

So we use **modes** of operation: **user mode** and **kernel mode**. A bit, called the **mode bit**, is added to the hardware of the computer to indicate the current mode: kernel (0) or user (1).

When the computer is executing on behalf of a user application, the system is in user mode. However, when the same application requests a service from the OS, the system must transition form user to kernel mode to fulfill the request.

![[Pasted image 20240521203300.png]]

**privileged instructions:** machine instructions that may cause harm, and can only be executed in kernel mode

maybe see **protection rings, virtual machine manager**

### Timer

Used to ensure that the OS maintains control over the CPU. Sends interrupts to transfer control automatically to the OS (think not responding error message)

## 1-5 Resource Management

### Process Management

*process* - instance of a program in execution

A program by itself is **not** a process. A program is a **passive** entity, like the contents of a file store on disk, whereas a process is an **active** entity. A single-threaded process has one **program counter** specifying the next instruction to execute. The execution must be sequential; further, at any time, one instruction at most is executed on behalf of the process. 

process management OS responsibilities:
- Creating and deleting both user and system processes
- Scheduling processes and threads on the CPUs
- Suspending and resuming processes
- Providing mechanisms for process synchronization
- Providing mechanisms for process communication

### Memory Management

- Keeping track of which parts of memory are currently being used and which process is using them
- Allocating and deallocating memory space as needed
- Deciding which processes (or parts of processes) and data to move into and out of memory

### File-system Management

**file**: an abstracted logical storage unit. A collection of related information defined by its creator. Commonly, they represent programs and data. 

Data files may be numeric, alphabetic, alphanumeric, or binary. Files may be free-form (for example, text files), or they may be formatted rigidly (for example, fixed fields such as an mp3 music file). Clearly, the concept of a file is an extremely general one.

- Creating and deleting files
- Creating and deleting directories to organize files
- Supporting primitives for manipulating files and directories
- Mapping files onto mass storage
- Backing up files on stable (nonvolatile) storage media

### Mass-storage Management

- Mounting and unmounting
- Free-space management
- Storage allocation
- Disk scheduling
- Partitioning
- Protection

### Cache Management

>[!info] caching
>Putting often-used information into the cache temporarily to use it later.

![[Pasted image 20240521204835.png]]

- **cache coherency**: when all values of a specific variable should be the same across all caches

### I/O System Management

- A memory-management component that includes buffering, caching, and spooling
- A general device-driver interface
- Drivers for specific hardware devices

# Extra Reading

## 1-3 Computer-System Architecture

### Single-Processor Systems

**Core:** the component that executes instructions and contains registers for storing data locally.

- main CPU with its core is capable of executing a general-purpose instruction set, including instructions from processes.
- special-purpose processor run a limited instruction set and don't run processes. OS cannot communicate with these; they run autonomously.

Single processor systems have only one general-purpose CPU w/ a single processing core. These are rare in contemporary times.

### Multiprocessor Systems

- 2 or more processors, each with a single-core CPU. $N$ processors $\neq$ $N$ times the speed (in throughput terms). This is because a certain amount of overhead is incurred in keeping all the parts working correctly.
- Most common multiprocessor systems use **symmetric multiprocessing** (SMP), in which each peer CPU processor performs all tasks, including OS functions and user processes. 

![[Pasted image 20240602035551.png]]

- many processes can run simultaneously
- since the CPUs are separate, one may be sitting idle while another is overloaded; this type of inefficiency can be avoided if the processors share certain data structures.

In modern times: **multiprocessor** includes **multicore**.

- dual-core design, each core has their own local cache, often known as level 1/L1 cache. There is level 2/L2 cache that is local to the chip but shared by the cores:

![[Pasted image 20240602035955.png]]

- $N$ cores appears to OS as $N$ standard CPUs. 

>[!info] Definitions of computer system components
>- **CPU**—The hardware that executes instructions.
>- **Processor**—A physical chip that contains one or more CPUs.
>- **Core**—The basic computation unit of the CPU.
>- **Multicore**—Including multiple computing cores on the same CPU.
>- **Multiprocessor**—Including multiple processors.

- Once we add too many CPUs, contention for the system bus becomes a bottleneck.
- An alternative approach (**non-uniform memory access/NUMA**) is to provide each CPU/group of CPUs with its own local memory that is accessed via a small, fast local bus. The CPUs are connected by a **shared system interconnect**, so that all CPUs share one physical address space.

![[Pasted image 20240602040823.png]]

A potential drawback of NUMA is increased latency when a CPU must access remote memory across the system interconnect. OSs can minimize this penalty through careful CPU scheduling and memory management.

**Blade servers** are systems in which multiple processor boards, I/O boards, and networking boards are placed in the same chassis.

### Clustered Systems

Gathers together multiple CPUs. Differ from multiprocessor in that they are composed of 2 or more individual systems - or nodes - joined together; each node is typically a multicore system. These systems are considered **loosely coupled**. 

Clustering is usually used to provide reliability through redundancy.

The ability to continue providing service proportional to the level of surviving hardware is called **graceful degradation**. Some systems go beyond this and are called **fault tolerant**, because they can suffer a failure of any single component and still continue operation.

Clustering can be structured asymmetrically or symmetrically. 
- asymmetric clustering - one machine is in **hot-standby mode** while the other is running the applications. The former does nothing but monitor the active server. If that server fails, the hot-standby host becomes the active server. 
- symmetric clustering - two or more hosts are running applications and are monitoring each other. This structure is more efficient, but it requires that more than one application be available to run.
Clustering can be used to provide **high-performance computing** through **parallelization**, which divides a program into separate components that run in parallel on individual cores in a computer or computer in a cluster.

Parallel clusters allow multiple hosts to access the same data on shared storage. Most OSs lack support for simultaneous data access by multiple hosts, so parallel clusters usually require the use of special versions of software and special releases of applications.

To provided this shared access, the system must also supply access control and locking to ensure that no conflicting operations occur through a **distributed lock manager** (DLM).

**storage-area networks** (SANs) - allow many systems to attach to a pool of storage. Applications/data can be stored on the SAN, and the cluster software can assign applications to any host attached to the SAN. 

![[Pasted image 20240602042303.png]]

## 1-6 Security and Protection

Mechanisms ensure that files, memory segments, CPU, and other resources can be operated on by only processes that have gained proper authorization from the OS.

**Protection**: any mechanism for controlling the access of processes or users to the resources defined by a computer system.

- can improve reliability by detecting latent errors at the interfaces between component subsystems
- provides a means to distinguish between authorized and unauthorized usage

**Security**: the mechanisms that defend a system from external and internal attacks.

- Both require the system to be able to distinguish among all its users. Most OSs maintain a list of user names and associated **user identifiers** (user IDs). Windows --> security ID (SID). Unique per user.
- When we want to distinguish among sets of users rather than individual users, we need to define a group name and the set of users belonging to that group. **group identifiers**.
- In the course of normal system use, the user ID and group ID for a user are sufficient. However, the user may need to **escalate privileges** to gain extra permissions for an activity.

## 1-7 Virtualization

A technology that allows us to abstract the hardware of a single computer into several different execution environments, creating the illusion that each separate environment is running on its own private computer.

Allows OSs to run as applications within other OSs.

Virtualization software is one member of a class that also includes **emulation**, which involves simulating computer hardware in software. Is typically used when the source CPU type is different from the target CPU type.

Emulation can be slow since machine-level instructions that run natively on the source system must be translated to the target system. Virtualization involves running another OS that is native to the same CPU.

**guest**: virtual machines
**host**: the non-virtual machine
**virtual machine manager (VMM):** VMware

![[Pasted image 20240602043905.png]]

## 1-8 Distributed Systems

A collection of physically separate, possibly heterogeneous computer systems that are networked to provide users with access to the various resources that the system maintains.

A **network** is a communication path between 2 or more systems. Networks vary by the protocols used, the distances between nodes, and the transport media. **TCP/IP** is the most common network protocol. 

Networks are characterized based on the distances between their nodes. A local-area network (LAN) connects computers within a room/building/campus. A wide-area network (WAN) usually links buildings/cities/countries.

A **network operating system** is an OS that provides features such as file sharing across the network, along with a communication scheme that allows different processes on different computers to exchange messages. These are aware of the network and available to communicate with other computers, but are still autonomous. Distributes OSs provide less autonomy; different computers communicate closely enough to provide the illusion that only a single OS controls the network.

## 1-9 Kernel Data Structures

### Lists, stacks, and queues

- array - simple data structure in which each element can be accessed directly
- list - represents a collection of data values as a sequence
- linked list - most common implementation of a list, where items are linked to one another.
	- singly linked - each item points to its successor
	- double linked - a given item can refer either to its predecessor or to its successor
	- circularly linked - the last element in the list refers to the first element, rather than to null
- stack - sequentially ordered data structure that uses the LIFO principle for adding/removing items. The operations for inserting/removing are push/pop. An OS commonly uses a stack when invoking function calls
- queue - sequentially ordered data structure that uses the FIFO principle. Queues are also often used in OSs, such as a job queue for a printer or CPU scheduling.
- tree - data structure that can be used to represent data hierarchically. 
	- general tree - parent may have an unlimited number of children
	- binary tree - parent may have at most two children
	- binary search tree - left children must be $\le$ right children
	- balanced binary search tree - ensures worst-case performance of $O(\log n)$.
- Hash function - takes data as input, performs numeric operation on data, and returns a numeric value. This value can then be used as an index into a table (typically an array) to quickly retrieve the data.
- hash collision - resolved by chaining
- hash map - associates key:value pairs using a hash function
- bitmap - a string of $n$ bits that can be used to represent the status of $n$ items. Space efficient. Example: disk blocks.





---
# *References*
![[Operating System Concepts - Abraham Silberschatz, Peter Bae.pdf]]