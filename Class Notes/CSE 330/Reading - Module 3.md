202406032050
Meta Tags: #class
Tags: [[OS]]

# Reading - Module 3

>3.1-3.6

## 3.1 Process concept

>A *process* is a program in execution. A process will need certain resources - such as CPU time, memory, files, and I/O devices - to accomplish its task. These resources are typically allocated to the process while it is executing.
>
>A process is the unit of work in most systems. Systems consist of a collection of processes: OS processes execute system code, and user processes execute user code. All these processes may execute concurrently.
>
>Modern OSs support processes having multiple *threads* of control. On systems with multiple hardware processing cores, these threads can run in parallel.
>
>One of the most important aspects of an OS is how it schedules threads onto available processing cores. Several choices for designing CPU schedulers are available to programmers.

### Process Concept

CPU activities are processes.

A process is a program in execution. The status of the current activity of a process is represented by the value of the **program counter** and the contents of the processor's registers. The memory layout of a process is typically divided into multiple sections:
- Text section - the executable code
- Data section - global variables
- Heap section - memory that is dynamically allocated during program run time
- Stack section - temporary data storage when invoking functions

Each time a function is called, an **activation record** containing function parameters, local variables, and the return address is pushed onto the stack; when control is returned from the function, the activation record is popped from the stack. Similarly, the heap will grow as memory is dynamically allocated, and will shrink when memory is returned to the system. Although the stack and heap sections grow toward one another, the OS must ensure they do not overlap.

A program by itself is **not** a process. A program is a **passive** entity, such as a file containing a list of instructions stored on disk (often called an **executable file**). In contrast, a process is an **active** entity, with a program counter specifying the next instruction to execute and a set of associated resources. A program becomes a process when an executable file is loaded into memory.

Note that a process itself can be an execution environment for other code. The Java programming environment provides a good example.

### Process State

As a process executes, it changes **state**. The state is defined in part by the current activity of that process:
- **New** - the process is being created
- **Running** - instructions are being executed
- **Waiting** - the process is waiting for some event to occur
- **Ready** - the process is waiting to be assigned to a processor
- **Terminated** - the process has finished execution

### Process Control Block

Each process is represented in the OS by a **process control block** (PCB) - also called a **task control block**. It contains many pieces of info such as:
- **Process state**
- **Program counter** - indicates the address of the next instruction to be executed for this process
- **CPU registers** - accumulators, index registers, stack pointers, and general-purpose registers. Need to be saved when an interrupt occurs
- **CPU-scheduling info** - includes a process priority, pointers to scheduling queues, and other parameters
- **Memory-management info** - value of the base and limit registers and the page/segment tables depending on the memory system used by the OS
- **Accounting info:** the amount of CPU and real time used, time limits, account numbers, job or process numbers, etc.
- **I/O status info:** list of I/O devices allocated to the process, a list of open files, and so on.

### Threads

'subprocesses' - subunits of processes

## 3-2 Process Scheduling

- The objective of multiprogramming is to maximize CPU utilization by having a process running at all times
- The objective of time sharing is to switch a CPU core among processes so frequently that users can interact with each program while it is running
- To meet these objectives, the **process scheduler** selects an available process for execution on a core. Each core can run one process at a time.
- The number of processes currently in memory is known as the **degree of multiprogramming**.
- In general, most processes can be described as:
	- **I/O-bound** - spends more of its time doing I/O than it spends doing computations
	- **CPU-bound** - generates I/O requests infrequently, using more of its time doing computations

### Scheduling Queues

As processes enter the system, they are put into a **ready queue**, where they are ready and waiting to execute on a core. This queue is generally a linked list; a ready-queue header contains pointers to the first PCB in the list, and each PCB includes a pointer field that points to the next PCB in the ready queue.

Processors that are waiting for a certain event to occur are placed in a **wait queue**.

![[Pasted image 20240603211807.png]]

![[Pasted image 20240603211849.png]]

A common representation of process scheduling is the **queueing diagram** above. 
- A new process is initially put in the ready queue until it is dispatched to the a CPU core.
- One of the following events happens
	- I/O request
	- create a child process
	- interrupt or having time slice expire
- Then the process is put in a wait queue until it reaches the ready queue after an event happens

### CPU Scheduling

The role of the **CPU Scheduler** is to select from among the processes that are in the ready queue and allocate a CPU core to one of them. The CPU scheduler must select a new process for the CPU frequently. 

Some OSs have an intermediate form of scheduling known as **swapping**, where the key idea is that sometimes it can be advantageous to remove a process from memory and thus reduce the degree of multiprogramming.

### Context Switch

When an interrupt occurs, the system needs to save the current **context** of the process running on the CPU core so that it can restore it when its processing is done. The context is represented in the PCB of the process.

