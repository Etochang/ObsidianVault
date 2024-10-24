202410071611
Meta Tags: #class 
Tags:

# Zero Trust in Embedded Research

## TII - RISC-V International - ZT Hardware Design for Embedded Systems

- Attack Vectors: 
	- physical tampering
	- remote exploits 
	- firmware manipulation
	- side-channel attacks
	- sensor spoofing
- Usually, when you break into the perimeter of the system, you get access to the whole system. 
- Current security measures:
	- RoT (Root of Trust)
	- TEE (Trusted Execution Environment)
	- Sensor and flight controller redundancy
	- Secure storage (data at rest)
	- Secure boot
	- Hardened SW and HE
- Limitations: single point of failure
- To minimize lateral access:
	- least privilege access
	- micro-segmentation
	- continuous monitoring
	- minimizing implicit trust zones
- ZT in SoC design:
	- conception
	- fabrication
	- deployment
	- end-of-life
- Current Zero Trust Implementation on Al Saqr 2:
	- Confidential Computing into RISC-V
	- ML based Control Flow Integrity for RISC-V
	- Platform wide TEE
	- CHERI security capabilities for RISC-V
	- RTL Concolic testing and LLM based security vulnerability identification
	- IP / Peripheral authentication
	- Side Channels resistance
	- AI based Secure run Time Assurance
	- Supply chain security with Logic Locking
	- Test SoCs with Proof of Concepts in pipeline.

## Ultimate Guide to Embedded Systems Security - BlackBerry QNX

- **attack vector:** path an attacker/malicious process could take to compromise a system
- **attack surface:** target point of exposure, or end goal of the attack vector. (Network driver, user app, file system)
- **threat actor:** source with malicious intent
- **attacker:** individual performing malicious act in real time
- **vulnerability:** weakness that can be exploited by a threat actor to perform unauthorize actions within an embedded system/computer

### Software security vs. physical security for embedded systems

- **Physical security** keeps an unauthorized person present on location from accessing an embedded system, physically damaging it or stealing it. Physical security limits access to sensitive areas and equipment. Physical security may also include attributes of a device itself, including immutable memory tech, such as eFuses to store secure bootloader keys, tamper-resistant memory, protected key stores and security enclaves to protect sensitive code and data.
- **Software security** manages and responds to malicious behavior happening in the system, both during the initialization process and during run time. Software security features include authentication of a device to a network, firewalling network traffic and stringent hardening of system software to name a few.

### Qualities of embedded systems that affect security

#### Connected Systems

The most secure embedded system is one that is turned off, and the next most secure system is completely isolated. Embedded systems are now often connected to a communications network that exposes the system to more threat actors.

#### Cyberattack targets

All elements of the hardware and software architecture need to be secure. Each of the components of embedded system architecture creates an attack surface, from the firmware and embedded operating system (OS) to middleware and user applications. **The embedded OS, a foundational piece of embedded systems security, plays the leading role as the backbone of security for an embedded system.**

#### Design + Maintenance lifecycle

Design with patches and longevity in mind.

### Anatomy of an embedded systems exploit

1. Get network (or physical) access
2. Understand the underlying processes, hardware and embedded OS (reconnaissance)
3. Find a vulnerability in the host-based protection, such as within a programmable logic controller (PLC), embedded OS or middleware
4. Manipulate the controller
5. Exploit the vulnerability to attack the system or others

### Embedded system attack vectors

- The larger system (the host) that includes the embedded system
- The Internet or a communications network that connects the embedded system with other devices
- A physical device, such as a USB drive or disk with malicious code on it
- Vulnerabilities present in the embedded software from the beginning

### Embedded software vulnerabilities

- Buffer overflow
	- occur when a threat actor writes data or code to a memory buffer, overruns the buffer's limits and starts overwriting adjacent memory addresses. If the application uses the new data or new executable code, the threat actor may be able to take control of the system or cause it to crash
- Improper input validation
	- if an embedded system requires user input, a malicious user or process may provide unexpected input that causes an application to crash, consume too many resources, reveal confidential data or execute a malicious command. The unexpected input could be a negative value, no input at all, a path name outside of a restricted directory, or special characters that change the flow of the program
- Improper authentication
	- authentication proves users and processes are who they say they are. Improper authentication may allow a threat actor to bypass authentication, repeatedly try to guess a password, use stolen credentials or change a password with a weak password-recovery mechanism
- Improper restriction of operations within the bounds of a memory buffer
	- if the plang or the embedded OS don't restrict a program from directly accessing memory locations that are outside of the intended boundary of the memory buffer, a threat actor may be able to take control of the system or cause it to crash, much like a buffer overflow attack
- Information exposure
	- data spoofing and device hijacking are two of the ways threat actors expose sensitive info

### Security advantages of microkernel

A microkernel OS is structured with a tiny kernel space with services like file systems provided in user space, drivers or network stacks. Less code running in kernel space reduces the attack surface and increases security. The microkernel works with a team of optional cooperating processes that run outside kernel space (in the user space) and provide higher-level OS functionality. Only the core OS kernel is granted access to the entire system, and component isolation prevents an error in one component from affecting other parts of the system. a determined hacker, as long as they don't have root access, can only crash one component at a time when the system runs a microkernel OS or a secure embedded hypervisor. 

### Embedded security is a hardware-software partnership

