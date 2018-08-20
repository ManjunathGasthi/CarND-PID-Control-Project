## Udacity Self-Driving Car Enginer Nanodegree - PID Control Project
### Introduction

The purpose of this project was to "build a PID controller and tune the PID hyperparameters by applying the general processing flow as described in the lessons,
" and to "test your solution on the simulator!" The simulator provides cross-track error (CTE), speed, and steering angle data via local websocket. 
The PID (proportional/integral/differential) controller must respond with steering and throttle commands to drive the car reliably around the simulator track.

## Reflection
### Describe the effect each of the P, I, D components had in your implementation.

The P, or "proportional", component had the most directly observable effect on the car's behavior. 
cross-track error, or CTE is essentially how far from the middle line of the road the car is, which is proporational to Steering.
if the car is far to the right it steers hard to the left, if it's slightly to the left it steers slightly to the right.
the coefficient is set too high for P, the car will oscillate a ton, as the car will constantly overcorrect and overshoot the middle. 
If the coefficient is too low, the car may react too slowly to curves when the car gets off-center with a higher CTE.

The I, or "integral", component counteracts a bias in the CTE which prevents the P-D controller from reaching the center line. 
If the coefficient is too high for I, the car tends to have quicker oscillations, and does not tend to get up to a quick speed. 
A low coefficent for I will cause the car to tend to drift to one side of the lane or the other for longer periods of time.

The D, or "differential", component counteracts the P component's tendency to ring and overshoot the center line.
A properly tuned D parameter will cause the car to approach the center line smoothly without ringing.
if the derivative is quickly changing, the car will correct itself (i.e. higher steering angle) faster, such as in the case of a curve,
and if the car is moving outward from the middle, this will cause the steering to get larger, but if the car is moving toward the center,
the car's steering angle will get smoothed out, leading to a more smoother driving experience.  

### Finding the right coefficients

The final values were determined by manual tuning. The ratio of the coefficients to each other that I chose (0.111222,0.0043165,1.05256) seemed to work well, 
and I also tried lowering & raising them in conjunction with each other as well as tuning each individually. I typically found that I was creating too high of steering angles (causing crashes if the speed had gotten too high on a straight) by raising them in conjunction with each other, 
while lowering all of them together meant the car struggled on the larger curves, sometimes not turning enough and shooting off the track.


