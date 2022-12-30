---
layout: page
title: Mechanisms
nav_order: 2
parent: Robot Programming
---

# Mechanisms

* [Description](#description)
* [Mechanism Class](#mechanism-class)
* [Mechanism State](#mechanism-state)
* [Controller Functions](#controller-functions)

## Description

Mechanisms are a way that we organize our code on team 1511. Other teams may use the WPILib "Command-Based" solution and use "Subsystems" instead, but we like to use our own way of organizing our code.

## Mechanism Class

The `Mechanism` base class is a class that all robot mechanism classes [inherit](/cpp_docs/classes/#class-inheritance) from, such as `Drive`, `Controls`, and `Intake`. This class provides a number of functions to override:

1. `process()`
  - This function is meant to be called every 20ms when the mechanism is supposed to be running. For example, the `Drive` mechanism's `process()` function should be called during teleop and autonomous, but not during disabled.
2. `resetToMode(MatchMode mode)`
  - This function is meant to be called when the robot enters a specific mode. For example, when the robot switches from disabled to teleop, the mechanism's `resetToMode()` function should be called with the `MatchMode::Teleop` parameter. In this function, we like to reset the mechanism's state, stop all motors from running, and abandon any commands that are currently running.
3. `sendFeedback()`
  - This function is meant to be called during all modes to send diagnostic data the driver station via NetworkTables. The more data we send, the easier it is to debug our robot.
4. `doPersistentConfiguration()`
  - This function is meant to be called only during configuration. It's purpose is to configure the mechanism's motors and sensors, then save the configuration to flash memory. This function should __NOT__ be called during initialization or anytime during a match to prevent damage to hardware. After this function is called, a call to `resetToMode()` will follow.

Typically, whenever programming a mechanism on the robot, we will create a new class that inherits from `Mechanism` and overrides the functions we need to use.

## Mechanism State

The state of the mechanism is usually stored in a private [Enum](/cpp_docs/enums/) variable. For example, the `Drive` mechanism might have a `DriveMode` enumeration that stores whether it is stopped, under manual control, or is running a trajectory.

## Controller Functions

To control a mechanism, we usually create "Controller functions" to set it's state and properties. For example, the `Drive` mechanism could have a `tankDrive(double left, double right)` function that sets the `DriveMode` to `DriveMode::Manual` and stores the left and right motor speeds. Then in the `process()` function, we can check the `DriveMode` and the stored properties to control the motors. This way we can centralize all the code that controls the motors in one place instead of having it scattered throughout the different controller functions.
The controller functions of each mechanism are then called by the [Controls class](/robot_programming/controls/) depending on input from the game controllers and switch panel.