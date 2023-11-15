202311081705
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Exceptions

When executing C++ code, different errors can occur, whether made by the programmer, due to wrong input, or other unforeseeable things.

When an error occurs, C++ will normally stop and generate an error message. The technical term for this is: C++ will throw an **exception** (throw an error).

## try and catch

Exception handling in C++ consists of three [[keyword|keywords]]: `try`, `throw`, and `catch`:
- `try` - allows you to define a block of code to be tested for errors while it is being executed.
- `throw` - throws an exception when a problem is detected, which lets us create a custom error.
- `catch` - allows you to define a block of code to be executed, if an error occurs in the try block.

`try` and `catch` comes in pairs:

```
try {  
  // Block of code to try  
  throw _exception_; // Throw an exception when a problem arise  
}  
catch () {  
  // Block of code to handle errors  
}
```

**Consider the following example:**

```
try {  
  int age = 15;  
  if (age >= 18) {  
    cout << "Access granted - you are old enough.";  
  } else {  
    throw (age);  
  }  
}  
catch (int myNum) {  
  cout << "Access denied - You must be at least 18 years old.\n";  
  cout << "Age is: " << myNum;  
}
```

- `try` block - if `age < 18`, an exception is thrown, which will be caught by our `catch` block.
- in the `catch` block, we catch the error and do something about it. The `catch` statement takes a **parameter**: in our example we use an `int` variable (`myNum`) (because we are throwing an exception of type `int` in the `try` block (`age`)), to output the value of `age`.
- If no error occurs, the `catch` block is skipped.

You can also use the `throw` [[keyword]] to output a reference number, like a custom error number/code for organizing purposes:

```
try {  
  int age = 15;  
  if (age >= 18) {  
    cout << "Access granted - you are old enough.";  
  } else {  
    throw 505;  
  }  
}  
catch (int myNum) {  
  cout << "Access denied - You must be at least 18 years old.\n";  
  cout << "Error number: " << myNum;  
}
```

## Handle Any Type of Exception (...)

If you don't know the `throw` **type** used in the `try` block, you can also use the "three dots" syntax (`...`) inside the `catch` block, which will handle any type of exception. 

```
try {  
  int age = 15;  
  if (age >= 18) {  
    cout << "Access granted - you are old enough.";  
  } else {  
    throw 505;  
  }  
}  
catch (...) {  
  cout << "Access denied - You must be at least 18 years old.\n";  
}
```


---
# *References*

[C++ Exceptions (w3schools.com)](https://www.w3schools.com/cpp/cpp_exceptions.asp)