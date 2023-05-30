---
layout: page
title: Homer's Dashboard
nav_order: 3
parent: 1511 Software
---

# Homer's Dashboard
* [Description](#description)
* [Usage](#usage)
* [Tools](#tools)
  - [Camera Streams](#camera-streams)
  - [Network Table Viewer](#network-table-viewer)
  - [Auto Mode Selector](#auto-mode-selector)
  - [LED Control](#led-control)
  - [Robot Pose Viewer](#robot-pose-viewer)
  - [Motion Profile](#motion-profile)
* [Installation](#installation)
* [Building](#building)

## Description
Homer's Dashboard is a custom dashboard that was created during the 2022 offseason. It was designed to be a simple dashboard that could be easily customized and improved upon. Originally, Homer's Dashboard was created to only be used for Homer, but it has since been expanded to be used for future 1511 robots as well.

The code for Homer's Dashboard is hosted on GitHub [here](https://github.com/frc1511/HomersDashboard).

<img src="/assets/images/homers_dashboard/homers_dashboard.jpg" alt="Homer's Dashboard" width="800"/>

## Usage
To make the FRC Driver Station open the dashboard on launch, edit the `DashboardCmdLine` entry in `C:\Users\Public\Documents\FRC\FRC DS Data Storage.ini` with the path to the executable.

## Tools
Homer's Dashboard is made up of a few different tools that can be used to view diagnostic information about the robot and control different aspects of the robot.

### Camera Streams
In camera-server builds, the dashboard contains camera stream views for cameras connected to the robot. If any of the camera streams fail to load, the view will present the words "No Camera" in the view.

### Network Table Viewer
The Network Tables page presents a list of key-value pairs in the SmartDashboard network table. The values are readonly and are sorted alphabetically.

<img src="/assets/images/homers_dashboard/network_tables.png" alt="Homer's Dashboard Network Tables" width="500"/>

### Auto Mode Selector
The Auto Mode Selector page allows the user to configure the Autonomous subsystem of the robot. The user can use the "Auto Mode" dropdown menu to select the autonomous mode to run. The user can also set the delay time before the autonomous mode starts. The tool sets the SmartDashboard network table values `Auto_Mode` and `Auto_Delay` to the selected autonomous mode and delay time respectively.

<img src="/assets/images/homers_dashboard/auto_chooser.png" alt="Homer's Dashboard Auto Chooser" width="400"/>

### LED Control
The LED Control page allows the user to control the LEDs on the robot. The user can use the "LED Mode" dropdown to select the desired configuration for the LEDs:
* Robot State
  - Colors change depending on the robot's state (Disabled = Orange, Enabled = Alliance Color, Crater Mode = Green, etc).
* Alliance
  - The alliance color.
* Custom
  - A custom color. When this mode is selected, the user can use the "Custom Color" color picker to select the custom color to use.
* Off
  - Off.

The tool sets the SmartDashboard network table value `LED_Mode` to the selected LED mode, and the "LED_Custom_Color_R", "LED_Custom_Color_G", and "LED_Custom_Color_B" network table values to the red, green, and blue components of the custom color.

<img src="/assets/images/homers_dashboard/blinky_blinky_custom.png" alt="Homer's Dashboard LED Control" width="400"/>

### Robot Pose Viewer
The Robot Pose Viewer page allows the user to view the robot's pose on the field. The robot's pose is determined by the `thunderdashboard_drive_x_pos`, `thunderdashboard_drive_y_pos`, and `thunderdashboard_drive_ang` network table values. The robot's pose is displayed as a yellow dot on the field, with a yellow line representing the robot's rotation.

<img src="/assets/images/homers_dashboard/robot_pose_0_0.png" alt="Homer's Dashboard Robot Pose" width="500"/>

### Motion Profile
The Motion Profile Page allows users to record positional data of the robot over a period of time and plot it on a graph. The user can record an entire autonomous mode or just an interval, and can adjust the period at which data is recorded. The user can specify which pieces of data are plotted on the graph and how the graph is structured (based on time or position). The `/home/lvuser/trajectory_motion.csv` file stored on the RoboRIO contains the same data recorded by the Motion Profile Page for autonomous modes. Switching to the "File" tab will present the option to load a CSV file for examination on the graph.

<img src="/assets/images/homers_dashboard/motion_profile.png" alt="Homer's Dashboard Motion Profile" width="500"/>

## Installation
* [Executable Download](https://github.com/petelilley/HomersDashboard/releases/latest)

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

{: .important }
OpenCV is used for creating the camera pages so it is required to be installed when building and running the app. On Windows, the app searches for OpenCV binaries in `C:\Program Files\opencv\`, so make sure to add `C:\Program Files\opecv\build\x64\v15\bin` to Path. As an alternative, the `-DDASHBOARD_WITH_CS=0` flag may be added to the cmake configuration to build without the camera server if OpenCV is not installed.

Problems have emerged when compiling the wpilib libraries (ntcore, cscore, wpiutil), so the `-DDASHBOARD_DOWNLOAD_WPILIB=1` flag may be added to the cmake configuration to download and link to pre-built libraries instead. The version downloaded can be specified by adding the `-DDASHBOARD_DOWNLOAD_WPILIB_VERSION=YEAR.X.X` flag.
