202312061731
Meta Tags: #textbook  
Tags: [[computer organization]]

# Introduction

Computers are an essential product of the bustling IT industry, responsible for a significant portion of the US GDP. They have led to a third revolution for civilization, the "information revolution", up in ranks with the agricultural and industrial revolution. In the recent past, many applications of computers were considered "science fiction":

- *Computers in automobiles*: today, computers reduce pollution, improve fuel efficiency, and increase safety in automobiles.
- *Cell phones*: portable person-to-person communication to anyone anywhere in the world.
- *Human genome project*: analyzing human DNA sequences for tailored medical care.
- *The Internet*: digital media and services replacing physical ones.
- *Search Engines*: fast and easy information retrieval.

Clearly, advances in computer technology affect almost every aspect of our society. 

## Classes of Computing Applications and Their Characteristics

Broadly speaking, computers have three different categories:

### Personal Computers (PCs)
In the form of laptops, they are possibly the best known form of computing. They emphasize good performance-to-cost ratios and usually execute third-party software.
>[!info] personal computer (PC)
>A computer designed for use by an individual, usually incorporating a graphics display, a keyboard, and a mouse.

### Servers
 
They are oriented towards carrying large workloads, ranging from complex applications to small jobs, usually accessed via a network. 

Servers have the same technology as regular desktops but provide far greater computing, storage, and I/O capacity. In general, servers also place a greater emphasis on dependability, since a crash is usually more costly that it would be on a single-user PC.
>[!info] server
>A computer used for running larger programs for multiple users, often simultaneously, and typically accessed only via a network.

Servers have the widest range in cost and capability. At the low-end, a server may be just a desktop computer without a screen or keyboard and cost a thousand dollars; these are typically used for:
- file storage
- small business applications
- simple web serving

The other extreme is **supercomputers**, which are made up of hundreds of thousands of processors and many *terabytes* of memory, costing tens to hundreds of millions of dollars. Supercomputers are usually used for high-end scientific and engineering calculations, such as:
- weather forecasting
- oil exploration
- protein structure determination
- other large-scale problems
>[!note] supercomputer
>A class of computers with the highest performance and cost; they are configured as servers and typically cost tens to hundreds of millions of dollars.

>[!note] terabyte(TB)
>Originally $1,099,511,627,776$ ($2^{40}$) bytes, although communications and secondary storage systems developers started using the term to mean $1,000,000,000,000$ ($10^{12}$) bytes. To reduce confusion, we now use the term **tebibyte (TiB)** for $2^{40}$ bytes, defining _terabyte_ (TB) to mean $10^{12}$ bytes. The table below shows the full range of decimal and binary values and names.
>>[!example] The $2^X$ vs. $10^Y$ bytes ambiguity was resolved by adding a binary notation for all the common size terms.
>>![[F000011f01-01-9780128201091.jpg]]
>>

### Embedded Computers

The largest class of computers spanning the widest range of applications and performance. Some examples are:

- microprocessors in a car
- computers in a television set
- networks of processors that control an airplane

A popular term today is **Internet of Things (IoT)**, which suggests many small devices that all communicate wirelessly over the Internet. Embedded computing systems are designed for one purpose/set of purposes and are normally integrated with the hardware; thus, most users never really see that they are using a computer in most scenarios!

>[!note] embedded computer
>A computer inside another device used for running one predetermined application or collection of software.

Embedded applications often have unique application requirements that combine a minimum performance with tight constraints on cost or power. However, despite their lost cost, embedded computers have a lower tolerance for failure, as they are used in important scenarios (imagine if the computer in a plane malfunctions). 

>[!tip] Elaboration
>Many embedded processors are designed using _processor cores_, a version of a processor written in a hardware description language, such as Verilog or VHDL (see [[The Processor|Chapter 4]]). The core allows a designer to integrate other application-specific hardware with the processor core for fabrication on a single chip.

## Welcome to the PostPC Era

Replacing  the PC is the **personal mobile device (PMD)**. PMDs are battery operated with wireless connectivity, typically cost hundred of dollars, and, like PCs, users can download software ("apps") to run on them. 

>[!note] Personal mobile devices (PMDs)
>are small wireless devices to connect to the Internet; they rely on batteries for power, and software is installed by downloading apps. Conventional examples are smart phones and tablets.

>[!example] The number manufactured per year of tablets and smart phones, which reflect the PostPC era, versus personal computers and traditional cell phones.
>![[F000011f01-02-9780128201091 1.jpg]]

