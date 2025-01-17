---
layout: page
title: ThunderAuto
nav_order: 1
parent: 1511 Software
---

# ThunderAuto

* [Description](#description)
* [Creating a Project](#creating-a-project)
* [Editing Paths](#editing-paths)
    * [Navigating Editor](#navigating-the-editor)
    * [Adding/Removing Points](#addingremoving-points)
    * [Point Properties](#point-properties)
    * [Linking Points](#linking-points)
    * [Point Actions](#point-actions)
    * [Reversing Paths](#reversing-paths)
    * [Constraints](#constraints)
* [Managing Paths](#managing-paths)
* [Exporting Paths](#exporting-paths)
    * [CSV Format](#csv-format)
* [Building from Source](#building-from-source)

## Description
ThunderAuto is a tool used by FRC teams to create efficient trajectories for autonomous robots to follow. Trajectories created in ThunderAuto can be exported to CSV files which can be easily read from the robot program.

<a href="https://apps.microsoft.com/detail/9n2hbs3wm7cm?mode=direct">
    <img src="https://get.microsoft.com/images/en-us%20dark.svg" width="200"/>
</a>

ThunderAuto's code is hosted on GitHub [here](https://github.com/frc1511/ThunderAuto).

<img src="/assets/images/thunderauto/main.png" alt="ThunderAuto Path Editor" width="800">

## Creating a Project

Select the "New Project" button on the Welcome popup, or use the shortcut Ctrl+N.

<img src="/assets/images/thunderauto/new_project.png" alt="ThunderAuto New Project Window" width="300" style="display: block; margin-left: auto; margin-right: auto; width: 50%;">

<dl>
  <dt>Path</dt>
  <dd>The location to save the <b>.thunderauto</b> project and all of the exported <b>.csv</b> files. Somewhere in the <b>deploy</b> folder of the robot project is recommended.</dd>
  <dt>Field</dt>
  <dd>Which field to use. The application is updated with each year's game field every year. To import a custom field image, select <b>Custom</b> and choose an image file.</dd>
  <dt>Controller Type</dt>
  <dd>The type of drivetrain the robot has. Only Holonomic (Swerve) drivebases are currently supported. Ramsete drivebases coming soon.</dd>
  <dt>Robot Length</dt>
  <dd>Length of the robot with bumpers (meters).</dd>
  <dt>Robot Width</dt>
  <dd>Width of the robot with bumpers (meters).</dd>
</dl>

## Editing Paths

### Navigating The Editor

Pan around with __Shift+Left-Click__ or __Middle-Click__. Zoom with the scroll wheel.

To reset the view, use the shortcut __Ctrl+0__, or select __View -> Reset View__ from the top menu bar.

### Adding/Removing Points

Ways to add waypoints:
* Right-click anywhere in the editor to open a context menu:
    - You may add a point to the start/end of the path, or before/after the currently selected point.
* Double-click the curve to add in a point, or double-click anywhere else to add a point to the closest end of the path.

Ways to remove waypoints:
* Select a point and press the __Delete__ or __Backspace__ key.
* Right-click a point and select __Delete__ from the context menu.

<img src="/assets/images/thunderauto/new_point.png" alt="ThunderAuto Editor New Point" width="350">

### Point Properties

<img align="right" src="/assets/images/thunderauto/dragging.gif" alt="ThunderAuto Editor Dragging GIF" width="350">

Points can be selected and dragged around in the editor page.

Point properties such as position, rotation, and heading can be manually edited in the Properties page.

If the __Stop__ checkbox is checked, the robot will decelerate to a stop at that waypoint. When stopped, the point's incoming and outgoing headings can differ.

### Linking Points

<img align="right" src="/assets/images/thunderauto/properties_page.png" alt="ThunderAuto Properties" width="200">

The position of waypoints can be linked together in the properties page. Open the waypoint link popup by clicking the link icon next to a corresponding waypoint. In the popup, you can create a named link or select an existing link.

Links are useful when creating sequential paths that share endpoints.

### Point Actions

Actions can be assigned to waypoints in the Properties page. Actions are simply flags that can be checked on/off for each waypoint. Actions can be used in the robot program to trigger certain behaviors.

### Reversing Paths

Reverse a path in the top menu bar, or by right-clicking a path in the path manager page.

### Constraints

Constrain the robot's maximum linear acceleration, linear velocity, and centripetal acceleration in the properties page.

## Managing Paths

<img align="right" src="/assets/images/thunderauto/path_manager.png" alt="ThunderAuto Path Manager Page" width="200">
Paths can be created, renamed, duplicated, and deleted in the Path Manager page.

Double-click a path to rename it.
Right-click a path to duplicate or delete it.

## Exporting Paths

Export individual paths in the Properties page, or export all paths with the menu bar button.

### CSV Format

Paths are exported to CSV files in the project's directory. Each CSV file shares the name of the path it corresponds to.

The CSV file contains the following columns:

1. Time (s)
2. X Position (m)
3. Y Position (m)
4. Velocity (m/s)
5. Rotation (rad)
6. Action (bit field)

For reading the CSV from a robot program, see 1511's 2023 robot code [here](https://github.com/frc1511/thunderbot2023/blob/main/src/Trajectory/CSVTrajectory.cpp#L7).

## Building from Source

ThunderAuto uses CMake to generate build files. To build ThunderAuto from source, follow these steps:

1. Clone the repository
```bash
git clone https://github.com/frc1511/ThunderAuto
cd ThunderAuto
```

2. Update submodules
```bash
git submodule init
git submodule update
```

3. Configure the project

    {: .note }
    For Windows, ThunderAuto supports both DirectX11 and OpenGL backends. DirectX11 is the default, but you can switch to OpenGL by setting the `TH_OPENGL` CMake option to `ON`.

    ```bash
    cmake . -B build
    ```

4. Build the project
```bash
cmake --build build
```

