---
layout: page
title: 11/12/2022
nav_order: 2
parent: Pre-Season
---

# November 12th Pre-Season Meeting

* [Description](#description)
* [PWM Motor](#pwm-motor)
* [TalonSRX Motor Controller](#talonsrx-motor-controller)
* [Digital IO Sensors](#digital-io-sensors)

## Description
Today we will start learning about how to program motors and basic sensors! We will cover how to spin a PWM Servo motor, how to spin a motor using a TalonSRX motor controller, and how to use a digital IO sensor.

## PWM Motor
PWM Motors are one of the most basic types of motors. Typically, the only control you have over a PWM motor is the speed and direction in which it spins.

To control a PWM Servo Motor on the test board, see [this page](/robot_programming/motors_encoders/#pwm-servo).

## TalonSRX Motor Controller
TalonSRX motor controllers are connected to the CAN bus and provide more control than PWM motors. They can be used to control the speed and direction of a motor, as well as provide ways to control the motor's position and velocity.

To control motors using a TalonSRX motor controller, see [this page](/robot_programming/motors_encoders/#can-talon-srx).

## Digital IO Sensors
Digital IO sensors are sensors that can be connected to the digital IO ports on the RoboRIO. These sensors provide a digital 1 or 0 signal, which can be used to determine if the sensor is triggered or not. Some digital IO sensors include beam breaks, limit switches, and flag sensors.

To use a digital IO sensor, see [this page](/robot_programming/dio_sensors/).
