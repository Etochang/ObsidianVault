202312022209
Meta Tags: #concept 
Tags: [[C++]] [[programming language]] [[computer science]]

# Automatic (Local) vs. Dynamically Allocated Variables & Objects in C++

## Automatic (Local) Variables & Objects

Automatic [[C++ Variables|variables]]/[[object|objects]] are allocated on the [[stack]], and their [[lifetime - C++|lifetimes]] are determined by the [[scope]] in which they are [[declaration|declared]]. 
### Scope

Automatic variables and objects are local to the block (within curly brace `{}`) in which they are declared. They are created when the [[program]] enters the block and destroyed when the block is exited.

```
void exampleFunction() {
	int x = 10; //Automatic variable
} //x is destroyed when this block ends
```

### Lifetime

The lifetimes of automatic variables/objects are tied to the execution of the block in which they are defined. They are automatically deallocated when the program leaves the scope:

### No Manual Cleanup

The [[compiler]] automatically manages the [[memory]] occupied by automatic variables.

## Dynamically Allocated Variables/Objects

Dynamically allocated variables/objects are created on the [[heap]] using dynamic memory allocation [[C++ Operators|operators]] like `new` and `delete`.
 
```
int* dynamicInt = new int; //dynamically allocate an int
```

### Lifetime

The lifetime is not bound by the scope in which the variables/objects are created. They persist until explicitly deallocated.

### Manual Cleanup

The `delete` operator needs to be used to release the memory occupied by the objects/variables.

```
delete dynamicInt; //release the allocated memory
```


---
# *References*