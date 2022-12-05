---
layout: page
title: Controls
nav_order: 3
parent: Robot Programming
---

# Controls

* [Description](#description)
* [HID](#hid)
  - [Game Controller IDs](#game-controller-ids)
    - [Xbox Controller](#xbox-controller-ids)
    - [PS4 Controller](#ps4-controller-ids)

## Description

Every robot program that we write has a class named `Controls` that is used to handle reading input from game controllers and switch panels connected to the driver station. This class inherits from the [Mechanism class](/robot_programming/mechanisms/) and functions similar to other mechanisms (`process()` and `resetToMode()`). However, the `Controls` class does not have any controller functions of its own because its purpose is to call the controller functions of all the other mechanisms.

## HID

To read input from Human Interface Devices (HID) such as game controllers, switch panels, etc., we can use the `frc::GenericHID` class. The class is initialized with the slot number of the device that is set in the FRC Driver Station.  This class has a number of functions that can be called to get input from the device:
1. `GetRawAxis(int axis)`
  - This function returns the value of the specified axis. This can be used with joysticks on game controllers to read how much they are pushed in the X and Y directions, and with triggers to read how much they are pressed. Typically this value reads from -1 to 1, although the back triggers on some game controllers read from 0 to 1 instead.
2. `GetRawButton(int button)`
  - This function returns whether the specified button is pressed or not.
3. `GetRawButtonPressed(int button)`
  - This function returns true when a button is initially pressed. This is useful for things like toggles, where you want to toggle a value when the button is pressed, but not when it is held down.
4. `GetRawButtonReleased(int button)`
  - Similar to `GetRawButtonPressed()`, although it returns true when a button is released instead of pressed.
3. `GetPOV()`
  - This function returns the angle of the DPad in 45 degree increments starting with 0 at the top and going clockwise. If the DPad is not pressed, this function returns -1.

To determine the IDs of a HID's buttons and axes, you can use USB Devices page in the FRC Driver Station to see what values change when you press buttons or move axes.

### Game Controller IDs

The IDs for the axes and buttons on a game controller are different for each type of controller (Xbox, PS4, Logitech, etc.). You can query the `ThunderXboxController` and `ThunderPS4Controller` classes ([Homer Example](https://github.com/petelilley/Homer/tree/main/src/Main/Wrappers/GameController)) to get the correct IDs for a specific controller, or use the tables below.

#### Xbox Controller IDs

| Axis         | ID |
|:-------------|:---|
| Left X       | 0  |
| Left Y       | 1  |
| Right X      | 4  |
| Right Y      | 5  |
| Left Trigger | 2  |
| Right Trigger| 3  |

| Button       | ID |
|:-------------|:---|
| A            | 1  |
| B            | 2  |
| X            | 3  |
| Y            | 4  |
| Left Bumper  | 5  |
| Right Bumper | 6  |
| Back         | 7  |
| Start        | 8  |
| Left Stick   | 11 |
| Right Stick  | 12 |

#### PS4 Controller IDs

| Axis         | ID |
|:-------------|:---|
| Left X       | 0  |
| Left Y       | 1  |
| Right X      | 2  |
| Right Y      | 5  |
| Left Trigger | 3  |
| Right Trigger| 4  |

| Button       | ID |
|:-------------|:---|
| Square       | 1  |
| Cross        | 2  |
| Circle       | 3  |
| Triangle     | 4  |
| Left Bumper  | 5  |
| Right Bumper | 6  |
| Share        | 9  |
| Options      | 10 |
| Left Stick   | 11 |
| Right Stick  | 12 |