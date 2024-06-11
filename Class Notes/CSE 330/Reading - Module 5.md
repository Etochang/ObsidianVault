202406041845
Meta Tags: #class
Tags: [[OS]]

# Reading - Module 5

>5.1-5.3, 5.5

## 5-1 Basic Concepts

CPU scheduling is the basis of multiprogrammed OSs. 

- a single CPU core --> only one process runs at a time.
- The objective of multiprogramming is to have some process running at all times, to maximize CPU utilization.
- In a simple computer system, the CPU just sits idle when a process is waiting; multiprogramming lets the CPU go to another process during the waiting time

### CPU-I/O burst cycle

- The success of CPU scheduling depends on an observed property of processes: process execution consists of a **cycle** of CPU execution and I/O wait.
- Process execution begins with a **CPU burst**. That is followed by an **I/O burst**, and the cycle continues. 
- Eventually, the final CPU burst ends with a system request to terminate execution.

![[Pasted image 20240604185859.png]]

- An I/O-bound program typically has many short CPU bursts
- A CPU=bound program might have a few long CPU bursts

### CPU scheduler

carries out the selection of a process in the ready queue to be executed, and allocates the CPU to that process. The records in the queues are generally the PCBs of the processes.

### Preemptive and nonpreemptive scheduling

CPU-scheduling decisions may take place under the following 4 circumstances:
1. When a process switches from the running state to the waiting state
2. When a process switches from the running state to the ready state
3. When a process switches from the waiting state to the ready state
4. When a process terminates

For 1 & 4, there is no choice in terms of scheduling;  a new process must be selected for execution. There is a choice, however, for 2 & 3.

When scheduling take place only under 1 & 4, we say that the scheduling scheme is **nonpreemptive** or **cooperative**. Otherwise, it is **preemptive**. Under nonpreemptive scheduling, once the CPU has been allocated to a process, the process keeps the CPU until it releases it either by terminating or by switching to the waiting state. Virtually all modern OSs use preemptive scheduling algorithms.

Preemptive scheduling can result in race conditions when data is shared among several processes - this also affects the design of the OS kernel. OS kernels can be designed as either nonpreemptive or preemptive.

Because interrupts can occur at any time and because they cannot always be ignored by the kernel, the sections of code affected by interrupts must be guarded from simultaneous use. So that these sections of code are not accessed concurrently, they disable interrupts at entry and reenable interrupts at exit.

### Dispatcher

Another component involved in the CPU-scheduling function that gives control of the CPU's core to the process selected by the CPU scheduler. This includes:
- Switching context from one process to another
- Switching to user mode
- Jumping to the proper location in the user program to resume that program
The dispatcher should be as fast as possible since it is invoked during every context switch. The time it takes for the dispatcher to stop one process and start another running is known as the **dispatch latency**.

![[Pasted image 20240604193710.png]]

How often do context switches occur? On a system-wide level, the number of context switches can be obtained by using the `vmstat` command.

![[Pasted image 20240604193856.png]]

The first line gives the average number of context switches over 1 second since the system booted, and the next two lines give the number of context switches over two 1-second intervals. 

We can also use the `/proc` file system to determine the number of context switches for a given process. `proc/pid#/status` will list these statistics for the process with `pid = pid#`.

**voluntary context switch** - occurs when a process has given up control of the CPU because it requires a resource that is currently unavailable.
**nonvoluntary context switch** - occurs when the CPU has been taken away from a process, such as when its time slice has expired or it has been preempted by a higher-priority process.

## 5-2 Scheduling criteria

- **CPU utilization** - we want to keep the CPU as busy as possible. In a real system, it should range from 40% to 90%
- **Throughput** - if the CPU is busy executing processes, then work is being done. Throughput is the number of processes that are completed per time unit
- **Turnaround time** - from the pov of a particular process, the important criterion is how long it takes to execute that process. The interval from the time of submission of a process to the time of completion is the turnaround time. It is the sum of the periods spent waiting in the ready queue, executing on the CPU, and doing I/O
- **Waiting time** - the algorithm doesn't affect the amount of time during which a process executes or does I/O. It affects only the amount of time that a process spends waiting in the ready queue. Waiting time is the sum of the periods spent waiting in the ready queue
- **Response time** - the time from the submission of a request until the first response is produced. The time it takes to start responding, not the time it takes to output the response

