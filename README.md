# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program

[//]: # (Image References)

[image1]: ./examples/code_snipet.png "State Machine"
[image2]: ./examples/result.png "Result"

![alt text][image2]
  
### Simulator.
You can download the Term3 Simulator which contains the Path Planning Project from the [releases tab (https://github.com/udacity/self-driving-car-sim/releases/tag/T3_v1.2).  

To run the simulator on Mac/Linux, first make the binary file executable with the following command:
```shell
sudo chmod u+x {simulator_file_name}
```

### Goals
Implementation of highway driving, using localization and sensor fusion. Below I will address each point in the [project rubric](https://review.udacity.com/#!/rubrics/1971/view)

#### 1. The car is able to drive at least 4.32 miles without incident..
After running the finished implementation in the simulator my personal best is 6.23 miles without any incident. Although the simulation is not without any incident, they are certainly rare. For the vast majority of the ride, the car has no incidents.
#### 2. The car drives according to the speed limit.
This is achieved by using a simple if condition. Because of road obstacles the vehicle velocity is incrementally increased and decreased. While increasing the vehicle velocity I used a simple if condition that checks if the velocity is above 49.5. If it is below the velocity is incremented if it is already at the maximum value nothing happens and the car continues with the current speed.

#### 3. Max Acceleration and Jerk are not Exceeded.
This is also achieved by incrementally increasing and decreasing vehicle velocity. If there is no obstacle in front of the vehicle, with each interaction between my code and the simulator I only add 0.224 to the velocity, with that I have ensured that no sudden change in vehicle speed by accelerating. With the the max acceleration and jerk requirements are satisfied.

#### 4. Car does not have collisions.
By using the data from the sensor fusion we can get the information about other vehicles in the highway, like their position, velocity, s and d coordinates. By using Frenet coordinates we can check weather we have a vehicle in front of us and or to the left or right. With this information we can take action to avoid any collision, such as decreasing vehicle velocity or changing lanes if possible. 

#### 5. The car stays in its lane, except for the time between changing lanes.
This requirement is met by using spline.h library. By using spline we are able to smooth out the calculated path of the vehicle and ensure that sharp turns are not a problem for the vehicle to handle. 

#### 6. The car is able to change lanes
For the lane change a simple state machine is implemented. By processing the data provided by the sensor fusion module, we are able to make estimation of the position of the vehicles around us. For the lane change is is important to estimate weather there is a vehicle in the same lane we are in and that the vehicle is directly in front of us. With this we see there is a need for a lane change. We also need to make estimation weather there are any vehicles in the lanes to the left or right, or that it is possible to make a lane change. 

If there is a vehicle in front of us we simply change the lane state variable to the lane next to us that is available. If there are no lanes available we stay in the current lane and decrease speed. The default state of the state machine is the center lane. The vehicle will move back to the center lane after the lane change if there are no obstacles that prohibit that.

![alt text][image1]
