202402021529
Meta Tags: #homework 
Tags: [[CSE 325]]

# Project Two Report

## Project Specifications

- Simulate Morse Code using the FRDM's onboard LEDs
	- Use Green LED for even numbered words, use Red LED for odd numbered words
	- For a dot, the chosen LED should be on for 200 ms. For a dash, 500 ms
	- The delay between dots and dashes should be 250 ms
	- The delay betwwen words should be 600 ms
- `main()`
	- `displayMorse()` should display a predetermined sentence in morse code **once**
	- After which, an infinite loop runs until the reset switch is pressed
- Reset switch
	- After switch is pressed, if currently in the infinite loop, start the message sequence again

## Implementation

### Hardware Setup

No external connections. Only using the onboard green LED (PTD5), red LED (PTE29), and SW1 (PTC3).

### Software Algorithm

>**Setup**: 

The LEDs and the switch were set up the same way as in project 1. I configured TPM0 to stop on overflow, and use the OSCERCLK (8MHz).

>**TPM**: 

Since I needed a lot of different delays (200 ms, 250 ms, 500 ms, 600 ms), I decided to create a function that would take an input of ms and delay for a corresponding amount of time. 

Since TPM0 uses OSCERCLK, that means that each incrementation of the TPM counter takes
$$\frac{1}{8 \cdot 10^6} s $$
and factoring in the prescalar factor (using 128 as default):
$$\frac{128}{8\cdot 10^6}s$$
This means that the time it takes for TPM0 to reach overflow is:
$$\frac{128}{8\cdot 10^6}(MOD+1)s$$

Now, let's say I want to have a delay of $T$ ms. 
$$T \ \text{ms} = T\cdot10^{-3} \ \text{s} = \frac{128}{8\cdot 10^6}(MOD+1)s$$

Since we can only change MOD now, let's find MOD(T).

$$T\frac{8\cdot 10^3}{128}-1=MOD$$
$$62.5T-1=MOD$$
Now that we have MOD as a function of T (delay in milliseconds), we can easily create a delay by setting MOD to a corresponding value of T and setting the return condition of the delay to be the TOF(Timer Overflow Flag) bit. This is shown in the `delay_ms()` function in my source code.


>**String to Morse Code**

First, since each character has its own unique sequence, I needed to split the predetermined sentence into characters. This was easily done, as a string in C is just an array of characters.

Second, I needed to differentiate letters on the morse code sheet from spaces, as there was a requirement for different behavior between words. I used an `if` statement to separate these cases, and created a `wordIndex` variable to keep track of even and odd words. `wordIndex` increments every time a space is reached. 

In `displayMorseChar()`, I implemented the translation from a character to a sequence of LED inputs. Since there are only dots and dashes in morse, code, I used a binary tree-like approach, where it would see if the character was one that had a dash first or a dot first, blink the LED accordingly, then see if it had a dash second or a dot second, and so on and so forth. If the character wasn't 5 dots or dashes long, the function would just return. 

To do the character comparisons, I used a regEx like approach where I created strings that contained all the characters that corresponded to a certain signal at a certain position:

`char* dot4 = "bcfhlpzBCFHLPZ45678";`

and made a function, `isCharInString`, which is pretty self-explanatory.

>**LEDs**

This was the easiest part. I made a dot and dash function for both the red and green LEDs, where I enabled the respective LED for the corresponding amount of time, and delayed for 250 ms after turning off the LED. 

When the program would reach a space character, I would delay for 350 ms instead of 600 ms, because I accounted for the 250 ms delay from the last character that was morse-coded.

## Results

Images of TPM registers, in rough chronological order:

![[tpmregister1.png]]
![[tpmregister2.png]]
![[tpmregister3.png]]
![[tpmregister4.png]]
![[tpmregister5.png]]
![[tpmregister6.png]]
![[tpmregister7.png]]

Dropbox Video:

https://www.dropbox.com/scl/fi/zbqg1vk2thtatnvxh7z7i/IMG_1985.MOV?rlkey=wj13vdejcbn679gfmls4qqniv&dl=0

## Discussion

**Some challenges I faced were:**

>No regEx in MCUXpresso

I actually tried to implement regexes for each of the comparators, but it turned out that the library isn't pre-installed in MCUXpresso.

>`char` and `char*` mixups

I had a lot of type errors for a while because I mistyped one variable declaration.

**Debugging Methods:**

I just used breakpoints, like project 1. It helped me fix some minor things in the translation of character to morse code, as I could see which characters didn't translate correctly.

**General Difficulties:**

I found the hardest part of this project to be figuring out how to instantiate TPM0. It was tedious to read through the configuration and SC registers, to see what they did.


---
# *References*