202310301729
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Variables

Variables are containers for storing data values.

In C++, there are different **types** of variables (defined w/ different [[keyword|keywords]]):
- `int` - stores integers (whole numbers), w/o decimals, such as 123 or -123
- `double` - stores floats, with decimals, such as 19.99 or -19.99
- `char` - stores single characters, such as 'a' or 'B'. Char values are surrounded by single quotes
- `string` - stores text, such as "Hello World". String values are surrounded by double quotes
- `bool` - stores values with two states: true or false

## Declaring Variables

To create a variable, specify the type and assign it a value:

`type variableName = value;`

where `type` is one of the C++ types, and variableName is the name of the variable. The **equal sign** is used to assign values to the variable. 

To create a variable that should store a number:

`int myNum = 15;`

You can also declare a variable w/o assigning the value, and assign the value later:

```
int myNum;
myNum = 15;
cout << myNum;
```

## Display Variables

The `cout` [[C++ Objects|object]] is used together with the `<<` [[C++ Operators|operator]] to display variables.

To combine both text and a variable, separate them with `<<`:

```
int myAge = 35;
cout << "I am " << myAge << " years old.";
```

## Add Variables Together

To add a variable to another variable, you can use the `+` [[C++ Operators|operator]]:

```
int x = 5;
int y = 6;
int sum = x + y;
cout << sum;
```


## Declaring Many Variables

To declare more than one variable of the **same type**, use a comma-separated list:

```
int x = 5, y = 6, z = 50;
cout << x + y + z;
```

## One Value to Multiple Variables

You can also assign the **same value** to multiple variable in one line:

```
int x, y, z;
x = y = z = 50;
cout << x + y + z;
```

## Constants

To make a variable **unchangeable and read-only**, use the `const` [[keyword]]:

```
const int myNum = 15; // myNum will always be 15
myNum = 10; //error: assignment of read-only variable 'myNum'
```

You should always declare the variable as constant when you have values that are unlikely to change:

```
const int minutesPerHour = 60;
const float PI = 3.14;
```


# [[C++ User Input]]

---
# *References*

[C++ Variables (w3schools.com)](https://www.w3schools.com/cpp/cpp_variables.asp)