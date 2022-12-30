---
layout: page
title: RollingRaspberry
nav_order: 3
parent: 1511 Software
---

# RollingRaspberry

* [Description](#description)
* [Building](#building)
* [Installation](#installation)
* [Configuration](#configuration)
* [Monitoring](#monitoring)
* [Disabling](#disabling)
* [Additional Tools](#additional-tools)
  - [ThunderCameraCalibrator](#thundercameracalibrator)
    * [Description](#description-1)
    * [Usage](#usage)
  - [ThunderImageCapture](#thunderimagecapture)
    * [Description](#description-2)
    * [Usage](#usage-1)
* [How it Works](#how-rollingraspberry-works)
  * [AprilTag Detection](#apriltag-detection)
  * [Camera Calibration](#camera-calibration)
  * [Pose Estimation and Ambiguity Problems](#pose-estimation-and-ambiguity-problems)

## Description
RollingRaspberry is a program for Raspberry Pi co-processors on robots that's main purpose is to handle Vision Processing with AprilTags.

RollingRaspberry's code is hosted on GitHub [here](https://github.com/frc1511/RollingRaspberry).

## Building
RollingRaspberry is meant to be run on a Raspberry Pi, but can also be run perfectly fine on a normal computer for testing purposes. However, it is not recommended to install it on any computer other than a Raspberry Pi.

When cloning the repository onto the Raspberry Pi, make sure to resolve all the git submodules,

{% highlight bash %}
git submodule init
git submodule update
{% endhighlight %}

For Raspberry Pi builds, Debian Bulseye is recommended to ensure compatibility.

RollingRaspberry requires a recent C++20 compiler, such as GCC 10 and CMake to build. RollingRaspberry also depends on a few libraries, which can be installed by running the `setup.sh` script in the `scripts` directory (Raspberry Pi only).

{% highlight bash %}
sudo ./scripts/setup.sh
{% endhighlight %}

To build RollingRaspberry, run the `build.sh` script in the `scripts` directory.

{% highlight bash %}
./scripts/build.sh
{% endhighlight %}

## Installation
RollingRaspberry should only be installed on Raspberry Pi devices. To install RollingRaspberry, run the `install.sh` script in the `scripts` directory. The script will display a prompt asking if you want to enable the systemd service. This will make the RollingRaspberry program start on boot.

{% highlight bash %}
sudo ./scripts/install.sh
{% endhighlight %}

To disable the systemd service, see the [Disabling](#disabling) section.

## Configuration
RollingRaspberry's configuration json files are located in the `/boot/frc1511/` directory. They are placed in the `boot` partition of the SD card because that partition is formatted as [FAT32](https://en.wikipedia.org/wiki/File_Allocation_Table), allowing files in it to be edited from Windows and macOS computers as an alternative to SSHing into the Raspberry Pi.

The configuration files are as follows:
* [camera_properties.json](https://github.com/frc1511/RollingRaspberry/blob/main/config/camera_properties.json)
  - Contains a list of camera models, each with their properties. These camera models can be referenced in the `camera_settings.json` file when declaring which the cameras to use. Each camera model requires a few properties:
    * `"intrinsic_matrix"`
      - The 3x3 intrinsic matrix of the camera. This matrix can be found by calibrating the camera using the [ThunderCameraCalibrator](#thundercameracalibrator) tool. The matrix should be formatted as a 1D array of 9 elements.
    * `"width"`, `"height"`
      - The width and height of the image that the camera was calibrated with.
    * `"distortion_coefficients"`
      - The 5-element distortion coefficients of the camera. This is also outputted when calibrating the camera using the [ThunderCameraCalibrator](#thundercameracalibrator) tool. The coefficients should be formatted as a 1D array of 5 elements.
* [field_layouts.json](https://github.com/frc1511/RollingRaspberry/blob/main/config/field_layouts.json)
  - Contains a list of AprilTag field layouts. These field layouts can be referenced in the `vision_settings.json` file when declaring which field layout to use.
* [vision_settings.json](https://github.com/frc1511/RollingRaspberry/blob/main/config/vision_settings.json)
  - Contains the vision settings for RollingRaspberry to use.
    * `"apriltag_family"` - The AprilTag family to use. For the 2023 season, this should be set to `"tag16h5"`.
    * `"apriltag_size"` - The size of the AprilTag in meters. For the 2023 season, the AprilTags are 6 inches, so this should be set to `0.1524`.
    * `"field_layout"` - The AprilTag field layout to use. This is referencing a field layout defined in the `field_layouts.json` file.
    * `"min_decision_margin"` - The minimum decision margin for the AprilTag detector. This value is very important, as it is one of the main ways to filter out false detections. From initial testing, values over 100 work best.
    * `"pose_estimate_iterations"` - The number of iterations to run when estimating the pose of AprilTags. This can improve the accuracy of the pose estimation, but will also increase the time it takes to process the image.
    * `"usb_cameras"` and `"mjpg_cameras"` - Lists of USB/MJPG cameras for the Raspberry Pi to use for vision processing.
      * usb_camera specific properties:
        * `"dev"` - The device index of the USB camera.
        * `"host_stream"` - A boolean value indicating whether the camera stream should be hosted on the Raspberry Pi. Camera streams start at port 1181 and increment by 1 for each camera stream hosted.
      * mjpg_camera specific properties:
        * `"url"` - The URL of the MJPG camera stream.

      * `"props"`
        - `"name"` - A name for the camera.
        - `"model"` - The camera model to use. This is referencing a camera model defined in the `camera_properties.json` file.
        - `"width"`, `"height"` - The resolution of the camera image to use for vision processing. To help the Raspberry Pi process images faster, it is recommended to use a lower resolution than the camera's native resolution.
        - `"fps"` - The framerate of the camera to use for vision processing. 30 FPS works well.
        - `"position"` - The position of the camera relative to the robot's center (relative to its wheels) in meters. This contains three elements, `"x"`, `"y"`, and `"z"`. +y is forward, +x is right, and +z is up.
        - `"rotation"` - The rotation of the camera relative to the robot in radians. This contains three elements,
          - `"roll"` - The counterclockwise rotation angle around the X axis.
          - `"pitch"` - The counterclockwise rotation angle around the Y axis.
          - `"yaw"` - The counterclockwise rotation angle around the Z axis.

          The rotations are applied in the order roll, pitch, yaw.

## Monitoring
To monitor the output of the RollingRaspberry systemd service, use `journalctl` to view the logs.

{% highlight bash %}
sudo journalctl -f -u RollingRaspberry
{% endhighlight %}

## Disabling
To disable the RollingRaspberry systemd service, use `systemctl` as shown below.

{% highlight bash %}
sudo systemctl stop RollingRaspberry
sudo systemctl disable RollingRaspberry
{% endhighlight %}

## Additional Tools
RollingRaspberry also includes a few additional tools for setup and configuration. Tools are located in the [tools](https://github.com/frc1511/RollingRaspberry/tree/main/tools) directory of the RollingRaspberry repository.

## ThunderCameraCalibrator
* [Description](#description-1)
* [Usage](#usage)

### Description
By utilizing a number of images of a chessboard pattern taken by the camera, ThunderCameraCalibrator can calculate the camera's intrinsic matrix and distortion coefficients. These values can then be used by the RollingRaspberry service to undistort frames from the camera and calculate accurate distances to vision targets.

<img src="/assets/images/rollingraspberry/calibration.png" alt="ThunderCameraCalibrator" width="800"/>

### Usage
For input, the program requires images of a chessboard pattern taken by the camera from different angles. To produce the best results possible, 20 to 30 images is recommended. A 7x6 chessboard pattern that can be printed on a standard 8 1/2" x 11" sheet of paper can be found [here](https://github.com/frc1511/RollingRaspberry/blob/main/tools/camera_calibrator/7x5_chessboard.pdf). When printed, the squares should be 3cm x 3cm. When preparing to take the calibration images, make sure that the chessboard is placed on a flat surface so that the camera can see the entire board. The chessboard should also be placed in a location where the lighting is consistent.

The program is written in Python 3 and utilizes OpenCV and numpy.

To calculate the camera's intrinsic matrix and distortion coefficients, run the following command:

{% highlight bash %}
python3 camera_calibrator.py ./path/to/input/directory
{% endhighlight %}

The program will use all '.jpg' images in the specified directory in the calibration process.

When the program is finished, it will output the camera's intrinsic matrix and distortion coefficients to the terminal. 

## ThunderImageCapture
* [Description](#description-2)
* [Usage](#usage-1)

### Description
ThunderImageCapture is a simple program that can be used to quickly capture images from a camera and save them to a directory.

### Usage
The program is written in Python 3 and utilizes OpenCV.

To start the program, run the following command:

```bash
python3 image_capture.py 0 ./path/to/output/directory
```
The first argument is the video index. This is the number that is used to identify which camera to use.

The second argument is the path to the directory where the images will be saved.

When the program is running, press the 's' key to capture an image. Images will be saved as #.jpg, where # is the number of images that have been captured. Note that images will be overwritten without warning if they already exist in the specified directory. Press the 'q' key to quit the program.

## How RollingRaspberry Works

* [AprilTag Detection](#apriltag-detection)
* [Camera Calibration](#camera-calibration)
* [Pose Estimation and Ambiguity Problems](#pose-estimation-and-ambiguity-problems)

### AprilTag Detection
For each camera, RollingRaspberry creates a new thread, called a [Vision Module](https://github.com/frc1511/RollingRaspberry/blob/main/src/include/RollingRaspberry/vision/vision_module.h) to handle the grabbing frames from the camera and running the AprilTag detector. To detect AprilTags in a given frame, use either the AprilTag library's [apriltag_detector_detect()](https://github.com/AprilRobotics/apriltag/blob/master/apriltag.h#L262) function, or WPILib's [AprilTagDetector::Detect()](https://github.com/wpilibsuite/allwpilib/blob/main/apriltag/src/main/native/include/frc/apriltag/AprilTagDetector.h#L236) function. These functions output the image coordinates of the AprilTag's corners and the ID of the detected tag, along with some other information about the detection. However, most of the detections outputted by this function are false positives, so it is important to filter out the bad detections with the detection's [Decision Margin](https://github.com/AprilRobotics/apriltag/blob/master/apriltag.h#L217). This value is a measure of how confident the detector is about the detection. From initial testing, the best detections result in a decision margin over 100.

### Camera Calibration
It is essential to know the intrinsic properties of the camera in order to properly undistort the image and calculate the pose of AprilTags. ThunderCameraCalibrator calculates the camera's 3x3 intrinsic matrix, which is defined as:

$$ camera\:matrix\:\:=\:\:\begin{pmatrix}fx&0&cx\\ 0&fy&cy\\ 0&0&1\end{pmatrix} $$

where $$fx$$ and $$fy$$ are the x and y focal lengths of the camera, and $$cx$$ and $$cy$$ are the x and y coordinates of its principal point. Both of these values are measured in pixels, so they are relative to the resolution of the calibration images. If the vision processing is being run at a different resolution than the calibration images, the camera matrix will have to be [adjusted](https://github.com/frc1511/RollingRaspberry/blob/main/src/lib/vision/camera_model.cpp#L3) accordingly.

### Pose Estimation and Ambiguity Problems

<img align="right" src="/assets/images/rollingraspberry/ambiguity_1.png" alt="Pose Ambiguity" width="200"/>

Using the properties of the camera and the image coordinates of the AprilTag corners, it is possible to calculate the pose of the AprilTag relative to the camera. However, this process is inherently ambiguous. Humans can use lighting or background cues to determine the orientation of objects in space; however, computers can't and may be fooled by similar-looking targets, as shown in the image to the right.

To get the two possible poses of the AprilTag relative to the camera, use either the AprilTag library's [estimate_tag_pose_orthogonal_iteration()](https://github.com/AprilRobotics/apriltag/blob/master/apriltag_pose.h#L55) function, or WPILib's [AprilTagPoseEstimator::EstimateOrthogonalIteration()](https://github.com/wpilibsuite/allwpilib/blob/main/apriltag/src/main/native/include/frc/apriltag/AprilTagPoseEstimator.h#L103) function.

For some detections, ambiguity can be dismissed if the ratio of the pose reprojection errors is less than 0.2. However, ratios above 0.2 are likely to be ambiguous. In this case, there are a few things that can be done to help distinguish which pose is correct,
1. Calculate the robot's pose based on both the estimated AprilTag poses. The incorrect pose can be spotted if:
  - The calculated robot pose is above or below the ground (If there's a game with ramps/elevated platforms, change this to be above the platform).
  - The calculated robot pose is very far away from its previous pose (> 1m) (remember that this is running ~50 times per second, so the robot shouldn't be moving that much from one frame to the next).
2. If the poses are very close to each other, forget about 'em.

If there are multiple other AprilTag detections with no ambiguity, then it might be a good idea just to forget about the ambiguous ones. Incorrect poses can be detremental to the overall accuracy of the robot's pose.

Finally, once the ambiguity has been resolved, the robot's pose can be calculated by adding the transform from the AprilTag to the camera to the AprilTag's known pose, then adding the transform from the camera to the robot's center. Discard any outliers, because those were likely false detections. Finally, input all the estimated poses into a Kalman filter and use the filter's output as the robot's pose. It can also help to input odometry data from the drivetrain into the Kalman filter to improve the result.
