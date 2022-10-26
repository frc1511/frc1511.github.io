---
layout: page
title: Important Stuff
nav_order: 2
---

# Important Stuff
* [SVN](#svn)
* [Official Documentation](#official-documentation)
* [Miscellaneous](#miscellaneous)

## SVN
On team 1511, we use a version control software called SVN (short for "Subversion") to keep track of changes to our code. SVN allows us to incrementally "commit" our code changes, allowing us to have a comprehensive history of the codebase. When working on a project with others, SVN can help merge people's code changes together and help maintain a centralized version of the codebase.

Detailed instructions about how to setup SVN can be found [here](https://wiki.penfieldrobotics.com/wiki/index.php?title=SVN_Setup).

The SVN repositories from previous years are stored at [svn.penfieldrobotics.com](https://svn.penfieldrobotics.com).

## Official Documentation
Utilizing the official documentation for the individual vendor APIs is an essential skill for programmers on the team. Knowing when to use the functionality of each API can make it easier to find solutions to problems.
* [FRC Control System Documentation](http://docs.wpilib.org/)
  - Documentation for the FRC Control System and comprehensive examples for most things.
* [WPILib C++ API](https://first.wpi.edu/wpilib/allwpilib/docs/release/cpp/index.html)
  - WPILib API Reference.
* [CTRE Phoenix Documentation](https://docs.ctre-phoenix.com/en/latest/index.html)
  - Documentation for Cross-The-Road Electronics hardware, such as TalonFX motor controllers, CANCoders, and Pigeon IMUs.
* [CTRE Phoenix C++ API](https://api.ctr-electronics.com/phoenix/release/cpp/index.html)
  - CTRE Phoenix API Reference.
* [REV Documentation](https://docs.revrobotics.com/docs/rev-ion)
  - Documentation for REV Robotics hardware, such as SparkMax Motor Controllers and REV ION stuff.
* [REVLib C++ Documentation](https://codedocs.revrobotics.com/cpp/index.html)
  - REVLib API Reference.

## Miscellaneous

Some useful things to remember:
* Camera Server Port is 1181 ([link](http://roborio-1511-frc.local:1181/stream.mjpg))
* Limelight Port is 5801 (for configuration), 5800 (for stream)
* Color sensor proximity reading ranges from 0-2048, the higher the value the closer the surface. A reading of ~300 or greater is enough for a reliable color read 