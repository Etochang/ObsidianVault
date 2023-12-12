202312070127
Meta Tags: #textbook 
Tags: [[computer organization]]

# Performance

Performance assessment is difficult, due to the scale and intricacy of modern software systems accompanied by the wide range of performance improvement techniques employed by hardware designers.

Performance is an important attribute when choosing among different computers. Hence, understanding how to best measure performance and the limitations of performance measurements is important in selecting a computer.

The rest of this section describes different ways in which performance can be determined; then, we describe the metrics for measuring performance from the viewpoint of both a computer user and a designer. We also look at how these metrics are related and present the **classical processor performance equation**, which we will use throughout the text.

## Defining Performance

What does one computer having "better performance" than another really mean? Let's think about a passenger airplane: the figure below lists some typical passenger airplanes, together with their cruising speed, range, and capacity.

>[!example] The capacity, range, and speed for a number of commercial airplanes.
>![[F000011f01-14-9780128201091.jpg]]

If we wanted to know *which* of the planes in this table had the best performance, we would first need to *define* performance. For example, we can see that the Concorde has the highest cruising speed, the Airbus has the highest passenger capacity, and the Boeing has the longest cruising range.

Let's suppose we define performance in terms of speed. This still leaves two possible definitions: you could define the fastest plane as the one with the highest cruising speed or the one who transports the most amount of passengers per unit time. Similarly, we can define computer performance in several different ways; let's describe two different scenarios.

If you were running a program on two different desktop computers, you'd say that the faster one is the desktop computer that **finishes the program first**. If you were running a datacenter that had several servers running jobs submitted by many users, you'd say that the faster computer was the one that **completed the most jobs during a day**. As an individual computer user, you are interested in reducing **response time** - the time between the start and completion of a task - also referred to as **execution time**. Datacenter managers are often interested in increasing **throughput** or **bandwidth** - the total amount of work done in a given time. 

Hence, in most cases, we will need different performance metrics as well as different sets of applications to benchmark personal mobile devices, which are more focused on response time, versus servers, which are more focused on throughput.

>[!note] response time
>Also called **execution time**. The total time required for the computer to complete a task, including disk accesses, memory accesses, I/O activities, operating system overhead, CPU execution time, and so on.

>[!note] throughput
>Also called **bandwidth**. Another measure of performance, it is the number of tasks completed per unit time.

>[!example] Throughput and Response Time
>Do the following changes to a computer system increase throughput, decrease response time, or both?
>1. Replacing the processor in a computer with a faster version
>2. Adding additional processors to a system that uses multiple processors for separate tasks—for example, searching the web
>
>**Answer:**
>Decreasing response time almost always improves throughput. Hence, in case 1, both response time and throughput are improved. In case 2, no one task gets work done faster, so only throughput increases.
>
If, however, the demand for processing in the second case was almost as large as the throughput, the system might force requests to queue up. In this case, increasing the throughput could also improve response time, since it would reduce the waiting time in the queue. Thus, in many real computer systems, changing either execution time or throughput often affects the other.

We will primarily be concerned with response time for the first few chapters. To maximize performance, we want to minimize response time or execution time for some task. Thus we can relate performance and execution time for a computer X:

$$\text{Performance}_X=\frac{1}{\text{Executiontime}_x}$$
This means that for two computers X and Y, if the performance of X is greater than the performance of Y, we have
$$\text{Performance}_X > \text{Performance}_Y$$
$$\frac{1}{\text{Executiontime}_X}>\frac{1}{\text{Executiontime}_Y}$$
$$\text{Executiontime}_Y > \text{Executiontime}_X$$
That is, the execution time on Y is longer than that on X, if X is faster than Y.

In discussing a computer design, we often want to relate the performance of two different computers quantitatively. We will use the phrase “X is _n_ times faster than Y”—or equivalently “X is _n_ times as fast as Y”—to mean
$$\frac{\text{Performance}_X}{\text{Performance}_Y} = n$$
If X is _n_ times as fast as Y, then the execution time on Y is _n_ times as long as it is on X:
$$\frac{\text{Performance}_X}{\text{Performance}_Y} =\frac{\text{Executiontime}_Y}{\text{Executiontime}_X}= n$$

>[!example] Relative Performance
>If computer A runs a program in 10 seconds and computer B runs the same program in 15 seconds, how much faster is A than B?
>
>**Answer:**
>Using the above equation, $15/10 = 1.5$ so 1.5 times faster.
>

## Measuring Performance

Time is the measure of computer performance. Program *execution time* is measured in seconds per program. However, time can be defined in different ways, depending on what we count. The most straightforward definition of time is called *wall clock time*, *response time*, or *elapsed time*. These terms mean the **total time** to complete a task, including:

