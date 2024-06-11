202406031645
Meta Tags: #class
Tags: [[OS]]

# Reading - Module 2


>2.1-2.4, 2.7-2.9

## 2-1 Operating-system services

- The design of a new OS is a major task; it is important that the goals of the system be well-defined before the design begins
- We can view an OS from several vantage points:
	- focusing on the services that the system provides
	- focusing on the interface that it makes available to users and programmers
	- focusing on its components and their interconnections

- An OS provides an environment for the execution of programs
- It provides some services that can be categorized into common classes:
![[Pasted image 20240603165953.png]]
One set of OS services provides functions that are helpful to the user:
- **User interface:** this interface can take several forms. 
	- **graphical user interface (GUI)** - the interface is a window system with a mouse that serves as a pointing device and a keyboard to enter text.
	- **touch-screen interface** - enabling users to use fingers instead
	- **command-line interface** - uses text commands and a method for entering them
- **Program execution:** the system must be able to load a program into memory and to run that program. The program must be able to end its execution, either normally or abnormally.
- **I/O Operations:** OS must provides a means to do I/O, control the I/O devices
- **File-system manipulation:** programs need to read/write files and directories. They also need to create/delete them by name, search for a given file, and list file information.
- **Communications:** when one process needs to exchange info with another; communications may be implemented via shared memory or message passing.
- **Error detection:** The OS needs to be detecting and correcting errors constantly
Another set of OS functions exists not for helping the user but rather for ensuring the efficient operation of the system itself. 
- **Resource allocation:** when there are multiple processes running at the same time, resources must be allocated to each of them. The OS manages many different types of resources.
- **Logging:** We want to keep track of which programs use how much and what kinds of computer resources
- **Protection and Security:** The owners of information stored in a multiuser/networked computer system may want to control use of that information. Security is also important.

## 2-2 User and OS Interface

### Command Interpreters

- Most OSs tread the command interpreter as a special program that is running when a process is initiated or when a user first logs on.
- On systems with multiple command interpreters to choose from, the interpreters are known as **shells**.
- C-shell, Bourne-Again shell (bash), Korn shell
- The main function of the command interpreter is to get and execute the next user-specified command. These commands can be implemented in 2 general ways:
	- the interpreter itself contains the code to execute the command. The command interpreter jumps to a section of its code that sets up parameters and makes the appropriate system call
	- implements most commands through system programs. The command interpreter doesn't understand the command - it merely used it to identify a file to be loaded into memory and executed

### Graphical User Interface

- rather than entering commands directly, users employ a mouse-based window-and-menu system characterized by a **desktop** metaphor. 

### Touch-screen interface

- Users interact with the mobile system by making gestures on the touch screen.

The UI can vary from system to system and from user to user; however, it typically is substantially removed from the actual system structure and its design is not a direct function of the OS.

## 2-3 System Calls

provide an interface to the services made available by an OS.

>[!example]
>![[Pasted image 20240603172140.png]]

### Application Programming Interface
Most programmers never see the amount of system calls that are used by the OS. Typically, application developers design programs according to an API. The API specifies a set of functions that are available to an application programmer, including the parameters that are passed to each function and the return values the programmer can expect.

Three of the most common APIs available to application programmers are the Windows API, the POSIX API, and the Java API. 

A programmer accesses an API via a library of code provided by the OS.

Benefits:
- program portability - programmer can expect program to compile/run on any system that supports the same API
- system calls can often be more detailed and difficult to work with than the API available

Another important factor in handling system calls is the **run-time environment** (RTE), the full suite of software needed to execute applications written in a given programming language, including its compilers or interpreters, as well as other software such as libraries and loaders. The RTE provides a **system-call interface** that serves as the link to system calls made available by the OS. 

The system-call interface intercepts function calls in the API and invokes the necessary system calls within the OS. Typically, a number is associated with each system call, and the system-call interface maintains a table indexed according to these numbers. The system-call interface then invokes the intended system call in the OS kernel and returns the status of the system call.

Three general methods are used to pass parameters to the OS:
1. pass the parameters in registers
2. store the parameters in a block/table in memory, and the address of the block is passed as a parameter
3. push parameters onto a stack through the program and pop the off using the OS

### Types of System Calls

- **Process control:** 
	- a running program needs to be able to halt its execution either normally (`end()`) or abnormally (`abort()`). If a syscall is made to terminate the running program abnormally, or if the program causes an error trap, a memory dump is sometimes taken and an error message is generated.
	- A process executing one program may want to `load()` and `execute()` another program. Where control is returned when the loaded program terminates decides the implementation of the system call.
	- If we create a new process/set of processes, we should be able to control their execution. This control requires the ability to determine (`get_process_attributes()`) and reset (`set_process_attributes()`) the attributes of a process. We may also want to terminate a process that we created (`terminate_process()`) if we find that it is incorrect or no longer needed
	- We may need to wait for processes to finish executing. Maybe a certain amount of time (`wait_time()`), a specific event to occur (`wait_event()`), etc. The processes should then signal when that event has occurred (`signal_event()`)
	- Quite often, 2 or more processes may share data. **Locking** shared data ensures the integrity of the data being shared. (`acquire_lock(), release_lock()`)
	    - create process, terminate process
	    - load, execute
	    - get process attributes, set process attributes
	    - wait event, signal event
	    - allocate and free memory
