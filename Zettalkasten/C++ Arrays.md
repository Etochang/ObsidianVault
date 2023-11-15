202311041143
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Arrays

Arrays are used to store multiple variables in a single variable, instead of declaring separate variables for each value.

**Declaration:**
`string cars[4];`
- string is the variable type
- cars is the name
- 4 specifies the number of elements the array should store

To insert values to it, we can use an array literal (comma-separated list inside curly braces):
`string cars[4] = {"Volvo", "BMW", "Ford", "Mazda"};`

## Accessing Elements

`cout << cars[0]; // prints out "Volvo"`

## Change Array Element

`cars[0] = "Opel";`

## Omit Array Size

You don't have to specify the size of the array in C++. The compiler can determine the  size of the array based on the number of inserted values:

`string cars[] = {"Volvo", "BMW", "Ford"}; //Three array elements`

## Omit Elements on Declaration

```
string cars[5];
cars[0] = "Volvo";
cars[1] = "BMW";
```
## Get the Size of an Array

Use the `sizeof()` operator:

```
int myNums[5] = {1, 2, 3, 4, 5};
cout << sizeof(myNums); // Outputs 20
```

`sizeof()` returns size of a type in bytes. So the size of an array of type *type* would be
`sizeof(type) * numElements`. Subsequently, dividing the `sizeof()` of an array by its type will return the length, or number of elements in the array.

## Multidimensional Arrays

To declare a multidimensional array, define the variable type, the name, followed by how many elements the main array, followed by how many elements the sub-arrays should have:

`string letters[2][4];`

## Accessing Multidimensional Arrays

`cout << letter[0][2]; // accesses first row and third column of letter array`

## Change Multidimensional Element

`letters[0][0] = "Z";`

>[!note] Multidimensional Arrays as Parameters of Function
>When passing a multidimensional array to a function, you typically need to specify the dimensions of all but the first dimension. This is because the compiler needs the other dimensions of the array to deduce the size of each dimension and index properly.
>```
>void processArray(int arr[][3]) {
>	// code
>	// number of rows can be deduced by sizeof(arr)/sizeof(arr[0])
>}
>```

# [[C++ Structures]]

---
# *References*

[C++ Arrays (w3schools.com)](https://www.w3schools.com/cpp/cpp_arrays.asp)