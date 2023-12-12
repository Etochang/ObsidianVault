202312062223
Meta Tags: #textbook 
Tags: [[computer organization]]

# Under the Covers

The underlying hardware in any computer performs the same basic functions:
- inputting data
- outputting data
- processing data
- storing data

How these functions are performed is the primary topic of this book.

When we come to an important point in this book, a point so important that we hope you will remember it forever, we emphasize it by identifying it as a _Big Picture_ item. We have about a dozen Big Pictures in this book, the first being the five components of a computer that perform the tasks of inputting, outputting, processing, and storing data.

>[!note] input device
>A mechanism through which the computer is fed information, such as a keyboard.

>[!note] output device
>A mechanism that conveys the result of a computation to a user, such as a display, or to another computer.

Two key components of computers are **input devices**, such as a microphone, and **output devices**, such as a speaker. Input feed the computer, and output is the result of the computation sent to the user. Some devices, such as wireless networks, provide both input and output to the computer.

Let's take an introductory tour through the computer hardware, starting with the external I/O devices.

>[!important] The BIG Picture
>Tie five classic components of a computer are input, output, memory, datapath, and control, with the last two sometimes combined and called the processor. This image shows the standard organization of a computer.
>![[F000011f01-05-9780128201091.jpg]]
>This organization is independent of hardware tech: you can place every piece of every computer, past and present, into one of these five categories. To help you keep all this in perspective, the five components of a computer are shown on the front page of each of the following chapters, with the portion of interest to that chapter highlighted.

## Through the Looking Glass

>*Through computer displays I have landed an airplane on the deck of a moving carrier, observed a nuclear particle hit a potential well, flown in a rocket at nearly the speed of light and watched a computer reveal its innermost workings.*
>
>— Ivan Sutherland, the “father” of computer graphics, _Scientific American_, 1984

The most fascinating I/O device is probably the **graphics display**. Most PMDs use **liquid crystal displays (LCDs)** to get a thin, low-power display. The LCD is not the source of light; instead, it controls the transmission of light. A typical LCD includes rod-shaped molecules in a liquid that form a twisting helix that bends light entering the display, from either a light source behind the display or less often from reflected light. The rods straighten out when a current is applied and no longer bend the light. Since the liquid crystal material is between two screens polarized at 90 degrees, the light cannot pass through unless it is bent. Today, most LCD displays use an **active matrix** that has a tiny transistor switch at each pixel to precisely control current and make sharper images. A red-green-blue mask associated with each dot on the display determines the intensity of the three-color components in the final image; in a color active matrix LCD, there are three transistor switches at each point.

>[!note] liquid crystal display
>A display technology using a thin layer of liquid polymers that can be used to transmit or block light according to whether a charge is applied.

>[!note] active matrix display
>A liquid crystal display using a transistor to control the transmission of light at each individual pixel.

The image is composed of a matrix of picture elements, or **pixels**, which can be represented as a matrix of bits, called a *bit map*. Depending on the size of the screen and the resolution, the display matrix in a typical tablet ranges in size from 1024 ☓ 768 to 2048 ☓ 1536. A color display might use 8 bits for each of the three colors (red, blue, and green), for 24 bits per pixel, permitting millions of different colors to be displayed.

>[!note] pixel
>The smallest individual picture element. Screens are composed of hundreds of thousands to millions of pixels, organized in a matrix.

The computer hardware support for graphics consists mainly of a _raster refresh buffer_, or _frame buffer_, to store the bit map. The image to be represented onscreen is stored in the frame buffer, and the bit pattern per pixel is read out to the graphics display at the refresh rate. The image below shows a frame buffer with a simplified design of just 4 bits per pixel.

>[!example] Each coordinate in the frame buffer on the left determines the shade of the corresponding coordinate for the raster scan CRT display on the right.
>![[F000011f01-06-9780128201091.jpg]]

The goal of the bit map is to faithfully represent what is on the screen. The challenges in graphics systems arise because the human eye is very good at detecting even subtle changes on the screen.

