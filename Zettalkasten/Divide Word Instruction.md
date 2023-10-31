202310211655
Meta Tags: #definition  
Tags: [[MIPS]] [[assembly language]]

# Divide Word Instruction

![[Pasted image 20231021165549.png]]

The 2 32-[[bit]] words in `$src1` and `$src2` are treated as signed integers. The 32-[[bit]] quotient is written to LO an the 32-[[bit]] remainder is written to HI. These values can be moved to other [[register|registers]] using the `mfhi` and `mflo` instructions.

![[Pasted image 20231021165911.png]]


---
# *References*