- **File management:**
	- We need to be able to `create()` and `delete()` files. Once the file is created, we need to `open()` it and use it. We may also `read()`, `write()`, or `reposition()` (rewind/skip to the end of the file, for example). Finally, we need to `close()` the file.
	- We may need these same sets of operations for directories. In addition, for both files and directories, we need to be able to determine the values of various attributes and set them if necessary.
	    - create file, delete file
	    - open, close
	    - read, write, reposition
	    - get file attributes, set file attributes
- **Device management:**
	- The various resources controlled by the OS can be thought of as devices. Some of these are physical while others can be thought of as abstract.
	- A system with multiple users may require us to first `request()` a device. After we are finished, we `release()` it. These are similar to `open()` and `close()` for files.
	- Once the device has been requested, we can `read()`, `write()`, and (possibly) `reposition()` the device, just as we can with files. 
	    - request device, release device
	    - read, write, reposition
	    - get device attributes, set device attributes
	    - logically attach or detach devices
- **Information maintenance:**
	- Many syscalls exist simply for the purpose of transferring info between the user program and the OS. Most systems have a syscall to return the current `time()` and `date()`.
	- Another set of syscalls is helpful in debugging. Many systems provide syscalls to `dump()` memory. 
	- In addtion, the OS keeps info about all its processes, and syscalls are used to access this info.
	    - get time or date, set time or date
	    - get system data, set system data
	    - get process, file, or device attributes
	    - set process, file, or device attributes
- **Communications:**
	- In the message-passing model, the communication processes exchange messages w/ one another to transfer info. Before communication can happen, a connection must be opened; the name of the other communicator must be known, be it another process on the same system or a process on another computer connected by a network.
	- Each computer in a network has a host name by which it is commonly known. A host also has a network identifier, such as an IP address. Similarly, each process has a process name, and this name is translated into an did by which the OS can refer to the process (`get_hostid()` and `get_processid()`).
	- The ids are then passed to the general-purpose `open()` and `close()` or to specific `open_connection()` and `close_connection()` syscalls. 
	- The recipient process usually must give permission through an `accept_connection()` call.
	- Most processes that will be receiving connections are special-purpose **daemons**, which are system programs provided for that purpose. They execute a `wait_for_connection()` call and are awakened when a connection is made. The source of communication is the client, and the receiving daemon is the server.
	- These then exchange messages through `read_message()` and `write_message()`. The `close_connection()` call terminates the communication.
	- In the shared-memory model, processes use `shared_memory_create()` and `shared_memory_attach()` syscalls to create and gain access to regions of memory owned by other processes. 
	    - create, delete communication connection
	    - send, receive messages
	    - transfer status information
	    - attach or detach remote devices
- **Protection:**
	- Provides a mechanism for controlling access to the resources provided by a computer system.
	- `set_permission()` and `get_permission()` manipulate the permission settings of resources
	- The `allow_user()` and `deny_user()` syscalls specify whether particular users can/cannot be allowed access to certain resources.
	    - get file permissions
	    - set file permissions

## 2-4 System Services

aka **system utilities**, provide a convenient environment for program development and execution. Some of them are simply user interfaces to system calls. Others are considerably more complex.
- File management - these programs create, delete, copy, rename, print, list, and generally access and manipulate files/directories
- Status information - some programs simply ask the system for the date, time, amount of available memory/disk space, number of users, etc. Others are more complex, providing detailed performance, logging, and debugging info. Typically, these programs format and print the output to the terminal/other output devices; some systems also support a **registry**, which is used to store and retrieve configuration information.
- File modification - text editors may be available to create/modify the content of files stored on disk or other storage devices
- Programming-language support - compilers, assemblers, debuggers, and interpreters for common programming languages are often provided with the OS or available as a separate download.
- Program loading/execution - Once a program is assembled or compiled, it must be loaded into memory to be executed.
- Communications - these provide the mechanism for creating virtual connections among processes, users, and computer systems
- Background services - All general-purpose systems have methods for launching certain system-program processes at boot time. Some of these terminate after completion, while others continue to run until the system is halted. Constantly running system-program processes are known as **services, subsystems, or daemons**.

## 2-7 Operating-system design and implementation

### Design Goals

The first problem in designing a system is to define goals and specifications. At the highest level, the design will be affected by the choice of hardware and the type of system: traditional desktop/laptop, mobile, distributed, or real time.

