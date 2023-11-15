202311041123
Meta Tags: #definition 
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Conditions

C++ has the following conditional statements:
- `if` to specify a block of code to be executed, if a specified condition is true
- `else` to specify a block of code to be executed, if the same condition is false
- `else if` to specify a new condition to test, if the first condition is false
- `switch` to specify many alternative blocks of code to be executed

## if, elseif, else statements

```
if (condition1) {
	//executed if the condition1 is true
} else if (condition2) {
	//executed if condition2 is true and condition1 is false
} else {
	//executed if both condition1 and condition2 are false
}
```

>[!info] Short Hand If...Else (Ternary Operator)
>`variable = (condition) ? expressionTrue : expressionFalse;`
>
>instead of:
>
>```
>if (condition) {
>	variable = expressionTrue;
>} else {
>	variable = expressionFalse;
>}
>```

## switch statement

```
switch(expression) {
	case x:
		//code block if expression == x
		break;
	case y:
		//code block if expression == y
		break;
	default:
		//code block if expression != x and expression != y
}
```

# [[C++ Loops]]


---
# *References*

[C++ If ... Else (w3schools.com)](https://www.w3schools.com/cpp/cpp_conditions.asp)