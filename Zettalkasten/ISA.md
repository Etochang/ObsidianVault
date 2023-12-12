202310220828
Meta Tags: #definition
Tags: [[computer organization]]

# ISA

![[Pasted image 20231108172147.jpg]]

Stands for **instruction set architecture**, and is used interchangeably with [[instruction set]]. The ISA defines the instructions that a processor can execute, but doesn't actually provide a hardware implementation - that is accomplished by the [[microarchitecture]]. 

## Key Concepts

### 1. Instructions:
- The basic operations that a [[CPU]] can perform, represented by unique binary patterns.
### 2. Registers:
- The number of registers and their capabilities are defined by the ISA, but the actual implementation is up to the [[microarchitecture]].
### 3. Data Types:
- Defines the types of data that can be used, i.e. integers, characters.
### 4. Addressing Modes
- Specifies how the [[CPU]] accesses data from [[memory]]. For example, [[direct addressing]], [[indirect addressing]], [[immediate addressing]], etc. 
### 5. Control Flow:
- [[instruction|Instructions]] for altering the execution sequence, i.e. [[function]] calls, [[conditional branch|conditional branches]], loops.
### 6. Privilege Levels:
- Some ISAs have different levels of privilege that only let certain programs or entities to use certain [[instruction|instructions]].

```ad-info
title: CISC vs. RISC
CISC (Complex Instruction Set Computing) and RISC (Reduced Instruction Set Computing) are two different design philosophies for ISAs. The former aims to provide a large set of complex instructions while the latter aims to provide a smaller set of faster, simpler instructions.

```



---
# *References*