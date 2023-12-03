202311191505
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Templates

A **template** is a simple yet very powerful tool in C++.  The simple idea is to pass the *data type* as a parameter so that we **don't need to write the same code** for different data types.

```ad-example
A software company may need to sort() for different data types; rather than writing and maintaining multiple codes, we can write **one** sort() and pass the data type as a parameter.

```

C++ adds two new keywords to support templates: `template` and `typename`. The second keyword can always be replaced by the keyword `class`. 

## How do Templates Work?

Templates are expanded at [[compile time]]. The idea is simple - source code contains only function/class, but compiled code may contain multiple copies of the same function/class.

```ad-info
title: What is "expansion"?
collapse: closed
When you use a template in C++, the compiler doesn't generate actual code until you instantiate the template with a **specific data type**. 

The instantiation process first involves replacing the template parameters with the actual data type or class, and *afterwards* generating the code for that specific combination. This generation of code during compilation is what is meant by "expanding".
```
![[Pasted image 20231119151655.jpg]]

## Function Templates

A **generic function** can be used for different data types. Examples of function templates are `sort()`, `max()`, `min()`, and `printArray()`. 

```
// C++ Program to demonstrate
// Use of template
#include <iostream>
using namespace std;

// One function works for all data types. This would work
// even for user defined types if operator '>' is overloaded
template <typename T> T myMax(T x, T y)
{
	return (x > y) ? x : y;
}

int main()
{
	// Call myMax for int
	cout << myMax<int>(3, 7) << endl;
	// call myMax for double
	cout << myMax<double>(3.0, 7.0) << endl;
	// call myMax for char
	cout << myMax<char>('g', 'e') << endl;

	return 0;
}
```

## Class Templates

Like function templates, class templates are useful when a class defines something that is independent of the data type. Can be useful for classes like LinkedList, BinaryTree, Stack, Queue, Array, etc.

```
// C++ Program to implement
// template Array class
#include <iostream>
using namespace std;

template <typename T> class Array {
private:
	T* ptr;
	int size;

public:
	Array(T arr[], int s);
	void print();
};

template <typename T> 
Array<T>::Array(T arr[], int s)
{
	ptr = new T[s];
	size = s;
	for (int i = 0; i < size; i++)
		ptr[i] = arr[i];
}

template <typename T> 
void Array<T>::print()
{
	for (int i = 0; i < size; i++)
		cout << " " << *(ptr + i);
	cout << endl;
}

int main()
{
	int arr[5] = { 1, 2, 3, 4, 5 };
	Array<int> a(arr, 5);
	a.print();
	return 0;
}
```

```ad-question
title: Can there be more than one argument for templates?
collapse: closed
Yes, like normal parameters, we can pass more than one data type as arguments to templates.

`template <class T, class U>`
```

```ad-question
title: Can we specify a default value for template arguments?
collapse: closed
Yes, like normal parameters, we can specify default arguments to templates.

`template <class T = int, class U = char>`
```

```ad-question
title: What is the difference between function overloading and templates?
collapse: closed

They are both examples of polymorphism features of OOP. Function overloading is used when multiple function do quite similar (not identical) operations, whereas templates are used when multiple functions do identical operations.

```

```ad-question
title: What happens when there is a static member in a template class/function?
collapse: closed

Each instance of a template contains its own [[static]] variable.
```

```ad-question
title: What is template specialization?
collapse: closed

Template specialization allows us to have different codes for a particular data type. See [[C++ Template Specialization]] for more details.
```

```ad-question
title: Can we pass non-type parameters to templates?
collapse: closed

We can pass non-type arguments to templates. Non-type parameters are mainly used for specifying max or min values or any other constant value for a particular instance of a template. 

The important thing to note about non-type parameters is, that they must be `const`. The compiler must know its value at [[compile time]], because the compiler needs to create functions/classes for a specified non-type value at [[compile time]].
```

## Template Argument Deduction

Template argument deduction automatically deduces the data type of the argument passes to the class or function templates. This allows us to instantiate the template without explicitly specifying the data type. 

```
template <typename t>
t multiply (t num1, t num2) { return num1*num2; }
```

In general, when we want to use the multiply() function for integers, we have to do:

`multiply<int> (25, 5);`

But we can also do:

`multiply(23, 5);`





---
# *References*

[Templates in C++ with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/templates-cpp/#)