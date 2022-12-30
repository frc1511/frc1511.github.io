---
layout: page
title: Configuring a Device's CAN ID
nav_order: 4
parent: Tutorials
---

# Configuring a Device's CAN ID

CAN devices on the robot's CAN bus must be configured with a unique CAN ID. Unlike other motors and sensors, CAN devices are not plugged directly into an identifiable port on the RoboRIO. Instead, they are linked together in a long "CAN Bus" (yellow and green wires connecting each device), so they must be configured with a unique ID so that the RoboRIO can identify them. Depending on the vendor of the device, the process for configuring the CAN ID may differ. Devices made by REV Robotics (ex. SparkMax Motor Controllers) require the [REV Hardware Client](/programming_tools/rev_hardware_client/) to be installed on the computer configuring the device, and devices made by CTR Electronics (ex. TalonFX Motor Controllers, CANCoders) require the [CTRE Phoenix Tuner](/programming_tools/phoenix_framework/). You can jump to the section for your device's vendor below.

* [REV Robotics](#rev-robotics)
* [CTR Electronics](#ctr-electronics)

## REV Robotics

1. Make sure the most recent version of the [REV Hardware Client](/programming_tools/rev_hardware_client/) is installed on the computer you are using to configure the device.
2. Connect the device to the computer using a USB cable.
  - SparkMax Motor Controllers come with an orange USB-C to USB-A cable for this purpose.
3. Open the REV Hardware Client, or scan for devices if it is already open.
  - Occasionally, scanning for devices will not work. If this happens, close the REV Hardware Client and reopen it.
4. Select the device you want to configure from the list of devices.
5. Under the "Basic" tab, change the "CAN ID" field to the desired CAN ID, then click "Save Configuration".
  <img src="/assets/images/rev_hardware_client/rev_hardware_client_1.svg" width="800">
6. You can also change a number of other configuration settings, such as inversion, motor type, etc. These settings can also be changed in the code, so it is not super important to configure them here. If you do change them here, make sure to click the "Burn Flash" button to save the changes to the device's flash memory.

## CTR Electronics
1. Make sure the most recent version of [CTRE Phoenix Tuner](/programming_tools/phoenix_framework/) is installed on the computer you are using to configure the device.
2. Turn on the robot and connect the roboRIO to the computer using a USB-B to USB-A cable.
3. Open the CTRE Phoenix Tuner and select "RoboRIO Over USB" from the "Diagnostic Server Address or Team Number" dropdown menu, and make sure the "Port" field is set to 1250.
4. Select the "CAN Devices" tab, then click the device you want to configure.
5. Modify the "Change the ID" field to the desired CAN ID, then click "Change ID".
  <img src="/assets/images/phoenix_tuner/phoenix_tuner_1.png" width="800">
