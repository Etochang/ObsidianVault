202311081639
Meta Tags: #definition  
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Files

The `fstream` [[library]] allows us to work with files.

To use it, include both the standard `<iostream>` AND the `<fstream>` [[header file]].

There are three classes included in `fstream`, which are used to create, write or read files:

| Class      | Description                 |
| ---------- | --------------------------- |
| `ofstream` | Creates and writes to files |
| `ifstream` | Reads from files            |
| `fstream`  | `ofstream` + `ifstream`: creates, reads, and writes to files                            |

## Create and Write to a File

Use either the `ofstream` or `fstream` class, and specify the name of the file.

To write to the file, use the `<<` operator. 

```
#include <iostream>  
#include <fstream>  
using namespace std;  
  
int main() {  
  // Create and open a text file  
  ofstream MyFile("filename.txt");  
  
  // Write to the file  
  MyFile << "Files can be tricky, but it is fun enough!";  
  
  // Close the file  
  MyFile.close();  
}
```

```ad-question
title: Why do we close the file?
It is considered good practice, and it can clean up unnecessary memory space.

```

## Read a File

Use either the `ifstream` or `fstream` class, and the name of the file.

Note that we also use a `while` loop together with the `getline()` function (which belongs to the `ifstream` class) to read the file line by line, and to print the content of the file:

```
// Create a text string, which is used to output the text file  
string myText;  
  
// Read from the text file  
ifstream MyReadFile("filename.txt");  
  
// Use a while loop together with the getline() function to read the file line by line  
while (getline (MyReadFile, myText)) {  
  // Output the text from the file  
  cout << myText;  
}  
  
// Close the file  
MyReadFile.close();
```

# [[C++ Exceptions]]


---
# *References*

[C++ Files (w3schools.com)](https://www.w3schools.com/cpp/cpp_files.asp)