## Touchscreen

While PCs also use LCD displays, the tablets and smartphones of the PostPC era have replaced the keyboard and mouse with touch sensitive displays, which has the wonderful user interface advantage of users pointing directly what they are interested in rather than indirectly with a mouse.

While there are a variety of ways to implement a touch screen, many tablets today use capacitive sensing. Since people are electrical conductors, if an insulator like glass is covered with a transparent conductor, touching distorts the electrostatic field of the screen, which results in a change in capacitance. This technology can allow multiple touches simultaneously, which allows gestures that can lead to attractive user interfaces.

## Opening the Box

The image below shows the contents of the Apple iPhone Xs Max smart phone. Unsurprisingly, of the five classic components of the computer, I/O dominates this device. The list of I/O devices includes a capacitive multitouch LCD display, front-facing camera, rear-facing camera, microphone, headphone jack, speakers, accelerometer, gyroscope, Wi-Fi network, and Bluetooth network. The datapath, control, and memory are a tiny portion of the components.

>[!example] Apple iPhone Xs Max
>![[F000011f01-07-9780128201091.jpg]]

The small rectangles in the image below contain the devices that drive our advancing technology, called **integrated circuits** and nicknamed **chips**. The A12 package seen in the middle of the image contains two large ARM processors and four little ARM processors that operate with a clock rate of 2.5 GHz. The _processor_ is the active part of the computer, following the instructions of a program to the letter. It adds numbers, tests numbers, signals I/O devices to activate, and so on. Occasionally, people call the processor the **CPU**, for the more bureaucratic-sounding **central processor unit**.

>[!note] integrated circuit
>Also called a chip. A device combining dozens to millions of transistors.

>[!note] central processor unit (CPU)
>Also called processor. The active part of the computer, which contains the datapath and control and which adds numbers, tests numbers, signals I/O devices to activate, and so on.

>[!example] Logic Board of the Apple iPhone Xs Max
>![[F000011f01-08-9780128201091.jpg]]

Descending even lower into the hardware, the image below reveals details of the microprocessor. The processor logically comprises two main components: datapath and control, the respective brawn and brain of the processor. The **datapath** performs the arithmetic operations, and **control** tells the datapath, memory, and I/O devices what to do according to the wishes of the instructions of the program. [[The Processor|Chapter 4]] explains the datapath and control for a higher performance design.

>[!note] datapath
>The component of the processor that performs arithmetic operations.

>[!note] control
>The component of the processor that commands the datapath, memory, and I/O devices according to the instructions of the program.

>[!example] The Processor Integrated Circuit Inside the A12 package.
>![[F000011f01-09-9780128201091.jpg]]

The iPhone Xs Max package in the second image also includes a memory chip with 32 gibibits or 2 GiB of capacity. The **memory** is where the programs are kept when they are running; it also contains the data needed by the running programs. The memory is a DRAM chip. _DRAM_ stands for **dynamic random access memory**. DRAMs are used together to contain the instructions and data of a program. In contrast to sequential access memories, such as magnetic tapes, the _RAM_ portion of the term _DRAM_ means that memory accesses take basically the same amount of time no matter what portion of the memory is read.

>[!note] memory
>The storage area in which programs are kept when they are running and that contains the data needed by the running programs.

>[!note] dynamic random acceess memory (DRAM)
>Memory built as an integrated circuit; it provides random access to any location. Access times are 50 ns and cost per gigabyte in 2020 was $3 to $6.

Descending into the depths of any component of the hardware reveals insights into the computer. Inside the processor is another type of memory—cache memory. **Cache memory** consists of a small, fast memory that acts as a buffer for the DRAM memory. (The nontechnical definition of _cache_ is a safe place for hiding things.) Cache is built using a different memory technology, **static random access memory (SRAM)**. SRAM is faster but less dense, and hence more expensive, than DRAM (see Chapter 5). SRAM and DRAM are two layers of the **memory hierarchy**.

