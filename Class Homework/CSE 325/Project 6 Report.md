# Project 6 Report

## Description

1. The robot, when turned on, should stay idle until SW1 is pressed. 
2. When SW1 is pressed, the robot should start moving along the black line underneath it, and when it meets an obstacle in front of it, it should avoid it from the left and eventually return to the black line.
3. The robot should trace a full circle around a predetermined path.

## Implementation

### Hardware Setup:

The new things regarding hardware were the two line sensors. The electrical connections were straightforward, as the info is on the project pdf, but there was experimentation involved in finding the right height for the sensors to work properly. I looked up the board online, and people recommend to put it 3mm away from the detected surface; I used two nuts on each screw to put the sensor as close as possible to the surface without affecting the functionality of the robot itself.

### Software Setup:

For the black line tracing, I first had to figure out what values were being outputted by the sensor to my board through the ADC. I initialized the ADC by referencing the reference manual and the example on Canvas, and I used the debug console to see what values corresponded to black and white. black was around 220-250 while white was around 150-180, so I put my threshold as 200.

I didn't use interrupts - instead, I 'sectioned' off my main function into two behaviors, "avoiding" and "tracing". "Tracing" would happen when no obstacle has been detected (code from last project) and avoiding isn't the current state, and "avoiding" would happen when an object was detected by the ultrasonic sensor. 

For "tracing", when the left line sensor sensed black, I made the robot turn slightly to the left, and vice versa for the right line sensor. For "avoiding", I disabled the ADC and instead used the code from project 5, marking my current horizontal position and hugging the obstacle until the same horizontal position was met again.

I also used the same vertical distance variable to limit the distance the robot would go; I manually tuned this value until my robot went a full circle. 

I also noticed that the track on the pdf had sharp corners, and my robot did successfully traverse those. However, the track in the lab was too big, and if my robot went across the sharp corners, it would fall off the table.

## Results

https://www.dropbox.com/scl/fi/keevctj9xktl5ezcisjvb/IMG_0314.MOV?rlkey=54mipgvh9dsbavpsvvyabb8sd&dl=0

## Discussions

One challenge I faced was the lack of friction on the track. Sometimes my wheels would slip, thus throwing off the line-tracing system. I couldn't really fix this, but luckily it didn't happen too often.

I also had some trouble with initializing the ADC, and the solution to that was just carefully going over the reference manual and Canvas modules.

The most useful debugging tool for me was the console, as I could see where exactly my code went wrong with a few well-placed printf statements.