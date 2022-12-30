---
layout: page
title: 11/5/2022
nav_order: 1
parent: Pre-Season
---

# November 5th Pre-Season Meeting

* [Description](#description)
* [IDE Overview](#ide-overview)
* [Creating a Project](#creating-a-project)
* [Robot Code Structure](#robot-code-structure)
* [Running the Robot Code](#running-the-robot-code)

## Description

This is the first hands-on meeting of the 2022-2023 Pre-Season! We will be going over how to create a robot program in VS Code, what each part of the program does, and how to run the program on the robot.

## IDE Overview

An IDE (Integrated Development Environment) is a program that centralizes all of the tools you need to write code. We use a special version of Visual Studio Code for FRC called WPILib VS Code. It contains tools to help you create, debug, and deploy robot code.

### Creating a Project

To create a project, follow [this tutorial](/tutorials/creating_project/).

## Robot Code Structure

The robot's source code can be found in the `src/main` folder. Inside of this folder, there are three folders:
* `cpp` - This is where the C++ source code is stored (.cpp files).
* `include` - This is where the C++ header files are stored (.h files).
* `deploy` - This is where random files go that need to be deployed to the robot (ex. Autonomous path files, configuration files, etc.).

For a detailed explanation of the C++ header/source file structure, see the page on C++ classes [here](/cpp_docs/classes/). A simple explaination is that the header files (.h) contain the class declarations and no actual function implementations. The source files (.cpp) contain the function implementations and other symbols.

The robot program begins with the `src/main/include/Robot.h` and `src/main/cpp/Robot.cpp` files. These files contain code for the `Robot` class, which handles the distribution of processes during the robot's runtime. The `Robot` class is a subclass of the `frc::TimedRobot` class, which provides functions that run during the robot's different states.

For example, the `Robot::RobotInit()` function is called when the robot is first turned on. The `Robot::RobotPeriodic()` function is called every 20ms while the robot is on. There are also other 'Init' and 'Periodic' functions for specific robot states, such as `Robot::AutonomousInit()` and `Robot::AutonomousPeriodic()` for when the robot is in autonomous mode. For a detailed explanation of the `frc::TimedRobot` class, see the page on it [here](/robot_programming/timed_robot/).

{% highlight cpp %}
#include <Robot.h>
#include <iostream>

void Robot::RobotInit() {
    // Called once when the robot is turned on.

    puts("RobotInit"); // Print to the console.
}

void Robot::RobotPeriodic() {
    // Called every 20ms while the robot is on. Rain or shine it is always being called.
}

void Robot::AutonomousInit() {
    // Called each time the robot enters autonomous mode.

    puts("AutonomousInit");
}

void Robot::AutonomousPeriodic() {
    // Called every 20ms while the robot is enabled in autonomous mode.
}

void Robot::TeleopInit() {
    // Called each time the robot enters teleop mode.

    puts("TeleopInit");
}

void Robot::TeleopPeriodic() {
    // Called every 20ms while the robot is enabled in teleop mode.

    puts("TeleopPeriodic");
}

void Robot::DisabledInit() {
    // Called each time the robot enters disabled mode.

    puts("DisabledInit");
}

void Robot::DisabledPeriodic() {
    // Called every 20ms while the robot is disabled.
}

void Robot::TestInit() {
    // Called each time the robot enters test mode.
    
    puts("TestInit");
}

void Robot::TestPeriodic() {
    // Called every 20ms while the robot is enabled in test mode.
}

// The main function. This is where the robot program begins. Leave it alone.
int main() {
    return frc::StartRobot<Robot>();
}
{% endhighlight %}

## Running the Robot Code

To run the robot code, you need to first build the project into an executable file that the robot can run. To do this, click on the WPILib icon in the top right corner of VS Code and select the `Build Robot Code` option from the command palette. Depending on your computer, this may take a few minutes. If you get any errors, make sure to read and try to fix them because they will prevent the robot from running. Getting an error means that the code is not valid C++, so it is impossible for the compiler to generate an executable file for the robot to run.

To deploy the code to the robot, make sure to connect to the robot's network via the Wi-Fi menu on your computer. Alternatively, an Ethernet cable or a USB-B cable can be used to manually tether the robot to your computer. Then, click on the WPILib icon and select the `Deploy Robot Code` option from the command palette. This will check to make sure the code is built, then send the program to the robot and start running it.