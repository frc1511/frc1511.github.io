---
layout: page
title: Cameras
nav_order: 8
parent: Robot Programming
---

# Cameras

* [Description](#description)
* [USB Cameras](#usb-cameras)
  - [Initialization](#initialization)
  - [Hosting a MJPG Stream](#hosting-a-mjpg-stream)
  - [Submitting Images to the MJPG Stream](#submitting-images-to-the-mjpg-stream)
* [MJPG Streams](#mjpg-streams)
  - [Initialization](#initialization-1)
* [Getting Camera Images](#getting-camera-images)

## Description

Cameras are a great way to get information during a match, whether it's though relaying the image to the driver station or using vision processing to track targets on the field.

There are a number of different kinds of cameras that can be used on the robot, including USB cameras plugged into the roboRIO, and cameras on the network that are accessed through a MJPG stream.

## USB Cameras
USB Cameras get plugged into the roboRIO, and can be accessed through the [cs::UsbCamera](https://github.wpilib.org/allwpilib/docs/release/cpp/classcs_1_1_usb_camera.html) class.

### Initialization
Initializing a `cs::UsbCamera` object requires a name, and the device id of the camera.

{% highlight cpp %}
#include <cscore.h>

cs::UsbCamera camera("intake_camera", 0);

// Configuration
camera.SetResolution(320, 240);
camera.SetFPS(30);
{% endhighlight %}

### Hosting a MJPG Stream
In order to transmit the camera's image to the driver station, it must be hosted on a MJPG stream. This can be done by using the [frc::CameraServer::PutVideo](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_camera_server.html#a459e76a3835a8151e492c52dde0d4b2a) method. This will host the a MJPG stream on port 1181. Subsequent calls to `PutVideo` will increment the port number up to 1190.

{% highlight cpp %}
#include <cameraserver/CameraServer.h>

// Host the camera stream at http://roborio-1511-frc.local:1181/stream.mjpg
cs::CvSource source = frc::CameraServer::PutVideo("intake_camera", 320, 240);
{% endhighlight %}

### Submitting Images to the MJPG Stream
Using the `cs::CvSource` object returned from the call to `PutVideo()`, it is possible to submit images to the MJPG stream. This is usually done after vision processing has been done on the image to visualize the results. This only needs to be done if the camera image is being modified in any way; otherwise, the image will be automatically submitted to the stream. Using an OpenCV `cv::Mat` image matrix representing the frame ([Getting camera frames section](#getting-camera-images)), the image can be submitted to the stream using the [PutFrame](https://github.wpilib.org/allwpilib/docs/release/cpp/classcs_1_1_raw_cv_source.html#a2c2e08e1006cdcee282de2c3f1ce7ebd) method.

{% highlight cpp %}
cv::Mat frame;

// Vision processing...

source.PutFrame(frame);
{% endhighlight %}

## MJPG Streams
MJPG Camera Streams hosted by devices other than the roboRIO (ex. Limelight, Raspberry Pi) can be accessed through the [cs::HttpCamera](https://github.wpilib.org/allwpilib/docs/release/cpp/classcs_1_1_http_camera.html) class.

### Initialization
Initializing a `cs::HttpCamera` object requires a name, and the URL of the MJPG stream.

{% highlight cpp %}
#include <cscore.h>

cs::HttpCamera camera("limelight", "http://limelight-homer.local:5800/stream.mjpg", cs::HttpCamera::HttpCameraKind::kMJPGStreamer);

// Configuration
camera.SetResolution(320, 240);
camera.SetFPS(30);
{% endhighlight %}

## Getting Camera Images
To do vision processing with the camera, you need to use the [OpenCV vision library](https://opencv.org/). Images in OpenCV are stored using the [cv::Mat](https://docs.opencv.org/3.4/d3/d63/classcv_1_1Mat.html) class. To get the camera's image, you need to create an instance of the `cs::CvSink` class using the camera object (`cs::UsbCamera`, `cs::HttpCamera`, etc.).

{% highlight cpp %}
#include <opencv2/opencv.hpp>

cs::CvSink cvSink("intake_camera_sink");
cvSink.SetSource(camera);
cvSink.SetEnabled(true);

cv::Mat frame;
std::uint64_t frame_time = cvSink.GrabFrame(frame);
if (!frame_time) {
    fmt::print("Error grabbing frame: {}\n", cvSink.GetError());
}
{% endhighlight %}
