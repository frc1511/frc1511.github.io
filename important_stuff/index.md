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
In order to keep track of the changes we make to our code on the team, we use a version control software called SVN (short for "subversion"). SVN allows us to incrementally "commit", our code changes as we code so we know exactly when something is added, and so we can always go back to a previous version of the code easily. When working on the same code with other members of the team, SVN can help "merge" people's code together and help maintain a centralized version of the code.

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