It is desirable to maximize CPU utilization and throughput and to minimize turnaround, waiting, and response time. 

In most cases, the average is optimized. However, under some circumstances, we prefer to optimize the mix/max values. Investigators have even suggested that minimizing the variance in response time is more important than minimizing the average response time.

## 5-3 Scheduling algorithms

### First-come, first-served scheduling

FCFS scheduling - the process that requests the CPU first is allocated the CPU first. When a process enters the ready queue, its PCB is linked onto the tail of the queue. When the CPU is free, it is allocated to the process at the head of the queue. The running process is then removed from the queue. 

On the negative side, the average waiting time under FCFS is often quite long. 

**convoy effect** - many processes wait for one or more big processes to get off the CPU

FCFS is nonpreemptive. Once the CPU has been allocated to a process, that process keeps the CPU until it releases it, either by terminating or by requesting I/O. Thus, FCFS is not good for interactive systems, where it's important that each process get a share of the CPU at regular intervals.

![[Pasted image 20240604195428.png]]

### Shortest-job-first scheduling

SJF associates with each process the length of the process's next CPU burst. When the CPU is available, it is assigned the process that has the smallest next CPU burst. If the next CPU bursts of 2 processes are the same, FCFS is used to break the tie. This is more like **shortest-next-CPU-burst**, because scheduling depends on the length of the next CPU burst of a process, rather than its total length.

SJF is provably optimal in that it gives the min. avg. waiting time for a given set of processes. However, it cannot be implemented at the level of CPU scheduling, as there is no way to know the length of the next CPU burst. One approach to this problem is approximation.

The next CPU burst is generally predicted as an **exponential average** of the measure lengths of previous CPU bursts. We can define the exponential average with the following formula. Let $t_n$ be the length of the $n$th CPU burst, and let $\tau_{n+1}$ be our predicted value for the next CPU burst. Then, for $\alpha$, $0 \le \alpha \le 1$, define
$$\tau_{n+1} = \alpha t_n + (1-\alpha)\tau_n$$
The parameter $\alpha$ controls the relative weight of recent and past history in our prediction. If $\alpha = 0$, then current conditions are assumed to be transient and recent history, $t_n$, has no effect. If $\alpha = 1$, then history is assumed to be old and irrelevant, and the recent CPU burst is the only thing that matters.

![[Pasted image 20240604200154.png]]

The SJF algorithm can be either preemptive or nonpreemptive. The choice arises when a new process arrives at the ready queue while a previous process is still executing. The next CPU burst of the newly arrived process may be shorter than what is left of the currently executing process. A preemptive SJF algorithm will preempt the currently executing process, whereas a nonpreemptive SJF algorithm will allow the currently running process to finish its CPU burst. Preemptive SJF scheduling is sometimes called **shortest-remaining-time-first** scheduling.

### Round-robin scheduling

The RR algorithm is similar to FCFS< but preemption is added to enable the system to switch between processes. A small unit of time, called a **time quantum/time slice**, is defined. A time quantum is generally from 10 to 100 ms. The CPU scheduler goes around the ready queue, allocating the CPU to each process for a timer interval of up to 1 time quantum.

To implement RR, we again treat the ready queue as a FIFO queue of processes. New processes are appended to the tail of the ready queue; the CPU scheduler picks the first process form the ready queue, sets a timer to interrupt after 1 time quantum, and dispatches the process.

The process may have a CPU burst of less than 1 time quantum. In this case, the process will release the CPU voluntarily, and the scheduler will then proceed to the next process.

The process also may have a CPU burst greater than 1 time quantum, where the timer will go off and a context switch will be executed, and the process will be put at the tail of the ready queue.

![[Pasted image 20240604200906.png]]

The average waiting time under RR is often long.

The performance of RR depends heavily on the size of the time quantum. At one extreme, if it is extremely large, RR is the same as FCFS. If it is extremely small, RR can result in a large number of context switches.

![[Pasted image 20240604201139.png]]

Thus, we want the time quantum to be large with respect to the context-switch time.

