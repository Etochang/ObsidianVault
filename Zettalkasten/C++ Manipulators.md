202311031634
Meta Tags: #definition
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Manipulators

Manipulators are special functions/objects that are used in conjunction with input and output operations (`<<` and `>>`) to modify the behavior or format of the data being read from or written to streams. They are part of the `<iomanip>` [[header file]] in C++.

## Commonly Used Manipulators

### **std::setw(int n)**
Sets the width of the next input or output field to be n characters:
```
std::cout << std::setw(10) << 42; // Outputs "        42"
```

### std::setprecision(int n)
Sets the precision of floating-point output:
```
std::cout << std::setprecision(4) << 3.1415926; // Outputs "3.142"
```

### std::fixed
Forces floating-point numbers to be printed in fixed-point notation (with a fixed number of decimal places).
```
std::cout << std::fixed << std::setprecision(2) << 3.1415;
// Outputs "3.14"
```

### std::scientific
Forces floating-point numbers to be printed in scientific notation.
```
std::cout << std::scientific << std::setprecision(2) << 12345.6789;
// Outputs "1.23e+04"
```

### std::boolalpha
Prints `true` or `false` for Boolean values instead of `1` or `0`. 
```
std::cout << std::boolalpha << true; // Outputs "true" instead of 1
```


---
# *References*

https://chat.openai.com/share/0f233956-2f98-4e2d-b40e-4e5572bd8993