>[!note] cache memory
>A small, fast memory that acts as a buffer for a slower, larger memory.

>[!note] static random access memory (SRAM)
>Also memory built as an integrated circuit, but faster and less dense than DRAM.

![[F000011icon04-9780128201091 1.jpg]]

As mentioned above, one of the great ideas to improve design is **abstractions**. One of the most important ones is the interface between the hardware and the lowest-level software. Software communicates to hardware via a "vocabulary". the words of the vocabulary are called **instructions**, and the vocabulary itself is called the **[[ISA|instruction set architecture (ISA)]]**, or simply **architecture**, of a computer. The ISA includes:

- instructions
- I/O devices
- etc.

Typically, the OS will encapsulate the details of doing I/O, allocating memory, and other low-level system functions so that application programmers don't need to worry about them. The combination of the basic instruction set and the OS interface provided for application programmers is called the **application binary interface (ABI)**.

![[F000011icon01-9780128201091 3.jpg]]

>[!note] instruction set architecture (ISA)
>Also called **architecture**. An abstract interface between the hardware and the lowest-level software that encompasses all the information necessary to write a machine language program that will run correctly, including instructions, registers, memory access, I/O, and so on.

>[!note] application binary interface (ABI)
>The user portion of the instruction set plus the operating system interfaces used by application programmers. It defines a standard for binary portability across computers.

An ISA allows computer designers to separate functions from the hardware that performs them. For example, we can talk about the functions of a digital clock (keeping time, displaying the time, setting the alarm) without bringing up the clock hardware (quartz crystal, LED displays, plastic buttons). 

In the same way, computer designers distinguish an ISA from an **implementation** of an ISA: an implementation is hardware that adherers to the ISA abstraction. These ideas bring us to another Big Picture:

>[!important] The BIG Picture
>Both hardware and software consist of hierarchical layers using abstraction, with each lower layer hiding details from the layers above. One key interface between the levels of abstraction is the *ISA* - the interface between the hardware and low-level software. This abstract interface enables many *implementations* of varying cost and performance to run identical software.

>[!note] implementation
>Hardware that obeys the architecture abstraction.

## A Safe Place for Data

Thus far, we have seen how to input data, compute using data, and display data. If we were to lose power to the computer, however, everything would be lost because the memory inside the computer is **volatile** - that is, when it loses power, it forgets. In contrast a DVD disk doesn't forget the movie when you turn off the power to the DVD player, and thus is a **nonvolatile memory** technology.

>[!note] volatile memory
>Storage, such as DRAM, that retains data only if it is receiving power.

>[!note] nonvolatile memory
>A form of memory that retains data even in the absence of a power source and that is used to store programs between runs. A DVD disk is nonvolatile.

**Main/primary memory** is equivalent to volatile memory, and **secondary memory** is equivalent to nonvolatile memory. Secondary memory is the next lower layer of the **memory hierarchy**. 

DRAMs have dominated main memory since 1975, but **magnetic disks** dominated secondary memory starting even earlier. Because of their size and form factor, personal Mobile Devices use **flash memory**, a nonvolatile semiconductor memory, instead of disks. The image of the logic board of the iPhone shows the chip containing the 64 GiB flash memory of the iPhone Xs. While slower than DRAM, it is much cheaper than DRAM in addition to being nonvolatile. Although costing more per bit than disks, it is smaller, it comes in much smaller capacities, it is more rugged, and it is more power efficient than disks. Hence, flash memory is the standard secondary memory for PMDs. Alas, unlike disks and DRAM, flash memory bits wear out after 100,000 to 1,000,000 writes. Thus, file systems must keep track of the number of writes and have a strategy to avoid wearing out storage, such as by moving popular data. Chapter 5 describes disks and flash memory in more detail.

![[F000011icon04-9780128201091 2.jpg]]

>[!note] main memory
>Also called **primary memory**. Memory used to hold programs while they are running; typically consists of DRAM in today’s computers.

