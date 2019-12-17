# rosplan_demo_stage

This package contains:

- Launch files for two different worlds in [Stage](http://wiki.ros.org/stage).
- PDDL files for the inspection mission.
- Scripts to control the mission, including waypoint generation, sampling, task plannning, and exectuion.
- A configuration and script for the ROSPlan sensing interface.

### Demo Description

The demo has been tested with ROS melodic. The demo is an inspection mission that illustrates *Task-Aware Waypoint Sampling*. The demo should do the following:

1.  The simulation, rviz visualisation, and ROSPlan nodes are launched.
2. A goal is posted to deliver an order, which requires making several inspections.
3. A probabilistic roadmap is generated, **N** waypoints are sampled, and loaded into the ROSPlan knowledge base as PDDL objects.
4. The planner is called to generate a plan.
5. If the planner proved the problem unsolvable, **N** is increased and the waypoints are resampled (from 3).
6. If a planner timed out, then **N** is decreased and the waypoints are resampled (from 3).
7. Once a plan is produced, the demo is complete.

See image below showing the demo and rviz visualisation.

<img alt="demo screenshot" src="rosplan_waypoint_demo.png" width="50%">

### Installation

### Running

-  **Export the Turtlebot3 configuration**
```
export TURTLEBOT3_MODEL=waffle
```
- **Launch the demo**  
Begin the simulation, rviz visualisation, and ROSPlan nodes using the `lt13_filtering.launch`:
```
roslaunch rosplan_demo_stage lt13_filtering.launch
```
The launch file has the following useful arguments:
  - *approach*: sets the approach to waypoints generation; (0: task-aware waypoint sampling, 1: single dense PRM, 2: fixed waypoint generation).
  - *max_sample_size*: the maximum number of waypoints that will be sampled using the task-aware waypoint sampling approach before returning failure. The default is 50.
  - *max_prm_size*: the size of the PRM from which to sample waypoints, or the maximum size of the PRM in approach 1. The default is 1000 nodes.
  - *rviz*: if set to *false*, then the STAGE and RVIZ windows will not be displayed.
  - *objects_file*: path to the object configuration file that specifies the initial positions of each machine in the world. A number of these configuration files are available in the ROB-IS repository.
  - *hppit_file*: optional path to the hidden cost configuration file that speficies some additional preferences over where the robot is allowed to perform inspections. A number of these configuration files are available in the ROB-IS repository.
  - *initial_state*: the initial state file that specifies the goal for the problem, and corresponds to the objects file. These are also available in the ROB-IS repository.