In the same sense, the traditional server is being overtaken by **Cloud Computing**, which relies on giant datacenters that are now known as *Warehouse Scale Computers* (WSCs). Companies like Amazon and Google build these WSCs containing 50,000 servers to rent them out to others, who proceed to develop and provide software services to PMDs w/o having to invest in server costs. **Software as a Service (SaaS)** is also revolutionizing the software industry just as PMDs and WSCs are revolutionizing the hardware industry.

>[!note] Cloud Computing
>refers to large collections of servers that provide services over the Internet; some providers rent dynamically varying numbers of servers as a utility.

>[!note] Software as a Service (SaaS)
>delivers software and data as a service over the Internet, usually via a thin program such as a browser that runs on local client devices, instead of binary code that must be installed, and runs wholly on that device. Examples include web search and social networking.

## What You Can Learn in This Book

Performance of computer programs has always been a major concern, and in the 1960s and 1970s, the primary constraint on computer performance was the **size of the computer's memory**. Thus, the main effort at that time was to **minimize memory space**. However, in recent times, advances in computer design and memory technology have mostly made memory size a nonissue, excluding embedded computing systems.

Now, programmers should worry about "the parallel nature of processors", "the hierarchical nature of memories", and the energy efficiency of their programs, which requires "understanding what is below your code". 

This book will investigate the software below the program, as well as the hardware under the covers of the computer. By the end of the book, you will be able to answer the following questions:

- How are programs written in a high-level language, such as C or Java, translated into the language of the hardware, and how does the hardware execute the resulting program?
	- Comprehending these concepts forms the basis of understanding the aspects of both the hardware and software that affect program performance.
- What is the interface between the software and the hardware, and how does software instruct the hardware to perform needed functions?
	- These concepts are vital to understanding how to write many kinds of software.
- What determines the performance of a program, and how can a programmer improve the performance?
	- As we will see, this depends on the original program, the software translation of that program into the computer’s language, and the effectiveness of the hardware in executing the program.
- What techniques can be used by hardware designers to improve performance?
	- This book will introduce the basic concepts of modern computer design. The interested reader will find much more material on this topic in our advanced book, _Computer Architecture: A Quantitative Approach_.
- What techniques can be used by hardware designers to improve energy efficiency?
	- What can the programmer do to help or hinder energy efficiency?
- What are the reasons for and the consequences of the switch from sequential processing to parallel processing?
	- This book gives the motivation, describes the current hardware mechanisms to support parallelism, and surveys the new generation of **“multicore” microprocessors** (see Chapter 6).
- Since the first commercial computer in 1951, what great ideas did computer architects come up with that lay the foundation of modern computing?

>[!example] multicore microprocessor
>A microprocessor containing multiple processors (“cores”) in a single integrated circuit.

Without understanding these answers, improving program performance and evaluating the differences between computer applicability will be a process of trial and error, rather than a scientific procedure driven by insight and analysis. 

>[!important] Understanding Program Performance
>The performance of a program depends on a combination of the effectiveness of the algorithms used in the program, the software systems used to create and translate the program into machine instructions, and the effectiveness of the computer in executing those instructions, which may include input/output (I/O) operations. This table summarizes how the hardware and software affect performance.
>

|Hardware or software component|How this component affects performance|Where is this topic covered?|
|---|---|---|
|Algorithm|Determines both the number of source-level statements and the number of I/O operations executed|Other books!|
|Programming language, compiler, and architecture|Determines the number of computer instructions for each source-level statement|Chapters 2 and 3|
|Processor and memory system|Determines how fast instructions can be executed|Chapters 4, 5, and 6|
|I/O system (hardware and operating system)|Determines how fast I/O operations may be executed|Chapters 4, 5, and 6|

>[!warning] Check Yourself
>_Check Yourself_ sections are designed to help readers assess whether they comprehend the major concepts introduced in a chapter and understand the implications of those concepts. Some _Check Yourself_ questions have simple answers; others are for discussion among a group. Answers to the specific questions can be found at the end of the chapter. _Check Yourself_ questions appear only at the end of a section, making it easy to skip them if you are sure you understand the material.
>1.  The number of embedded processors sold every year greatly outnumbers the number of PC and even PostPC processors. Can you confirm or deny this insight based on your own experience? Try to count the number of embedded processors in your home. How does it compare with the number of conventional computers in your home?
>2. As mentioned earlier, both the software and hardware affect the performance of a program. Can you think of examples where each of the following is the right place to look for a performance bottleneck?
>	1. The algorithm chosen
>	2. The programming language or compiler
>	3. The operating system
>	4. The processor
>	5. The I/O system and devices

# [[Seven Great Ideas in Computer Architecture]]


---
# *References*