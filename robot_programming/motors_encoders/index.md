---
layout: page
title: Motors & Encoders
nav_order: 4
parent: Robot Programming
---

# Motors & Encoders

* [Description](#description)
* [Encoder](#encoder)
  - [Header](#header)
  - [Initialization](#initialization)
  - [Usage](#usage)
* [PWM Servo](#pwm-servo)
  - [Header](#header-1)
  - [Initialization](#initialization-1)
  - [Percent Output](#percent-output)
* [CAN Spark Max](#can-spark-max)
  - [Header](#header-2)
  - [Initialization](#initialization-2)
  - [Percent Output](#percent-output-1)
  - [Idle Mode](#idle-mode)
  - [Encoder](#encoder-1)
  - [PID Controller](#pid-controller)
* [CAN Talon FX](#can-talon-fx)
  - [Header](#header-3)
  - [Initialization](#initialization-3)
  - [Percent Output](#percent-output-2)
  - [Idle Mode](#idle-mode-1)
  - [Encoder](#encoder-2)
  - [PID Controller](#pid-controller-1)
* [CAN Talon SRX](#can-talon-srx)
  - [Header](#header-4)
  - [Initialization](#initialization-4)
  - [Percent Output](#percent-output-3)
  - [Idle Mode](#idle-mode-2)
  - [Encoder](#encoder-3)
  - [PID Controller](#pid-controller-2)
* [CANCoder](#cancoder)
  - [Header](#header-5)
  - [Initialization](#initialization-5)
  - [Absolute Position](#absolute-position)
* [Spark](#spark)
  - [Header](#header-6)
  - [Initialization](#initialization-6)
  - [Percent Output](#percent-output-4)

## Description

This section covers the basics of using different kinds of motor controllers and encoders. Motors are typically controlled through either PWM or CAN. PWM is a protocol that uses a single wire to send data to the motor controller, so it cannot provide back any information or sensor data from the motor. CAN is more advanced and allows for more information to be sent to and from the motor controller, such as configuration data, encoder position, temperature, current draw, etc.

## Encoder
Typically when using dedicated encoders, you can use the [frc::Encoder](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_encoder.html#a3755cf5bfbedf7d2c3f335bc82c6a23e) class.

#### Header
{% highlight cpp %}
#include <frc/Encoder.h>
{% endhighlight %}

#### Initialization
{% highlight cpp %}
frc::Encoder encoder{0, 1};
{% endhighlight %}

#### Usage
{% highlight cpp %}
encoder.Get(); // Position (in ticks)
encoder.GetRate(); // Velocity (RPM)
{% endhighlight %}

## PWM Servo

PWM Servos can be controlled with the [frc::Servo](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_servo.html) class.

#### Header
{% highlight cpp %}
#include <frc/Servo.h>
{% endhighlight %}

#### Initialization
{% highlight cpp %}
frc::Servo servo { 0 };
{% endhighlight %}

#### Percent Output
{% highlight cpp %}
servo.Set(0.5);
{% endhighlight %}

## CAN Spark Max

CAN Spark Max motor controllers are used to control REV motors, such as Neos or Neo 550s. They can be controlled with the [rev::CANSparkMax](https://codedocs.revrobotics.com/cpp/classrev_1_1_c_a_n_spark_max.html) class.

#### Header
{% highlight cpp %}
#include <rev/CANSparkMax.h>
{% endhighlight %}

#### Initialization
{% highlight cpp %}
frc::CANSparkMax motor { 0, rev::CANSparkMax::MotorType::kBrushless }; // kBrushless or kBrushed
{% endhighlight %}

#### Percent Output
{% highlight cpp %}
motor.Set(0.5);
{% endhighlight %}

#### Idle Mode
{% highlight cpp %}
motor.SetIdleMode(rev::CANSparkMax::IdleMode::kCoast); // kCoast or kBrake
{% endhighlight %}

#### Encoder
{% highlight cpp %}
rev::SparkMaxRelativeEncoder encoder(motor.GetEncoder());
double position = encoder.GetPosition();
double velocity = encoder.GetVelocity();
{% endhighlight %}

#### PID Controller
{% highlight cpp %}
rev::SparkMaxPIDController pidController = motor.GetPIDController();
// Configure the PID Controller
pidController.SetP(0.1);
pidController.SetI(0.0);
pidController.SetD(0.0);
pidController.SetFF(0.0);
pidController.SetIZone(0.0);
// Set the reference (kVelocity, kPosition, kCurrent, etc.).
pidController.SetReference(1.0, rev::ControlType::kVelocity);
{% endhighlight %}

## CAN Talon FX
CAN Talon FX motor controllers are used to control CTRE motors, predominantly the Falcon 500. They can be controlled with the [ctre::phoenix::motorcontrol::can::TalonFX](https://api.ctr-electronics.com/phoenix/release/cpp/classctre_1_1phoenix_1_1motorcontrol_1_1can_1_1_talon_f_x.html) class.

#### Header
{% highlight cpp %}
#include <ctre/Phoenix.h>
{% endhighlight %}

#### Initialization
{% highlight cpp %}
ctre::phoenix::motorcontrol::can::TalonFX motor { 0 };
{% endhighlight %}

#### Percent Output
{% highlight cpp %}
motor.Set(ctre::phoenix::motorcontrol::ControlMode::PercentOutput, 0.5);
{% endhighlight %}

#### Idle Mode
{% highlight cpp %}
motor.SetNeutralMode(ctre::phoenix::motorcontrol::NeutralMode::Coast); // Coast or Brake
{% endhighlight %}

#### Encoder
{% highlight cpp %}
double position = motor.GetSelectedSensorPosition(0);
double velocity = motor.GetSelectedSensorVelocity(0);
{% endhighlight %}

#### PID Controller
{% highlight cpp %}
motor.Config_kP(0, 0.1);
motor.Config_kI(0, 0.0);
motor.Config_kD(0, 0.0);
motor.Config_kF(0, 0.0);
motor.Config_IntegralZone(0, 0.0);
// Set the reference (Position, Velocity, Current, etc.).
motor.Set(ctre::phoenix::motorcontrol::TalonFXControlMode::Velocity, 1.0);
{% endhighlight %}

## CAN Talon SRX
CAN Talon FX motor controllers are used to control CTRE motors, predominantly the Falcon 500. They can be controlled with the [ctre::phoenix::motorcontrol::can::TalonSRX](https://api.ctr-electronics.com/phoenix/release/cpp/classctre_1_1phoenix_1_1motorcontrol_1_1can_1_1_talon_s_r_x.html) class.

#### Header
{% highlight cpp %}
#include <ctre/Phoenix.h>
{% endhighlight %}

#### Initialization
{% highlight cpp %}
ctre::phoenix::motorcontrol::can::TalonSRX motor { 0 };
{% endhighlight %}

#### Percent Output
{% highlight cpp %}
motor.Set(ctre::phoenix::motorcontrol::ControlMode::PercentOutput, 0.5);
{% endhighlight %}

#### Idle Mode
{% highlight cpp %}
motor.SetNeutralMode(ctre::phoenix::motorcontrol::NeutralMode::Coast); // Coast or Brake
{% endhighlight %}

#### Encoder
{% highlight cpp %}
double position = motor.GetSelectedSensorPosition(0);
double velocity = motor.GetSelectedSensorVelocity(0);
{% endhighlight %}

#### PID Controller
{% highlight cpp %}
motor.Config_kP(0, 0.1);
motor.Config_kI(0, 0.0);
motor.Config_kD(0, 0.0);
motor.Config_kF(0, 0.0);
motor.Config_IntegralZone(0, 0.0);
// Set the reference (Position, Velocity, Current, etc.).
motor.Set(ctre::phoenix::motorcontrol::TalonSRXControlMode::Velocity, 1.0);
{% endhighlight %}

## CANCoder
The CTRE CANCoder is an absolute encoder, meaning that it's position won't reset when the robot is powered off. They can be controlled with the [ctre::phoenix::sensors::CANCoder](https://api.ctr-electronics.com/phoenix/release/cpp/classctre_1_1phoenix_1_1sensors_1_1_c_a_n_coder.html) class.

#### Header
{% highlight cpp %}
#include <ctre/Phoenix.h>
{% endhighlight %}

#### Initialization
{% highlight cpp %}
ctre::phoenix::sensors::CANCoder canCoder { 0 };

// Signed_PlusMinus180 or Unsigned_0_to_360
canCoder.ConfigAbsoluteSensorRange(ctre::phoenix::sensors::AbsoluteSensorRange::Signed_PlusMinus180);
{% endhighlight %}

#### Absolute Position
{% highlight cpp %}
canCoder.GetAbsolutePosition();
{% endhighlight %}

## Spark
PWM Spark motor controllers can be controlled with the [frc::Spark](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_spark.html) class.

#### Header
{% highlight cpp %}
#include <frc/Spark.h>
{% endhighlight %}

#### Initialization
{% highlight cpp %}
frc::Spark motor { 0 };
{% endhighlight %}

#### Percent Output
{% highlight cpp %}
motor.Set(0.5);
{% endhighlight %}