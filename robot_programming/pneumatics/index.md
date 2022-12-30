---
layout: page
title: Pneumatics
nav_order: 6
parent: Robot Programming
---

# Pneumatics

* [Description](#description)

## Description
Pneumatics are a great way to control mechanisms on robots. They are often favorable to motors because they require less power, are usually easier to control, and cost less.

## Control Hardware
There are two options for controlling pneumatics on the robot:
- CTRE Pneumatics Control Module
  - Addressed in code as `frc::PneumaticsModuleType::CTREPCM`
- REV Robotics Pneumatics Hub
  - Addressed in code as `frc::PneumaticsModuleType::REVPH`

On 1511, we typically use the CTRE Pneumatics Control Module on our robots.

## Compressor
The compressor is a device that compresses air to a high pressure, which is then stored in a tank.

By default, the compressor on the robot will be set to "Closed Loop" mode. You probably shouldn't change this. In closed loop mode, the compressor will automatically turn on when the pressure in the tank is below a certain threshold, and will turn off when the pressure reaches ~120 psi.

If you want to check the status of the compressor or turn it on or off, you can use the [frc::Compressor](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_compressor.html) class.

{% highlight cpp %}
#include <frc/Compressor.h>

// CTRE PCM
frc::Compressor pcmCompressor {frc::PneumaticsModuleType::CTREPCM};

// Enable the compressor's closed loop control mode.
pcmCompressor.EnableDigital();

// Disable the compressor.
pcmCompressor.Disable();

// Is the compressor enabled???
bool enabled = pcmCompressor.Enabled();

// 120 psi yet??
bool pressureSwitch = pcmCompressor.GetPressureSwitchValue();

// Maybe you're bored and want to know how much current the compressor is using.
double current = pcmCompressor.GetCompressorCurrent();

{% endhighlight %}

## Solenoids

Solenoids are used to control the flow of air in a pneumatic system. They are typically used to control the actuation of pistons on the robot. Solenoids are controlled directly by the PCM or PH. There are two types of solenoids:
* Single Solenoid
  - Single acting solenoids have one output port and operate in one direction. These solenoids are typically used in situations where an external force, such as a spring or gravity, provides the return action of the cylinder. They can also be used in pairs to act as a double solenoid.

* Double Solenoid
  - Double acting solenoids have two output ports and operate in both directions. These solenoids allow for the extension and retraction of the cylinder, both with air pressure.

### Single Solenoid

Single solenoids can be controlled using the [frc::Solenoid](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_double_solenoid.html) class.

{% highlight cpp %}
#include <frc/Solenoid.h>

frc::Solenoid singleSolenoid {frc::PneumaticsModuleType::CTREPCM, 0};

// Extend the solenoid.
singleSolenoid.Set(true);

// Retract the solenoid.
singleSolenoid.Set(false);

// Is the solenoid extended?
bool extended = singleSolenoid.Get();

{% endhighlight %}

### Double Solenoid

Double solenoids can be controlled using the [frc::DoubleSolenoid](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_double_solenoid.html) class.

{% highlight cpp %}
#include <frc/DoubleSolenoid.h>

frc::DoubleSolenoid doubleSolenoid {frc::PneumaticsModuleType::CTREPCM, 0, 1};

// Extend the solenoid.
doubleSolenoid.Set(frc::DoubleSolenoid::Value::kForward);

// Retract the solenoid.
doubleSolenoid.Set(frc::DoubleSolenoid::Value::kReverse);

// Turn off the solenoid (Similar to setting a single solenoid to false).
doubleSolenoid.Set(frc::DoubleSolenoid::Value::kOff);

// Get the position of the solenoid.
frc::DoubleSolenoid::Value position = doubleSolenoid.Get();

{% endhighlight %}
