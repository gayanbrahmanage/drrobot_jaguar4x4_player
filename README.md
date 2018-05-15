# drrobot_jaguar4x4_player H20_motion

(catkin version)

This package provides all the necessary drivers and programs for H20 robot. Initail programs provided by the Dr.Robot Inc have been improved to make the robot more stable in motion. The control program is based on tuned PID controller developed by Robotics and Sensor Group at the University of Calgary, AB, Canada.

## How to install
First, install dependency packages.

### Install joystick 

The driver package for joystick operation can be installed using the following documentation.

[Configuring and Using a Linux-Supported Joystick with ROS](http://wiki.ros.org/joy/Tutorials/ConfiguringALinuxJoystick)

### Install the dependency packages
The H20 driver needs dependency package `DrRobotMotionSensorDriver`
To install, `git clone` the `DrRobotMotionSensorDriver` package to the  directory `catkin_ws/src`

`git clone https://github.com/gayanbrahmanage/DrRobotMotionSensorDriver.git `

source your environment `source devel/setup.bash `

Run `catkin_make`

### Install `drrobot_jaguar4x4_player` from the same directory `catkin_ws/src`

`git clone` to present working directory.

`catkin_ws/src`

## How to run

`roslaunch drrobot_jaguar4x4_player H20base_player_joystick.launch `

`roslaunch drrobot_jaguar4x4_player H20base_player.launch `

### Additional information for data recording
The package can subscribe to the topic `/scan` and publishes the topic `/Rscanpose` that contains `laser scan data`, `pose` and individual encoder readings registered at each `timestamp`.

See `rostopic list`
