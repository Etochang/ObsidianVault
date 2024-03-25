202402120948
Meta Tags: #definition 
Tags: [[C]] [[programming language]]

# C Output

## Print Text

```
#include <stdio.h>

int main() {
	printf("Hello World!");
	return 0;
}
```

## Double Quotes

Text must be wrapped inside double quotation marks.

>[!error]
>```
>printf(This sentence will produce an error.);
>```

`printf()` does not insert a new line at the end of the output.

## New Lines

Use the `\n` character to insert a new line.

>[!note] What is \\n exactly?
>The newline character is called an **escape sequence**, and it forces the cursor to change its position to the beginning of the next line on the screen.

# [[C Comments]]


---
# *References*