- disk accesses
- memory accesses
- I/O activities
- OS overhead
- everything else!

Computers are often shared, however, and a processor may work on several programs simultaneously. In such cases, the system may try to optimize throughput rather than attempt to minimize the execution time for one program. Hence, we might want to distinguish between execution time and time over which the processor is working on the program.

**CPU execution time** or simply **CPU time** is the time the CPU spends computing for the task and does not include time spent waiting for everything else.

>[!important] 
>Remember, though, that the response time experienced by the user will be the elapsed time of the program, not the CPU time.

CPU time can be further divided into:

- **user CPU time**: the CPU time spent in the program
- **system CPU time**: the CPU time spent in the OS

Differentiating between system and user CPU time is difficult to do accurately, because it is often hard to assign responsibility for operating system activities to one user program rather than another and because of the functionality differences among operating systems.

>[!note] CPU execution time
>Also called **CPU time**. The actual time the CPU spends computing for a specific task.

>[!note] user CPU time
>The CPU time spent in a program itself.

>[!note] system CPU time
>The CPU time spent in the operating system performing tasks on behalf of the program.

For consistency, we maintain a distinction between performance based on elapsed time and that based on CPU execution time.

We will use the term **_system performance_** to refer to **elapsed time** on an unloaded system and **_CPU performance_** to refer to **user CPU time**.

>[!important] Understanding Program Performance
>Different applications are sensitive to different aspects of the performance of a computer system. Many applications, especially those running on servers, depend as much on I/O performance, which, in turn, relies on both hardware and software. Total elapsed time measured by a wall clock is the measurement of interest. In some application environments, the user may care about throughput, response time, or a complex combination of the two (e.g., maximum throughput with a worst-case response time). To improve the performance of a program, one must have a clear definition of what performance metric matters and then proceed to look for performance bottlenecks by measuring program execution and looking for the likely bottlenecks. In the following chapters, we will describe how to search for bottlenecks and improve performance in various parts of the system.

Although, as computer users, we care about time, when we examine the details of a computer it's convenient to thing about performance in other metrics. For example, computer designers may want to use a measure that relates to how fast the hardware can perform basic functions.

Almost all computers are constructed using a clock that determines when events take place in the hardware. These discrete time intervals are called **clock cycles** (or **ticks**, **clock ticks**, **clock periods**, **clocks**, **cycles**). designers refer to the length of a **clock period** both as the time for a complete *clock cycle* (e.g., 250 ps) and as the *clock rate* (e.g., 4 GHz), which is the inverse of the clock period.
$$\text{Clockperiod} = \frac{1}{\text{Clockrate}}; \ \ \ T = \frac{1}{f}$$
In the next subsection, we will formalize the relationship between the clock cycles of the hardware designer and the seconds of the computer user.

>[!note] clock cycle
>Also called **tick**, **clock tick**, **clock period**, **clock**, or **cycle**. The time for one clock period, usually of the processor clock, which runs at a constant rate.

>[!note] clock period
>The length of each clock cycle.

>[!note] clock rate
>The inverse of clock period.

>[!warning] Check Yourself
>1. Suppose we know that an application that uses both personal mobile devices and the Cloud is limited by network performance. For the following changes, state whether only the throughput improves, both response time and throughput improve, or neither improves.
>	1. An extra network channel is added between the PMD and the Cloud, increasing the total network throughput and reducing the delay to obtain network access (since there are now two channels).
>	2. The networking software is improved, thereby reducing the network communication delay, but not increasing throughput.
>	3. More memory is added to the computer.
>2. Computer C’s performance is 4 times as fast as the performance of computer B, which runs a given application in 28 seconds. How long will computer C take to run that application?

## CPU Performance and Its Factors

So, users and designers often examine performance using different metrics. If we could relate these different metrics, we could determine the effect of a **design change** on the **performance as experienced by the user**.

Since we are confining ourselves to CPU performance at this point, the bottom-line performance measure is *CPU execution time*. A simple formula relates the most basic metrics (clock cycles and clock period) to CPU time:
$$\text{CPU}_{\text{exectime/program}} = \text{CPU}_{\text{cycles/program}} \times \text{Clockperiod}$$
Alternatively, because clock period and clock rate are inverses:
$$\text{CPU}_{\text{exectime/program}} = \frac{\text{CPU}_{\text{cycles/program}}}{\text{Clockrate}}$$
This formula clarifies that the hardware designer can improve performance by reducing the \# of clock cycles required for a program, or the clock period. As we will see in later chapters, the designer often faces a trade-off between the number of clock cycles needed for a program and the length of each cycle. Many techniques that decrease the number of clock cycles may also increase the clock cycle time.

