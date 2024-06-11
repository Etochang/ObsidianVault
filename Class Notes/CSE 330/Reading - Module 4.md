202406040326
Meta Tags: #class
Tags: [[OS]]

# Reading - Module 4

>4.1, 4.2, 4.3, 4.7

## 4-1 Overview

### Introduction

Virtually all modern OSs provide features enabling a process to contain multiple threads of control.

### Overview

A thread is a basic unit of CPU utilization; it comprises a thread ID, a program counter (PC), a register set, and a stack. It shares w/ other threads belonging to the same process its code section, data section, and other OS resources, such as open files and signals.

A traditional process has a single thread of control. If a process has multiple threads of control, it can perform more than one task at a time.

![[Pasted image 20240604033216.png]]

### Motivation

In certain situations, a single application may be required to perform several similar tasks. For example, a web server with many clients concurrently accessing it.

One solution is to have the server run as a single process that accepts requests. When the server receives a request, it creates a separate process to service that request. However, process creation is time consuming and resource intensive. It is generally more efficient to use one process that contains multiple threads.

![[Pasted image 20240604033704.png]]

Most OS kernels are also multithreaded. 

### Benefits

1. **Responsiveness** - multithreading an interactive application may allow a program to continue running even if part of it is blocked/is performing a length operation. Especially useful in designing user interfaces.
2. **Resource sharing** - processes can share resources only through techniques such as shared memory and message passing. Such techniques must be explicitly arranged by the programmer. However, threads share the memory and the resources of the process to which they belong by default.
3. **Economy** - allocating memory and resources for process creation is costly. Also, context switching is typically faster between threads than between processes
4. **Scalability** - a single-threaded process can run on only one processor, regardless of how many are available. Threads can run parallel on different processing cores.

## 4-2 Multicore programming

**multicore** - multiple computing cores on a single processing chip where each core appears as a separate CPU to the OS.

- On a system w/ a single computing core, concurrency merely means that the execution of threads will be interleaved over time.
- On a system w/ multiple cores, concurrency means that some threads can run in parallel
- There is a distinction between **concurrency** and **parallelism**

### Programming Challenges

1. **Identifying tasks** - involves examining applications to find areas that can be divided into separate, concurrent tasks. Ideally, tasks are independent of one another and thus can run in parallel.
2. **Balance** - while identifying tasks that can run in parallel, programmers must also ensure that the tasks perform equal work of equal value. Using a separate core to run a insignificant task may not be worth the cost.
3. **Data splitting** - just as applications are divided into separate tasks, the data accessed and manipulated by the tasks must be divided to run on separate cores
4. **Data dependency** - the data accessed by the tasks must be examined for dependencies between two or more tasks. Programmers must ensure that dependent tasks are synchronized to accommodate data dependency.
5. **Testing/Debugging** - when a program is running in parallel, many different execution paths are possible, thus making testing/debugging inherently more difficult.

>[!info] Amdahl's law
>A formula that identifies potential performance gains from adding additional computing cores to an application that has both serial (nonparallel) and parallel components. If $S$ is the portion of the application that must be performed serially on a system with $N$ processing cores, the formula appears as follows:
>$$speedup \le \frac{1}{S + \frac{1-S}{N}}$$
>The fundamental principle is that the serial portion of an application can have a disproportionate effect on the performance we gain by adding additional computing cores.

### Types of Parallelism

- **Data parallelism** - focuses on distributing subsets of the same data across multiple cores and performing the same operation on each core.
- **Task parallelism** - involves distributing not data but tasks (threads) across multiple computing cores. Each thread is performing a unique operation. Different threads may be operating on the same data, or they may be operating on different data.

![[Pasted image 20240604035309.png]]

## 4-3 Multithreading models

Support for threads may be provided either at the user level, for **user threads**, or by the kernel, for **kernel threads**. The former are supported above the kernel and are managed w/o kernel support, whereas the latter are managed directly by the OS.

![[Pasted image 20240604035611.png]]

### Many-to-one model

