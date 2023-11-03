202311021752
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Operators

Operators are used to perform operations on variables and values.

C++ divides the operator into the following groups:
- Arithmetic
- Assignment
- Comparison/Relational
- Logical
- Bitwise
- Others

## Arithmetic:

| Operator | Name           | Description                            | Example |
| -------- | -------------- | -------------------------------------- | ------- |
| +        | Addition       | Adds together two values               | x + y   |
| -        | Subtraction    | Subtracts one value from another       | x - y   |
| *        | Multiplication | Multiplies two values                  | x * y   |
| /        | Division       | Divides one value by another           | x / y   |
| %        | Modulus        | Returns the division remainder         | x % y   |
| ++       | Increment      | Increases the value of a variable by 1 | ++x     |
| --       | Decrement      | Decreases the value of a variable by 1 | --x        |

## Assignment:

Assignment operators are used to assign values to variables.

| Operator | Example |
| -------- | ------- |
| =        | x = 5   |
| +=       | x += 5  |
| -=       | x -= 5  |
| \*=      | x \*= 5 |
| /=       | x /= 5  |
| %=       | x %= 5  |
| &=       | x &= 5  |
| \|=      | x \|= 5 |
| ^=       | x ^= 5  |
| >>=      | x >>= 5 |
| <<=      | x <<= 5        |

## Comparison/Relational:

Comparison operators are used to compare two values. The return value of a comparison is either `1` or `0`, which means true or false respectively. 

| Operator | Name                     | Example |
| -------- | ------------------------ | ------- |
| ==       | Equal to                 | x == y  |
| !=       | Not equal                | x != y  |
| >        | Greater than             | x > y   |
| <        | Less than                | x < y   |
| >=       | Greater than or equal to | x >= y  |
| <=       | Less than or equal to    | x <= y        |

## Logical:

As with comparison operators, you can also test for true and false values with logical operators.

| Operator | Description                                              | Example            |
| -------- | -------------------------------------------------------- | ------------------ |
| &&       | Returns true if both statements are true                 | x < 5 && x < 10    |
| \|\|     | Returns true if one of the statements is true            | x < 5 \|\| x > 10  |
| !        | Reverses the result, returns false if the result is true | !(x < 5 && x < 10) |

## Bitwise:

Bitwise operators are used to perform operations on individual bits. They can only be used alongside `char` and `int` data types. 

| Operator | Description             |
| -------- | ----------------------- |
| &        | Binary AND              |
| \|       | Binary OR               |
| ^        | Binary XOR              |
| ~        | Binary One's Complement |
| <<       | Binary Shift Left       |
| >>       | Binary Shift Right                        |

## Others:

| Operator | Description                                            | Example                                               |
| -------- | ------------------------------------------------------ | ----------------------------------------------------- |
| sizeof   | returns the size of data type                          | `sizeof(int); // 4`                                   |
| ?:       | returns value based on the condition                   | `string result = (5 > 0) ? "even" : "odd"; // "even"` |
| &        | represents memory address of the operand               | `&num // address of num`                              |
| .        | accesses members of structs or class objects           | `s1.marks = 92;`                                      |
| ->       | used with pointers to access class or struct variables | `ptr->marks = 92;`                                    |
| <<       | prints the output value                                | `cout << 5`                                           |
| >>       | gets the input value                                   | `cin >> num`                                                      |


---
# *References*