>[!example] Improving Performance
>Our favorite program runs in 10 seconds on computer A, which has a 2 GHz clock. We are trying to help a computer designer build a computer, B, which will run this program in 6 seconds. The designer has determined that a substantial increase in the clock rate is possible, but this increase will affect the rest of the CPU design, causing computer B to require 1.2 times as many clock cycles as computer A for this program. What clock rate should we tell the designer to target?
>
>**Answer:**
>$$\text{CPUA}_{\text{exectime/program}} = 10; \ \text{ClockrateA} = 2 \times 10^9$$
>$$\text{CPUA}_{\text{exectime/program}} \times \ \text{ClockrateA} = \text{CPUA}_{\text{cycles/program}}$$
>$$\text{CPUA}_{\text{cycles/program}} = 2 \times 10^{10}$$
>$$\text{CPUB}_{\text{cycles/program}} = 1.2 \cdot \text{CPUA}_{\text{cycles/program}}$$
>$$\text{CPUB}_{\text{cycles/program}} = 2.4 \times 10^{10}$$
>$$\text{CPUB}_{\text{exectime/program}}=6$$
>$$\text{ClockrateB} = \frac{\text{CPUB}_{\text{cycles/program}}}{\text{CPUB}_{\text{exectime/program}}}=4 \times 10^9 \ \text{Hz}$$

## Instruction Performance

The performance equations above didn't include any reference to the number of instructions needed for the program. However, since the compiler clearly generated instructions to execute, and the computer had to execute the instructions to run the program, the execution time must depend on the number of instructions in a program.

One way to think about execution time is that it equals the number of instructions executed multiplied by the average time per instruction. Therefore, the number of clock cycles required for a program can be written as 
$$\text{CPU}_\text{cycles/program}=\text{Instructions}_\text{program} \times \overline{\text{Cycles}_\text{instruction}}$$
The term **clock cycles per instruction**, which is the average number of clock cycles each instruction takes to execute, is often abbreviated as **CPI**. Since different instruction take different amounts of time, CPI is an average of all the instructions execute in the program. CPI provides one way of comparing two different implementations of the same instruction set architecture, since the number of instructions executed for a program will, of course, be the same.

>[!note] clock cycles per instruction (CPI)
>Average number of clock cycles per instruction for a program or program fragment.

>[!example] Using the Performance Equation
>Suppose we have two implementations of the same instruction set architecture. Computer A has a clock cycle time of 250 ps and a CPI of 2.0 for some program, and computer B has a clock cycle time of 500 ps and a CPI of 1.2 for the same program. Which computer is faster for this program and by how much?
>
>**Answer:**
>$$\text{InstructionsA}_\text{program} = \text{InstructionsB}_\text{program} = I$$
>$$\text{CPI}_\text{A}=2.0;\ \text{CPI}_\text{B}=1.2$$
>$$\text{Cperiod}_\text{A} = 250 \times 10^{-12};\ \text{Cperiod}_\text{B} = 500 \times 10^{-12}$$
>$$\text{CPU}_{\text{exectime/program}} = \text{CPU}_{\text{cycles/program}} \times \text{Cperiod}$$
>$$\text{CPUA}_{\text{exectime/program}} = 500I \times  \times 10^{-12}$$
>$$\text{CPUB}_{\text{exectime/program}} = 600I \times  \times 10^{-12}$$
>Computer A is faster by 1.2 times.

## The Classic CPU Performance Equation

We can now write this basic performance equation in terms of **instruction count** (the number of instructions executed by the program), CPI, and clock cycle time:
$$\text{CPU}_{\text{exectime}} = \text{Instructioncount} \times \text{CPI} \times \text{Clockperiod}$$
or alternatively,
$$\text{CPU}_{\text{exectime}} = \frac{\text{Instructioncount} \times \text{CPI}}{\text{Clockrate}}$$
>[!note] instruction count
>The number of instructions executed by the program.

>[!example] Comparing Code Segments
>A compiler designer is trying to decide between two code sequences for a particular computer. The hardware designers have supplied the following facts:
>![[Pasted image 20231207025128.png]]
>For a particular high-level language statement, the compiler writer is considering two code sequences that require the following instruction counts:
>![[Pasted image 20231207025143.png]]
>Which code sequence executes the most instructions? Which will be faster? What is the CPI for each sequence?
>
>**Answer:**

>[!important] The BIG Picture
>The image below shows the basic measurements at different levels in the computer and what is being measured in each case. We can see how these factors are combined to yield execution time measured in seconds per program:
>$$\frac{\text{Seconds}}{\text{Program}} = \frac{\text{Instructions}}{\text{Program}} \times \frac{\text{Cycles}}{\text{Instruction}} \times \frac{\text{Seconds}}{\text{Cycle}}$$
>>[!example] The basic components of performance and how each is measured.
>>![[F000011f01-15-9780128201091.jpg]]
>
>Always bear in mind that the only complete and reliable measure of computer performance is time. For example, changing the instruction set to lower the instruction count may lead to an organization with a slower clock cycle time or higher CPI that offsets the improvement in instruction count. Similarly, because CPI depends on type of instructions executed, the code that executes the fewest number of instructions may not be the fastest.
>

