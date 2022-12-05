---
layout: page
title: Networking
nav_order: 6
parent: Robot Programming
---

# Networking

* [Description](#description)
* [Network Tables](#network-tables)
  - [Initialization](#initialization)
  - [Reading Data](#reading-data)
  - [Writing Data](#writing-data)

## Description
Networking on the robot is fun! Not only that, but it is important to feedback diagnostic information to the driver station to help drivers know the robot's state during a match and help programmers debug issues with the robot.

## Network Tables
WPILib provides the NetworkTables library for communicating data between devices on the robot and the driver station. NetworkTables is a key-value store, meaning that data is stored in a table with a key (name) and a value. The value can be strings, booleans, doubles, etc.

There are several different "Tables" on the robot, each with a different purpose.
* SmartDashboard
  - Used to communicate information to the dashboard on the driver station computer.
* FMSInfo
  - Used to communicate match information from the field management system to the robot.
* Limelight (May be named differently, ex. "limelight-homer")
  - Used to communicate information from the Limelight sensor to the roboRIO and the driver station.

### Initialization
To get a NetworkTable, you first have to get the [nt::NetworkTableInstance](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table_instance.html) object using the [nt::NetworkTableInstance::GetDefault](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table_instance.html#a02ea00d4a2a77b564d384b037f2045e6) method. Then, using that `NetworkTableInstance` object, you can get a [nt::NetworkTable](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table.html) using the [nt::NetworkTableInstance::GetTable](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table_instance.html#a9ff8c68eddac070d825193d3253b612c) method.

{% highlight cpp %}
#include <networktables/NetworkTableInstance.h>
#include <networktables/NetworkTable.h>

// Get the default NetworkTableInstance object
nt::NetworkTableInstance ntinst = nt::NetworkTableInstance::GetDefault();

// Get the SmartDashboard table
std::shared_ptr<nt::NetworkTable> sd = ntinst.GetTable("SmartDashboard");
{% endhighlight %}

### Reading Data
To read data, you can use the "Get" methods of the `nt::NetworkTable` object, such as
* [GetNumber](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table.html#a8d63c89472c45a9ad28ad81f08b58249)
  - Gets a `double` value from the table.
* [GetBoolean](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table.html#abc5ca5e31da28ee0d73f558002ad9906)
  - Gets a `bool` value from the table.
* [GetString](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table.html#abc840459114e3320a16962ca2321c86d)
  - Gets a `std::string` value from the table.

All the "Get" methods require the key (name) of the value to get, and a fallback value to return if the key does not exist in the table.

{% highlight cpp %}
double double_value = sd->GetNumber("my_number", 0.0);
bool bool_value = sd->GetBoolean("my_bool", false);
std::string str_value = sd->GetString("my_string", "");
{% endhighlight %}

### Writing Data
To write data, you can use the "Put" methods of the `nt::NetworkTable` object, such as
* [PutNumber](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table.html#a15a85814c448e325c9ba6f0944bdc5d5)
  - Puts a `double` value from the table.
* [PutBoolean](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table.html#a62b0e2ad8439a6047372c36c27b1bfad)
  - Puts a `bool` value from the table.
* [PutString](https://github.wpilib.org/allwpilib/docs/release/cpp/classnt_1_1_network_table.html#a64baf7d7711b2e1ff140c2e0051e29ab)
  - Puts a `std::string` value from the table.

All the "Put" methods require the key (name) of the value to get, and the value to put.

{% highlight cpp %}
sd->PutNumber("my_number", 4.2);
sd->PutBoolean("my_bool", true);
sd->PutString("my_string", "Hi!");
{% endhighlight %}