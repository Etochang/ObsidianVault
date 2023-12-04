202312030216
Meta Tags: #definition #textbook 
Tags: [[Python]] [[programming language]] [[computer science]]

# Python Variables

Again, Python has no command for [[declaration|declaring]] a [[variable]]. A variable is created the moment you first assign a value to it.

>[!example]
>```
>x = 5  
y = "John"  
print(x)  
print(y)
>```

Variables do not need to be declared with any particular *[[data type|type]]*, and can even change type after they have been set.

>[!example]
>```
>x = 4       # x is of type int  
x = "Sally" # x is now of type str  
print(x)
>```

## Casting

If you want to specify the data type of a variable, you can cast it:

>[!example]
>```
>x = str(3)    # x will be '3'  
y = int(3)    # y will be 3  
z = float(3)  # z will be 3.0
>```

## Get the Type

You can get the data type of a variable with the `type()` function.

>[!example]
>```
>x = 5  
y = "John"  
print(type(x))  
print(type(y))
>```

## Single or Double Quotes?

String variables can be declared either by using single or double quotes:

>[!example]
>```
>x = "John"  
"is the same as"  
x = 'John'
>```

## Case-Sensitive

>[!example] This will create two variables:
>```
>a = 4  
A = "Sally"  
#A will not overwrite a
>```

## Variable Names

A variable can have a short name (like x and y) or a more descriptive name (age, carname, total_volume). Rules for Python variables:

- A variable name must start with a letter or the underscore character
- A variable name cannot start with a number
- A variable name can only contain alpha-numeric characters and underscores (A-z, 0-9, and _ )
- Variable names are case-sensitive (age, Age and AGE are three different variables)
- A variable name cannot be any of the [Python keywords](https://www.w3schools.com/python/python_ref_keywords.asp).

##  Assigning Multiple Values

>[!example]
>```
>x, y, z = "Orange", "Banana", "Cherry"  
print(x)  
print(y)  
print(z)
>```

>[!note]
>Make sure the number of variables matches the number of values, or else you will get an error.

### Unpacking a Collection

If you have a collection of values in a list, tuple etc. Python allows you to extract the values into variables. This is called _unpacking_.

>[!example] Unpacking a list:
>```
>fruits = ["apple", "banana", "cherry"]  
x, y, z = fruits  
print(x)  
print(y)  
print(z)
>```

## Output Variables

The Python `print()` function is often used to output variables.

>[!example]
>```
>x = "Python is awesome"  
print(x)
>```

In the `print()` function, you output multiple variables, separated by a comma:

>[!example]
>```
>x = "Python"  
y = "is"  
z = "awesome"  
print(x, y, z) #puts a space between each variable
>```

You can also use the `+` operator to output multiple variables:

>[!example]
>```
>x = "Python "  
y = "is "  
z = "awesome"  
print(x + y + z) #doesn't put a space between each variable
>```

For numbers, the `+` character works as a mathematical operator:

>[!example]
>```
>x = 5  
y = 10  
print(x + y)
>```

In the `print()` function, when you try to combine a string and a number with the `+` operator, Python will give you an error:

>[!error] TypeError
>```
>x = 5  
y = "John"  
print(x + y)
>```

The best way to output multiple variables in the `print()` function is to separate them with commas, which even support different data types:

>[!example]
>```
>x = 5  
y = "John"  
print(x, y)
>```

## Global Variables

Variables that are created outside of a [[function]] (as in all of the examples above) are known as global variables.

Global variables can be used by everyone, both inside of functions and outside.

>[!example]
>```
>x = "awesome"  
def myfunc():  
  print("Python is " + x)  #awesome
myfunc()
>```

If you create a variable with the same name inside a function, this variable will be local, and can only be used inside the function. The global variable with the same name will remain as it was, global and with the original value.

>[!example]
>```
>x = "awesome"  
def myfunc():  
  x = "fantastic"  
  print("Python is " + x)  #fantastic
myfunc()  
print("Python is " + x) #awesome
>```

### The global keyword

Normally, when you create a variable inside a function, that variable is local, and can only be used inside that function.

To create a global variable inside a function, you can use the `global` keyword.

>[!example]
>```
>def myfunc():  
  global x  
  x = "fantastic"  
myfunc()  
print("Python is " + x) #fantastic
>```

Also, use the `global` keyword if you want to change a global variable inside a function.

>[!example]
>```
>x = "awesome"
>def myfunc():  
  global x  
  x = "fantastic"  
myfunc()  
print("Python is " + x) #fantastic
>```
# [[Python Data Types]]


---
# *References*