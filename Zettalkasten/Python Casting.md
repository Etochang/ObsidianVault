202312032054
Meta Tags: #definition #textbook 
Tags: [[computer science]] [[programming language]] [[Python]]

# Python Casting

## Specify a Variable Type

There may be times when you want to specify a [[data type|type]] on to a [[Python Variables|variable]]. This can be done with casting. Python is an [[OOP|object-orientated language]], and as such it uses [[class|classes]] to define data types, including its primitive types.

Casting in python is therefore done using constructor functions:

- `int()` - constructs an integer number from an integer literal, a float literal (by removing all decimals), or a string literal (providing the string represents a whole number)
- `float()` - constructs a float number from an integer literal, a float literal or a string literal (providing the string represents a float or an integer)
- `str()` - constructs a string from a wide variety of data types, including strings, integer literals and float literals

>[!example] Integers
>```
>x = int(1)   # x will be 1  
y = int(2.8) # y will be 2  
z = int("3") # z will be 3
>```

>[!example] Floats
>```
>x = float(1)     # x will be 1.0  
y = float(2.8)   # y will be 2.8  
z = float("3")   # z will be 3.0  
w = float("4.2") # w will be 4.2
>```

>[!example] Strings
>```
>x = str("s1") # x will be 's1'  
y = str(2)    # y will be '2'  
z = str(3.0)  # z will be '3.0'
>```

# [[Python Strings]]


---
# *References*