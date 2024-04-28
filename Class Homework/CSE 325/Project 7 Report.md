# Project 7 Report

## Description

![[Pasted image 20240423111120.png]]
1. When starting in one of the numbered positions detailed above, the robot should identify its current position using the color sensor and accordingly determine the direction it should move and where it should stop.
2. "The robot should follow the direction of traffic: if the robot is positioned on any of the locations 1-4, it should move in the anti-clockwise direction and if the robot is positioned on any of the locations 5-8, it should move in the clockwise direction."
3. The robot should move between the two black lines no matter what.
4. Table below shows destination based on the starting position:
   
| Starting Color | Destination |
| -------------- | ----------- |
| Blue (1)       | Red (4)     |
| Yellow (2)     | Red (4)     |
| Green (3)      | Blue (1)    |
| Red (4)        | Green (3)   |
| Blue (5)       | Red (8)     |
| Yellow (6)     | Red(8)      |
| Green (7)      | Blue (5)    |
| Red (8)        | Green (7)   |

## Implementation

### Hardware Setup

When I was setting up my hardware, I first verified that my project 4 code still worked. Since I didn't need the servo or ultrasonic sensor for this project, I removed them from the robot and disconnected their respective pin connections.

Then, I installed the color sensor to the bottom of my robot.  I connected the GND pin on the sensor to the ground rail on my breadboard, the 3.3V pin on the sensor to the 3.3V rail on my breadboard, the SDA pin on the sensor to PTC9 on the FRDM (I2C0_SDA), and the SCL pin on the sensor to PTC8 on the FRDM (I2C0_SCL). 

All the other connections remained the same from project 6. The diagram I used as reference is provided below:

![[Pasted image 20240423112721.png]]

### Software Setup

My algorithm is as follows:

1. initialize SW1, but not other modules so power is saved
2. Wait until SW1 is pressed, then continue 
3. initialize the rest of the modules
	1. TPM1 to increment counter w/ interrupt, TPM0 to serve as a blocking delay
	2. GPIO output pins w/o PWM enabled to serve as the motor control, w/ PWM enabled to serve as the motor power, and GPIO input pins with interrupts enabled to record encoder periods
	3. ADC0 to be able to read left and right line sensor values. Switch between the two to not use another ADC module
	4. I2C0 to setup FRDM I2C module in the master configuration
	5. Write bytes to control registers on the color sensor to configure it as a slave
4. stop and delay for 1 second, just so that the button can be pressed w/o affecting the robot movement
5. go straight for a certain amount dictated by the \# of encoder periods that have passed
6. turn 90 degrees right
7. stop and read the RGBC values from the sensor, store the color as a string in `initial_color` and `current_color`
8. Depending on what `initial_color` is, set `destination_color` to respective value and enter associated behavior loop (if `initial_color` is not a valid color, then immediately exit program)
9. While `current_color` isn't `destination_color`:
	1. Repeat `n` times:
		1. `ADC_start_conversion()` for left or right line sensor
		2. Navigate based on line sensor value:
			1. if left line sensor is black, turn right
			2. if right line sensor is black, turn left
			3. if none are black, go straight
	2. Stop and wait a little to get rid of momentum
	3. Read RGBC values from the sensor and store color in `current_color`
10. Stop to get rid of momentum
11. Go straight for a specified amount of encoder periods
12. Turn right
13. Go straight until destination has been reached

The only non-automated components of this algorithm are the initial and final distances that the robot has to go straight for. As such, I believe that my algorithm would be easy to tune in case of a change in the project directions, and that it would work very well in any similar track.

Here are some extra pseudocode blocks for the I2C and ADC:

**I2C:** 

Setup:
1. Enable Clock Gating for I2C module and port
2. Setup pin MUX for respective pins
3. Reset all I2C registers
4. Write 0x50 to FLT register to clear all bits
5. Set I2C Divider Register to get a clock frequency less than 400 kHz as specified on the sensor datasheet - uses bus clock which is 24 MHz, so any combination of mult and SCL divider that is above 60 works
6. Set bit to enable the I2C module

