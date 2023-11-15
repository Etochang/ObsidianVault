202311041132
Meta Tags: #definition  
Tags: [[computer science]] [[programming language]] [[C++]]

# C++ Loops

## While Loop

Loops through a block of code as long as the specified condition is `true`. Each time the loop is 'entered', it checks the condition.

```
// checks condition before execution
while (condition) {
	// code block to be executed
}
```
## Do/While Loop

Variant of the `while` loop. Will execute the code block one, before checking if the condition is true.

```
do {
	// code block to be executed
}
while (condition); // checks condition after execution
```

```ad-important
title: While Loop Tip
**Note:** Do not forget to increase the variable used in the condition, otherwise the loop will never end!

```

## For Loop

Use the `for` loop when you know exactly how many times you want to loop through a block of code:

```
for (executeBeforeCodeOnce; condition; executeAfterCode) {
	// code block to be executed
}
// Basically just a while loop with necessary code integrated into syntax
```

## foreach Loop

Used exclusively to loop through elements in a data set:

```
for (type variableName : datasetName) {
	// code block to be executed
}
```

## Break

As seen before in the `switch` statement, the `break` statement is used to 'jump out' of things. In the context of loops, the `break` statement is used to jump out of the current loop.

## Continue

The `continue` statement breaks one iteration (in the loop) and continues with the next iteration in the loop.

# [[C++ Arrays]]

---
# *References*

[C++ Switch (w3schools.com)](https://www.w3schools.com/cpp/cpp_switch.asp)