Turnaround time also depends on the size of the time quantum. In general, the avg. turnaround time can be improved if most processes finish their next CPU burst in a single time quantum.

![[Pasted image 20240604201145.png]]

### Priority scheduling

SJF is a special case of the general **priority-scheduling algorithm**. A priority is associated w/ each process, and the CPU is allocated to the process w/ the highest priority.

Priorities are generally indicated by some fixed range of numbers, but there is no general agreement on whether 0 is the highest or lowest priority. 

![[Pasted image 20240604201415.png]]

Priorities can be defined internally or externally:
- internally - uses some measurable quantity/quantities to compute the priority of a process, i.e. time limits, memory requirements, number of open files, etc.
- externally - set by criteria outside of the OS, such as the importance of the process, the type and amount of funds being paid for computer use, etc.

Can be either preemptive or nonpreemptive. When a process arrives at the ready queue, its priority is compared with the priority of the currently running process. Preemptive will preempt the CPU i f the priority of the newly arrive process is higher, while nonpreemptive will simply put the new process at the head of the ready queue.

A major problem is **indefinite blocking/starvation**. A process that is ready to run but waiting for the CPU can be considered blocked. Low-priority processes can wait indefinitely; in a heavily loaded system, a steady stream of higher-priority processes can prevent a low-priority process from ever getting the CPU.

A solution to the problem of indefinite blocking is **aging**. This involves gradually increasing the priority of processes that wait in the system. Another option is to combine RR and priority scheduling in such a way that the system executes the highest-priority process and runs processes w/ the same priority using RR. 

### Multilevel queue scheduling

With both priority/RR, all processes may be placed in a single queue. Depending on how the queues are managed, an $O(n)$ search may be necessary to determine the highest-priority process. In practice, it is often easier to have separate queues for each distinct priority. This approach is known as **multilevel queue**.

![[Pasted image 20240604202056.png]]

Multilevel queue can also be used to partition processes into several separate queues based on the process type. For example, a common division is made between **foreground** (interactive) and **background** (batch) processes. These two types have different response-time requirements and different scheduling needs. In addition, foreground may have priority over background. Separate queues may be used for foreground/background, and each queue might have its own algorithm.

![[Pasted image 20240604202217.png]]

In addition, there must be scheduling among the queues, which is commonly implemented as fixed-priority preemptive scheduling. See above.

Another possibility is to time-slice among the queues. Here, each queue gets a certain portion of the CPU time.

### Multilevel feedback queue scheduling

Normally, when the multilevel queue scheduling algorithm is used, processes are permanently assigned to a queue when they enter the system.  This setup has the advantage of low scheduling overhead, but it is inflexible.

The **multilevel feedback queue** algorithm, in contrast, allows a process to move between queues. The idea is to separate processes according to the characteristics of their CPU bursts. If a process uses too much CPU time, it will be moved to a lower-priority queue. In addition, a process that waits too long in a lower-priority queue may be moved to a higher-priority queue.

![[Pasted image 20240604202607.png]]

In general, a multilevel feedback queue scheduler is defined by the following parameters:
- number of queues
- scheduling algorithm for each queue
- method used to determine when to upgrade a process to higher-priority queues
- method used to determine when to demote a process to lower-priority queues
- method used to determine which queue a process will enter when that process needs service

Very complex.

## 5-5 Multi-processor scheduling

If multiple CPUs are available, **load sharing**, where multiple threads may run in parallel, becomes possible. However, scheduling issues become correspondingly more complex.

**multiprocessor** nor applies to the following system architectures:
- Multicore CPUs
- Multithreaded cores
- NUMA systems
- Heterogeneous multiprocessing

### Approaches to multiple-processor scheduling

- **asymmetric multiprocessing** - having all the scheduling decisions, I/O processing, and other system activities handles by a single processor, the main server; simple, but the main server becomes a potential bottleneck where overall system performance may be reduced
- **symmetric multiprocessing** (SMP), where each processor is self-scheduling. Scheduling proceeds by having the scheduler for each processor examine the ready queue and select a thread to run. Two possible strategies for organizing the threads eligible to be scheduled are:
	1. All threads may be in a common ready queue
	2. Each processor may have its own private queue of threads

![[Pasted image 20240604210902.png]]

