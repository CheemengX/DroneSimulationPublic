# Drone Simulation Project

## Contents
- Project Overview
- The Simulation
- New Features
- UML
- Video
- Please contact me to see code as it is private

## Project Overview
The project simulates a Drone Delivery System around the University of Minnesota Campus. The robots act as packages, and users can place these robots around the campus to be delivered to a specified drop-off destination. A drone will pick up the robot and deliver them to their drop-off destination. To compile this project, we used:

- C++ Visual Studio Code
- GitHub
- Debugging Tools: GDB and Valgrind
- Documentation Tools: Google Code Styling and Doxygen
- Asset Imports: Charging Stations, Humans, Helicopters

The project started off with some given support code in the app folder and libs folder, which contained files for visualization, routing, and entity properties. Over a 3-month period, more functionality was added to the drone delivery system through the use of design patterns such as the Factory, Strategy, and Decorator pattern. To finalize the project and showcase the design patterns, two new features were added: a Weather system using the singleton pattern, and Charging Stations for the drone's battery using the Factory and Decorator pattern.

## Running the Simulation
To run the simulation, clone the repository somewhere onto your system. Then, using a terminal, navigate into the project directory and build the simulation using:
- make -j

Now that the simulation is built, you can run the simulation using:
- ./build/bin/transit_service 8081 apps/transit_service/web/

If the 8081 port is in use, connect to a different port (8082, 8083, etc) and replace 8081 in the above command with the chosen port. 


**Note:** If you are using your own machine, you will have to SSH into a CSE Lab Machine using port forwarding before running these commands. To do this, SSH into a CSE Lab Machine using the follow command:
- ssh -L 8081:127.0.0.1:8081 x500@csel-xxxx.cselabs.umn.edu

### Visualizing the Simulation
After running the simulation, navigate to the scheduling and visualization pages:
- Schedule robots at http://127.0.0.1:8081/schedule.html
- Watch the simulation at http://127.0.0.1:8081/

### Scheduling Robots
On the scheduling page, type in the name of the robot to be delivered, then click two points on the campus map for the robot to be picked up and dropped off at. Then, choose a path finding strategy for the robot. The path finding strategies consist of:
- Astar: uses the Astar path finding algorithm to determine the path 
- DFS: uses the DFS path finding algorithm to determine the path
- Dijkstra: uses the Dijkstra path finding algorithmn to determine the path

### Watch the Simulation!
After scheduling the robots, go to the visualization page and the available drone(s) should be moving to pick up the robots and drop them off at their final destination. Depending on which path finding strategy was used for the robot, the drone will travel the path found by that strategy to the final destination. The robot will also have a celebratory dance that it will do based on its path finding strategy once dropped off. In the top right, you can lock the camera view onto certain entities on the map, and you can also change the simulation speed. There is also an option to check the box that displays all of the routes given by the path finding strategies.

## New Features
Along with the basic Drone Delivery System, there are two extra features which help simulate two real-world problems with this delivery system: Weather and Battery. 

### Weather Feature
The original simulation does not consider the types of weather conditions that could affect our drone delivery service. Our first additional feature is a weather feature which affects the drone's speed and drain rate depending on the weather conditions. This feature is important to simulate real-world weather conditions that may affect automated delivery systems. If a drone was travelling through a storm, how would it react? Do certain weather conditions act as a hurdle for the drone? This is a question that our weather feature answers. 

### What Our Weather Feature Accomplishes
Our weather feature is implemented using the singleton pattern. All of the weather is generated randomly through the singleton, and all of the drones have access to the weather through the singleton. The singleton pattern was the most optimal choice for a weather feature, as it allows all entities to easily have access to the weather at runtime. 

Different weather conditions affect the drone's speed, color, and drain rate which is implemented in our charging/battery feature. Listed are the following effects of each weather condition on the drone:
- **Sunny:**  Color = Yellow, Speed = 100%,   Drain Rate = 2%
- **Rainy:**  Color = Blue, Speed = 80%,    Drain Rate = 3.6%
- **Snowy:**  Color = White,     Speed = 50%,     Drain Rate = 3%
- **Windy:**  Color = Green,     Speed = 20%,     Drain Rate = 2.4%
- **Stormy:** Color = Black,     Speed = 0%,     Drain Rate = 0%

This feature is NOT user interactable. The weather is generated on its own, and the drone's behavior is affected accordingly to the weather condition. The color is merely a visual indicator for the weather.

### Drone Battery and Charging Stations Feature
The original simulation does not consider the fact that drones run on a limited power source. Our second additional feature adds a depleting battery pack to the drone, which must be recharged by travelling to a charging station around the campus. This feature is important to simulate the real-world condition where drones are powered by some type of power source. In the real world, drones do not have an unlimited supply of battery life, so there must be a method of recharging these drones so they can deliver things. We have created charging stations for the drones to recharge their battery life if they cannot complete a trip. This feature answers the question: how would a drone conduct maintenance on itself to be able to continuously conduct deliveries?

### What Our Battery and Charging Stations Feature Accomplishes
The battery was implemented using the decorator pattern. The decorator pattern was the most optimal choice, as it allows us to flexibly add new behaviors/functionality to the drone. In this case, the new functionality to the drone was battery life. There are 5 charging stations placed around the campus which were implemented using the factory pattern. The factory pattern was the most optimal choice for adding charging stations to the simulation as it allows us to easily create entities. Starting from 100%, the drone's battery continuously drains as it travels around campus. The drone's battery depletion rate is also dependent on the weather condition in place (listed above). The drone calculates how much battery it will take to complete a trip to pick up the robot, or a trip to drop off the robot at the final destination. If the drone does not have enough battery to make a trip, it will redirect itself to the nearest charging station to recharge. Once the drone has enough battery to safely complete a trip, it will begin delivering robots again. 


## UML!
[Homework 4 UML Diagram](https://media.github.umn.edu/user/26424/files/1b616e41-e609-47ba-9012-ee938a61f084)

## Video Demonstration
https://www.youtube.com/watch?v=RCmQpRpvRYc