Maps many user threads to one kernel thread. Thread management is done by the thread library in user space, so it is efficient. However, the entire process will block if a thread makes a blocking system call. Also, because only one thread can access the kernel at a time, multiple threads are unable to run in parallel on multicore systems.

Very few systems continue to use the model because of its inability to take advantage of multiple processing cores.

![[Pasted image 20240604035758.png]]

### One-to-one model

Maps each user thread to a kernel thread. It provides more concurrency than the many-to-one model by allowing another thread to run when a thread makes a blocking system call. It also allows multiple threads to run in parallel on multiprocessors. 

The only drawback to this model is that creating a user thread requires creating the corresponding kernel thread, and a large number of kernel threads may burden the performance of the system.

![[Pasted image 20240604035923.png]]

### Many-to-many model

MUXs many user-level threads to a smaller or equal number of kernel threads. The number of kernel threads may be specific to either a particular application or a particular machine.

While the many-to-one model doesn't result in parallelism and the one-to-one model results in limited threads within an application, the many-to-many model suffers from neither of these shortcomings.

![[Pasted image 20240604040220.png]]

One variation on the many-to-many model still multiplexes many user-level threads to a smaller or equal number of kernel threads, but also allows a user-level thread to be bound to a kernel thread, the **two-level model**.

![[Pasted image 20240604040228.png]]

- It is difficult to implement. IN addition, with an increasing number of processing cores appearing on most systems, limiting the number of kernel threads has become less important. 

## 4-7 OS examples

### Windows threads

A Windows application runs as a separate process, and each process may contain one or more threads. Additionally, Windows uses the one-to-one model.

The general components of a thread include:
- A thread ID uniquely identifying the thread
- A register set representing the status of the processor
- A program counter
- A user stack, employed when the thread is running in user model, and a kernel stack, employed when the thread is running in kernel mode
- A private storage area used by various run-time libraries and dynamic link libraries (DLLs)

The register set, stacks, and private storage area are known as the **context** of the thread.

The primary data structure of a thread include:
- ETHREAD - executive thread block
- KTHREAD - kernel thread block
- TEB - thread environment block

The key component of the ETHREAD include a pointer to the process to which the thread belongs and the address of the routing in which the thread starts control. The ETHREAD also contains a pointer to the corresponding KTHREAD.

The KTHREAD includes scheduling and synchronization info for the thread. In addition, the KTHREAD includes the kernel stack (used when the thread is running in kernel mode) and a pointer to the TEB.

The ETHREAD and KTHREAD exist entirely in kernel space; this means that only the kernel can access them. The TEB is a user-space data structure that is accessed when the thread is running in user mode. The TEB contains the thread identifier, a user-mode stack, and an array for thread-local storage.

![[Pasted image 20240604041000.png]]

### Linux threads

Linux provides the `fork()` syscall with the traditional functionality of duplicating a process. Linux also provides the ability to create threads using the `clone()` syscall. However, Linux doesn't distinguish between processes and threads. In fact, Linux uses the term **task** - rather than **process** or **thread** - when referring to a flow of control within a program.

When `clone()` is invoked, it is passed a set of flags that determine how much sharing is to take place between the parent and child tasks. Some of these flags are listed below:
![[Pasted image 20240604041230.png]]
Using `clone()` with certain flags is equivalent to creating a thread, since the parent task shares most of its resources with its child task. However, if none of these flags is set when `clone()` is invoked, no sharing takes place, resulting in functionality similar to that provided by the `fork()` system call.

The varying level of sharing is possible because of the way a task is represented in the Linux kernel. A unique kernel data structure exists for each task; this data structure, instead of storing data for the task, contains pointers to other data structures where these data are stored - for example, data structures that represent the list of open files, signal-handling info, and virtual memory. When `fork()` is invoked, a new task is created, along with a **copy** of all the associated data structures of the parent process. A new task is also created when the `clone()` system call is made. However, rather than copying all data structures, the new task **points** to the data structures of the parent task depending on the set flags.


---
# *References*
![[Operating System Concepts - Abraham Silberschatz, Peter Bae.pdf]]