>No matter how advanced and security-aware, software alone cannot ensure embedded systems security. Hardware, software and cloud vendors must work together. For example, hardware technologies ensure device boot integrity, and on-chip security capabilities enable robust key management and encryption, which is too computation-intensive for embedded software alone. Hardware capabilities enable the OS to provide functionality, such as access control policies, encrypted file systems, rootless execution, path space control and thread-level anomaly detection.

#### Root of trust (RoT)

Manages keys, performs encryption and decryption functions, and embeds keys for OS and application use. Often these SoC components provide CPU offload for bulk encryption and decryption, and they may also be used to offload network cryptographic functions.

During manufacturing, a private key can be generated on a chip or injected into each chip to serve as a RoT. when the private key is certified by a PKI, the secure device id can become a foundational component of trusted device connectivity.

#### Secure boot

Leverages the signature provided by a device trust anchor, the public part of the root of PKI used to sign device code. When the embedded system boots, the boot image will be validated using this public key and the corresponding trust chain to ensure that boot-time software hasn't been tampered with. Establishing the provenance of the original software and of any software updates typically relies on digital signatures from a public key cryptosystem. 

But in some instances, a hybrid model can be used. Symmetric key cryptography is used to validate software integrity and speed the boot code verification process for time-critical startup requirements. Unlike code verified with a public key, the symmetric key must remain secret, known only to the device.

#### TEE

Provides hardware-enforced isolation in a secure area built into the main processor, which allows the software developer to establish a device root of trust. A TEE may run in a secure mode of a processor or on a separated, isolated CPU core that acts as a security co-processor to the SoC. 

#### Trusted platform module (TPM)

Provides hardware-based security functions such as a cryptoprocessor to generate, store and use internal cryptographic keys; encryption of keys and other sensitive material stored in device memory; and measurement and attestation of the integrity of a system state during the boot process.

### Essential defense mechanisms of a secure OS

#### Executable space protection

Marks specific memory regions as non-executable, so that an attempt to execute machine code in those regions causes an exception.

#### Address space layout randomization

Allocates the base address of the stack, heap and shared memory regions to new locations every time a new process is executed, making buffer overflow attacks difficult.

#### Stack canaries

Allow the OS to detect a stack buffer overflow before executing malicious code. The OS places a small random integer before the stack return pointer and checks for it before overwriting memory. If the stack value has changed, the OS will stop execution and cause an exception.

| Challenge                                       | Goal                                                                                                                                                                            | Mitigation                                                                                                                                                                                     |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Data Confidentiality at Rest                    | Prevent a threat actor from seeing, modifying, or exfiltrating sensitive data on the system                                                                                     | File-based encryption                                                                                                                                                                          |
| Data Integrity                                  | Package system assets in an integrity-protected container that can be mounted at any time on the system for access                                                              | Mark all executables as non-writable  <br>  <br>Use an integrity-protected disk solution  <br>  <br>Secure boot                                                                                |
| Unrestricted Access to System Resource Managers | Prevent unauthorized system components from accessing system resource manager channels or restrict the operations they can request after they connect                           | Security policies  <br>  <br>POSIX permissions and access control lists (ACLs)                                                                                                                 |
| Filesystem Object Access Control                | Restrict access to filesystem objects by various processes                                                                                                                      | POSIX permissions and access control lists (ACLs)                                                                                                                                              |
| Untrusted Code Execution                        | Prevent a threat actor from running or loading an untrusted binary from a filesystem                                                                                            | Use a utility to mark files and filesystems as trusted                                                                                                                                         |
| Redirect Control Flow                           | Prevent a threat actor from modifying executable control flow                                                                                                                   | Use a compiler to mark the relocation sections of an executable as read-only                                                                                                                   |
| Repeatability of Attacks                        | Make it harder for an attacker to guess where code is loaded in memory                                                                                                          | Address space layout randomization (ASLR)                                                                                                                                                      |
| Buffer Overflows                                | Instrument code to mitigate potential buffer overflow attacks                                                                                                                   | Use a compiler with fortified function support to detect out-of-bounds memory accesses                                                                                                         |
| Stack Overflows                                 | Instrument code to mitigate stack overflow attacks                                                                                                                              | Compile code with stack canaries                                                                                                                                                               |
| Revealing Sensitive System Information          | Prevent a threat actor from being able to inspect the private information of other processes on the system                                                                      | Secure the /proc filesystem  <br>  <br>Security policies                                                                                                                                       |
| Process Execution with Least Privileges         | Configure the system to restrict privileges on processes to make sure that they execute with the least privileges necessary for their tasks                                     | Security policies  <br>  <br>Use a granular system of policies to govern which operations a particular process is permitted to do  <br>  <br>POSIX permissions and access control lists (ACLs) |
| Device Hardware Access to Kernel Memory         | Prevent a threat actor from using a device (such as a GPU or network card) to directly memory access (DMA) addresses to which the device has not been explicitly granted access | Use a system memory management unit manager that uses DMA containment                                                                                                                          |
| Denial of Service                               | Prevent a threat actor from interfering with critical systems by exhausting system resources                                                                                    | Set resource limits, such as setrlimit() system calls in C                                                                                                                                     |


---
# *References*
https://www.youtube.com/watch?v=gGqHGfMJOCU
https://blackberry.qnx.com/en/ultimate-guides/embedded-system-security#:~:text=Embedded%20system%20attack%20vectors,embedded%20software%20from%20the%20beginning