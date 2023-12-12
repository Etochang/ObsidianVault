202312070520
Meta Tags: #textbook 
Tags: [[computer organization]]

# MIPS Assembly Language Programming and MARS

A software tool called an **assembler** reads an assembly language source code file and writes an **object code file** containing the equivalent machine language instructions. The **linker** is a software tool that combines multiple object code files (possibly including object code from system libraries) to create a single **executable file**. 

MARS contains an assembler and linkers that will build our executable files.

## Labels

A **label** is a name associated with a **memory location**. In MARS, labels may be written using lower/upper case letter, digits, and the underscore character, and cannot start with a digit. Labels are **case-sensitive**, so *one*, *One*, and *ONE* are three separate labels.

## Directives

Most assembly languages include **directives** which are not assembly language code, but rather are like "message" which control the assembler. In the MIPS documentation, these are referred to as *pseudo op-codes*.

### *.text*

Syntax: `.text`

>Creates a section called the text section, which is the section where instructions are written.

>[!example]
>```
>.text 
>main: 
>	li $v0, 4           # $v0 ← SysPrintStr code 
>	la $a0, hello_str   # $a0 ← addr of "Hello world.\n" 
>	syscall             # Call SysPrintStr
>```

When a source code file is assembled, the instructions which are in the `.text` section of the source code file are outputted to the `.text` section of the object code file. 

The linker, which combines all of the `.o` files together, knows that bytes in the `.text` section represent instructions and it will place all of those instructions in a section named `.text` in the binary executable file. 

The *loader* (the program in your OS that loads a program from secondary storage into RAM for execution) will place the instructions in the `.text` section of the binary in a memory region allocated just for instructions.

### *.asciiz* 

Syntax: `.asciiz string`

>Allocates space in memory for the characters of *string*. A null character will be placed in memory following the last character of *string* to form a zero-terminated string.

>[!example]
>```
>hello_str: .asciiz "Hello world.\n" # Allocates 14 bytes of memory
>```

### *.data*

Syntax: `.data`

>Creates a section called the data section, which is the section where string literals and global data are allocated.

>[!example]
>```
>.data 
>hello_str: .asciiz "Hello world.\n" # Allocates 14 bytes in the data section
>```

### *.byte* 

Syntax: `.byte value1 [, value2...]` or `.byte value : n`

>The first form allocates one or more bytes in the data section, the number depending on the number of values that are listed. Each byte will be initialized to the corresponding value. The second form allocates n bytes in the data section with each byte initialized to (the same) *value*.

>[!example]
>```
>.data 
>space_char: .byte 32 
>array1: .byte 0, 1, 2, 3 
>array2: .byte -1 : 50
>```

`space_char` is allocated one byte and is initialized to 32, which is the ASCII value of the space character. `array1` is allocated as an array of four bytes, with `array1[0]` being initialized to 0, `array1[1]` being initialized to 2, ..., and `array1[3]` to 3. `array2` is allocated as an array of fifty bytes, with each array element initialized to -1.

### *.word*

Syntax: `.word value1 [, value2...]` or `.word value : n`

>Allocates word values in the data section.

>[!example]
>```
>.data
>m: .word 100 
>array3: .word 10, 20, 30, 40, 50 
>array4: .word 18 : 22
>```

`m` is allocated one word and is initialized to 100. `array3` is an array of five words, with the elements being initialized to 10 (`array1[0]`) to 50 (`array3[4]`). `array4` is allocated as an array of 22 words, each initialized to the integer 18.

### *.space*

Syntax: `space n`

>Allocates n bytes of memory - each byte is initialized to 0 - in the data section.

>[!example]
>```
>.data 
>array5: .space 400 # Equivalent to: int array5[100] = { 0 }
>```

### *.eqv*

Syntax: `.eqv symbol expression`

>The assembler will replace occurrences of `symbol` in the source code file with `expression`. Can be used to define named constants to improve readability of the code.

>[!example]
>```
>.eqv MAX_TIME 100 
>.eqv SYS_PRINT_STR 4
>```

If you know C, this is equivalent to `#define MAX_TIME 100` and `#define SYS_PRINT_STR 4`.

## MIPS Memory Usage in the MARS Simulator

## MARS System Services

The MARS "OS" provides several useful services, invoked by the MIPS `syscall` instruction with a **service code** which must be in $v0. Refer to the MARS Help system for a complete list of services. In general, the procedure to invoke a system service is:

1. Load the service code in $v0.
2. Load any required arguments in the argument registers $a0, $a1, $a2, and $a3.
3. Issue the `syscall` instruction.
4. Retrieve any return values from the specified registers, often $v0 and $v1.

| Service       | Code | Arguments                                                   | Result                                   |
| ------------- | ---- | ----------------------------------------------------------- | ---------------------------------------- |
| Print integer | 1    | $a0 = integer to print                                      | Prints contents of $a0 to console        |
| Print string  | 4    | $a0 = addr of null-terminated string                        | Prints string to console                 |
| Read integer  | 5    |                                                             | $v0 contains integer read from keyboard  |
| Read string   | 8    | $a0 = addr of string buffer; $a1 = max num of chars to read | See MARS Help for more info              |
| Exit          | 10   |                                                             | Terminates the program                   |
| Print char    | 11   | $a0{7:0} = ASCII values of char                             | Prints ASCII char to console             |
| Read char     | 12   |                                                             | $v0 contains the char read from keyboard |





---
# *References*