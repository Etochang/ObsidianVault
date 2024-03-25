# Project 3 Report

## Project Description

- Have two motors turn the wheels of a two wheeled robot in such a manner that it can go straight, rotate in place, turn smoothly, and stop in an ordered sequence.
	- Two sequences that should be activated by SW1 and SW2 (Labeled SW3 on the board) respectively are a '5' with sharp corners, and a 'S' with smooth bends.
	- When the FRDM board is initially powered on, it should be idle.
	- The switches can be pressed in any order, but not in the middle of another switch press sequence.
	- The program should not have to be reset.

## Implementation

Explain your System Design in detail - Hardware Setup and Software Algorithm with the Pseudo code. What observations led to your design? How robust is your algorithm to changes? How often does your system work in the desired way? How did you conduct the experiments?

### Hardware Setup

The pin connection and robot assembly was completely done by following the instruction manual for the project: [Project 3: Build Robot - Motors (asu.edu)](https://canvas.asu.edu/courses/177170/assignments/4856147). The only effort on my part was finding space to put everything on a small breadboard.

The only other connections not covered in the manual were the encoder pins for the motor; I just stuck those in unpowered breadboard slots to not affect the rest of my circuit.

### Software Setup

First, before I even started to implement the project specifications, I made sure that all the pins and modules on the FRDM were setup correctly. That means that making sure the proper pins were set up as PWMs, The TPM modules had proper configuration values, the GPIO pins were correctly set to either input and output, and so on. 

Of course, during this process, I ran the problem of deciding MOD and PS for TPM2. Since the manual told me a frequency around 1 kHz was ideal, I set MOD to its max value, 65335, set the period to 1/1000, and calculated PS based off of that value. I found that the value I got was under 1, so I simply left the PS as one for TPM2. Reverse calculating the MOD value, I got 7999.

After finishing the barebones setup, I tried abstracting the details of the project from code to functions. I recognized that there were just a few basic motions that the robot was specified to do:
- move straight at a certain speed for a certain amount of time.
- rotate left/right at a certain speed for a certain amount of time.
- turn left/right at a certain speed for a certain amount of time.
- stop.
Since most of these motions required an amount of time to be counted, I initialized TPM0 to act as a counter. I decided to use the same period for TPM0 as TPM2 (1 ms) and just created a function that would take a short (in ms) as input, and go through one full period of TPM0 that many times. `delay_ms()`.

As for the speed and direction, I first looked at this table:

![[Pasted image 20240223142533.png]]

And then made functions with the specified inputs:

- `straight`: equal right CW Rotation and left CCW Rotation
- `sharp_left`: equal right CW Rotation and left CW Rotation
- `sharp_right`: equal right CCW Rotation and left CCW Rotation
- `smooth_left`: greater right CW Rotation and lesser left CCW Rotation
- `smooth_left`: lesser right CW Rotation and greater left CCW Rotation
- `stop`: set all GPIO outputs to low. 

I made each function have an input `strength` that would sort of act like a decimal 'level' for the PWM. The CnV for each TPM2 channel would be set to $c\cdot strength$, where c was a value based on the functionality above.

Since each of the individual motions worked now, I just made an infinite loop that would poll for SW1 and SW2 button presses, and do a sequence of motions based on which one was pressed. 

Regarding the specific timings to make the '5' and 'S' actually look the part, I just backpropagated through the algorithm and adjusted `delay_ms` values for each of the motion individually.

## Results

Picture of 1st level:

![[Pasted image 20240223143952.jpg]]

Picture of 2nd level:

![[Pasted image 20240223144005.jpg]]

Picture of 3rd Level:

![[Pasted image 20240223144014.jpg]]

Picture of Final Product:

![[Pasted image 20240223144027.jpg]]

Picture of Final Product (Top-Down):

![[Pasted image 20240223144038.jpg]]

Video Link:
https://www.dropbox.com/scl/fi/bp7z23966hp7mxdfcyuri/IMG_1996.MOV?rlkey=uwjnt68yudplnjb7ky7jn3c8h&dl=0

## Discussions

I found the software design and hardware setup to be rather easy - what challenged was debugging which component of the robot was faulty. Testing the voltage drop over each connection with a voltmeter was an arduous process that I don't want to go through again. 

If the problem of faulty components could be solved somehow, I think this project and later ones would go smoothly. However, with the fact that we are using lent robot kits, faulty components are an inevitability. 