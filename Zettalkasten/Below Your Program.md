

202312062137
Meta Tags: #textbook 
Tags: [[computer organization]]

# Below Your Program

A typical application may consist of millions of lines of code and rely on sophisticated software libraries that implement complex functions in support of the application. However, the hardware in a computer can only execute **extremely simple low-level instructions** - going from a complex application to the simple instructions requires several layers of software to interpret or translate high-level operations into simple computer instructions, an example of the great idea of **[[Seven Great Ideas in Computer Architecture#Use Abstraction to Simplify Design|abstraction]]**.

![[F000011icon01-9780128201091 1.jpg]]

The image below shows that these "layers of software" are organized in a hierarchical fashion, with applications being the outermost ring and a variety of **systems software** sitting between the hardware and applications software.

>[!note] systems software
>Software that provides services that are commonly useful, including **operating systems**, **compilers**, **loaders**, and **assemblers**.

![[F000011f01-03-9780128201091.jpg]]

There are many types of systems software, but two types of systems software are central to every computer system today: an **operating system (OS)** and a **compiler**. An OS interfaces between a **user's program** and the **hardware**, providing a variety of services and functions including:

- Handling basic I/O operations
- Allocating storage and memory
- Providing for protected sharing of the computer among multiple applications using it simultaneously.

>[!tip] The "mailroom" analogy
>The OS manages the "mailroom" that delivers "mail" between the application and the hardware. It sends and accepts "mail" from both sides, organizes the "mail" within the "mailroom", and lets multiple people use the "mailroom" at a time.

>[!note] operating system (OS)
>Supervising program that manages the resources of a computer for the benefit of the programs that run on that computer.

Examples of OSs are Linux, iOS, Android, and Windows.

**Compilers** perform another *vital* function: the translation of a program written in a high-level language ([[C]], [[C++]], [[Java]], or [[Visual Basic]]) into instructions that the hardware can execute. 

>[!note] compiler
>A program that translates high-level language statements into assembly language statements.

## From a High-Level Language to the Language of Hardware

To speak to **electronic** hardware, you need to send **electrical** signals. The easiest signals for computers to understand are *on* and *off*, which are represented by the numbers 1 and 0 respectively. We commonly think of the computer language as numbers in base 2, or *binary numbers*. We refer to each "letter" as a **[[bit]]**.

Computers are slaves to our commands, which are called **[[instruction|instructions]]**. Instructions, which are just collections of bits that the computer understands and obeys, can be thought of as numbers. For example the bits
$$1000110010100000$$
tell one computer to add two numbers. [[Instructions: Language of the Computer|Chapter 2]] explains why we use numbers for instructions *and* data.

>[!note] bit
>One of the two numbers in base 2 (0 or 1) that are the components of information.

>[!note] instruction
>A command that computer hardware understands and obeys.

The first programmers communicated to computers in binary numbers, but the process was **extremely** tedious. So, the invented notations for bit sequences that were closer to the way humans think, like having `add` for some long string of bits that tells the computer to add two numbers. However, translating these notations was still frustrating, so they invented programs to translate from symbolic notation to binary. The first of these 'translators' was named an **assembler**. For example, the programmer would write
```
add A, B
```
and the assembler would translate this notation into
```
1000110010100000
```
This instruction tells the computer to add the two numbers `A` and `B`. The name coined for this symbolic language, still used today, is **assembly language**. In contrast, the binary language that the machine understands is the **machine language**. 

>[!note] assembler
>A program that translates a symbolic version of instructions into the binary version.

>[!note] assembly language
>A symbolic representation of machine instructions.

>[!note] machine language
>A binary representation of machine instructions.

Assembly language, while being a massive improvement, is still far from being easy to grasp; it requires the programmer to **write one line for every instruction that the computer will follow**, forcing the programmer to think like the computer itself.

Programmers today owe their productivity - and their sanity - to the creation of **high-level programming languages** and compilers that translate programs in such languages into computer instructions. The image below shows the relationships among these programs and languages, which are more example of the power of **[[Seven Great Ideas in Computer Architecture#Use Abstraction to Simplify Design|abstraction]]**.

![[F000011icon01-9780128201091 2.jpg]]

>[!note] high-level programming language
A portable language such as C, C++, Java, or Visual Basic that is composed of words and algebraic notation that can be translated by a compiler into assembly language.

>[!example] **C program compiled into assembly language and then assembled into binary machine language.**
>![[F000011f01-04-9780128201091.jpg]]

A compiler enables a programmer to write this high-level language expression:
```
A + B
```
The compiler would compile it into this assembly language statement:
```
add A, B
```
As shown above, the assembler would translate this statement into the binary instructions that tell the computer to add the two numbers `A` and `B`. 

High-level programming languages offer several important benefits:

- Allowing the programmer to think more naturally
- Allowing languages to be designed according to their intended use
	- Fortran - scientific computation
	- Cobol - business data processing
	- Lisp - symbol manipulation
	- etc.
- Improving programmer productivity
- Allowing programs to be independent of the computer on which they were developed

# [[Under the Covers]]

---
# *References*