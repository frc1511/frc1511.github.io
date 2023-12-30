---
layout: page
title: ThunderAuto
nav_order: 2
parent: 1511 Software
---

# ThunderAuto

* [Description](#description)
* [Creating a Project](#creating-a-project)
* [The Editor](#the-editor)
    * [Path Editor Page](#path-editor-page)
    * [Path Manager Page](#path-manager-page)
    * [Properties Page](#properties-page)
    * [Actions Page](#actions-page)
* [Installation](#installation)

## Description
ThunderAuto is a custom tool for creating pahts for FRC robots.

ThunderAuto's code is hosted on GitHub [here](https://github.com/frc1511/ThunderAuto).

Supported on Windows and macOS.

<img src="/assets/images/thunderauto/main.png" alt="ThunderAuto Path Editor" width="800">

## Creating a Project

Select the "New Project" button on the Welcome popup, or press Ctrl+N.

You need to specify a few settings to create a project:

<dl>
  <dt>Path</dt>
  <dd>The location to save the <b>.thunderauto</b> project and all of the exported <b>.csv</b> files.</dd>
  <dt>Field</dt>
  <dd>Which field to use. I will update the app with every year's game field, although choosing <b>Custom</b> will open a popup to select a custom field image.</dd>
  <dt>Controller Type</dt>
  <dd>What kind of drivetrain the robot uses. Only Holonomic (Swerve) drivebases are currently supported by ThunderAuto, with Ramsete drivebases soon? to come.</dd>
  <dt>Robot Length</dt>
  <dd>Length of the robot (meters).</dd>
  <dt>Robot Width</dt>
  <dd>Width of the robot (meters).</dd>
</dl>

<img src="/assets/images/thunderauto/new_project.png" alt="ThunderAuto New Project Window" width="300" style="display: block; margin-left: auto; margin-right: auto; width: 50%;">

## The Editor

### Path Editor Page

<img align="right" src="/assets/images/thunderauto/dragging.gif" alt="ThunderAuto Editor Dragging GIF" width="350">

The Path Editor page presents the current path on top of the field image. Points can be selected and dragged around to shape the desired path.

Pan around with __Shift+Left-Click__ or __Middle-Click__. Zoom with the scroll wheel.

__Double-Click__ to create a point. Double-clicking the curve will insert the new point into it. Double-clicking anywhere else will add a point to whichever end is closer to the cursor.

Use the __Delete__ or __Backspace__ keys to delete the selected point.

A tooltip is shown when the cursor hovers over the curve.
The tooltip includes the time, velocity, centripetal acceleration, and curvature at the hovered point.

By default, the color of the curve represents the velocity of the robot (blue = slow, magenta = fast). This can be changed in the [Properties page](#properties-page).

### Path Manager Page

<img align="right" src="/assets/images/thunderauto/path_manager.png" alt="ThunderAuto Path Manager Page" width="200">

The Path Manager page presents a list of all paths in the project.

The selected path in this page is shown in the Path Editor and Properties pages.

Rename a path by double-clicking its name.

Delete a path by clicking the trash can icon.

### Properties Page

<img align="right" src="/assets/images/thunderauto/properties_page.png" alt="ThunderAuto Properties Page" width="200">
The Properties page presents properties related to the currently selected point and general path properties.

The __Point__ dropdown contains tools related to the selected point. Properties include the point's position, heading, heading weights, rotation, and whether to stop there.

If the __Stop__ checkbox is checked the robot will decelerate to a stop at that point. When stopped, the point's incoming and outgoing headings may be different.

There is also a dropdown named __Actions__ where actions from the [Actions Page](#actions-page) can be checked on/off for the point.

The __Path__ dropdown contains tools related to the selected path.

The __Export__ button will export the path to a CSV file in the project's directory. The CSV file is named using the path's name shown in the [Path Manager Page](#path-manager-page).

The __Linear Accel__ and __Linear Velocity__ fields edit the robot's maximum allowable acceleration and velocity when traveling the path.

The __Centripetal Accel__ field controls the maximum centripetal acceleration of the robot as it makes a turn.


The following fields control what's displayed in the [Path Editor Page](#path-editor-page). The __Curve Overlay__ field controls the color of the curve. The __Show Tangents__, __Show Rotation__, and __Show Tooltip__ checkboxes control whether their respective items are rendered.

### Actions Page

<img align="right" src="/assets/images/thunderauto/actions_page.png" alt="ThunderAuto Actions Page" width="200">

The Actions page presents the global list of actions. Actions can be assigned to points in the [Properties Page](#properties-page).

## Installation
* [Releases](https://github.com/petelilley/ThunderAuto/releases)

Keep ThunderAuto up to date! Backwards compatibility is not guaranteed!