Generically we perform a **state save** of the current state of the CPU core, be it in kernel or user mode, and then a **state restore** to resume operations.

Switching the CPU core to another process, performing a state save of the current process and a state restore of a different one is known as a **context switch**.

Context-switch times are highly dependent on hardware support.

## 3-3 Operations on processes

### Process Creation

- tree of processes
- Most OSs identify processes according to a unique process identifier (or pid), which is typically an integer.
![[Pasted image 20240603222159.png]]

- In general, when a process creates a child process, that child process will need certain resources (CPU time, memory, files, I/O devices) to accomplish its task
- A child process may get resources directly from the OS or it may be constrained to a subset of the resources of the parent process
- The parent may have to partition its resources among its children, or it may be able to share some resources among several of its children. Restricting a child process to a subset of the parent's resources prevents any process from overloading the system by creating too many child processes
- In addition to supplying various physical and logical resources, the parent process may pass along initialization data to the child process
- When a process creates a new process, 2 possibilities for execution exist:
	1.  The parent continues to execute concurrently with its children
	2. The parent waits until some or all of its children have terminated
- There are also 2 address-space possibilities for the new process:
	1. The child process is a duplicate of the parent process (it has the same program and data as the parent)
	2. The child process has a new program loaded into it

### Process Termination

A process terminates when it finished executing its final statement and asks the OS to delete it by using the `exit()` syscall. At that point, the process may return a status value to its waiting parent process (via the `wait()` syscall). All the resources of the process are deallocated and reclaimed by the OS.

Termination can also be a result of another process via an appropriate system call, or a user/misbehaving application arbitrarily doing so. Note that a parent needs to know the identities of its children if it is to terminate them. Thus, when one process creates a new process, the identity of the newly created process is passed to the parent

Reasons for termination:
- The child has exceeded its usage of some of the resources that it has been allocated
- The task assigned to the child is no longer required
- The parent is exiting and the OS doesn't allow a child to continue if its parent terminates
	- Referred to as **cascading termination**.
- A parent process may wait for the termination of a child process by using the `wait()` system call. The `wait()` system call is passed a parameter that allows the parent to obtain the exit status of the child. This syscall also return the pid of the terminated child so that the parent can tell which of its children has terminated.
- When a process terminates, its resources are deallocated by the OS. However, its entry in the process table must remain there until the parent calls `wait()`, because the process table contains the process's exit status. A process that has terminated but whose parent hasn't yet called `wait()` is known as a **zombie** process.
- Once the parent calls `wait()`, the pid of the zombie process and its entry in the process table are released.
- If a parent terminates before invoking `wait()`, the child processes become orphans.

## 3-4 Interprocess Communication

Processes executing concurrently in the OS may be either:
- independent - if it doesn't share data with any other processes executing in the system
- cooperating - if it can affect/be affected by the other processes executing in the system

Reasons for providing an environment that allows process cooperation:
- Information sharing - since several applications may be interested in the same piece of info
- Computation speedup - parallel subtasks: needs multiple processing cores
- Modularity - dividing system functions into separate processes or threads

Cooperating processes require an **interprocess communication** (IPC) mechanisms that will allow them to exchange data.

Two models of interprocess communication:
- Shared memory - a region of memory is shared by the cooperating processes
	- can be faster than message passing since message passing is typically implemented using syscalls and thus requires more kernel intervention
	- syscalls are only required here to establish shared-memory regions; once they are established, all accesses are treated as routine memory accesses.
- message passing - communication takes place by means of messages exchange between the cooperating processes
	- useful for exchanging smaller amounts of data, because no conflicts need be avoided
	- easier to implement in a distributed system than shared memory

![[Pasted image 20240603224659.png]]

## 3-5 IPC in shared-memory systems

- requires communicating processes to establish a region of shared memory
- this region usually resides in the address space of the process creating the shared-memory segment; other processes that wish to communicate using it must attach it to their address space
- Normally, the OS tries to prevent one process from accessing another process's memory; shared memory requires that 2 or more processes agree to remove this restriction
- producer-consumer problem - a producer process produces information that is consumed by a consumer process
- to allow producer and consumer processes to run concurrently, we must have available a buffer of items that can be filled by the producer and emptied by the consumer. This buffer will reside in a region of memory that is shared by the producer and consumer processes.
- The producer and consumer must be synchronized, so that the consumer doesn't try to consume an item that hasn't yet been produced.
- Two types of buffers can be used:
	- unbounded buffer - places no practical limit on the size of the buffer; the consumer may have to wait for new items, but the producer can always produce new items
	- bounded buffer - fixed buffer size; consumer must wait if the buffer is empty, producer must wait if it is full