How can we determine the value of these factors in the performance equation? We can measure the CPU execution time by running the program, and the clock cycle time is usually published as part of the documentation for a computer. The instruction count and CPI can be more difficult to obtain. Of course, if we know the clock rate and CPU execution time, we need only one of the instruction count or the CPI to determine the other.

We can measure the instruction count by using software tools that profile the execution or by using a simulator of the architecture. Alternatively, we can use hardware counters, which are included in most processors, to record a variety of measurements, including the number of instructions executed, the average CPI, and often, the sources of performance loss. Since the instruction count depends on the architecture, but not on the exact implementation, we can measure the instruction count without knowing all the details of the implementation. The CPI, however, depends on a wide variety of design details in the computer, including both the memory system and the processor structure (as we will see in Chapter 4 and Chapter 5), as well as on the mix of instruction types executed in an application. Thus, CPI varies by application, as well as among implementations with the same instruction set.

The above example shows the danger of using only one factor (instruction count) to assess performance. When comparing two computers, you must look at all three components, which combine to form execution time. If some of the factors are identical, like the clock rate in the above example, performance can be determined by comparing all the nonidentical factors. Since CPI varies by **instruction mix**, both instruction count and CPI must be compared, even if clock rates are identical. Several exercises at the end of this chapter ask you to evaluate a series of computer and compiler enhancements that affect clock rate, CPI, and instruction count. In **[[Historical Perspective and Further Reading - Computer Abstractions and Technology|Section 1.13]]**, we’ll examine a common performance measurement that does not incorporate all the terms and can thus be misleading.

>[!note] instruction mix
>A measure of the dynamic frequency of instructions across one or many programs.

>[!important] Understanding Program Performance
>The performance of a program depends on the algorithm, the language, the compiler, the architecture, and the actual hardware. The following table summarizes how these components affect the factors in the CPU performance equation.

|Hardware or software component|Affects what?|How?|
|---|---|---|
|Algorithm|Instruction count, possibly CPI|The algorithm determines the number of source program instructions executed and hence the number of processor instructions executed. The algorithm may also affect the CPI, by favoring slower or faster instructions. For example, if the algorithm uses more divides, it will tend to have a higher CPI.|
|Programming language|Instruction count, CPI|The programming language certainly affects the instruction count, since statements in the language are translated to processor instructions, which determine instruction count. The language may also affect the CPI because of its features; for example, a language with heavy support for data abstraction (e.g., Java) will require indirect calls, which will use higher CPI instructions.|
|Compiler|Instruction count, CPI|The efficiency of the compiler affects both the instruction count and average cycles per instruction, since the compiler determines the translation of the source language instructions into computer instructions. The compiler’s role can be very complex and affect the CPI in complicated ways.|
|Instruction set architecture|Instruction count, clock rate, CPI|The instruction set architecture affects all three aspects of CPU performance, since it affects the instructions needed for a function, the cost in cycles of each instruction, and the overall clock rate of the processor.|

>[!important] Elaboration
>Although you might expect that the minimum CPI is 1.0, as we’ll see in [[The Processor|Chapter 4]], some processors fetch and execute multiple instructions per clock cycle. To reflect that approach, some designers invert CPI to talk about _IPC_, or _instructions per clock cycle_. If a processor executes on average 2 instructions per clock cycle, then it has an IPC of 2 and hence a CPI of 0.5.

>[!important] Elaboration
>Although clock cycle time has traditionally been fixed, to save energy or temporarily boost performance, today’s processors can vary their clock rates, so we would need to use the _average_ clock rate for a program. For example, the Intel Core i7 will temporarily increase clock rate by about 10% until the chip gets too warm. Intel calls this _Turbo mode_.

>[!warning] Check Yourself
>A given application written in Java runs 15 seconds on a desktop processor. A new Java compiler is released that requires only 0.6 as many instructions as the old compiler. Unfortunately, it increases the CPI by 1.1. How fast can we expect the application to run using this new compiler? Pick the right answer from the three choices below:
>1. $$\frac{1.5 \times 0.6}{1.1} = 8.2$$
>2. $$15 \times 0.6 \times 1.1 = 9.9$$
>3. $$\frac{1.5 \times 1.1}{0.6} = 27.5$$
>   
>   **Answer:**
>   $$\text{CPU}_{\text{exectime}} = \text{Instructioncount} \times \text{CPI} \times \text{Clockperiod}$$
>   2



---
# *References*