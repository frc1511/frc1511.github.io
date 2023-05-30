---
layout: page
title: BizarroHomer
nav_order: 1
parent: 1511 Software
---

# BizarroHomer

* [Description](#Description)
* [Setup](#Setup)
* [Software Structure](#Software-Structure)
   - [Main Program](#Main-Program)
   - [Hardware Control Program](#Hardware-Control-Program)
   - [DualShock4-LED-Control-Program](#DualShock4-LED-Control-Program)
* [Pairing DualShock4 Controller](#Pairing-DualShock4-Controller)
* [DualShock4 LED Status Patterns](#DualShock4-LED-Status-Paterns)

## Description
Code for FRC Team 1511's T-Shirt Robot, BizarroHomer (a.k.a. "ThunderShot").

The robot is controlled from a Raspberry Pi which takes input from a single Bluetooth DualShock4 controller. Controlling the robot using a Raspberry Pi gives us much more flexibility for control over solutions such as the NI roboRIO. Since BizarroHomer (a.k.a. "ThunderShot") was designed specifically for use at demonstrations and outreach events for the team, a simple and straightforward control solution was greatly desired.

BizarroHomer's code is hosted on GitHub [here](https://github.com/frc1511/BizarroHomer).

## Setup
1. Enable hardware control
   - Add these lines to `/boot/config.txt` to assign hardware pins.
     ```
     dtoverlay=pwm-2chan,pin=12,func=4,pin2=13,func2=4
     ```
2. Setup workspace
   - Create directory `/var/frc151/BizarroHomer` and give the pi user permissions to access it.
     ```bash
     $ sudo mkdir -p /var/frc1511/BizarroHomer
     $ sudo chown pi: /var/frc1511
     $ sudo chmod u+w /var/frc1511
     ```
   - Create IPC Message Queue Key file.
     ```bash
     $ touch /var/frc1511/BizarroHomer/ipc_msg_queue_key
     ```
3. Install tools
   ```
   $ sudo apt-get update
   $ sudo apt-get install -y --no-install-recommends bluez libsdl2-dev
   ```
4. Restart Raspberry Pi for changes to take effect.
5. [Pair a DualShock4 controller](#Pairing-DualShock4-Controller)
6. Compile and install using CMake

## Software Structure

The software is split up into several different programs, each with different permissions and purposes.
### Main Program
The main program is run as the pi user. It reads controller input and handles the main logic of the robot software. It communicates with the [Hardware Control](#Hardware-Control-Program) program to interact with robot hardware and the [DualShock4 LED Control](#DualShock4-LED-Control-Program) program to control the color of the DualShock4 controller's LEDs.

### Hardware Control Program
The hardware control program is run as the root user. It contols the motors, encoders, etc. on the robot. It receives control messages to control hardware, and sends status messages to provide feedback such as motor internal encoder measurements. This program also will disable all hardware outputs when the main program stops. This keeps things operating safely.

### DualShock4 LED Control Program
The DualShock4 LED control program is run as the root user. It controls the LEDs on the DualShock4 controller. The LED colors signify different states/errors of the robot program. For example, if the main program exits then the LEDs will signify that to alert the driver.

## Pairing DualShock4 Controller
Start up bluetoothctl.
```
$ bluetoothctl
```
Then, turn on bluetooth and scan for devices.
```
[bluetooth]# power on
[bluetooth]# agent off
[bluetooth]# agent NoInputNoOutput
[bluetooth]# default-agent
[bluetooth]# scan on
```
When the controller appears in the scan, pair to it using its Bluetooth address.
```
[bluetooth]# pair XX:XX:XX:XX:XX:XX
[bluetooth]# trust XX:XX:XX:XX:XX:XX
```
Now the Bluetooth device should automatically connect to the Pi. To check paired devices,
```
[bluetooth]# paired-devices
```

## DualShock4 LED Status Paterns
The LEDs on the DualShock4 controller is used to signify different states/errors of the robot program. 

| Color           | Description                 |
| --------------- | --------------------------- |
| Flashing White                                    | Controller is searching for robot. Give it some time to connect. If controller turns off, turn it back on again until it connects. |
| <span style="color:green">Solid Green</span>      | Everything is good |
| <span style="color:green">Flashing Green</span>   | Robot pressurized and armed. Be on alert and step away from the robot. |
| <span style="color:blue">Solid Blue</span>        | Controller is connected, although main program and/or LED control program is not running. Probably just have to wait for them to start up. |
| <span style="color:blue">Flashing Blue</span>     | Main program stopped/crashed. Wait for it to reboot. |
| <span style="color:red">Flashing Red</span>       | Robot battery low. |
| <span style="color:yellow">Flashing Yellow</span> | DualShock4 battery low. |
| Off                                               | LED control program isn't running, or the controller is turned off/out of battery. If the controller is off, Peter is disappointed. |