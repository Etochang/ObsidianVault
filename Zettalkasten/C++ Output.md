202310301713
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]] 

# C++ Output

## Print Text

The `cout` [[C++ Objects|object]], together with the `<<` [[C++ Operators|operator]], is used to output values/print text:
```
#include <iostream>  
using namespace std;  
  
int main() {  
  **cout** << "Hello World!";  
  return 0;  
}
```
You can add as many `cout` objects as you want, but note that it doesn't insert a new line at the end of the output:
```
#include <iostream>  
using namespace std;  
  
int main() {  
  **cout** << "Hello World!";  
  **cout** << "I am learning C++";  
  return 0;  
}
```

## New Lines

To insert a new line, you can use the `\n` character:
```
#include <iostream>  
using namespace std;  
  
int main() {  
  cout << "Hello World! **\n**";  
  cout << "I am learning C++";  
  return 0;  
}
```
Another way to insert a new line, is with the `endl` [[C++ Manipulators|manipulator]]:
```
#include <iostream>  
using namespace std;  
  
int main() {  
  cout << "Hello World!" << **endl**;  
  cout << "I am learning C++";  
  return 0;  
}
```

```ad-seealso
title: Escape Sequences
Both `\n` and `endl` are used to break lines, but `\n` is more common.

**But what is `\n` exactly?**

The newline character `\n` is an [[escape sequence]] that forces the curson to change its position to the beginning of the next line on the screen. This results in a new line.
```

# [[C++ Variables]]
---
# *References*