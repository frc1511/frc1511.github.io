---
layout: page
title: Digital IO Sensors
nav_order: 5
parent: Robot Programming
---

# Digital IO Sensors

* [Description](#description)
* [Initialization](#initialization)
* [Reading Input](#reading-input)

## Description
Digital IO sensors are sensors that can be connected to the digital IO ports on the RoboRIO. These sensors provide a digital 1 or 0 signal, which can be used to determine if the sensor is triggered or not. Some digital IO sensors include beam breaks, limit switches, and flag sensors.

## Initialization
To read input from a digital IO sensor, we utilize the [frc::DigitalInput](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_digital_input.html) class. The `frc::DigitalInput` class is initialized with the port number of the digital IO sensor on the roboRIO.

{% highlight cpp %}
#include <frc/DigitalInput.h>

frc::DigitalInput sensor {0};
{% endhighlight %}

## Reading Input
To read input from a digital IO sensor, we use the `frc::DigitalInput::Get()` method. This method returns a boolean value, which is `true` if the sensor is triggered and `false` if the sensor is not triggered.

{% highlight cpp %}
bool triggered = sensor.Get();
{% endhighlight %}
