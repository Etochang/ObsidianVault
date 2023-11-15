202311031512
Meta Tags: #definition  
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Strings

A `string` variable contains a collection of characters surrounded by double quotes:

```
string greeting = "Hello";
```

To use strings, you must include an additional [[header file]] in the source code, the `<string>` [[library]]:

```
#include <string>
```

## Concatenation

The `+` operator can be used between strings to add them together to make a new string. This is called **concatenation**.

### Append

A string in C++ is actually an [[C++ Objects|object]], which contains functions that can perform certain operations on strings. For example, you can also concatenate strings with the `append()` function:

```
string firstName = "John ";
string lastName = "Doe";
string fullName = firstName.append(lastName);
cout << fullName;
```

## Numbers and Strings

If you add two numbers, the result will be a number. If you add two strings, the result will be a string concatenation. If you try to add a number to a string, an error occurs.

>[!error]
>```
>string x = "10";
>int y = 20;
>string z = x + y;
>```

```ad-seealso
title: Characters and Numbers
In C++, you can add integers to characters. When you do this, the integer value is treated as an ASCII code, and the character is converted to its corresponding ASCII value.

```

## String Length

To get the length of a string, use the `length()` function:

```
string txt = "ASDFGHJKL";
cout << "The length of the text string is: " << txt.length();
```
 
 ```ad-tip
title: `length()` vs. `size()`
`size()` is just an alias of `length()`. They are interchangeable.
```

## Access Strings

You can access the characters in a string by referring to its index number inside square brackets `[]`.

```ad-note
title: String Indexes
String indexes start with 0: [0] is the first character, [1] is the second character, etc.

```

### Change String Characters

```
string myString = "hello!";
myString[0] = 'J';
cout << myString; //Jello! instead of hello!
```

## Special Characters in Strings

The backslash (`\`) escape character turns special characters into string characters.

## User Input Strings

It is possible to use the extraction operator `>>` on `cin` to store a string entered by a user. However, `cin` considers a space (whitespace, tabs, etc) as a terminating characters, which means that it can only store a single word.

That's why we often use the `getline()` function to read a line of text. It takes `cin` as the first parameter, and the string variable as second:

`getline (cin, fullName);`

## Omitting Namespace

The `using namespace std` line can be omitted and replaced with the `std` [[keyword]], followed by the `::` operator for `string` and `cout` objects.

# [[C++ Math]]

---
# *References*

[C++ Strings (w3schools.com)](https://www.w3schools.com/cpp/cpp_strings.asp)