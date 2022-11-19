---
layout: page
title: 11/19/2022
nav_order: 3
parent: Pre-Season
---

# November 19th Pre-Season Meeting

* [Description](#description)
* [Game Controllers](#game-controllers)
  - [Joysticks](#joysticks)
  - [Buttons](#buttons)
  - [D-Pad](#d-pad)
* [Encoders](#encoders)
* [Analog Sensors](#analog-sensors)

## Description

Hi! Today we will be learning about how to get input from Game Controllers to control functionality of the robot, and look into how to use input from encoders and analog sensors.

## Game Controllers

The primary way we control our robot is through game controllers (XBox Controllers, PS4 Controllers, Logitech Controllers, etc.). We can read values from the joysticks and buttons on the controllers to do things. Often we will also use a "Switch Panel", a board with buttons and switches that we can use to configure properties of the robot which can be addressed just like buttons on a controller.

To access the buttons and joysticks of a game controller, create an instance of the `frc::GenericHID` class. First, make sure to include the header,
{% highlight cpp %}
#include <frc/GenericHID.h>
{% endhighlight %}

Create a variable of type `frc::GenericHID` and initialize it with the slot number of the controller in the Driver Station. For example, if the controller is in slot 0, the code would look like this:
{% highlight cpp %}
frc::GenericHID controller { 0 };
{% endhighlight %}

### Joysticks

To access the values of the joysticks and triggers, use the `GetRawAxis()` method of the `frc::GenericHID` class. The method takes an integer as a parameter, which is the axis number. The axis number depends on the controller; you can find the correct axis number in the Driver Station. The method returns a double between -1 and 1, which is the position of the joystick.

{% highlight cpp %}
double x = controller.GetRawAxis(0);
double y = controller.GetRawAxis(1);
{% endhighlight %}

### Buttons

To access the values of the buttons, use the `GetRawButton()` method of the `frc::GenericHID` class. The method takes an integer as a parameter, which is the button number. The button number depends on the controller; you can find the correct button number in the Driver Station. The method returns a boolean, which is whether the button is pressed or not.

{% highlight cpp %}
bool pressed = controller.GetRawButton(1); // Called every iteration when the button is pressed.
{% endhighlight %}

The `GetRawButton()` method will return true every iteration that the button is pressed. If you want to use the button to toggle something, you can use the `GetRawButtonPressed()` method. This method will return true only once, when the button is first pressed. Similarly, you can use the `GetRawButtonReleased()` method to return true only once, when the button is first released.

{% highlight cpp %}
bool pressed = controller.GetRawButtonPressed(1); // Called once when button is pressed.
bool released = controller.GetRawButtonReleased(1); // Called once when button is released.
{% endhighlight %}

### D-Pad

To access the value of the D-Pad, use the `GetPOV()` method of the `frc::GenericHID` class. The method returns an integer, which is the angle of the D-Pad. The angle is in increments of 45 degrees; 0 when the D-Pad is north, 45 when it is north east, 90 when it is east, 180 when it is south, etc. If the D-Pad is not pressed, the method returns -1.

{% highlight cpp %}
int dPadAngle = controller.GetPOV();

if (dPadAngle == 0) {
    // D-Pad is up.
}
if (dPadAngle == 90) {
    // D-Pad is right.
}
if (dPadAngle == 180) {
    // D-Pad is down.
}
if (dPadAngle == 270) {
    // D-Pad is left.
}
{% endhighlight %}

## Encoders

Encoders are sensors that are used to measure the rotations of a shaft. Using encoders, we can measure the distance traveled by the robot, determine the speed of the robot, and determine the position of different mechanisms on the robot. For example, in order to position a pivoting intake arm to a certain angle, you would be required to use an encoder to measure the position of the arm.

You may encounter two different types of encoders: integrated encoders and dedicated encoders. Integrated encoders are built into the motor, and dedicated encoders are separate and are wired to the RoboRIO. Integrated encoders are often used for drivetrains, and dedicated encoders are often used for mechanisms.

Most encoders are relative encoders, which means that they measure the number of rotations since the last reset. When the robot is turned off, the position of the encoder is lost. For mechanisms like a swerve drive where knowing the rotation of the modules is important, you would want to use an absolute encoder instead. Absolute encoders measure the position of the shaft relative to a fixed point, so the position is not lost when the robot is turned off. These typically utilize magnets, and are more expensive than relative encoders.

## Analog Sensors

On our robots we also use a myriad of analog sensors to measure different things. These sensors include potentiometers and gyros. Analog sensors are wired to the RoboRIO, and can be read using their respective WPILib classes.