---
layout: page
title: ThunderAuto
nav_order: 1
parent: 1511 Software
---

# ThunderAuto

* [Description](#description)
* [Usage](#usage)
* [Robot Code](#robot-code)
    * [Movement](#movement)
    * [Actions](#actions)
* [Installation](#installation)
* [Building](#building)

## Description
ThunderAuto is a custom tool for planning autonomous paths for FRC robots.

ThunderAuto's code is hosted on GitHub [here](https://github.com/frc1511/ThunderAuto).

## Usage
When starting the program, the user has the option to either create a new project or open a previously saved one. If the user chooses to create a new project, they can customize various settings, including the maximum velocity and acceleration, the dimensions of the robot, and the field image.

<img src="/assets/images/thunderauto/screenshot_2.png" alt="ThunderAuto New Project Window" width="500">

Upon creating a new project, the user is presented with multiple windows including the Path Selector, Path Editor, and Properties Editor.

<img src="/assets/images/thunderauto/screenshot_1.png" alt="ThunderAuto Path Editor" width="800">

The Path Selector window provides the tools for selecting, creating, deleting, and renaming paths. The Path Editor displays the current path as a Bézier curve on the field image, with a gradient representing the robot's velocity (blue for slow, red/pink for fast). The user can add or remove waypoints and adjust their attributes, such as the robot's desired position, rotation, and heading, either directly in the Path Editor or by selecting a waypoint in the Path Editor and using the Properties Page's 'Point' dropdown.

In the Properties Page, the user can also flag a waypoint for the robot to stop at by checking the 'Stop' checkbox. This causes the app to calculate the robot's deceleration to a complete stop at the selected point and its subsequent acceleration as it continues the trajectory. When a waypoint is marked as stopped, the Path Editor separates the heading handles, allowing the robot to resume the path at a different angle from when it reached the point.

ThunderAuto also has a feature called Actions, which allows the user to specify specific actions for the robot to perform at certain points along the trajectory. The Properties Page's dropdown menu provides tools for creating, deleting, and renaming Actions, and for selecting which Actions should be applied to each waypoint.

When the user is satisfied with the path they have created, they can use the Properties Page's 'Export' button (under the 'Curve' dropdown) to save the path as a CSV file in the project's directory. The CSV file contains a list of timestamps corresponding to the robot's desired position, rotation, velocity, and actions.

## Robot Code
The code needed to run a ThunderAuto trajectory on the robot does not need to be complex, as the app handles most of the motion calculations before the robot executes them.

You can refer to Homer's code [here](https://github.com/petelilley/Homer) for a simple example of how to use ThunderAuto's exported CSV files to execute a trajectory.

### Movement
To begin, the exported CSV file should be placed in a location on the robot that is easy to access, such as the deploy directory. Before the trajectory can be run, the robot's program must [parse the CSV file](https://github.com/petelilley/Homer/blob/main/src/Main/Trajectory/Trajectory.cpp#L13) and create two maps that represent the path's States and Actions over time. When the trajectory is being executed, the robot needs to keep track of the elapsed time and then use this information to [sample](https://github.com/petelilley/Homer/blob/main/src/Main/Trajectory/Trajectory.cpp#L34) the current State from the map of States. Adding [linear interpolation](https://github.com/petelilley/Homer/blob/main/src/Main/Trajectory/Trajectory.cpp#L66) between States can help smooth out the trajectory. The WPILib [HolonomicDriveController](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_holonomic_drive_controller.html) class can be used to calculate the optimal axis velocities for moving the robot based on the current State (as determined by odometry) and the desired State.

### Actions
To process Actions, the robot's program must have a [list of Actions](https://github.com/frc1511/Homer/blob/main/src/Main/Autonomous/Autonomous.h#L85) that matches the one used in the app. As the robot follows the path, the program should compare the set bits in the current action bit-field with the available actions. When a match is found, the program can execute any code related to that action. "Blocking" actions can be implemented by stopping the trajectory timer, but these should only be used at waypoints where the robot is supposed to stop.

## Installation
* [Executable Download](https://github.com/petelilley/ThunderAuto/releases/latest)

Keep ThunderAuto up to date! Due to the fact that ThunderAuto is a custom tool, backwards compatibility is not guaranteed!

## Building
Supported operating systems are Windows and macOS. Make sure to resolve all the git submodules before building!
{% highlight bash %}
git submodule init
git submodule update
{% endhighlight %}

Build projects can be generated using CMake. Tested targets include Visual Studio 2019 or 2022 on Windows and Xcode or Unix Makefiles on macOS. 
#### Configure Windows
{% highlight bash %}
cmake . -B build -G "Visual Studio 16 2019" -DCMAKE_BUILD_TYPE=Release
{% endhighlight %}

#### Configure macOS
{% highlight bash %}
cmake . -B build -G "Xcode" -DCMAKE_BUILD_TYPE=Release
{% endhighlight %}

#### Build
{% highlight bash %}
cmake --build build
{% endhighlight %}

All the app's resources (Images, Fonts, etc.) are built into the executable, so there's no need to worry about moving them around once it's built.