## 3-6 IPC in message-passing systems

- Message passing provides a mechanism to allow processes to communicate and to synchronize their actions w/o sharing the same address space. It is particularly useful in a distributed environment, where the communicating processes may reside on different computers connected by a network.
- A message-passing facility provides at least 2 operations:
	- `send(message)`
	- `receive(message)`
- messages sent by a process can be either fixed or variable in size. If only fixed-sized messages can be sent, the system-level implementation is straightforward. This restriction, however, makes the task of programming more difficult. Conversely, variable-sized messages are the opposite.
- If processes P and Q want to communication, they must send messages to and receive messages from each other: a communication link must exist between them logically:
	- direct or indirect communication
	- synchronous or asynchronous communication
	- automatic or explicit buffering

### Naming

Processes that want to communicate must have a way to refer to each other:
- direct communication - each process that wants to communicate must explicitly name the recipient or sender of the communication:
	- `send(P, message)` - send a message to P
	- `receive(Q, message)` - receive a message from Q
- A communication link in this scheme has the following properties:
	- it is established automatically between every pair of processes that want to communicate. The processes need to know only each other's identity to do so.
	- One link is associated with exactly two processes
- This scheme exhibits **symmetry** in addressing; that is, both the sender process and the receiver process must name the other to communicate. An example of asymmetry:
	- `send(P, message)` - send a message to P
	- `receive(id, message)` - receive a message from any process. The variable id is set to the name of the process with which communication has taken place
- Disadvantages:
	- limited modularity of the resulting process definitions
	- changing the id of a process may necessitate examining all other process definitions
	- all references to the old id must be found, so that they can be modified to the new identifier
- in general any such **hard-coding** techniques, where ids must be explicitly stated, are less desirable than techniques involving indirection.
- **indirect communication** - messages are sent to and received from **mailboxes**, or **ports**. A mailbox can be viewed abstractly as an object into which messages can be placed by processes and from which messages can be removed. Each mailbox has a unique identification - for example, POSIX message queues use an in value to identify a mailbox
- A process can communication with another process via a number of different mailboxes, but 2 processes can communicate only if they have a shared mailbox.
	- `send(A, message)` send a message to mailbox A
	- `receive(A, message)` receive a message from mailbox A
- In this scheme, a communication link has the following properties:
	- A link is established between a pair of processes only if both members of the pair have a shared mailbox
	- A link may be associated with more than two processes
	- Between each pair of communication processes, a number of different links may exist, with each link corresponding to one mailbox.
- If 2 or more processes `receive()` the same message in the mailbox:
	- allow a link to be associated with 2 processes at most
	- allow at most one process at a time to execute a `receive()`
	- allow the system to select arbitrarily which process will receive the message
- A mailbox may be owned either by a process or by the OS. If the mailbox is owned by the former (the mailbox is part of the address space of the process), then we distinguish between the owner (which can only receive messages through this mailbox) and the user (which can only send messages to the mailbox). Since each mailbox has a unique owner, there can be no confusion about which process should receive a message sent to this mailbox. 
- When a process that owns a mailbox terminates, the mailbox disappears. Any process that subsequently sends a message to this mailbox must be notified that it no longer exists.
- A mailbox owned by the OS has an existence of its own. The OS then must provide a mechanism that allows a process to do the following:
	- Create a new mailbox
	- Send a receive messages through the mailbox
	- delete a mailbox
- The process that creates a new mailbox is that mailbox's owner by default; initially, the owner is the only process that can receive messages through this mailbox.
- This ownership and receiving privilege may be passed to other processes through appropriate system calls. (This could result in multiple receivers for each mailbox)

### Synchronization

Message passing may be either:
- blocking (synchronous):
	- send - the sending process is blocked until the message is received by the receiving process or by the mailbox
	- receive - the receiver blocks until a message is available
- nonblocking (asynchronous)
	- send - the sending process sends the message and resumes operation
	- receive - the receiver retrieves either a valid message or null

### Buffering

- messages exchanged by communicating processes reside in a temporary queue. Implementations:
	- Zero capacity: the queue has a max length of 0; thus, the link cannot have any messages waiting in it. In this case, the sender must block until the recipient receives the message
	- Bounded capacity: the queue has finite length $n$; thus, at most $n$ messages can reside in it. If the queue isn't full when a new message is sent, the message is placed in the queue, and the sender can continue execution w/o waiting. The link's capacity is finite, however, if the link is full, the sender must block until space is available
	- Unbounded capacity: The queue's length is potentially infinite; thus, any number of messages can wait in it. The sender never blocks.


---
# *References*
![[Operating System Concepts - Abraham Silberschatz, Peter Bae.pdf]]