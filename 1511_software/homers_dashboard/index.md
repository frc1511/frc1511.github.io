---
layout: page
title: Homer's Dashboard
nav_order: 3
parent: 1511 Software
---

# Homer's Dashboard

* [Description](#description)
* [Installation](#installation)
  - [OpenCV vs Non-OpenCV Builds](#opencv-vs-non-opencv-builds)
    - [How to Install OpenCV (Windows x64)](#how-to-install-opencv-windows-x64)
  - [Launch the Dashboard Automatically from Driver Station](#launch-the-dashboard-automatically-from-driver-station)
* [Pages](#pages)
  - [Camera Stream Pages](#camera-stream-pages)
  - [Network Tables Page](#network-tables-page)
  - [Auto Chooser Page](#auto-chooser-page)
  - [Robot Position Page](#robot-position-page)
  - [Competition Info Page](#competition-info-page)
  - [2024 Arm Page](#2024-arm-page)
  - [2024 Hang Page](#2024-hang-page)
  - [2024 Game Piece Page](#2024-game-piece-page)
* [Building from Source](#building-from-source)
* [Creating a Page](#creating-a-page)

## Description
Homer's Dashboard is a custom dashboard used to interface with 1511's robots. It was created during the 2022 offseason and was originally designed only for Homer, but it has since been expanded for all competition robots. The dashboard is updated every year to fit the specific needs of each year's robot.

The code for Homer's Dashboard is hosted on GitHub [here](https://github.com/frc1511/HomersDashboard).

<img src="/assets/images/homers_dashboard/2024_everything.png" alt="Homer's Dashboard" width="800"/>

## Installation

You can download the latest release from the [GitHub releases page](https://github.com/frc1511/HomersDashboard/releases/latest). The dashboard is a standalone executable, so it can be run from anywhere on the computer.

On the releases page you will find multiple builds for different operating systems and architectures.

There's a posibility that you might need to install Bonjour print services on Windows if the dashboard can't resolve multicast DNS addresses.

### OpenCV vs Non-OpenCV Builds

For each platform there should be an OpenCV and a non-OpenCV build. The OpenCV build will require OpenCV to be installed on the system.

OpenCV is required for the camera pages, so if you don't need the camera pages, you can use the non-OpenCV build. The non-OpenCV build is also smaller in size and should run marginally faster.

#### How to Install OpenCV (Windows x64)

1. Download the latest OpenCV release from their [GitHub releases page](https://github.com/opencv/opencv/releases).
2. When the installer prompts you to select a location to extract OpenCV to, select `C:\Program Files\opencv\`.
3. Then, add `C:\Program Files\opencv\build\x64\v15\bin` to the path environment variable.

### Launch the Dashboard Automatically from Driver Station

To make the FRC Driver Station automatically open the dashboard, edit the `DashboardCmdLine` entry in `C:\Users\Public\Documents\FRC\FRC DS Data Storage.ini` with the path to the dashboard executable.

## Pages

### Camera Stream Pages
In OpenCV builds, the dashboard contains camera stream pages for cameras connected to the robot. If any of the camera streams fail to load, the view will present "🤯 No Camera".

The __Limelight__ camera page displays the camera stream at [http://limelight-homer.local:5800/stream.mjpg](http://limelight-homer.local:5800/stream.mjpg) named "limelight".

The __Intake__ camera page displays the camera stream at [http://roborio-1511-frc.local:5800/stream.mjpg](http://roborio-1511-frc.local:5800/stream.mjpg) named "intake\_camera". It's named intake camera because that's what it was in 2022, and we want to maintain compatibility. You can use it for any camera on the robot you want, just make sure to name it "intake\_camera".

### Network Tables Page
The Network Tables page presents a list of key-value pairs from the robot's network tables. Subtables are collapsible and expandable. The values are updated continuously and are read-only.

<img src="/assets/images/homers_dashboard/network_tables.png" alt="Homer's Dashboard Network Tables" width="500"/>

### Auto Chooser Page
The Autonomous chooser page allows the user to select an Autonomous mode to run.

The "Auto Mode" dropdown displays the available options for autonomous modes (sent from the robot). When the user selects an autonomous mode, the page sets the SmartDashboard network table value `Auto_Mode` to the selected autonomous mode index. When no autonomous modes are available, the page sets `Auto_Mode` to 0. Make sure the mode at index 0 does nothing!

The "Auto Delay" slider allows the user to set the delay time before the autonomous mode starts (in seconds). The page sets the SmartDashboard network table value `Auto_Delay` to the configured delay time.

<img src="/assets/images/homers_dashboard/2024_auto_chooser.png" alt="Homer's Dashboard Auto Chooser" width="400"/>

<!--
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
-->

### Robot Position Page
The Robot Position page displays the year's field image and the robot's position and orientation. The robot's position is set by the `thunderdashboard_drive_x_pos` and `thunderdashboard_drive_y_pos` SmartDashboard network table values, and the robot's orientation is set by the `thunderdashboard_drive_ang`.

<img src="/assets/images/homers_dashboard/2024_robot_position.png" alt="Homer's Dashboard Robot Pose" width="500"/>

<!--
### Motion Profile
The Motion Profile Page allows users to record positional data of the robot over a period of time and plot it on a graph. The user can record an entire autonomous mode or just an interval, and can adjust the period at which data is recorded. The user can specify which pieces of data are plotted on the graph and how the graph is structured (based on time or position). The `/home/lvuser/trajectory_motion.csv` file stored on the RoboRIO contains the same data recorded by the Motion Profile Page for autonomous modes. Switching to the "File" tab will present the option to load a CSV file for examination on the graph.

<img src="/assets/images/homers_dashboard/motion_profile.png" alt="Homer's Dashboard Motion Profile" width="500"/>
-->

### Competition Info Page

<img src="/assets/images/homers_dashboard/comp_info.png" alt="Homer's Dashboard Competition Info" width="200" align="right"/>

The Competition Info page reads data from FMS and displays it.
The page displays the current mode (Disabled, Teleop, Autonomous, etc.) in big text.
It also displays the Event Name, Game Message, Match Type, Match Number, Replay Number, Station Number, and Alliance Color.

### 2024 Arm Page

<img src="/assets/images/homers_dashboard/2024_arm_moving.png" alt="Homer's Dashboard 2024 Arm Moving" width="200" align="left"/>
<img src="/assets/images/homers_dashboard/2024_arm_at_target.png" alt="Homer's Dashboard 2024 Arm at Target" width="200"/>

The 2024 Arm page displays the current and target angles of the robot's arm.

The current angle is read from `thunderdashboard_2024_arm_pivot_deg` and the target angle is read from `thunderdashboard_2024_arm_pivot_target_deg`. These values should range from 0-85 degrees (the range of motion of the arm). Set the target angle to -1 to disable the target angle display.

If the current angle and target angle are close enough, the page will display the arm as green. Otherwise, the current angle will display as white and the target angle will display as gray.

The bumper colors of the robot in the visualization will change depending on the alliance read from the FMS.

### 2024 Hang Page

<img src="/assets/images/homers_dashboard/2024_hang.png" alt="Homer's Dashboard 2024 Hang" width="100" align="right"/>

The 2024 Hang page displays the extension of each hang arm.

The page reads the value of `thunderdashboard_2024_hang_left_percent` and `thunderdashboard_2024_hang_right_percent` and displays the extension of each arm. The values should range from 0-1.

### 2024 Game Piece Page

<img src="/assets/images/homers_dashboard/2024_no_gp.png" alt="Homer's Dashboard 2024 No Game Piece" width="100" align="left"/>
<img src="/assets/images/homers_dashboard/2024_gp.png" alt="Homer's Dashboard 2024 Game Piece" width="100"/>

The 2024 Game Piece page displays whether the robot as a note.

The page reads the value of `thunderdashboard_2024_has_gamepiece` and displays an orange note if the value is true, and a gray note if the value is false.

## Building from Source
Supported operating systems are Windows and macOS.

First, clone the repository and initialize the submodules.
{% highlight bash %}
git clone https://github.com/frc1511/HomersDashboard.git
cd HomersDashboard

git submodule init
git submodule update
{% endhighlight %}

#### Configure
Homer's Dashboard uses CMake to generate build projects for different platforms.

There are a number of options that can be set when configuring the build:
- `HD_WITH_CS` - Whether to build with the camera server and OpenCV. Default is `ON`.
- `HD_DOWNLOAD_WPILIB` - Whether to download and link to pre-built wpilib libraries instead of building them from source. Default is `OFF`. (Note: If this is set on Windows, you can't build in Debug mode, only Release or RelWithDebInfo because the pre-built libraries were built in Release mode).
  - `HD_DOWNLOAD_WPILIB_VERSION` - The version of the pre-built wpilib libraries to download (default is `2024.3.1`).
  - `HD_DOWNLOAD_WPILIB_ARCH` - Manually set the architecture of the pre-built wpilib libraries to download. If not set, the architecture will be detected automatically based on the host system (this option is only useful if you're cross-compiling).

For Windows, add the flag `-G "Visual Studio 17 2022"` to the cmake configuration to generate a Visual Studio solution. Add the `-A x64` or `-A ARM64` flag to specify the architecture.

For macOS, add the flag `-G "Xcode"` to the cmake configuration to generate an Xcode project. "Unix Makefiles" will also work.

{% highlight bash %}
cmake . -B build -G "Visual Studio 17 2022" -DCMAKE_BUILD_TYPE=Release -DHD_WITH_CS=OFF -DHD_DOWNLOAD_WPILIB=ON
{% endhighlight %}

#### Build
Either open the generated solution/project in the native IDE and build from there, or build from the command line:
{% highlight bash %}
cmake --build build
{% endhighlight %}

All the app's resources (Images, Fonts, etc.) are built into the executable, so there's no need to worry about moving them around once it's built.

## Creating a Page
To create a page in the dashboard, start with the following template header and cpp files.

{% highlight cpp %}
// HomersDashboard/pages/2024/my_page.h

#pragma once

#include <HomersDashboard/nt_handler.h>
#include <HomersDashboard/pages/page.h>

namespace y2024 {

class MyPage : public Page {
  NTHandler& m_nt_handler;

public:
  MyPage(NTHandler& nt_handler)
    : m_nt_handler(nt_handler) {}

  const char* name() const override { return "Page Name"; }
  void present(bool* running) override;
};

} // namespace y2024

{% endhighlight %}

{% highlight cpp %}
// HomersDashboard/pages/2024/my_page.cpp

#include <HomersDashboard/pages/2024/my_page.h>

using namespace y2024;

void GamePiecePage::present(bool* running) {
  ImGui::SetNextWindowSize(ImVec2(500, 500), ImGuiCond_FirstUseEver);
  if (!ImGui::Begin(name(), running,
                    ImGuiWindowFlags_NoCollapse | ImGuiWindowFlags_NoScrollbar |
                        ImGuiWindowFlags_NoScrollWithMouse)) {
    ImGui::End();
    return;
  }

  // Page content goes here...

  ImGui::End();
}
{% endhighlight %}

Add the name of the cpp file to the `/src/pages/CMakeLists.txt` file to add it to the build.

Now you can just add the page to the dashboard in the `app.h` by creating an instance of the page, and adding a pointer to it to the `m_2024_pages` set and the `m_all_pages` set.