>[!note] secondary memory
>Nonvolatile memory used to store programs and data between runs; typically consists of flash memory in PMDs and magnetic disks in servers.

>[!note]  magnetic disk
>Also called **hard disk**. A form of nonvolatile secondary memory composed of rotating platters coated with a magnetic recording material. Because they are rotating mechanical devices, access times are about 5 to 20 milliseconds and cost per gigabyte in 2020 was $0.01 to $0.02.

>[!note] flash memory
>A nonvolatile semi-conductor memory. It is cheaper and slower than DRAM but more expensive per bit and faster than magnetic disks. Access times are about 5 to 50 microseconds and cost per gigabyte in 2020 was $0.06 to $0.12.

## Communicating with Other Computers

We've explained how we can input, computer, display, and save data, but there is still one missing item found in today's computers: computer networks. Just as the processor is connected to memory and I/O devices, networks connect whole computers, allowing users to extend the power of computing by including communication. 

Networks have become so popular that they are the backbone of current computer systems; a new personal mobile device or server without a network interface would be ridiculed. Networked computers have several major advantages:

- _Communication_: Information is exchanged between computers at high speeds.
- _Resource sharing_: Rather than each computer having its own I/O devices, computers on the network can share I/O devices.
- _Nonlocal access_: By connecting computers over long distances, users need not be near the computer they are using.

Networks vary in length and performance, with the cost of communication increasing according to both the speed of communication and the distance that information travels. Perhaps the most popular type of network is _Ethernet_. It can be up to a kilometer long and transfer at up to 100 gigabits per second. Its length and speed make Ethernet useful to connect computers on the same floor of a building; hence, it is an example of what is generically called a **local area network**. Local area networks are interconnected with switches that can also provide routing services and security. **Wide area networks** cross continents and are the backbone of the Internet, which supports the web. They are typically based on optical fibers and are leased from telecommunication companies.

>[!note] local area network (LAN)
>A network designed to carry data within a geographically confined area, typically within a single building.

>[!note] wide area network (WAN)
>A network extended over hundreds of kilometers that can span a continent.

Networks have changed the face of computing in the last 40 years, both by becoming much more ubiquitous and by making dramatic increases in performance. In the 1970s, very few individuals had access to electronic mail, the Internet and web did not exist, and physically mailing magnetic tapes was the primary way to transfer large amounts of data between two locations. Local area networks were almost nonexistent, and the few existing wide area networks had limited capacity and restricted access.

As networking technology improved, it became much cheaper and had a much higher capacity. For example, the first standardized local area network technology, developed about 40 years ago, was a version of Ethernet that had a maximum capacity (also called bandwidth) of 10 million bits per second, typically shared by tens of, if not a hundred, computers. Today, local area network technology offers a capacity of from 1 to 100 gigabits per second, usually shared by at most a few computers. Optical communications technology has allowed similar growth in the capacity of wide area networks, from hundreds of kilobits to gigabits and from hundreds of computers connected to a worldwide network to millions of computers connected. This combination of dramatic rise in deployment of networking combined with increases in capacity have made network technology central to the information revolution of the last 30 years.

For the last 15 years another innovation in networking is reshaping the way computers communicate. Wireless technology is widespread, which enabled the PostPC Era. The ability to make a radio in the same low-cost semiconductor technology (CMOS) used for memory and microprocessors enabled a significant improvement in price, leading to an explosion in deployment. Currently available wireless technologies, called by the IEEE standard name 802.11ac, allow for transmission rates from 1 to 1300 million bits per second. Wireless technology is quite a bit different from wire-based networks, since all users in an immediate area share the airwaves.

>[!warning] Check Yourself
>- Semiconductor DRAM memory, flash memory, and disk storage differ significantly. For each technology, list its volatility, approximate relative access time, and approximate relative cost compared to DRAM.

# [[Technologies for Building Processors and Memory]]

---
# *References*