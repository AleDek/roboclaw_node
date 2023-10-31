# roboclaw_ros (ROS 1)
This is a ROS node to command the [Roboclaw motor drivers](https://www.basicmicro.com/motor-controller).

## Before you begin
Before you use this package you need to calibrate the velocity PID on the Roboclaw. This will require the
installation of the free software [BasicMicro Motion Studio](https://www.basicmicro.com/downloads) (Windows only).
You do not need to tune for position, just velocity. Read the [manual](https://downloads.basicmicro.com/docs/roboclaw_user_manual.pdf) to know how to do it.

Also, you need to install the `serial` module of python 3:

```bash
python -m pip install pyserial
```

Then you should set the Roboclaw driver in "Packet Serial" mode, since motor commands don't work if you don't set this mode. It is all explained in the user manual.

## Usage
To execute the node, you simply need to include it in your catkin workspace, compile everything and launch it using the apposite launchfile (see the [Parameters](#parameters) if you need to change something):

```bash
roslaunch roboclaw_node roboclaw.launch
```

## Parameters
The launch file can be configure at the command line with arguments, by changing the value in the launch file or through the rosparam server.

|Parameter|Default|Definition|
|-----|----------|-------|
|dev|/dev/ttyACM0|Dev that is the Roboclaw|
|baud|115200|Baud rate the Roboclaw is configured for|
|address|128|The address the Roboclaw is set to, 128 is 0x80|
|max_speed|2.0|Max speed allowed for motors in meters per second|
|ticks_per_meter|4342.2|The number of encoder ticks per meter of movement|
|base_width|0.315|Width from one wheel edge to another in meters|

## Topics
### Subscribed
/cmd_vel [(geometry_msgs/Twist)](http://docs.ros.org/api/geometry_msgs/html/msg/Twist.html)  
Velocity commands for the mobile base.

### Published
/odom [(nav_msgs/Odometry)](http://docs.ros.org/api/nav_msgs/html/msg/Odometry.html)  
Odometry output from the mobile base.
