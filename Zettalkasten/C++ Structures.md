202311041349
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Structures

Structures are a way to group several related variables into one place. They are mostly used for lightweight objects that primarily store data, as opposed to [[class#C++|classes]], which are used for complex objects with member [[C++ Functions|functions]].

Each variable in the structure is known as a **member** of the structure.

## Creation

Use the `struct` [[keyword]] and declare each of its members inside `{}`.

After the declaration, specify the name of the structure variable:

```
struct { // structure declaration
	int myNum; // member (int)
	string myString; // member (string)
} myStructure; // structure variable
```

## Access Structure Members

Use the `.` syntax.

```
myStructure.myNum = 1;
myStrucutre.myString = "Hello World!";

cout << myStructure.myNum;
cout << myStructure.myString;
```

## One Structure, Many Variables

```
struct {
	int myNum;
	string myString;
} s1, s2, s3; // multiple structure variables
```

## Named Structures

By giving a name to a structure, you can treat it as a data type, meaning you can create variables with said structure anywhere in the program at any time.

```
struct myDataType { // this struct is named "myDataType"
	int myNum;
	string myString;
}
```

To declare a variable that uses the structure, use the name of the structure as the data type of the variable:

`myDataType myVar;`

# [[C++ References]]

---
# *References*

[C++ Structures (struct) (w3schools.com)](https://www.w3schools.com/cpp/cpp_structs.asp)