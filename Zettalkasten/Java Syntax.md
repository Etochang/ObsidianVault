202401120929
Meta Tags: #definition
Tags: [[computer science]] [[programming language]] [[Java]]

# Java Syntax

>[!example] Main.java
>```
>public class Main {
>	public static void main(String\[\] args) {
>		System.out.println("Hello World!");
>	}
>}
>```

Every line of code that runs in Java **must** be inside a `class`. In the example above, we named the class `Main`. A class should always start with an uppercase first letter.

## The main Method

The `main()` method is required in every Java program:

>[!example] main Method Signature:
>```
>public static void main(String[] args)
>```

Anything inside the method will be executed.

>[!important]
>Every Java program has a `class` name which **must** match the filename, and every program **must** contain the `main()` method.

## System.out.println()

>[!example] 
>```
>public static void main(String[] args) {
>	System.out.println();
>}
>```

The `println()` method prints a line of text to the screen.

The curly braces `{}` mark the **beginning and end** of a **block of code**.

>[!note]
>`System` is a built-in Java class that contains useful members, such as `out`, which is short for "output". The `println()` method, short for "print line", is used to print a value to the screen (or a file).

# [[Java Output]]

---
# *References*