Write Byte:
1. Clear Status Flags
2. Send Start Signal
3. Write device address to FRDM data register + R/W bit
4. Wait for transfer to complete
5. if ACK, continue, if NACK, stop
6. Write register address to FRDM data register
7. Wait for transfer to complete
8. if ACK, continue, if NACK, stop
9. Write data byte to FRDM data register
10. Wait for transfer to complete
11. if ACK, continue, if NACK, notify Tx
12. Send stop signal

Read Block:
1. create dummy variable and clear status flags
2. send start signal
3. increment dummy variable to avoid warnings
4. Write device address to FRDM data register + R/W bit
5. Wait for transfer to complete
6. if ACK, continue, if NACK, stop
7. Write register address to FRDM data register
8. Wait for transfer to complete
9. if ACK, continue, if NACK, stop
10. Repeat start signal to start switch from Tx to Rx
11. Write device address + R/W bit
12. Wait for transfer to complete
13. if ACK, continue, if NACK, stop
14. Switch to Rx in C1
15. if block is one byte long, send NACK to indicate second to last byte
16. read dummy as second to last byte, or to initiate reading
17. for i in range 0 -> block length - 1
	1. Wait for transfer to complete
	2. if second to last byte, send NACK
	3. if last byte, send stop signal
	4. read data byte into destination array

Regarding the colors, the specific ranges are in the code. The sensor returns 16 bit resolution, with the top 8 bits being your standard 0-255 rgb values. Because these ranges were gathered strictly through trial and error, you can see them as constants to be taken for granted, not needing to be explained in this section.

**ADC:**

Initialization:
1. Enable clock gating for ports and pins
2. Set pin MUX for respective pins to ADC channels
3. Set bus clock div in CFG1 to get under 4 MHz, as specified by the line sensor data sheet
4. Enable max hardware averaging and start calibration
5. Wait for calibration to complete before adding respective gain values to PG and MG
6. disable hardware averaging
7. Set default options in SC2
8. Start conversion on channel 1 in SC1\[0\]

Start Conversion:
1. Wait for COCO (conversion complete) to set
2. if channel 0 (left) was converted previously
	1. read value into line_val_l
	2. start channel 1 (right) conversion
3. if channel 1 (right) was converted previously
	1. read value into line_val_r
	2. start channel 0 (left) conversion

## Results

Videos:

https://www.dropbox.com/scl/fi/b7mn8wvoo1n8pnw2tgjsy/IMG_2056.MOV?rlkey=05retk62lw2bx45j4yofwwxf8&dl=0

https://www.dropbox.com/scl/fi/4sri7qbo5eqm1p0th81yz/IMG_2055.MOV?rlkey=920n9ool9k2r61ucjl8axt7pk&dl=0

## Discussions

*Debugging:*
**For Colors:**

This was pretty simple. After I set up the I2C to communicate with the sensor, I just made a function that would print the values of the byte array that the `Write_Byte` function was writing to, with respective labels for clear, red, green, and blue. I then slowly dragged my robot across the areas of each color, trying to get minimum and maximum values for each color register, and afterwards creating ranges that were a little looser than the min-max values I got.

**For line sensors:**

I just slowed down my motor PWMs until the ADC could read values fast enough to react in time. The frequency was as fast as I could set it so that was the only way to fix the problem.

*Challenges:*

It was tedious to debug the robot, just because the cable would keep disconnecting. There would be this message: "Break at address 0xnnnnnnnn with no debugging information available", which is obviously not helpful. As such, I recommend that later classes provide better, or at least longer, cables to students.

I also couldn't get the ADC to work with interrupts. I followed the reference manual and the example on Canvas, but I could only get it to work in the main loop or in a function. Luckily, I was able to implement both the ADC and the I2C communication in the main loop without timing conflicts.

It was also a challenge to keep track of movement without something like an IMU. I used the encoders on the motors to measure distance relatively well, but sometimes the extra distance covered by inertia by stopping or the fact that the wheels didn't grip the surface enough messed up the calculations. As such, I recommend that students are provided with grippier tires, or perhaps a grippier testing surface.