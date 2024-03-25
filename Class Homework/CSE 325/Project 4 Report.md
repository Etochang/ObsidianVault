# Project 4 Report

## Project Description

- Maintain speed of robot under different conditions using a control system.
	- The robot should wait until SW1 is pressed, after which the robot should wait 2 more seconds, then start moving in a straight line for 6 seconds. 
	- The distance covered on two different surfaces for one button press should be the same. 
	- The control system must be a PID control system.
	- At least two interrupt handlers should be used.

## Implementation

### Hardware Setup

The hardware setup was mostly the same as the previous project; the only thing different was the encoder pins, where I used Figure 3 on the Project 4 pdf to make my connections.

### Software Algorithm

I started designing the software algorithm by breaking apart the project description into base functionalities. For example:

1. Wait for SW1 press
2. When pressed, delay for two seconds
3. After delay, start going straight
4. If robot is faster or slower than ideal speed, adjust speed accordingly
5. repeat step 4 periodically until six seconds have passed
6. Go back to step 1

These were the highest level steps I could think of for this project. I then tackled them one by one, listing out the finer details:

> Wait for SW1 press:
- Use interrupt handler for PORTC
	- SW1 is active-low, so trigger interrupt on falling edge
	- put main code in this handler

> When pressed, delay for two seconds
- Reuse project 3 delay code

> After delay, start going straight
- set PWM power level to a set level for both motors
- start a timer for six seconds that runs parallel to the program
	- Use PIT - when the interrupt happens, change a variable that will stop the robot

> If robot is faster or slower than ideal speed, change robot speed accordingly
- Calculate some measure of speed
	- Use \# of encoder input periods over the amount of seconds that have passed
		- Use interrupts at PORTA to record the \# of encoder input periods
		- Use earlier TPM module to measure amount of seconds that have passed, by using periodic interrupts to increment a counter
- Compare that measure of speed to the ideal speed value for both motors
	- Hardcode ideal value of speed (measured through using a control surface and printing out the speed in the console)
	- record the error for both motors in two variables
- Use a PID control system with those comparisons to change the power of the PWMs for both motors
	- Create a variable to store the total error for both motors
	- Create a variable to store the change in the error over time (derivative)
		- Create a variable to store the last error value
	- Change the power of the two motors using two separate functions of the error variables

> Repeat step 4 periodically until six seconds have passed
- Use another PIT channel with a smaller LDVAL

> Go back to step 1
- reset the variables back to a step 1 state
	- PITs get deactivated, robot stops, waiting for SW1 interrupt

It was relatively simple to actually code the algorithm once I created such a detailed framework. In regards to robustness to change, I believe that my algorithm is relatively strong. This is because I made it easy to test different parameters and PWM coefficients.

## Results

Video (*See Discussion*):
https://www.dropbox.com/scl/fi/5kgyfnlen13ixhz12kt7t/IMG_0278.MOV?rlkey=1md0u88jgrsksipo1rbdbn4jp&dl=0

Photo of right motor encoder oscilloscope (CW direction)
![[Pasted image 20240316024729.jpg]]

Photo of left motor encoder oscilloscope (CCW direction)
![[Pasted image 20240316024755.jpg]]

## Discussions

I had some trouble with configuring the PID control system because there were a lot of parameters to tune. I also ran into a problem with my speed calculations: I used to have my PIT record the \# of encoder periods every 50 ms, which caused a significant difference in the actual speed and recorded speed. However, when I made the PIT change every 500 ms, the PID control system worked too slow compared to the 6 seconds of run time. I believe this was what caused the discrepancy in distance I had in my video.

For this project, I mainly debugged through trial and error. I tested different coefficients for the PWMs, different coefficients for the PID, and different values for the PITs until my results improved.