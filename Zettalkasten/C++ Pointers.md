202311041409
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Pointers

## Creation

A **pointer** stores a [[memory address]] as its value.

A pointer variable points to a data type (like `int` or `string`) of the same type, and is created with the `*` operator. The address of the variable you're working with is assigned to the pointer:

```
string food = "Pizza";
string* foodptr = &food; //stores address of food
```

>[!tip]  Ways to declare pointer variables
> There are three ways to declare pointer variables, but the first way is preferred:
> ```
> string* mystring; //Preferred
> string *mystring;
> string * mystring;
> ```

## Dereferencing

You can also use the pointer to get the value of the variable it is pointing to by using the `*` operator (the **dereference** operator):

```
string food = "Pizza";
string* foodptr = &food; //stores address of food

cout << *foodptr; //Outputs the value of food
```

```ad-note
title: Clarification
- When used in declaration `(string* ptr)`, it creates a **pointer variable**.
- When not used in declaration, it acts as a **dereference operator**.
```

## Modifying Pointers

You can change the pointer's value with the dereference operator like:

`*foodptr = "Hamburger";`

This doesn't change the memory address of the original variable `food`, but does change the value of the original value.

```
cout << food; // Now outputs Hamburger
```

# [[C++ Functions]]

---
# *References*

[C++ Pointers (w3schools.com)](https://www.w3schools.com/cpp/cpp_pointers.asp)