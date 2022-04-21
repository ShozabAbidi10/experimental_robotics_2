# Assignment 2 of the Experimental Robotics course (MSc Robotics Engineering, Unige)
This project is an extention of the work done in the assignment 1 of the experimental robotics course which can be found here: https://github.com/ShozabAbidi10/experimental_robotics_1. In the previous project, a ROS package was developed for a toy simulation of Clauedo game in which a robot explore the environment to collect hints and deduced an hypothesis about who can be the killer. 

Building upon this architectural theme, the project contains some environment simulation and task-motion planning level upgrades. For environment simulation we have developed a scene in Gazebo simulator which contains a custom made robot model with an arm attached to its base. There are four hovering points (x,y,z) in the environment with the following 'x' and 'y' coordinates (-3,0), (3,0), (0,-3), (0,3) while the position of 'z' coordinate may be either 0.75 or 1.25 which is chosen randomly everytime. These four points depicts the locations of the four rooms where robot needs to place its arm's end-effector in order to collect the hints. 

![environment](https://user-images.githubusercontent.com/61094879/164345293-a30c2c7d-5e29-4571-8ec2-f61e762f1b93.png)

Besides this there are small walls in the simulation environment which can been seen in the above picture. These walls restraint the robot to reach the points coordinates with its mobile base, therefore robot plan its arm motion to placed it over the point coordinates in order to collect the hints. Similar to the previous project the deduced hypotheses has to be consistent and correct which means it has to be based on three different types of hints and its ID needs to match the ID of the correct hypotheses. The hnts are of following types:

1. who: Robot can find a name of a person as a hint which can be a killer e.g: Prof. Plum.
2. what: Robot can find a name of a weapon as a hint which killer might have used e.g: Dagger.
3. where: Robot can find a name of random place where the crime might have been committed e.g: Hall.

Statement of a consistent hypothesis will be something like this: “Prof. Plum with the Dagger in the Hall”. Incase the deduced hypotheses is wrong then the robot will visit the rooms again for new hints until it forms a consistent hypotheses. Similar to the previous project, ARMOR package has been used to deduced the hypothesis which is developed by researchers at University of Genova. ARMOR is versatile management system that can handle single or multiple-ontology archetectures under ROS. Please find more details regarding ARMOR from here: https://github.com/EmaroLab/armor

In addition to this, we have also used ROSPlan to plan the behaviour of the our robot. ROSPlan is a framework which provides collection of tools for AI Planning in a ROS system. Its variety of nodes encapsulate planning, problem generation, and plan execution in itself. In order to used ROSPlan, problem statement of the project that we diccussed above has been translated into PDDL problem files which contains the required objects like 'robot' and 'waypoint', initial condition and goals which describe the final desire state of the environment and domain file which contains the actions that robot can opt for in order to achieve the goal like 'goto_waypoint'. At the start of the simulation we execute the planning loop services of the ROSPlan which includes problem generation, planning, parsing and dispatching. During the execution its very likely that the robot will fail to complete the goals and to overcome this, the archieture of the project is developed in the way that can sense the failure duiring execution and goes into replaning. After replanning, the robot starts the execution of the new plan and it keeps doing it until the goals are achieved/

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

The code documentation is done using Doxygen tool. In the **main** branch the doxygen documentation can be found.

## Contant Info: 
1. Author: Shozab Abidi
2. Email: hasanshozab10@gmail.com
