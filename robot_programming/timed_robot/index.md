---
layout: page
title: Timed Robot
nav_order: 1
parent: Robot Programming
---

# Timed Robot

We use the `frc::TimedRobot` class as the base for our robot programs. Every robot program has a class (Typically named `Robot`) that [inherits](/cpp_docs/classes/#class-inheritance) from `frc::TimedRobot`. This class is where we write code to delegate tasks to the [Mechanism classes](/robot_programming/mechanisms/) depending on the current state of the robot.

This class provides a number of functions to override, which are called at different times during the match. The functions we use are:

  1. `RobotInit()`
  2. `DisabledInit()`
  3. `DisabledPeriodic()`
  4. `AutonomousInit()`
  5. `AutonomousPeriodic()`
  6. `TeleopInit()`
  7. `TeleopPeriodic()`
  8. `TestInit()`
  9. `TestPeriodic()`

For example, the Init functions are called when the robot enters a specific mode, and the Periodic functions are called every 20ms while the robot is in that mode. The exception is RobotInit() which is called only once when the robot is first powered on, and RobotPeriodic() which is called every 20ms regardless of the robot's state.

{: .important }
Due to the fact that the Periodic functions are called every 20ms, they should not contain any long-running code or else the robot will not respond to inputs in a timely manner. That means no long/infinite loops or constant motor configuration changes in the periodic functions!