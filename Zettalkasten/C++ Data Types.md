202310301947
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Data Types

As mentioned before, a variable in C++ must be a specified data type:

```
int myNum = 5;
float myFloat = 5.99;
double myDouble = 5.99;
char myLetter = 'D';
bool myBoolean = true;
string myText = "Hello!";
```

## Basic Data Types

The data type specifies the size and type of info that the variable will store:

| **Data Type** | **Size**  | **Description**                                                |
| ------------- | --------- | -------------------------------------------------------------- |
| `boolean`     | 1 byte    | Stores true or false values                                    |
| `char`        | 1 byte    | Stores a single character/letter/number/, or ASCII values      |
| `int`         | 2/4 bytes | Stores whole numbers, without decimals                         |
| `float`       | 4 bytes   | Stores fractional numbers, containing >=1 decimals. 6-7 digits |
| `double`      | 8 bytes   | Stores fractional numbers, containing >=1 decimals. 15 digits  ||              |           |                                                                |

### Numeric Types

Use `int` when you need to store a whole number w/o decimals, like 35 or 1000, and `float` or `double` when you need a floating point number, like 9.99 or 3.1415.

```ad-note
title: `float` vs. `double`

The **precision** of a floating point value indicates how many digits the value can have after the decimal point. The precision of `float` is only six or seven decimal digits, while `double` variables have a precision of about 15 digits. Therefore it is safer to use `double` for most calculations.

```

#### Scientific Numbers

A floating point number can also be a scientific number with an "e" to indicate the power of 10, like 35e3 or 12E4.

### Boolean Types

A boolean data type is declared with the `bool` [[keyword]] and can only take the values `true` or `false`. When the value is returned, `true = 1` and `false = 0`. 

```ad-seealso
title: Conditions

Booleans are mostly used for [[C++ Conditions|conditional testing]].

```

### Character Types

The `char` data type is used to store a **single** character. The character must be surrounded by single quotes, like 'A' or '1'.

Alternatively, ASCII values can be used to display certain characters, like `char a = 65, b = 66;`

### String Types

The `string` type is used to store a sequence of characters (text). This is not a built-in type, but it behaves like one. String values must be surrounded by double quotes, like "Hello!".

To use strings, you must include an additional [[header file]] in the source code, the `<string>` [[library]].

# [[C++ Operators]]

---
# *References*