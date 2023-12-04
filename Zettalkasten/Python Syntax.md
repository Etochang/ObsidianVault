202312030138
Meta Tags: #definition #textbook 
Tags:

# Python Syntax

## Python Indentation

Indentation refers to the spaces at the beginning of a code line.

Where in other programming languages the indentation in code is for readability only, the indentation in Python is very important.

Python uses indentation to indicate a block of code.

>[!example]
>```
>if 5 > 2:  
>	print("Five is greater than two!")
>```

Python will give you an error if you skip the indentation:


>[!error] Syntax Error
>```
>if 5 > 2:  
>print("Five is greater than two!")
>```

The number of spaces has to be at least one, and you have to use the same amount of spaces throughout the [[program]].

## Python Variables Intro

In Python, [[variable|variables]] are created when you assign a value to it:

>[!example]
>```
>x = 5  
y = "Hello, World!"
>```
>

Python has no command for declaring a variable.

## Comments

Python has commenting capability for the purpose of in-code documentation.

Comments start with a \#, and Python will render the rest of the line as a comment.

>[!example]
>```
>#This is a comment.  
print("Hello, World!")
>```

A comment does not have to be text that explains the code, it can also be used to prevent Python from executing code:

>[!example]
>```
>#print("Hello, World!")  
print("Cheers, Mate!")
>```

### Multiline Comments

Python does not really have a syntax for multiline comments.

To add a multiline comment you could insert a `#` for each line:

>[!example]
>```
>#This is a comment  
#written in  
#more than just one line  
print("Hello, World!")
>```

>[!info] Python ignores string literals not assigned to a variable
>```
>"""  
This is a comment  
written in  
more than just one line  
"""  
print("Hello, World!")
>```

# [[Python Variables]]


---
# *References*