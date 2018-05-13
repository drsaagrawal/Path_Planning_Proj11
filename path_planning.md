
# Compilation

## The code compiles correctly.

No changes were made in cmake file. Only added spline.h file which make you use spline instead of polynomials.

# Valid trajectories

## The car is able to drive at least 4.32 miles without incident.

I ran the simulator for 10 and 15 miles without incidents.

## The car drives according to the speed limit.

No red message for speed limit was seen.

## Max Acceleration and Jerk are not Exceeded.

No red message for max acceleration and jerk was seen.

## Car does not have collisions.

No collisions.

## The car stays in its lane, except for the time between changing lanes.

It stays in its lane, traffic makes it to change lane.

## The car is able to change lanes

The car change lane smoothly when there is slow car infront of it and its safe to change the lane.

# Reflection

The code can be separated into different functin but I prefer to have everything in a place. Comments are provided to improve readability.
The code consist of three parts:

## Prediction

The code for this is in 255-332 lines.

This part handles the telemetry and sensor fusion data. This has three aspects:
* If there is car infront of us and blocking you.
* If there is car at the right side and not safe to change lane.
* If there is car at the left side and not safe to change lane.

Above aspect are checked by considering 20m buffer ahead and back of car.

## Behavior 

The code for this is in 352-359 lines.

This comes into role after prediction. Based on prediction, this will increase/decrease the speed or make a lane change when it is safe.

## Trajectory

The code for this is in 364-474 lines.

This will calculate trajectory based on speed and lane output from the behaviour, car coordinates and past path points.

First, the last two points from the previous path or if there is no points in previous path, the last two car position are used in conjunction three points to initialize the spline function. To decrease the complication in spline calculation, the coordinates are transformed (shift and rotate) to local car coordinates.

To maintain the continuity, remaining points are added to the vector with the previous path ponits. Points are calculated considering the reference velocity, which helps to increase or decrese the speed of car.
