202310301656
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Syntax

### Example Code

```
#include <iostream>  
using namespace std;  
  
int main() {  
  cout << "Hello World!";  
  return 0;  
}
```

### Explanation

**Line 1:**
`#include <iostream>` is a [[header file library]] that lets us work with input and output objects, such as `cout` (in line 5). [[header file|Header files]] add functionality to C++ programs. 

**Line 2:**
`using namespace std` means that we can use names for [[C++ Objects|objects]] and [[C++ Variables|variables]] from the standard [[library]].

**Line 3:**
A blank line; C++ ignores whitespace, but we use it to make code more readable.

**Line 4:**
`int main()` always appears in a C++ [[program]]. This is called a [[function]]. Any code inside `{}` will be executed.

**Line 5:**
`cout` is an [[C++ Objects|object]] used together with the insertion [[C++ Operators|operator]] (`<<`) to output/print text.

**Line 6:**
`return 0` ends the main function's execution.

**Line 7:**
`}` ends the main function's syntax.

## Omitting Namespace

Some C++ programs run without the standard namespace [[library]]. `using namespace std` line can be omitted and replaced with the `std` [[keyword]], followed by the `::` [[C++ Operators|operator]] for some objects:

### Example

```
#include <iostream>  
  
int main() {  
  **std::**cout << "Hello World!";  
  return 0;  
}
```

# [[C++ Output]]
---
# *References*

[C++ Syntax (w3schools.com)](https://www.w3schools.com/cpp/cpp_syntax.asp)
