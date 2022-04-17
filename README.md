# Assignment 2 of the Experimental Robotics course (MSc Robotics Engineering, Unige)
This project is an extention of the work done in the experimental robotics assignment 1 which could be found here: https://github.com/ShozabAbidi10/experimental_robotics_1.


## Project Installation:

This project requires ROS with ARMOR and ROSplan packages to be install in the system. Please make sure you have alrady install it before following the instructions. 

For installing ARMOR package please follow the instructions available in this respository: https://github.com/EmaroLab/armor and for ROSPlan package please follow the instructions in this repository: https://github.com/KCL-Planning/ROSPlan.

1. Code available in **Main** branch is a ROS package which should be place in ROS workspace {ros1_ws}/src after downloading.
2. To successfully deploy and build the package run the following command.
```
catkin_make
cd devel/
source setup.bash
```
3. In order to use the python modules contained in armor_py_api package run the following command to add the path of the armor python modules to your PYTHONPATH environmental variable.
``` 
export PYTHONPATH=$PYTHONPATH:/root/ros_ws/src/armor/armor_py_api/scripts/armor_api/
```
4. Download the 'cluedo_ontology.owl' file provided in this repository and place it in the '/root/Desktop/' directory. 

## Running the Project Simulation:

1. After successfully installing the python package and other dependecies open a command window and start ROS master by using the following command:
```
roscore&
```
2. After that start the ARMOR service by using the following command:
```
rosrun armor execute it.emarolab.armor.ARMORMainService
```
3. Open the new tab in command terminal and run the ROS package launch file to start the simulation by using the following command: 
```
roslaunch erl2 assignment.launch
```
After running the command wait for the system to load all the files. Once all nodes are loaded open another terminal and execute assignment_services launch file by running the following command:
```
roslaunch erl2 assignment_services.launch
```
Once all the service nodes are completely loaded then run the rosplan_start.sh bash file in another terminal to start the planning and dispatching process. Use the following command:
```
rosrun erl2 rosplan_start.sh
```

## Software Architecture of the Project:

The project architecture based on the following main nodes. 

1. simulation.cpp
2. my_action.cpp
3. hint_collector.cpp 
4. replan.cpp
5. replan_sub.cpp
6. move_arm.cpp
7. hint_loader.py
8. set_orientation.py

## Project Simulation Demo:

https://user-images.githubusercontent.com/61094879/163715101-649eb0cc-f79e-4386-9ef6-c2675764e44f.mp4

## Code Documentation:

The code documentation is done using tools Doxygen. In the **main** branch the doxygen documentation can be found.

## Contant Info: 
1. Author: Shozab Abidi
2. Email: hasanshozab10@gmail.com