Beyond this highest design level, the requirements may be much harder to specify. They can be divided into 2 different groups:
- **user goals:** properties wanted by users in a system
- **system goals:** properties wanted by developers in a system

### Mechanisms and policies

One important principle is the separation of **policy** from **mechanism**. Mechanisms determine **how** to do something; policies determine **what** will be done.

### Implementation

- Assembly, C, C++
- Modern compilers are good at optimization
- interrupt handlers, I/O manager, memory manager, and CPU scheduler are probably the most critical routines

## 2-8 OS structure

### Monolithic Structure

Placing all of the functionality of the kernel into a single, static binary file that runs in a single address space. Everything below the system-call interface and above the hardware is the kernel. Performance is good, but are difficult to implement and extend.

![[Pasted image 20240603185545.png]]

### Layered Approach

The monolithic approach is often known as a **tightly coupled** system because changes to one part of the system can have wide-ranging effects on other parts.

Alternatively, we could design a **loosely coupled** system. Such a system is divided into separate, smaller components that have specific and limited functionality. All these components together comprise the kernel. 

A system can be made modular in many ways. One method is the **layered approach**, in which the OS is broken into a number of layers. The bottom layer is the hardware; the highest layer is the user interface.

![[Pasted image 20240603185535.png]]

An OS layer is an implementation of an abstract object made up of data and the operations that can manipulate those data. A typical OS layer consists of data structures and a set of functions that can be invoked by higher-level layers.

The main advantage is simplicity of construction and debugging. Since higher level layers only use layers below them, you can work from the bottom up with no concern. Also, higher level layers are abstracted from the lower level layers.

The overall performance is poor for purely layered systems, but **some** layering is common in contemporary OSs. 

### Microkernels

structures the OS by removing all nonessential components from the kernel and implementing them as user-level programs that reside in separate address spaces. The result is a smaller kernel. There is little consensus regarding which services should remain in the kernel and which should be implemented in user space.

The main function of the microkernel is to provide communication between the client program and the various services that are also running in user space.

One benefit of the approach is that it makes extending the OS easier. The microkernel also provides more security and reliability, since most services are running as user - rather than kernel - processes.

The performance can suffer due to increased system-function overhead.

![[Pasted image 20240603190239.png]]

### Modules

Perhaps the best current methodology for OS design involves using **loadable kernel modules** (LKMs). Here, the kernel has a set of core components and can link in additional services via modules, either at boot times or during run time.

The overall result resembles a layered system in that each kernel section has defined, protected interfaces; but it is more flexible, because any module can call any other module.

### Hybrid systems

Very few OSs adopt a single, strictly defined structure.

## 2-9 Building and Booting an OS
### OS Generation

1. Write the OS source code
2. Configure the OS for the system on which it will run
3. Compile the OS
4. Install the OS
5. Boot the computer and its new OS

- At one extreme, a sysadmin can use a configuration file to modify a copy of the OS source code. Then the OS is completely compiled (known as a **system build**)
- At a slightly less tailored level, the system description can lead to the selection of precompiled object modules from an existing library
- At the other extreme, it is possible to construct a system that is completely modular. Selection occurs at execution time rather than at compile or link time.

Steps to building a Linux system from scratch
1. Download the Linux source code
2. Configure the kernel using the `make menuconfig` command which generates the `.config` file
3. Compile the main kernel using the `make` command
4. Compile the kernel modules using the `make modules` command
5. Use the command `make modules_install` to install the kernel modules into `vmlinuz`, the kernel image.
6. Install the new kernel on the system by entering the `make install` command.

### System boot

After an OS is generated, it must be made available for use by the hardware. But how does the hardware know where the kernel is or how to load that kernel? The process of starting a computer by loading the kernel is known as **booting** the system. On most systems, the boot process proceeds as follows:
1. A small piece of code known as the **bootstrap program/boot loader** locates the kernel
2. The kernel is loaded into memory and started
3. The kernel initializes hardware
4. The root file system is mounted

Some computer systems use a multistage boot process:
- When the computer is first powered on, a small boot loader located in nonvolatile firmware known as **BIOS** is run. This initial boot loader usually does nothing more than load a second boot loader, which is located at a fixed disk location called the **boot block**.
Many recent computer systems have replaced the BIOS-based boot process with **UEFI** (Unified Extensible Firmware Interface). It has better support for 64-bit systems and larger disks. 

Whether booting from BIOS or UEFI, the bootstrap program can perform a variety of tasks:
- loading the file containing the kernel into memory (as mentioned)
- running diagnostics to determine the state of the machine
- initialize all aspects of the system from CPU registers to device controllers and the contents of main memory
- starting the OS
- mounting the root file system (at this point, the system is said to be **running**)




---
# *References*
![[Operating System Concepts - Abraham Silberschatz, Peter Bae.pdf]]