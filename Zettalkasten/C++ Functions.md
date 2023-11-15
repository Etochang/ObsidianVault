202311041421
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Functions

A function is a block of code which only runs when it is called.

You can pass data, known as parameters, into a function.

## Creation

C++ provides some pre-defined functions, such as `main()`, which is used to execute code. But you can also create your own:

```
type myFunction() { 
	//code to be executed
}
```

- myFunction() - name of function
- type - return type, void means no return value
## Calling a Function

Declared functions are not executed immediately. To call a function (execute it):

`myFunction();`

## Function Declaration and Definition

A C++ function consists of two parts:
- **Declaration**: the return type, the name of the function, and parameters (if any)
- **Definition**: the body of the function (code to be executed)

```ad-warning
A user-defined function has to be declared before the main function.

```

However, the definition can come afterwards, like so:

```
void myFunction();

int main() {
	myFunction();
	return 0;
}

void myFunction() {
	cout << "I just got executed!";
}
```

# Function Parameters

Parameters act as variables inside the function.

Parameters are specified after the function name, inside the parentheses:

```
void functionName(p1, p2, p3) {
	// definition
}
```

### Example:
```
void myFunction(string fname) {  
  cout << fname << " Refsnes\n";  
}  
  
int main() {  
  myFunction("Liam");  
  myFunction("Jenny");  
  myFunction("Anja");  
  return 0;  
}  
  
// Liam Refsnes  
// Jenny Refsnes  
// Anja Refsnes
```

>[!info]
> When a **parameter** is passed to a function, it is called an **argument**. So, from the example above: 
> `fname` is a **parameter**, while `Liam`, `Jenny` and `Anja` are **arguments**.

## Default Parameters

You can also set a default parameter value, by using `=`.

```
void myFunction(string country = "Norway") {  
  cout << country << "\n";  
}

myFunction("Sweden"); // outputs Sweden
myFunction(); // outputs Norway
```

```ad-info
A parameter with a default value, is often known as an "**optional parameter**". From the example above, `country` is an optional parameter and `"Norway"` is the default value.
```

## Passing Methods

### 1. Pass by Value

- When you pass a parameter by value, **a copy of the value is made and passed to the function**. This means that any changes made to the parameter inside the function **do not affect the original value outside the function**.
- This is suitable for simple types like integers, floats, or structs that are small and inexpensive to copy.
```
void increment(int x) { 
	x++; 
// Changes made to x do not affect the original value outside this function 
}
```

### 2. Pass by Reference

- When you pass a parameter by reference, you're actually **passing a reference to the original value in memory**. This allows the function to **directly modify the original value**.
- This is used when you want to avoid making a copy of a large or complex object.

```
void increment(int& x) {
    x++;  // Changes to x affect the original value outside this function
}
```

### 3. Pass by Pointer

- Similar to passing by reference, but in this case, you pass a pointer to the value. This gives more flexibility, as pointers can be NULL, and you can perform pointer arithmetic.

```
void increment(int* x) {
	(*x)++;  // Changes to the value pointed to by x affect the original
	         // value outside this function
}
```

### 4. Pass by Const Reference

- This is similar to passing by reference, but with the added constraint that the function promises not to modify the parameter. This can be more efficient for large objects.

```
void print(const string& str) {
    cout << str;  // This function promises not to modify str
}
```

## Passing Arrays

You can also pass arrays to a function:

```
void myFunction(int myNumbers[], size) {  
  for (int i = 0; i < size; i++) {  
    cout << myNumbers[i] << "\n";  
  }  
}  
  
int main() {  
  int myNumbers[5] = {10, 20, 30, 40, 50};  
  myFunction(myNumbers, 5);  
  return 0;  
}
```

Also see [[C++ Arrays]] for info on multidimensional arrays.

## Function Overloading

Multiple functions can have the same name with different parameters:

```
int myFunction(int x)  
float myFunction(float x)  
double myFunction(double x, double y)
```

```ad-note
Multiple functions can have the same name as long as the number and/or type of parameters are different.
```

## Recursion

Recursion is the technique of making a function call itself. This technique provides a way to break complicated problems down into simple problems which are easier to solve.

```
int sum(int k) {  
  if (k > 0) {  
    return k + sum(k - 1);  
  } else {  
    return 0;  
  }  
}  
  
int main() {  
  int result = sum(10);  
  cout << result;  
  return 0;  
}
```

>10 + sum(9)  
10 + ( 9 + sum(8) )  
10 + ( 9 + ( 8 + sum(7) ) )  
...  
10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 + sum(0)  
10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 + 0

# [[class#C++|C++ Classes]]

---
# *References*

[C++ Functions (w3schools.com)](https://www.w3schools.com/cpp/cpp_functions.asp)