- The first option has a possible race condition on the shared ready queue and must ensure that 2 separate processors don't choose to schedule the same thread and that threads are not lost from the queue. The second option permits each processor to schedule threads from its private run queue and therefore doesn't suffer from the possible performance problems associated with a shared run queue. Thus, it is the most common approach on SMP systems.

### Multicore processors

These may complicate scheduling issues. A **memory stall** is when a processor spends a significant amount of time waiting for memory to become available. This occurs primarily because modern processors operate at much faster speeds than memory. However, a memory stall can also occur because of a cache miss (accessing data that isn't in cache memory)

![[Pasted image 20240604211029.png]]

To remedy this situation, many recent hardware designs have implemented multithreaded processing cores in which two (or more) **hardware threads** are assigned to each core. That way, if one hardware thread stalls while waiting for memory, the core can switch to another thread.

![[Pasted image 20240604211215.png]]

From an OS perspective, each hardware thread maintains its architectural state, such as instruction pointer and register set, and thus appears as a logical CPU that is available to run a software thread. This technique known as **chip multithreading** (CMT) is illustrated below.

![[Pasted image 20240604211223.png]]

In general, there are 2 ways to multithread a processing core:
- **course-grained** - a thread executes on a core until a long-latency event such as a memory stall occurs. The core then switches to another thread to begin execution, which costs a lot since the instruction pipeline for the original thread must be flushed before the other can begin execution.
- **fine-grained** (or interleaved) - switches between threads at a much finer level of granularity, typically at the boundary of an instruction cycle. However, the architectural design of fine-grained systems include logic for thread switching. As a result, the cost is small.

It is important to note that the resources of the physical core (such as caches and pipelines) must be shared among its hardware threads, and therefore a processing core can only execute one hardware thread at a time. Consequently, a multithreaded, multicore processor actually requires two different levels of scheduling.

![[Pasted image 20240604211709.png]]

- scheduling decisions that must be made by the OS as it chooses which software thread to run on each hardware thread (logical CPU)
- how each core decides which hardware thread to run. 
	- RR
	- dynamic **urgency** value
- If the OS is aware of the level of processor resource sharing, it can schedule software threads onto logical processors that don't share resources.

### Load Balancing

attempts to keep the workload evenly distributed across all processors in an SMP system. This is typically only necessary on systems where each processor has its own private ready queue of eligible threads to execute. On systems with a common run queue, it is unnecessary, because once a processor becomes idle, it immediately extracts a runnable thread from the common ready queue.

Two general approaches:
- **push migration** - a specific task periodically checks the load on each processor and if it finds an imbalance, it evenly distributes the load by moving (pushing) threads from overloaded to idle/less-busy processors
- **pull migration** - an idle processor pulls a waiting task from a busy processor. 

These aren't mutually exclusive.

### Processor affinity

warm cache - successive memory accesses by a thread being satisfied in cache memory

- Because of the high cost of invalidating and repopulating caches, most SMP OSs try to avoid migrating a thread from processor to processor and instead attempt to keep a thread running on the same one. this is known as **processor affinity** - that is, a process has an affinity for the processor on which it is currently running
- If we adopt the approach of a common ready queue, a thready may be selected for execution by any processor. thus, if a thread is scheduled on a new processor, that processor's cache must be repopulated. With private, per-processor ready queues, a thread is always scheduled on the same processor and can therefore benefit from the contents of a warm cache. 

- **soft affinity** - when an OS has a policy of attempting to keep a process running on the same processor but not guaranteeing that it will do so
- **hard affinity** - a process has a subset of processors that are specified on which it can run

The main-memory architecture of a system can affect processor affinity as well.

Load balancing often counteracts the benefits of processor affinity. 

### Heterogeneous multiprocessing

systems that are designed using cores that run the same instruction set, yet vary in terms of clock speed/power management, including the ability to adjust the power consumption of a core to the point of idling it.

The intention behind HMP is to better manage power consumption.

By combining a number of slower cores w/ faster ones, a CPU scheduler can assign tasks that don't require high performance, but may need to run for longer periods, to slower cores, and vice versa.




---
# *References*
![[Operating System Concepts - Abraham Silberschatz, Peter Bae.pdf]]