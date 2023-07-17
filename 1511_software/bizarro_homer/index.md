---
layout: page
title: BizarroHomer
nav_order: 1
parent: 1511 Software
---

# BizarroHomer

* [Description](#description)
* [Section 1: Controls](#section-1-controls)
  - [1.1: Basic Usage](#11-basic-usage)
  - [1.2: Joystick and Button Mappings](#12-joystick-and-button-mappings)
  - [1.3: LED Status Patterns](#13-led-status-patterns)
    * [1.3.1: Independent States](#131-independent-states)
    * [1.3.2: Colors](#132-colors)
  - [1.4: Pairing a Controller](#14-pairing-a-controller)
* [Section 2: Raspberry Pi Setup](#section-2-raspberry-pi-setup)
* [Section 3: Software Overview](#section-3-software-overview)
  - [3.1: Main Program](#31-main-program)
  - [3.2: Hardware Control Program](#32-hardware-control-program)
  - [3.3: Diagnostic Server Program](#33-diagnostic-server-program)
  - [3.4: DualShock 4 LED Control Program](#34-dualshock4-led-control-program)

## Description
Code for FRC Team 1511's T-Shirt Robot, BizarroHomer (a.k.a. "ThunderShot").

The robot is controlled from a Raspberry Pi which takes input from a single Bluetooth DualShock4 controller. Controlling the robot using a Raspberry Pi gives us much more flexibility for control over solutions such as the NI roboRIO. Since BizarroHomer (a.k.a. "ThunderShot") was designed specifically for use at demonstrations and outreach events for the team, a simple and straightforward control solution was greatly desired.

BizarroHomer's code is hosted on GitHub [here](https://github.com/frc1511/BizarroHomer).

## Section 1: Controls

### 1.1: Basic Usage

The T-Shirt robot is controlled using a singular DualShock 4 Controller.

When the robot boots up, press the center Playstation button on the controller to turn on the controller. The controller should start flashing white, which signifies that the controller is looking for the robot. When the robot finishes booting up, it should automatically connect to the controller, and the controller’s LEDs should change to the current robot state, as seen in section 1.3. If the LEDs turn off, that probably means that the controller timed-out connecting and turned itself off, so you’ll want to press the Playstation button again to turn it back on.

### 1.2: Joystick and Button Mappings

### 1.3: LED Status Patterns

The LEDs on the DualShock4 controller are used to signify different states and errors of the robot program.

<style>
  .blink {
    animation: blinker 1s linear infinite;
  }

  @keyframes blinker {
    50% {
      opacity: 0;
    }
  }
</style>

#### 1.3.1: Independent States

These are basic states that signify something important. Most of them aren’t controlled by the robot control program.

| State | Description |
| ----- | ----------- |
| <span class="blink">Flashing White</span> | Controller is searching for the robot. Give it some time to connect. If the controller turns off, turn it back on again until it connects. If it continuously fails, make sure it is the correct controller that has been paired to the robot. |
| <span style="color:blue">Solid Blue</span> | Controller is connected, although the main program and/or LED control program is not running. Wait for them to start up. |
| <span style="color:blue" class="blink">Flashing Blue</span> | Main program stopped/crashed. It should start up again in a few seconds. |
| Off | Controller if off/dead or LED control program isn't running. Most likely the former though. |

#### 1.3.2: Colors

These colors may be blinking in combination with each other. Every color signifies a different thing.

| Color | Description |
| ----- | ----------- |
| <span style="color:red">Red</span> | Robot battery is low (less than 11.8 V). Battery should be replaced for the robot to function properly. |
| <span style="color:yellow">Yellow</span> | The controller battery is low (less than 30 percent). The controller should be charged or plugged into the robot to eliminate risk of bad things happening. |
| <span style="color:orange">Orange</span> | Robot program is doing setup work. Give it some time to become responsive to inputs. |
| <span style="color:green">Green</span> | Robot program is running fine. No pressure stored in the fill tank (presumably). |
| <span style="color:magenta">Magenta</span> | The fill tank is pressurized (presumably). Be cautious around the robot. |

### 1.4: Pairing a Controller

The process of pairing a new controller is a bit involved and hopefully won’t be necessary. If the controller isn’t connecting, make sure its battery is charged before attempting to repair it.

{: .note }
As a reminder, only attempt to use DualShock4 controllers with this robot. Other controllers may have different button/joystick interfaces which may result in rearranged buttons or unexpected inputs. Be cautious, and don’t blame Peter’s code if it doesn’t work properly.

Here are the instructions for pairing a controller…



First, put the DualShock4 controller into pairing mode by holding down the Playstation button and the share button until it starts flashing.

Next, start up bluetoothctl.

```bash
$ bluetoothctl
```

Turn on bluetooth and scan for devices.

```
[bluetooth]# power on
[bluetooth]# agent off
[bluetooth]# agent NoInputNoOutput
[bluetooth]# default-agent
[bluetooth]# scan on
```

This should start listing all the detected devices in the vicinity.

When the controller appears in the scan, pair to it using its Bluetooth address.

```
[bluetooth]# pair XX:XX:XX:XX:XX:XX
[bluetooth]# trust XX:XX:XX:XX:XX:XX
```

Now the Bluetooth device should automatically connect to the Pi.

To check paired devices,

```
[bluetooth]# paired-devices
```

## Section 2: Raspberry Pi Setup

If you need to set up a new Raspberry Pi to run the BizarroHomer control software, here are the steps to do so.

  1.  Install all the required tools!

      Assuming you’re using a Debian-based Linux distribution, here are some commands to run,

      BlueZ:
        ```bash
        $ sudo apt-get install bluez
        ```

      Git:
        ```bash
        $ sudo apt-get install git
        ```

      CMake:
        ```bash
        $ sudo apt-get install cmake
        ```

      SDL2:
        ```bash
        $ sudo apt-get install libsdl2-dev
        ```

      CAN Utils:
        ```bash
        $ sudo apt-get install can-utils	
        ```

  2.  Depending on which CAN adapter is being used, the setup will differ.
      
      1. For the Waveshare [RS485 CAN HAT](https://www.waveshare.com/rs485-can-hat.htm), add these lines to `/boot/config.txt`
      ```
      dtparam=spi=on
      dtoverlay=mcp2515-can0,oscillator=12000000,interrupt=25,spimaxfrequency=2000000
      ```

      2. For a CANable 2.0 device, add these lines to `/etc/network/interfaces`
      ```
      allow-hotplug can0
      iface can0 can static
      bitrate 1000000
      txqueuelen 1000
      up /sbin/ip link set $IFACE down
      up /sbin/ip link set $IFACE up type can
      ```
      This enables hot swapping, which seems to have good results.

      To validate the CAN network, run

      ```bash
      $ ifconfig
      ```

      Look for an entry named `can0`.

      You can see all incoming CAN traffic by running

      ```bash
      $ candump can0
      ```

  3.  Enable PWM0 and PWM1 by adding the following line to /boot/config.txt

      ```
      dtoverlay=pwm-2chan,pin=12,func=4,pin2=13,func2=4
      ```

  4.  Create directory `/var/frc1511/BizarroHomer` and give the pi user permission to access it.

      ```bash
      $ sudo mkdir -p /var/frc1511/BizarroHomer
      $ sudo chown pi: /var/frc1511
      $ sudo chmod u+w /var/frc1511
      ```

  5.  Create IPC message queue key file in the directory.

      ```bash
      $ touch /var/frc1511/BizarroHomer/ipc_msg_queue_key
      ```

  6.  Clone the `https://github.com/frc1511/BizarroHomer` repository.

      ```bash
      $ git clone https://github.com/frc1511/BizarroHomer.git
      ```

  7.  Initialize and update submodules

      ```bash
      $ git submodule init
      $ git submodule update
      ```

  8.  Build the project using CMake

      ```bash
      $ cmake . -Bbuild -DCMAKE_BUILD_TYPE=Release
      $ cmake --build build/
      ```

  9.  Install everything

      ```bash
      $ sudo cmake --install build/
      ```

  10. Restart the Raspberry Pi, and the systemd services should automatically start up  and everything should hopefully work as expected.

## Section 3: Software Overview

The software is split up into several different programs, each with different permissions and purposes. Each program is a systemd service that starts up at boot. There are four programs:

- Main program
  - Game Controller inputs.
  - Main logic of robot functionality.
  - Tells all the other programs what to do.
- Hardware Control program
  - Interfaces with all the motors, sensors, and things connected to the Raspberry Pi.
- Diagnostic Server program
  - Hosts a HTTP/1.1 server on port 80.
  - Webpage shows feedback values from the main program, and stdout and stderr files for all four programs
- DualShock4 LED Control program
  - Controls the colors of the DualShock 4 controllers connected to the Raspberry Pi.

The reasoning behind having multiple programs boils down to two factors:
- Permissions
  - Programs controlling motors and sensors need the highest permissions of the system, however the main program does not need those permissions. In fact, during testing I’ve found that when the main program is run as root, game controller input ceases to work as expected, so by giving each program different permissions keeps everything working splendidly.
- Safety
  - Using one program becomes unsafe when things don’t go as planned. For example, if a singular program crashes when controlling hardware, motors may continue moving in their previously controlled direction and other bad things may happen.
  - In this case, the hardware control program can detect when the main program starts/exits, so the hardware will be enabled/disabled appropriately. The hardware control program is simple, with very minimal chance of crashing. When debugging functionality in the main program, there is nothing to worry about if the program crashes or does something funny.
- Separation of Concerns
  - In Computer Science, it is best practice to separate functionality into distinct sections.

The programs communicate over Linux message queues.

### 3.1: Main Program

### 3.2: Hardware Control Program

### 3.3: Diagnostic Server Program

### 3.4: DualShock4 LED Control Program