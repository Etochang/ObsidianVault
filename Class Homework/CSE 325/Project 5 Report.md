# Project 5 Report


## Project Description

- Have robot navigate obstacles to reach a goal
	- The robot should wait until SW1 is pressed, after which the robot should wait 2 more seconds, then start moving.
	- The distance proximity sensor should continuously search for objects, and if there are any close by, the robot should stop.
	- The servo should then turn right, and if there is no object, turn right. Same thing for left
	- If there are objects on both sides, then the robot should do a uturn

## Implementation

### Hardware Setup

The hardware setup was mostly the same as the previous project; the only thing different was the servo and sensor pins. However, getting the servo attached to the frame of the robot was very hard, as the 3D printed frame did not match the dimensions of the servo.

### Software Algorithm

I started designing the software algorithm by breaking apart the project description into base functionalities. For example:

1. Wait for SW1 press
2. When pressed, delay for two seconds
3. After delay, start going straight
	1. Continuously poll for distance from object using PIT
	2. if distance is short, turn servo to the right
		1. if far, then turn right and servo back straight
		2. if close, servo goes to the left
			1. if far, then turn left and servo back straight
			2. if close, uturn
	3. if going backwards or away from the start-to-finish line, try to turn left or right accordingly every so often.
4. After vertical distance from start is greater than the goal distance, check if robot is within acceptable range horizontally. If not, turn accordingly and go straight to the acceptable range.
5. finish when distance travelled vertically from start point is greater than the goal distance, and when the horizontal distance from the goal is within an acceptable range.

It was relatively simple to code the navigation algorithm; after all, most of it was just logic. However, dealing with the sensor and the servo was a terrible experience, as the data sheets did not give enough information to be useful in the slightest for anything other than pinouts. Especially figuring how to correctly trigger the sensor and receive the echo.

The distance was calculated periodically by looking at the encoder periods, similar to project 4. Whether it was the horizontal or the vertical distance depended on the rotation of the robot, which I stored in an integer variable. 

## Results

Video (*See Discussion*):
https://www.dropbox.com/scl/fi/jisqwp8q9k7xk4d64c16i/IMG_0297.MOV?rlkey=9iubsuby0sc8qdngjkpeu26k0&dl=0

Photo of trigger 
![[Pasted image 20240322233654.jpg]]

Photo of echo
![[Pasted image 20240322233650.jpg]]

## Discussions

I believe that all the trouble I had during this lab was because of my servo. At first, I couldn't make sense of the data sheet so I had to spend a lot of time guessing what MOD and CnV values would make the servo turn the way I wanted to. After connecting the 3D printed mount on top of the servo, it fell off after a few turns. When I did some test runs on battery power, somehow my servo broke and started making high pitched whining sounds (as seen in my video), and at this point it was late Friday evening and I couldn't get a replacement part. My algorithm seemed to be working, so if I were to get a chance to change out my servo, I wholly believe that my robot would work as intended.