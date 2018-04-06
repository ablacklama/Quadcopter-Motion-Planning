## Project: 3D Motion Planning
![Quad Image](./misc/enroute.png)

---


# Required Steps for a Passing Submission:
1. Load the 2.5D map in the colliders.csv file describing the environment.
2. Discretize the environment into a grid or graph representation.
3. Define the start and goal locations.
4. Perform a search using A* or other search algorithm.
5. Use a collinearity test or ray tracing method (like Bresenham) to remove unnecessary waypoints.
6. Return waypoints in local ECEF coordinates (format for `self.all_waypoints` is [N, E, altitude, heading], where the drone’s start location corresponds to [0, 0, 0, 0].
7. Write it up.
8. Congratulations!  Your Done!

## [Rubric](https://review.udacity.com/#!/rubrics/1534/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

`*this`

### Explain the Starter Code

#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`
The path planning utils file contains functions to create a descritized grid, to run an a_star search on a grid with a start and goal location, and a heuristic function for it. It also contains an enumerated action class with a function to return all possible actions from a given state.

The motion planning file contains the code in charge of the brain of the drone. The MotionPlanning class is derived from the Udacidrone and uses callbacks to decide what the drone should do next. This class manages the states the drone could be in, the transitions between states, and what to do in each state. 

### Implementing Your Path Planning Algorithm

#### 1. Set your global home position
Extracted lat0 and lon0 as floats and used `set_home_position` to pass the values to Udacidrone.

#### 2. Set your current local position
Udacidrone automattically sets my local position if I tell it my global home position. 

#### 3. Set grid start position from local position
This was done using the offsets provided by the `create_grid` function. I took the ceilling of the local position minus the grid offset, and converted it to an int.

#### 4. Set grid goal position from geodetic coords
This can be done by either changing the default lat and lon values in the file, or passing --goal_lat --goal_lon and --goal_alt as arguments when running the file. This goal is then turned into local coordinates and passed to a_star.

#### 5. Modify A* to include diagonal motion (or replace A* altogether)
A* has been modified to use diagonal movement as well. I also added a `nearest_open` function to find the nearest point to the goal that doesn't have an obsical in it. This is only used if the goal is blocked.

#### 6. Cull waypoints 
i used a collinearity check  here to itterate through the waypoints and remove the middle of any 3 points that were collinear. 

### Execute the flight
#### 1. Does it work?
It does work. There are problems with the udacity simulator though. Some places are blocked via obstacles in the code but don't have anything blocking them in the simulator.

### Double check that you've met specifications for each of the [rubric](https://review.udacity.com/#!/rubrics/1534/view) points.
  



