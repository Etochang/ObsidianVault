202401252255
Meta Tags: #homework 
Tags: [[CSE 325]]

# Project One Report

## Project Specifications

- Roughly simulate a traffic light by utilizing the onboard LEDs (red, green) and an external LED (yellow, connected to a GPIO pin of your choice).
	- When the FRDM board is turned on, the red LED should turn on as well. 
	- After a delay, the green LED should turn on and the red LED should turn off. After another delay, the green should turn off and the yellow should turn on. Afterwards, the red LED should come on again, with the yellow turning off. This cycle should repeat until a switch of your choice is pressed.
- The LED behavior should change when the switch is pressed.
	- If the switch is pressed, only the yellow LED should blink.
	- If the switch is released after being pressed, the LEDs should return to their normal behavior.
## Implementation

### Hardware Setup

The setup for this project was relatively simple. The red and green LEDs were internal, connected to PTE29 and PTD5 respectively, so the only external connection I had to make was for the yellow LED. I put a M-M connector from PTD6 to the anode of the yellow LED, and another M-M connector from the cathode of the yellow LED to one of the ground terminals on the FRDM board. 

The voltage across the yellow LED when PTD6 is active is about 2.1V (checked with multimeter), so no resistor was needed. 

### Software Algorithm w/ Pseudocode

The specifications of this project made the number of outputs and inputs obvious, thankfully. Since there were three LEDs (two onboard), I needed to configure 3 GPIO pins to be outputs, two of them predetermined by the schematic; the button pin was also predetermined, but I need to configure it as an input. 

So, I found the ports for the red LED, green LED, SW1, and selected a random GPIO pin for the yellow LED.

| Port | Object |
| ---- | ---- |
| PTD5 | Green LED (Onboard) |
| PTD6 | Yellow LED (External) |
| PTE29 | Red LED (Onboard) |
| PTC3 | SW1 (Onboard) |

To configure these ports before entering my program loop, I had to go through a couple of steps. The actual code is in my source code, but here's the gist:

```
// enable clock gating for PORTC, PORTD, PORTE
SCGC5 |= PTCmask, PTDmask, PTEmask;

clear signal mux bits for PTD6, PTD5, PTE29;
clear signal mux and PE/PS bits for PTC3;

PCR PTD6 = GPIOMode;
PCR PTD5 = GPIOMode;
PCR PTE29 = GPIOMode;
PCR PTC3 = GPIOMode + PullEnable/PullSelect;

PTD6 PDDR = OutputMode;
PTD5 PDDR = OutputMode;
PTE29 PDDR = OutputMode;
PTC3 PDDR = InputMode;

// turn all leds to inactive state which
// depends on active-low or active-high
PTD6 = inactive;
PTD5 = inactive;
PTE29 = inactive;
```

Regarding the actual loop itself, I used a counter and if statements to create a "delay" between the switching of lights, and created an exit case that would go to the "toggle yellow led" code if the button was pressed:

```
while(true) {
	increment counter;
	if(button_not_pressed) {
		if (counter reaches a value) {
			turn red LED on, others off
		}
		if (counter reaches another value) {
			turn green LED on, others off
		}
		if (counter reaches ANOTHER value) {
			turn yellow LED on, others off
		}
 	}
 	else
 	{
	 	turn off red and green LEDs
	 	
	 	if (counter reaches a value) {
		 	toggle yellow LED between on and off
	 	}
 	}
}
```

I used if statements and a counter instead of an actual delay because I wanted to make the button press functionality more responsive. If I used a delay, the program would have to wait until the delay ended to start toggling the yellow LED, but with this configuration, the button condition is checked every time the counter is incremented, which is a very small amount of time.

The actual performance of the program was very good; it worked exactly how I thought it would, and how the project wanted it to work.  I went step by step through the debugger, set a breakpoint in every if statement, noted the state of the board at each moment, and checked the Peripherals+ tab: it followed the specifications very well. Perhaps the switching of the lights was too fast for the project to accurately model a traffic light, but the base functionality was completely there.

I did test my program with other ports for my external LED, but that was the extent of what I could play around with. The specifications of this project are too strict to change anything else, as 3/4 of the components are onboard and have predetermined connections.

I also shook the board a little, spammed SW1 and didn't clear the registers from test to test, and the program pulled through regardless. As such, I think the implementation is very stable.

## Results

### GPIO Register Images

**After the configuration code:**
![[afterportsetupenteringloop.png]]

**Before yellow LED turns on (regular behavior):**
![[yellowturnon_1.png]]

**After yellow LED turns on (regular behavior):**
![[yellowturnon_2.png]]

**Before yellow LED toggles (button behavior):**
![[yellowtoggle_1.png]]

**After yellow LED toggle (button behavior):**
![[yellowtoggle_2.png]]

**Dropbox Video Link:**
https://www.dropbox.com/scl/fi/u2c3awn2hrdrfvz082ubh/IMG_1977.MOV?rlkey=qsc6hu3ldfk11x13xjh46vp8y&dl=0

## Discussions

The one tool I used the most was breakpoints. They helped me solve a few issues while I was developing the algorithm for this project, such as:

### Active-Low, Active-High Debacles

I was really confused for a good hour because I thought every LED (including the external one) was active-low. I went step by step through the portions where I turned the yellow LED on and off using breakpoints, and I figured out that the external one was active-high.

### D13 is PTD5

I had an issue where the yellow LED was turning on even though it should have been turning off. Through breakpoints, I figured out that whenever my green LED would turn off, my yellow external LED would turn on, and vice versa. It turned out that the header I put my M-M connector into at first, D13, was actually connected to PTD5, the port for the green onboard LED. The program worked immediately after I changed ports.

>I will definitely be cross-checking the schematic and user manual more often going forward.


---
# *References*

[Report Format (asu.edu)](https://canvas.asu.edu/courses/177170/assignments/4930563)
