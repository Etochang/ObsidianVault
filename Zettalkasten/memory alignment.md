202310211621
Meta Tags: #concept
Tags: [[assembly language]] [[systems programming]]

# memory alignment

refers to the the practice of aligning [[memory address|memory addresses]] based on restraints imposed by underlying [[hardware architecture]]. 

The primary goal is to improve efficiency of data access by making it easy for the [[processor]] to handle data.

## Key Points

### 1. Data Size and Alignment
- Most [[processor|processors]] have a 'natural' data size that they are designed to handle well; for some, accessing data that is aligned to 4-bit or 8-bit sizes is much more efficient than handling unaligned data.
### 2. Alignment Constraints
- Different [[data type|data types]] require different alignment constraints. For example an `int` might require 4 [[byte|bytes]] while a `double` might require 8. 
### 3. Padding
- Compilers might insert extra bytes to conform to alignment constraints, ensuring that each element starts at a suitable address.
### 4. Performance Impact
- Unaligned can be much slower than aligned access, requiring extra [[memory fetch|memory fetches]] and additional processing.



---
# *References*