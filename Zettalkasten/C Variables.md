202402120955
Meta Tags: #definition  
Tags: [[C]] [[programming language]]

# C Variables

[[variable]]s are containers for storing data values, like numbers and characters. 

In C, there are different **types** of variables (defined with different keywords), for example:

- `int` - stores integers (whole numbers), without decimals, such as `123` or `-123`
- `float` - stores floating point numbers, with decimals, such as `19.99` or `-19.99`
- `char` - stores single characters, such as `'a'` or `'B'`. Characters are surrounded by **single quotes**

## Declaring Variables

Specify the **type** and assign it a **value**: `type variableName = value;`

You can also declare a variable w/o assigning the value, and assign the value later:

```
int myNum;
myNum = 15;
```

## Output Variables

It is not possible to directly use a print function to display the value of a variable:

>[!error]
>```
>int myNum = 15;
>printf(myNum); // Nothing happens
>```

## Format Specifiers

You use these to output variables; they are used together with the `printf()` function to tell the compiler what type of data the variable is storing. They are basically **placeholders** for the variable's value.

A format specifier starts with a percentage sign, `%`, followed by a character. The character represents the type of placeholder that the format specifier is.




---
# *References*