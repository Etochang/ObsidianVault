202311041359
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ References

A reference variable is a "reference", and it is created with the `&` operator:

```
string food = "Pizza";
string &meal = food;
```

We can use either the variable name `food` or the reference name `meal` to refer to the `food` variable.

```
cout << food; // Outputs Pizza
cout << meal; // Outputs Pizza
```

## Memory Address

The `&` operator (the **reference** operator) can also be used to get the [[memory address]] of a variable, which is the location of where the variable is stored on the computer.

When a variable is created in C++, a [[memory address]] is assigned to the variable. To access it, use the `&` operator, and the result will represent where the variable is stored:

`cout < &food; // Outputs 0x7ffc30f24330

```ad-question
title: Why is it useful to know the memory address?

**References** and **pointers** are important in C++, because they give you the ability to manipulate the data in the computer's memory, which can reduce code length and improve code performance.

```

# [[C++ Pointers]]

---
# *References*

[C++ References (w3schools.com)](https://www.w3schools.com/cpp/cpp_references.asp)